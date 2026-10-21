# Verification Register and Open Information Log

**Status date:** 21 October 2026  
**Purpose:** prevent unknowns from being presented as established facts

---

## 1. How to Use This Register

Each row covers a material claim or decision that needs supporting evidence. A row is closed only after the evidence is stored in the approved location, reviewed by the named owner, and the related documentation is updated.

The absence of a row does not make a claim verified. New material claims should be added before they are used externally.

---

## 2. Evidence Confirmed in This Repository

| Area | Confirmed item | Evidence held | Status |
| :--- | :--- | :--- | :--- |
| Legal registration | The enterprise name, Udyam number, dates, classification, activity, NIC codes, and address fields recorded on the certificate. | Original Udyam certificate PDF; printed 19 August 2026. | **Verified** |
| Documentation governance | This repository now defines claim labels, review rules, and an evidence log. | [Documentation Standards](Documentation-Standards.md) | **Verified** |
| Planned company actions | Address check, GST review, trademark filing, and policy evidence are still required. | This register and the compliance action register. | **Open** |

> Product behaviour, plan limits, infrastructure configuration, vendor enablement, performance, revenue, and support delivery are not independently verifiable from this documentation-only repository. They remain internal operational statements until supported by a dated release, export, contract, test, or system record.

---

## 3. Priority Open Items

| Priority | Item to verify or complete | Why it matters | Evidence required | Owner | Target state |
| :--- | :--- | :--- | :--- | :--- | :--- |
| P0 | Legal-policy pack | Customers need the exact terms, privacy, acceptable-use, cancellation/refund, and data-processing terms that govern use. | Approved policy PDFs or immutable published copies, version/effective date, approver. | Legal / Founder | **Needs confirmation** |
| P0 | GST, invoicing, and Merchant-of-Record position | Tax treatment must match the actual supply model and invoices. | GSTIN status search or tax-adviser memo; Dodo merchant agreement; sample redacted invoice; monthly reconciliation. | Finance / Founder | **Needs confirmation** |
| P0 | Production security and access controls | A documented security posture is not proof that controls are enabled. | Asset inventory, access-review record, MFA/SSO configuration evidence, secret-rotation record, vulnerability log. | Engineering | **Needs confirmation** |
| P0 | Data map and retention/deletion behaviour | Required to answer privacy, security, and customer due-diligence questions accurately. | Approved data inventory, vendor regions/DPAs, deletion test, retention-job evidence. | Privacy / Engineering | **Needs confirmation** |
| P1 | Live product capability and plan limits | Prevents support and sales commitments from drifting from production. | Versioned plan export, release checklist, automated entitlement test output. | Product / Engineering | **Needs confirmation** |
| P1 | Performance and availability claims | “Sub-50ms” and “99.9%” need scope, measurement method, and actual history. | Synthetic-monitoring configuration and monthly report with percentile, regions, and exclusions. | Engineering | **Needs confirmation** |
| P1 | Backups and restore readiness | Backup settings alone do not demonstrate recovery. | Provider configuration, successful restore-test record, RPO/RTO result, reviewer. | Engineering | **Needs confirmation** |
| P1 | Customer support and incident delivery | Published response targets need coverage and escalation ownership. | On-call roster, ticket sample, monthly SLA report, incident drill/postmortem. | Operations | **Needs confirmation** |
| P2 | Trademark filing | The mark should not be described as registered or protected until an application is filed and its status recorded. | Official filing receipt/application number for each class and mark. | Founder / Legal adviser | **Planned** |
| P2 | Company address reconciliation | The certificate’s city/district fields merit confirmation before they are repeated in public materials. | Udyam portal update or adviser confirmation. | Founder | **Needs confirmation** |

---

## 4. Claim-Conflict Decisions

| Topic | Documentation decision | Reason |
| :--- | :--- | :--- |
| Support timing | Describe first-response and target-resolution times separately; treat them as operating targets, not contractual terms, unless a signed SLA says otherwise. | Existing documents used “SLA” for both values. |
| Privacy | Describe technical practices and user rights separately from compliance conclusions. | Technical measures alone cannot establish legal compliance. |
| Infrastructure | Use “reported production architecture” until a current deployment inventory is retained here. | The source application repository is not present in this workspace. |
| Revenue and traction | Keep exact values absent until reconciled to payment and accounting records. | No revenue records are held in this repository. |
| Merchant of Record | State the documented role only where the executed agreement and live checkout support it. | Vendor marketing pages do not prove the account configuration. |

---

## 5. Review Log Template

Copy this table into a dated entry whenever an item is closed or materially changed.

| Date | Item / claim | Evidence location | Reviewer | Decision | Follow-up date |
| :--- | :--- | :--- | :--- | :--- | :--- |
| YYYY-MM-DD |  |  |  | Verified / revised / retired | YYYY-MM-DD |
