# Technical Architecture & Technology Stack: LinkForge

---

**Document status:** reported architecture. This repository does not include the source application, deployment manifests, environment configuration, or test output needed to independently verify these components.  
**Last reviewed:** 21 October 2026

---

## 1. Architecture Overview

LinkForge's reported architecture is multi-tenant and edge-first, with a design objective of low-latency redirects, asynchronously processed analytics, and workspace isolation. The architecture diagram is an intended/operating model until corroborated by a current deployment inventory and tests.

```
┌────────────────────────────────────────────────────────────────────────┐
│                        LinkForge Edge & Origin Architecture            │
└────────────────────────────────────────────────────────────────────────┘

  [ Visitor Traffic: go.linkforge.site / Custom Domains ]
                         │
                         ▼
             ┌─────────────────────────┐
             │ Cloudflare Edge Worker  │
             └─────────────────────────┘
                         │
           ┌─────────────┴─────────────┐
           ▼                           ▼
    [ Redis Edge Cache ]         [ Origin Fallback: Next.js ]
    (Sub-50ms HTTP 302)          (App Router / Node.js 24)
                                       │
                                       ▼
                             ┌───────────────────┐
                             │ PostgreSQL / RDS  │
                             │ (Prisma ORM 7)    │
                             └───────────────────┘
                                       ▲
                                       │
   [ BullMQ Persistent Worker ] ───────┘
   (Analytics Rollups, Scans, Webhooks, Emails)
```

---

## 2. Technology Stack Breakdown

### 2.1 Frontend & User Interface
- **Framework**: **Next.js 16** (App Router architecture with React Server Components)
- **UI Library**: **React 19**
- **Language**: **TypeScript 5** (Strict mode enabled, strict type boundaries)
- **Styling**: **Tailwind CSS v4** (Modern CSS variables, responsive breakpoints, dark/light theme tokens)
- **Iconography**: **Lucide React**
- **Data Visualization**: **Recharts** (Interactive time-series charts, browser distributions, device bars)
- **Geographic Mapping**: **Leaflet** (Country click choropleths and heatmaps)
- **Drag-and-Drop Interaction**: **@dnd-kit/core** & **@dnd-kit/utilities** (Creator bio page block reordering)
- **List Virtualization**: **@tanstack/react-virtual** (Smooth rendering of high-volume link and event tables)
- **Bot Mitigation UI**: **@marsidev/react-turnstile** (Cloudflare Turnstile CAPTCHA widget)

### 2.2 Backend & Application Services
- **Runtime**: **Node.js 24.x LTS**
- **API Architecture**: Next.js Route Handlers and Server Actions with strict input validation via **Zod 4**
- **Authentication Engine**:
  - Host-only session cookies with cryptographic HMAC signing (`SESSION_SECRET`)
  - Password hashing via **Argon2**
  - Passkeys & Biometric Auth via **@simplewebauthn/server** & **@simplewebauthn/browser** (FIDO2 / WebAuthn)
  - Direct **Google OAuth 2.0**
  - Email-based Two-Factor Authentication (2FA) via time-sensitive tokens
- **Image Processing**: **Sharp** & **@img/sharp-libvips-linux-x64** (Dynamic QR code rendering, avatar processing, and badge rasterization)
- **Vector & PDF Generation**: **qrcode** & **pdf-lib** (High-precision dynamic vector QR PDF/SVG generation)

### 2.3 Data Storage & Caching
- **Primary Database**: **PostgreSQL**
  - Relational multi-tenant schema with workspace foreign key cascades
  - Custom SQL migrations for PostgreSQL **GIN trigram indexes (`*_trgm_idx`)** for high-speed link and tag fuzzy searching
  - Partitioned time-series tables for analytics events
- **Database ORM**: **Prisma 7.8** with `@prisma/adapter-pg` driver adapter
- **Caching & In-Memory Store**: **Redis** via **ioredis**
  - High-speed redirect lookup caching with workspace-versioned cache invalidation
  - API rate-limiting token buckets
  - Short-lived analytics click-event ingestion buffer
- **Background Job Queue**: **BullMQ 5**
  - Persistent worker process (`workers/bootstrap.ts` and `workers/index.ts`)
  - Asynchronous analytics aggregation rollups
  - Outbox pattern for payment webhook retries and notification dispatch

### 2.4 Edge & Cloud Infrastructure
- **Edge Redirection**: **Cloudflare Worker** (`cloudflare/worker.ts`)
  - Direct global HTTP 302 redirects executed at the edge
  - Host-aware routing for shared platform domain (`go.linkforge.site`) and verified custom domains
- **Custom Domain Provisioning**: **Cloudflare for SaaS**
  - Programmatic custom hostname provisioning via CNAME target `cname.linkforge.site`
  - Automated SSL/TLS certificate generation and renewal
- **Object Storage**: **Cloudflare R2** (S3-compatible via `@aws-sdk/client-s3`)
  - Stores public workspace logos, creator profile images, and vector assets via `cdn.linkforge.site`
- **Transactional Email**: **Resend**
  - Direct API email delivery from verified domain `send.linkforge.site`
  - Authentication emails, password resets, verification codes, and security alerts

### 2.5 Third-Party Integrations & Security
- **Payment Gateway / MoR**: **Dodo Payments**
  - Dual-currency checkout catalog (INR via UPI/Netbanking/Cards; USD via International Cards)
  - Cryptographically verified webhook handling (`x-dodo-signature`)
- **Malware & Threat Scanning**: **Google Web Risk API**
  - Automated pre-flight scanning of user-submitted destination URLs before publishing links to protect edge IP reputation

---

## 3. High-Performance Redirect Hot Path

Redirect speed is critical to campaign ROI. LinkForge treats the redirect pipeline as a latency-critical hot path:

```
Step 1: Visitor clicks link (e.g., https://go.linkforge.site/campaign-slug)
Step 2: Cloudflare Edge Worker captures incoming request.
Step 3: Worker queries Redis edge cache.
         ├── Cache HIT (<15ms): Immediate HTTP 302 redirect returned.
         └── Cache MISS: Worker fetches destination from Origin API.
Step 4: Origin queries PostgreSQL, executes Smart Routing logic (Device, Geo, Referrer), 
        caches result in Redis, and returns HTTP 302.
Step 5: Non-blocking analytics touch event is buffered into Redis asynchronously.
```

> **Design requirement:** redirect handling should not synchronously depend on non-critical analytics writes. Confirm this behaviour with failure-path tests before representing it as a production guarantee.

---

## 4. Analytics Ingestion & Processing Pipeline

```
  [ Visitor Redirect ]
          │ (Asynchronous touch payload)
          ▼
  [ Redis Stream / Outbox ]
          │ (Batched counter aggregation)
          ▼
  [ BullMQ Worker Process ]
          │ (Periodic scheduled rollup)
          ▼
  [ PostgreSQL Analytics Rollups ]
  (Aggregated by Link, Domain, Country, City, Referrer, Device, Browser)
```

1. **Ingestion Buffer**: When a redirect occurs, visitor metadata (hashed IP, user-agent, referer, timestamp, country) is pushed into an in-memory Redis buffer.
2. **Cryptographic Anonymization**: The visitor IP is combined with `IP_HASH_PEPPER` and hashed using SHA-256 before any data is stored.
3. **Rollup Worker**: A persistent BullMQ worker periodically flushes the Redis buffer, reconciles event counts, and updates the aggregated database rollup tables.
4. **Historical Retention**: Raw events are purged according to plan retention limits (7 to 365 days), while aggregated rollups remain permanently available for reporting.

---

## 5. Security & Threat Mitigation Controls

- **IP handling (reported design):** IP-derived data is described as hashed with a server-side secret before storage. Verify application, proxy, observability, and vendor logs before claiming raw IPs are never retained.
- **Session isolation (reported design):** host-only session cookies and same-origin API protections are described. Verify cookie attributes and all authenticated routes in the deployed application.
- **Destination reputation scanning (reported design):** Google Web Risk is listed as a pre-flight control. Confirm coverage, failure behaviour, re-scan schedule, and moderation escalation.
- **Rate limiting (reported design):** Redis-backed limiters are listed for sensitive routes. Verify rules, bypasses, and monitoring.
- **Secret management requirement:** production secrets must be held only in approved secret stores and kept out of source control. Evidence should be maintained through access/change records, not values or screenshots of secrets.

---

## 6. Data, Trust, and Failure Boundaries

The following boundaries should be documented and tested for every production release:

| Boundary | Required decision / test | Evidence required |
| :--- | :--- | :--- |
| Visitor request to edge | Identify request fields used for routing, security, logging, and analytics. Test malformed, missing, and spoofed headers. | Request-field inventory and test result. |
| Edge to origin | Authenticate origin calls, enforce timeouts, and define behaviour when origin is unavailable. | Configuration record and failure-path test. |
| Workspace data isolation | Verify that an authenticated role cannot read or modify another workspace's links, domains, exports, or billing details. | Automated authorization test / review result. |
| Analytics pipeline | Define at-least-once/at-most-once semantics, duplication handling, backlog limits, and data-loss alerting. | Queue design and reconciliation record. |
| Provider integration | Verify webhook signatures, replay protection, retry/idempotency behaviour, least-privilege credentials, and failure alerts. | Integration test and provider configuration record. |
| Data lifecycle | Define collection, retention, deletion, backup expiry, and access controls for each data category. | Approved data map and deletion test. |

Do not infer a compliance result from the diagram. The data map, vendor register, access controls, and deployed behaviour must be reviewed together; see the [Compliance Action Register](../05-Legal-and-Registration/Compliance-Action-Register.md).
