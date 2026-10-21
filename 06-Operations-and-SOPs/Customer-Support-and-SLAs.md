# Standard Operating Procedure: Customer Support & Service-Level Agreements (SLAs)

---

**Document status:** support operating procedure and target timings. These are not contractual SLAs unless incorporated into a signed customer agreement or order form. Support coverage and delivery performance require ticketing/on-call evidence.  
**Last reviewed:** 21 October 2026

---

## 1. Overview & Support Philosophy

LinkForge is designed to support campaign link routing, dynamic QR codes, and analytics for marketing agencies, performance teams, and online creators. The reported support model is core-team managed; confirm the actual staffing and coverage before offering it as a commitment.

Our support philosophy is guided by three principles:
1. **Direct Technical Ownership**: Inquiries are handled by team members who understand the platform architecture, eliminating canned generic responses.
2. **Predictable Communication**: Use documented first-response and target-resolution times, then report exceptions rather than implying certainty.
3. **Data Privacy First**: Support should not request passwords, API secrets, or unnecessary visitor data, and should use scoped administrative views where available.

---

## 2. Inbound Support Channels & Routing Matrix

Customers and agencies interact with LinkForge across three official email communication channels:

| Channel | Inbox | Primary Scope | Responsible Lead |
| :--- | :--- | :--- | :--- |
| **Technical Support** | `support@linkforge.site` | Workspace configuration, custom domain DNS verification, QR generation, bio page setup, billing inquiries | Technical Support / Core Team |
| **Agency & Sales** | `sales@linkforge.site` | High-volume agency quotas, bulk migrations from Bitly, bespoke domain allocations, custom billing arrangements | Founder & Marketing Specialist (`vikram@linkforge.site`) |
| **Trust & Safety** | `abuse@linkforge.site` | Harmful links, phishing, malware, copyright infringement, DMCA notices | Security & Moderation Lead |

---

## 3. Plan-Based Support Targets

The following are target service levels stated in prior documentation. Confirm the live plan configuration, staffing coverage, and business-hours definition before publishing them:

| Plan Tier | Support Tier Level | Target First Response | Target Resolution | Inbound Channels |
| :--- | :--- | :--- | :--- | :--- |
| **Free** | `COMMUNITY` | Within 48 hours | 72 hours | Community guides, documentation, email (`support@linkforge.site`) |
| **Starter** | `STANDARD` | Within 12 hours | 24 hours | Standard email ticket queue |
| **Pro** | `PRIORITY` | Within 2 hours | 4 hours | Priority email queue with escalated technical triage |
| **Business / Agency** | `DEDICATED` | Within 30 minutes | 1 hour (Critical) | Dedicated escalation channel, direct senior routing, migration assistance |

*Business-hours target: Monday through Saturday, 09:00 to 19:00 IST. A 24/7 SEV-1 response claim must be backed by an on-call rota, alert-delivery test, and incident record; otherwise treat it as a goal.*

### What These Targets Mean

- **First response** is an acknowledgement by a person who has classified the request and provided a next update time.
- **Resolution** means the reported issue is fixed, a documented workaround is supplied, or the request is closed with the customer's acknowledgement. It does not mean a third-party destination, DNS registrar, or payment network is guaranteed to be restored.
- **Target** means an operational objective, not a service credit or contractual remedy. Any contractual availability, support, or credit term must appear in the signed agreement.

---

## 4. Multi-Tier Support Escalation Workflow

```
[ Customer Inquiry Received at support@linkforge.site ]
                         │
                         ▼
             [ Level 1: Initial Triage ]
  - Verify customer account & subscription plan tier
  - Classify category (DNS, QR, Billing, Routing, Bug)
  - Resolve known configuration and user guide inquiries
                         │ (If unresolved or technical defect)
                         ▼
         [ Level 2: Advanced Technical Support ]
  - Inspect Cloudflare CNAME and SSL handshake status
  - Verify Dodo Payments webhook receipt and plan entitlements
  - Validate BullMQ worker execution for bulk imports/exports
                         │ (If systemic anomaly or platform bug)
                         ▼
         [ Level 3: Core Engineering Escalation ]
  - Founder & Lead Engineer (Jayesh Lomate)
  - Edge Worker routing diagnostics and PostgreSQL index health
  - Hotfix deployment, code patch, and direct customer update
```

### Escalation Level Details
* **Level 1 (Triage & Account Assistance)**:
  - Password resets, workspace member management, plan upgrades, and feature walkthroughs.
  - Reference relevant documentation: [Product Overview](../02-Product/Product-Overview.md).
* **Level 2 (Systems & Integration Support)**:
  - Verifying CNAME propagation (`cname.linkforge.site`) for branded custom domains.
  - Investigating failed bulk CSV link imports or vector SVG rendering discrepancies.
  - Re-syncing missed Dodo Payments webhook events from the `/admin/operations` console.
* **Level 3 (Engineering & Architecture)**:
  - Investigating sub-50ms redirect latency spikes or unexpected 5xx errors.
  - Database constraint conflicts or partition boundary maintenance.
  - High-impact agency SLA escalation.

---

## 5. Scope of Support: Boundaries & Non-Supported Items

To maintain operational focus and system integrity, LinkForge defines clear boundaries on what falls within standard support coverage:

### Supported Inquiries
* Link creation, shortening, and smart device/geo-routing behavior.
* Dynamic vector QR code generation, styling, and scan attribution.
* Custom domain SSL provisioning and DNS routing via Cloudflare for SaaS.
* Drag-and-drop creator bio page rendering and link blocks.
* Cookieless analytics calculation, bot filtering, and CSV export generation.
* Subscription checkout, invoice download, and plan upgrades via Dodo Payments.

### Excluded (Non-Supported) Items
* **Third-Party Destination Outages**: LinkForge can investigate its own redirect behaviour, but is not responsible for the availability of a customer-selected destination URL.
* **Third-Party Analytics Discrepancies**: Variance caused by third-party tracking pixels (e.g., Google Tag Manager, Meta Pixel) installed on destination sites that block bots differently than LinkForge's privacy-first server engine.
* **External Domain Registrar Configuration**: While LinkForge provides precise CNAME records (`cname.linkforge.site`), configuration inside third-party registrars (GoDaddy, Namecheap, Google Domains) must be managed by the customer or agency IT team.
* **Direct Database Manipulation**: Support will not execute custom one-off manual SQL mutations on production tables to bypass product validation rules.

---

## 6. Ticket Lifecycle, Customer Updates, and Records

Every ticket should record a unique ID, requester/workspace, plan (where applicable), category, severity, first-response timestamp, next-update time, owner, actions, customer updates, resolution, and closure reason. Avoid placing credentials, payment details, or unnecessary visitor data in the ticket.

For material routing, billing, domain, data-access, or security issues:

1. acknowledge the request using the relevant target window;
2. state the impact and next update time, without speculating on root cause;
3. escalate using the incident or abuse procedure where appropriate;
4. update the customer at the agreed cadence; and
5. link the final resolution to any change record, incident, or refund/entitlement adjustment.

Review monthly: ticket volume by category, first-response performance, resolution performance, reopen rate, aged tickets, escalations, customer-impacting defects, and exceptions. Retain the source report and reviewer in the [Verification Register](../00-Governance/Verification-Register.md).


---

## 7. White-Glove Agency Onboarding & Migration SOP

For Business tier subscribers and agency partners migrating large link portfolios from Bitly, Rebrandly, or Short.io:
1. **Pre-Migration Intake**: The agency provides a sanitized export of active links, paths, and target destinations.
2. **Format Harmonization**: The technical lead validates CSV structure against LinkForge's bulk import validator (`src/lib/bulk-import/`).
3. **Staged Domain Cutover**: The agency provisions CNAME records pointing to `cname.linkforge.site` during scheduled low-traffic hours.
4. **Validation Sweep**: An automated test batch samples 50+ random redirects to ensure zero HTTP 404 or redirect loops before shutting down legacy subscriptions.
