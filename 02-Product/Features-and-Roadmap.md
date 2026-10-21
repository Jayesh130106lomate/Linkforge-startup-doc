# Features and Roadmap: LinkForge

---

**Document status:** feature inventory reported from prior internal documentation. The source application repository and release evidence are not in this workspace, so checked items must be verified before customer-facing use.  
**Last reviewed:** 21 October 2026

---

## 1. Feature Classification Framework

To keep product documentation accurate and trustworthy, LinkForge categorizes all functionality into three clear states:

```
┌───────────────────────────────┐
│  1. Implemented & Available   │ ──► Verified in production codebase & deployed live
└───────────────────────────────┘
               │
               ▼
┌───────────────────────────────┐
│  2. In Active Development     │ ──► Current engineering focus (testing & stabilization)
└───────────────────────────────┘
               │
               ▼
┌───────────────────────────────┐
│  3. Planned Roadmap Priorities│ ──► Exploratory initiatives guided by customer feedback
└───────────────────────────────┘
```

---

## 2. Implemented & Available Features

The following capabilities are reported as implemented in prior internal documentation. The checkboxes mean “reported as available”, not independently verified in this repository.

### Link Management & Redirection Engine
- [x] **Sub-50ms Global Redirects**: Cloudflare Worker edge routing combined with Redis cache for instant HTTP 302 redirects.
- [x] **Branded URL Shortening**: Custom slug assignment on the shared platform domain (`go.linkforge.site`) and customer custom domains.
- [x] **UTM Parameter Builder**: Automatic appending and preservation of standard UTM query tags.
- [x] **Link Cloaking & Password Protection**: Password-protect destinations and gate visitor access securely.
- [x] **Link Expiration & Scheduling**: Automated deactivation and redirection to fallback URLs based on date and time triggers.
- [x] **Tagging & Organization**: Fast workspace-level link categorization with multi-tag filtering.

### Dynamic Vector QR Code Studio
- [x] **Dynamic Destination Editing**: Update target URLs anytime without changing the printed QR matrix.
- [x] **Vector File Formats**: High-resolution exports in SVG, PNG, and PDF formats for commercial print production.
- [x] **Visual Customization**: Custom foreground colors, background colors, and corner eye patterns.
- [x] **Logo Embedding**: Center logo placement with error-correction tolerance.
- [x] **Dedicated Scan Analytics**: Distinguish physical offline scans from digital browser clicks.

### Smart Routing & Traffic Rules
- [x] **Device/OS-Aware Routing**: Target destinations based on visitor operating systems (iOS, Android, Windows, macOS, Linux).
- [x] **Geographic Routing**: Route visitors to regional destinations based on country of origin.
- [x] **Referrer Routing**: Custom destinations triggered by the referring website or platform.
- [x] **Guaranteed Fallback Routing**: Deterministic fallback path preventing broken user journeys.

### Creator Bio Link Pages
- [x] **Visual Drag-and-Drop Builder**: Reorder links and content blocks with intuitive drag-and-drop powered by `@dnd-kit`.
- [x] **Diverse Block Types**: Support for links, headers, text cards, social media icons, and media embeds.
- [x] **Custom Theme Controls**: Pre-built color palettes, customizable font stacks, and background styling.
- [x] **Custom Domain Mapping**: Host creator bio pages directly on client root domains or subdomains.

### Custom Domains & Edge Security
- [x] **Automated Domain Provisioning**: Cloudflare for SaaS integration via `cname.linkforge.site`.
- [x] **Automated SSL/TLS Issuance**: Automatic certificate generation and renewal.
- [x] **Domain Health Verification**: Dashboard DNS checks and real-time verification status monitoring.

### Privacy-Preserving Analytics
- [x] **Cookie-minimised tracking design**: Reported design avoids persistent analytics cookies. Confirm all deployed scripts, logs, regional requirements, and policy language before claiming legal compliance.
- [x] **Cryptographic IP Anonymization**: Immediate SHA-256 hashing using a high-entropy server pepper (`IP_HASH_PEPPER`).
- [x] **Bot & Spider Filtering**: Automated user-agent parsing and bot filtering via `ua-parser-js`.
- [x] **Dimension Breakdowns**: Geographic (country, city), device, browser, OS, referrer, and UTM campaign rollups.
- [x] **Asynchronous CSV Export**: Private export generation processed by background workers without silent row truncation.

### Workspace Governance & Platform Administration
- [x] **Multi-Tenant Workspaces**: Workspace isolation with role-based access control (`OWNER`, `ADMIN`, `MEMBER`, `ANALYST`, `VIEWER`).
- [x] **Platform Operations Console (`/admin`)**: Operations dashboard, user management, workspace auditing, abuse report moderation, and manual entitlement overrides.
- [x] **Authentication & Security**: Argon2 password hashing, Passkeys / WebAuthn support, Google OAuth, Email 2FA, and Cloudflare Turnstile bot challenges.
- [x] **Automated URL Threat Scanning**: Google Web Risk integration scanning destination links for malware and phishing.

### Commercial Billing Engine
- [x] **Regional Multi-Currency Pricing**: Configured regional pricing maps (INR for India; USD for Global).
- [x] **Dodo Payments Integration**: Webhook-driven subscription handling for Starter, Pro, and Business tiers.

---

## 3. Active Focus Areas (Priority 1 — Production Stability & Monetization)

Current engineering work is focused on reliability, monetization verification, and user activation:

1. **Redirect Latency & Edge Cache Tuning**: Further optimizing edge cache hit ratios and verifying cold-start behavior across all global Cloudflare points of presence.
2. **Analytics Outbox & Rollup Reconciliation**: Verifying that high-volume click spikes in Redis flush accurately into PostgreSQL rollup tables without data discrepancies.
3. **End-to-End Billing Lifecycle Testing**: Comprehensive testing of Dodo Payments webhook flows (card renewals, UPI completions, cancellations, refunds, and grace-period entitlement suspensions).
4. **Monitoring, Error Reporting & Observability**: Consolidating structured error logging, queue heartbeat alerts, and automated failure recovery procedures.
5. **Onboarding & Workspace Activation**: Streamlining first-time user flows to accelerate time-to-value for link creation and custom domain setup.

---

## 4. Planned Roadmap Priorities

The following initiatives represent LinkForge's structured development roadmap, prioritized by customer impact:

```
┌────────────────────────────────────────────────────────┐
│               LinkForge Product Roadmap                │
├────────────────────────────────────────────────────────┤
│ Priority 2: Developer Platform & Integrations          │
│ Priority 3: Campaign Analytics & Marketing Integrations│
│ Priority 4: Team & Enterprise Capabilities             │
│ Priority 5: Mobile Experience & Progressive Web App    │
└────────────────────────────────────────────────────────┘
```

### Priority 2: Developer Platform & Integrations
- **Public API Documentation & Key Management**: Complete public REST API documentation with scoped developer API tokens and granular rate limiting. *(Note: Base API routes exist in the codebase; formal developer onboarding and documentation are scheduled for release)*.
- **Signed Outbound Webhooks**: Provide customer-facing webhooks with cryptographic HMAC signatures, automated delivery retries, and an in-dashboard delivery log.
- **Automation Connectors**: Evaluate official integrations for workflow automation platforms such as Zapier, Make, and n8n.

### Priority 3: Campaign Analytics & Marketing Integrations
- **Retargeting Pixel Integrations**: Evaluate safe, client-side retargeting pixel injection (Meta Pixel, Google Ads, LinkedIn Insight Tag) on custom domain redirects.
- **Multi-Touch Attribution Modeling**: Enhance conversion tracking and campaign attribution across multi-step marketing funnels.
- **Custom Report Builders**: Expand scheduled executive summary PDF reports for marketing agencies delivering results to their end clients.

### Priority 4: Team & Enterprise Capabilities
- **Enhanced Collaboration Workflows**: Granular per-link permission delegation and internal campaign approval workflows.
- **Enterprise SSO / SAML**: Evaluate Okta, Azure AD, and Google Workspace SAML single sign-on when justified by enterprise customer volume.
- **Compliance Audit Log Export**: Automated streaming of workspace audit logs to client SIEM systems (e.g., Datadog, Splunk).

### Priority 5: Mobile Experience
- **Responsive Web Optimization**: Continual refinement of mobile touch interactions across complex data tables and analytics charts.
- **Progressive Web App (PWA) / Native Mobile**: Evaluate a dedicated mobile management app following validation of user demand and business priorities.

---

## 5. Roadmap Governance & Policy

- **No Speculative Commitments**: Delivery dates are not committed in advance. LinkForge operates on milestone-driven releases guided by production stability and verified user needs.
- **Customer-Driven Prioritization**: Roadmap items are continually re-evaluated against real feedback from active marketing agencies and power users.
- **Security & Reliability Precedence**: Any operational stability, abuse prevention, or data integrity requirement takes immediate priority over new feature development.

---

## 6. Release-Evidence Gate

Move an item from **reported** to **verified** only when the owner records all of the following in the [Verification Register](../00-Governance/Verification-Register.md):

1. release version, environment, and date;
2. successful primary and failure-path test result;
3. entitlement/plan test where limits apply;
4. security, privacy, retention, and support impact;
5. rollback or disablement path; and
6. approver and link to supporting evidence.

For externally announced functionality, also confirm that the help content, plan comparison, Terms/Privacy disclosures, and support team guidance have been updated.
