# LinkForge Startup Documentation

This repository is the internal documentation hub for **LinkForge**, a campaign-link management, smart-routing, dynamic QR code, creator bio page, and privacy-focused analytics product.

It is a working source of truth, not a marketing deck. It separates verified registration records from reported operating practices, targets, and roadmap ideas so the team can use the same material for product work, customer due diligence, and business operations without overstating what is known.

**Documentation status:** refreshed 21 October 2026  
**Primary verified artifact:** [Udyam registration certificate](05-Legal-and-Registration/Certificates/UDYAM-MH-24-0085874-LinkForge-Udyam-Registration-Certificate.pdf)

---

## Start Here

1. Read [Documentation Standards](00-Governance/Documentation-Standards.md) before changing a material claim.
2. Check the [Verification Register](00-Governance/Verification-Register.md) before using a product, pricing, performance, legal, tax, or security statement externally.
3. Use the index below to navigate by business need.
4. Record new evidence and its owner when closing an open item; do not silently convert a target into a fact.

---

## Documentation Map

| Area | Use this document for | Claim status / review need |
| :--- | :--- | :--- |
| Governance | [Documentation Standards](00-Governance/Documentation-Standards.md) | Documentation control, evidence rules, and review process. |
| Governance | [Verification Register](00-Governance/Verification-Register.md) | Central register of material gaps, conflicts, and required evidence. |
| Company | [Company Overview](01-Company/Company-Overview.md) | Company identity, operating principles, contacts, and organization. Verify public identity and contact statements before publication. |
| Company | [Business Plan](01-Company/Business-Plan.md) | Market problem, target customers, positioning, revenue model, risks, and milestones. Strategy, not a forecast. |
| Product | [Product Overview](02-Product/Product-Overview.md) | Product modules, personas, use cases, and documented boundaries. Validate against the live application before a sales commitment. |
| Product | [Features and Roadmap](02-Product/Features-and-Roadmap.md) | Feature classification, active work, and planned priorities. Roadmap dates are intentionally not commitments. |
| Technology | [Architecture and Tech Stack](03-Technology/Architecture-and-Tech-Stack.md) | Reported architecture, data flows, integrations, and technical safeguards. Requires deployment/source evidence for verification. |
| Technology | [Infrastructure and Operations](03-Technology/Infrastructure-and-Operations.md) | Reported host topology, health checks, backup/restore procedure, and operational targets. Validate current provider settings and restore tests. |
| Business | [Pricing and Revenue](04-Business-Growth/Pricing-and-Revenue.md) | Drafted plan matrix, billing model, and financial reporting boundary. Live catalog, invoice, and tax treatment need evidence. |
| Business | [Marketing and Sales](04-Business-Growth/Marketing-and-Sales.md) | Positioning, acquisition plan, migration approach, and marketing integrity rules. |
| Legal | [Registration and Compliance](05-Legal-and-Registration/Registration-and-Compliance.md) | Udyam details, legal-policy inventory, vendor register, and IP tracker. Not legal or tax advice. |
| Legal | [Compliance Action Register](05-Legal-and-Registration/Compliance-Action-Register.md) | P0/P1 actions required for policy, tax, data-protection, and IP readiness. |
| Operations | [Customer Support and SLAs](06-Operations-and-SOPs/Customer-Support-and-SLAs.md) | Support routing, target response/resolution timing, escalation, and migration. |
| Operations | [Abuse and Security Response](06-Operations-and-SOPs/Abuse-and-Security-Response.md) | Abuse intake, triage, suspension, appeal, and vulnerability-reporting process. |
| Operations | [Incident Management](06-Operations-and-SOPs/Incident-Management.md) | Severity model, diagnosis, degraded operation, customer communication, and postmortems. |
| Operations | [Access and Change Management](06-Operations-and-SOPs/Access-and-Change-Management.md) | Required controls for privileged access, production changes, secrets, and reviews. |

---

## Repository Structure

```text
LinkForge-Startup/
├── README.md
├── 00-Governance/
│   ├── Documentation-Standards.md
│   └── Verification-Register.md
├── 01-Company/
├── 02-Product/
├── 03-Technology/
├── 04-Business-Growth/
├── 05-Legal-and-Registration/
│   ├── Certificates/
│   └── Compliance-Action-Register.md
└── 06-Operations-and-SOPs/
```

---

## Current Documentation Boundary

The certificate in this repository is an original government record. The remaining material describes the intended or reported LinkForge operating model. The application source repository, provider configuration exports, signed vendor agreements, policy pack, payment reconciliation records, monitoring reports, and restore-test evidence are not stored here. Therefore, do not present the following as independently verified solely from this repository:

- live feature availability, plan limits, prices, provider configuration, or customer support performance;
- redirect latency, uptime, recovery objectives, or security-control effectiveness;
- revenue, active customers, paid subscribers, conversion, or retention;
- GST status, data-protection compliance, trademark status, or contractual SLAs.

The exact evidence required to strengthen each of these claims is in the [Verification Register](00-Governance/Verification-Register.md).

---

## Non-Negotiable Maintenance Rules

1. **Never invent business proof.** Do not add customer logos, testimonials, revenue, user counts, uptime, security certifications, partnerships, or performance results without dated evidence.
2. **Keep current, target, and planned separate.** A feature in source code, a provider capability, or a roadmap entry is not necessarily live or contractually available.
3. **Protect sensitive data.** Never commit passwords, API keys, secret URLs, raw analytics data, payment details, personal IDs, contracts containing unnecessary personal data, or private customer information.
4. **Use relative links.** Documents must work outside this local workspace; do not use `file:///` links.
5. **Preserve originals.** Do not alter government certificates or executed records. Add new versions with dates and record which one supersedes the old material.
6. **Review on change.** Pricing, legal policies, data flows, vendors, authentication, redirect infrastructure, and incident procedures must be reviewed when changed and at least quarterly.
