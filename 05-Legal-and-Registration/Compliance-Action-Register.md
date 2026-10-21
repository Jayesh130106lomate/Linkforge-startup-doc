# Compliance Action Register

**Scope:** administrative, privacy, tax, intellectual-property, and customer-policy readiness  
**Status date:** 21 October 2026  
**Important:** this is an operational tracker, not legal or tax advice. Obtain qualified advice for legal interpretation, tax registration, data-transfer assessments, or contractual commitments.

---

## 1. Decision Principles

- A government registration, vendor capability, or privacy feature does not by itself establish regulatory compliance.
- Public policy language must match the actual product, data flows, payment model, and signed contracts.
- Where an item is not confirmed, LinkForge should say so internally and avoid making the corresponding public promise.
- Completed items require a dated artifact and reviewer, not a verbal confirmation.

---

## 2. Action Register

| Priority | Action | Completion evidence | Current state |
| :--- | :--- | :--- | :--- |
| P0 | Publish and archive approved Terms of Service, Privacy Policy, Acceptable Use Policy, cancellation/refund policy, and Cookie Notice (if applicable). | Immutable copy, effective date, version, approver, public URL, previous-version archive. | **Open** |
| P0 | Execute or archive the relevant payment-provider agreement and reconcile the legal seller, invoice issuer, refund/chargeback responsibility, and tax responsibilities. | Executed agreement, account configuration, redacted sample invoice, reconciliation owner. | **Open** |
| P0 | Confirm GST registration position and ongoing filing obligations with a qualified Indian tax adviser. | Adviser memo or GST portal record, decision date, threshold-monitoring method. | **Open** |
| P0 | Produce a Record of Processing / data map. | Categories of data, data subjects, purpose, legal basis, recipients, locations, retention, and deletion method. | **Open** |
| P0 | Confirm each vendor's processing role, regions, DPA, security documentation, and incident-notification terms. | Vendor register with contract/DPA links and review dates. | **Open** |
| P1 | Test account deletion, export, link deletion, analytics retention, backup expiry, and deletion requests end to end. | Test record with test account, date, expected/actual results, exceptions, reviewer. | **Open** |
| P1 | Establish a data-subject request workflow. | Intake address/form, identity-verification rule, tracker, response ownership, escalation procedure. | **Open** |
| P1 | Document any international data-transfer mechanism that applies to actual customer data. | Legal assessment and executed contractual mechanism where needed. | **Open** |
| P1 | File trademark applications only after clearance and class specification review. | Application receipt, class, mark type, owner, application number, renewal diary entry. | **Planned** |
| P2 | Reconcile address fields in the Udyam registration with the intended correspondence and public business address. | Portal amendment or written professional advice explaining no change is necessary. | **Open** |

---

## 3. Data-Protection Operating Baseline

Before representing the service as privacy-compliant, the operating record should show:

1. a current inventory of personal data, including server logs, support tickets, authentication records, payment events, analytics fields, backups, and vendor telemetry;
2. a documented purpose and retention period for each category;
3. user-facing disclosure that matches the inventory and identifies contact routes for rights requests;
4. access controls, encryption, deletion, breach-response, vendor-management, and data-transfer procedures; and
5. a lawful basis and legal-review record appropriate to each applicable jurisdiction.

The existing statements about cookie use and IP hashing should be confirmed against production traffic, logs, Cloudflare/Vercel configuration, error monitoring, and all analytics scripts before being treated as final policy language.

---

## 4. Policy Version Register Template

| Policy | Version | Effective date | Approved by | Published URL | Archive location | Next review |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Terms of Service |  |  |  |  |  |  |
| Privacy Policy |  |  |  |  |  |  |
| Acceptable Use Policy |  |  |  |  |  |  |
| Refund / Cancellation Policy |  |  |  |  |  |  |
| Data Processing Addendum |  |  |  |  |  |  |
| Vulnerability Disclosure Policy |  |  |  |  |  |  |

---

## 5. Evidence Sources Used for Existing Statements

| Source | What it supports | Important limit |
| :--- | :--- | :--- |
| [Udyam registration certificate](Certificates/UDYAM-MH-24-0085874-LinkForge-Udyam-Registration-Certificate.pdf) | The registration fields printed in the certificate. | It does not establish GST registration, payment status, legal-policy compliance, or trademark ownership. |
| [IP India official fees](https://ipindia.gov.in/pages/trade-marks/learn/forms-and-official-fees) | Reduced TM-A filing fee category for an individual, startup, or small enterprise. | Eligibility and filing strategy should be confirmed for the applicant and classes before filing. |
| [Dodo Payments DPA](https://dodopayments.com/legal/dpa) | Dodo's published description of its independent-controller role as Merchant of Record for buyer data. | A published DPA does not confirm LinkForge's account configuration or contract. |

Review external sources at the time of use; regulations and vendor terms can change.
