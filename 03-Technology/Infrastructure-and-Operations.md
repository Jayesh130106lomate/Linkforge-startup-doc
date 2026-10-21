# Infrastructure and Operations: LinkForge

---

**Document status:** reported infrastructure design and operating procedure. Provider configuration, monitoring, backup settings, and restore tests are not held in this repository and must be checked before treating a target as an achieved service level.  
**Last reviewed:** 21 October 2026

---

## 1. Production Host Topology & Responsibilities

LinkForge separates operational responsibilities across dedicated hostnames to optimize edge caching, isolate authentication cookies, and secure administrative surfaces:

| Hostname | Infrastructure / Provider | Primary Responsibilities |
| :--- | :--- | :--- |
| `www.linkforge.site` | Vercel (Edge Network) | Public marketing website, feature pages, comparison routes, public guides, and abuse report submission. |
| `linkforge.site` | Cloudflare DNS / Page Rules | Permanent HTTP 301 redirect to `www.linkforge.site` to maintain canonical search authority. |
| `app.linkforge.site` | Vercel (Node.js Serverless) | Main web application: user authentication, workspace dashboard, settings, same-origin APIs, and `/admin` console. |
| `go.linkforge.site` | Cloudflare Workers | Reported edge redirection engine for shared-domain short-link and QR traffic. Low-latency behaviour is a design objective that requires regional synthetic measurements. |
| `cname.linkforge.site` | Cloudflare for SaaS | CNAME routing target for customer custom domains, handling automated TLS termination and edge proxying. |
| `cdn.linkforge.site` | Cloudflare R2 | Public storage for workspace logos, dynamic vector QR code downloads, and creator profile imagery. |
| `send.linkforge.site` | Resend Infrastructure | Verified email sending domain for transactional authentication, password resets, and security notifications. |

---

## 2. Infrastructure Deployment Stack

```
┌────────────────────────────────────────────────────────┐
│               Global Edge Tier (Cloudflare)            │
│    • Anycast DNS & WAF                                 │
│    • Edge Worker (Redirect Engine)                     │
│    • Cloudflare for SaaS (Custom Hostnames)            │
│    • Cloudflare R2 (Object Storage)                    │
└────────────────────────────────────────────────────────┘
                           │
                           ▼
┌────────────────────────────────────────────────────────┐
│             Application Origin Tier (Vercel)           │
│    • Next.js App Router (React 19 / Node.js 24)        │
│    • Same-Origin Session Authentication                │
│    • Platform Operations Console (/admin)              │
└────────────────────────────────────────────────────────┘
                           │
             ┌─────────────┴─────────────┐
             ▼                           ▼
┌─────────────────────────┐ ┌─────────────────────────┐
│ Managed PostgreSQL      │ │ Managed Redis           │
│   • Relational Schema   │ │   • Edge Redirect Cache │
│   • GIN Trigram Indexes │ │   • Rate Limiting Tokens│
│   • Partitioned Events  │ │   • BullMQ Queue Engine │
└─────────────────────────┘ └─────────────────────────┘
```

---

## 3. Database Management & Indexing Strategy

### Schema Evolution & SQL Migrations
- Managed via **Prisma ORM 7** with PostgreSQL.
- Production schema deployments are applied strictly via `npx prisma migrate deploy` (never `prisma migrate dev`).
- **GIN & Trigram Search Indexes**: PostgreSQL GIN trigram indexes (`*_trgm_idx`) provide sub-millisecond fuzzy matching across high-volume link slugs and tag searches. Because Prisma cannot model raw GIN indexes, these are maintained in custom SQL migrations.
- **Partitioning & Retention**: Time-series analytics events utilize scheduled table partitioning (`npm run partitions:maintain`) to ensure write performance does not degrade as event tables grow into millions of rows.

### Database Performance Auditing
- Continuous query profiling is audited using the integrated database audit suite (`npm run db:performance:audit`).
- Query inventory and execution plans are regularly reviewed against `docs/audits/DATABASE_QUERY_PERFORMANCE_AUDIT_2026-08-21.md`.

---

## 4. Background Processing & Queue Lifecycle

Asynchronous background tasks are decoupled from user requests and processed by persistent BullMQ background workers:

```
┌────────────────────────────────────────────────────────────────────────┐
│                    BullMQ Persistent Worker Subsystems                 │
└────────────────────────────────────────────────────────────────────────┘
  ├── Analytics Rollup Engine  ──► Flushes Redis click buffers into SQL rollups
  ├── Google Web Risk Scanner  ──► Asynchronously re-scans live link destinations
  ├── Payment Webhook Outbox   ──► Processes Dodo Payments webhook lifecycle events
  ├── Transactional Dispatch   ──► Enqueues and sends emails via Resend API
  └── Data Retention Cleaner   ──► Purges expired raw events per plan retention
```

### Worker Deployment & Heartbeat
- The worker runs as a dedicated Node.js service using:
  ```bash
  LINKFORGE_PROCESS_ROLE=worker node --conditions react-server --import tsx workers/bootstrap.ts
  ```
- Workers publish a periodic heartbeat to Redis. The application health check (`GET /api/health/ready`) verifies the worker heartbeat before marking the system healthy.
- Queue backlog, active jobs, and failed job retries are visible directly inside the Platform Operations Console (`/admin/operations`).

---

## 5. Reliability, Health Checks & Operational Targets

### Availability and recovery target
- **Availability target:** 99.9% for public link redirection, pending measured availability, defined exclusions, and contract review. It is not a contractual SLA solely because it is stated here.
- **Cache-first resilience design:** cached redirects are intended to remain available during some origin disruptions. Cache coverage, TTL, invalidation, upstream timeout, and cache-miss behaviour must be measured and tested; do not describe the fallback as uninterrupted without evidence.

### Health Probes & Readiness Gates
- `GET /api/health/ready`: Reported readiness endpoint for database, Redis, migrations, and worker heartbeat checks. Confirm its exact dependencies, authentication, and failure semantics in the deployed environment.
- `npm run release:check`: Reported release-readiness command. Retain each production execution result and define which failures block deployment.

---

## 6. Observability & Error Handling

- **Structured Server Logging**: Important application events (authentication failures, webhook anomalies, admin entitlement overrides, Google Web Risk flags) generate structured JSON log entries.
- **Client & Performance Auditing**:
  - Web Vitals tracked via Vercel Speed Insights (`@vercel/speed-insights`).
  - Automated Lighthouse CI performance and accessibility audits run on every deployment (`lighthouserc.json`).
- **Secret Protection Policy**: No sensitive information—such as database connection strings, API tokens, user passwords, or IP hashes—is ever emitted to application logs.

---

## 7. Disaster Recovery & Backup Restoration Runbook

This runbook outlines operational procedures for business continuity, database restoration, and degraded-mode edge resilience.

### 7.1 Recovery Objectives, Backup Topology, and Retention

The prior documentation describes PITR, daily logical backups, and version-controlled edge deployment. These are **unverified operational statements** until supported by provider settings and a restore test. Set and record the following values for each critical service instead of relying on generic assumptions:

| Service | Recovery point objective (RPO) | Recovery time objective (RTO) | Backup / rebuild evidence | Last restore test |
| :--- | :--- | :--- | :--- | :--- |
| PostgreSQL | To be set | To be set | Provider configuration + encrypted backup inventory | To be recorded |
| Redis / queue | To be set | To be set | Rebuild procedure + loss/replay behaviour | To be recorded |
| Object storage | To be set | To be set | Versioning/replication/lifecycle configuration | To be recorded |
| Edge and application configuration | To be set | To be set | Versioned infrastructure/configuration and deployment runbook | To be recorded |

### 7.2 Database Restoration Verification Procedure
In the event of database corruption or primary infrastructure failure:

1. **Target Provisioning**: Provision a fresh target PostgreSQL database in the designated recovery region.
2. **Migration Baseline**: Apply all committed SQL and Prisma migrations to ensure the relational schema is up to date:
   ```bash
   npx prisma migrate deploy
   ```
3. **Snapshot Restoration**: Restore the most recent verified logical backup or initiate point-in-time recovery via the database management console.
4. **Index & Partition Verification**: Confirm that PostgreSQL GIN trigram indexes and time-series partitions are intact:
   ```bash
   npm run partitions:maintain
   npm run db:indexes:deploy
   ```
5. **System Readiness Gate**: Run the automated production readiness verification script:
   ```bash
   npm run release:check
   ```
6. **DNS & Origin Cutover**: Update the database connection URI in the application hosting environment secrets and verify `GET /api/health/ready` returns HTTP `200`.

### 7.3 Cache Eviction & Degraded-Mode Resilience
- **Non-Permanent Cache Store**: Redis operates strictly as an ephemeral cache and job broker. It is never treated as the permanent source of truth for business data.
- **Graceful Origin Fallback**: If Redis experiences sudden connection failure, data eviction, or cold reboot:
  - The Cloudflare Edge Worker gracefully degrades to querying the origin application server directly over private edge connections (`EDGE_FORWARD_SECRET`).
  - Public redirects continue resolving without breaking visitor campaigns.
  - Analytics touch events are held in memory or recorded via the PostgreSQL fallback outbox until Redis connection recovers.

---

## 8. Operational Boundaries & Ongoing Enhancements

- **Disaster-recovery rehearsal:** schedule, perform, and document at least one controlled restoration exercise before representing recovery capability externally. Record the actual RPO/RTO, data-integrity checks, and corrective actions.
- **Worker redundancy:** worker topology and failover must be confirmed from the live deployment. If a singleton worker exists, document the impact of loss and a restart/failover procedure.
- **Monitoring and escalation:** identify alert routes, on-call coverage, delivery-failure behaviour, and escalation owner. Email-only alerts may not meet a 24/7 incident-response target without coverage evidence.

### Operational Evidence Required Each Quarter

Retain a current asset inventory, provider configuration review, access review, monitored availability/latency report, backup job report, restore-test result, change log, vulnerability/patch log, and incident/postmortem register. Link material exceptions to the [Verification Register](../00-Governance/Verification-Register.md).
