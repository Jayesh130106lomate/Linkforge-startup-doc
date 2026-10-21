# Standard Operating Procedure: Access and Change Management

**Scope:** production infrastructure, source control, hosting, data stores, payment configuration, DNS, domain management, email, analytics, and administrative tooling  
**Status:** operating baseline to implement and evidence  
**Last reviewed:** 21 October 2026

---

## 1. Objective

Protect customer data and redirect availability by ensuring that privileged access is minimal, attributable, reviewed, and removable; and that production changes are planned, reversible, and documented.

This SOP defines the control standard. It does not assert that every control is already enabled. Implementation evidence belongs in the [Verification Register](../00-Governance/Verification-Register.md).

---

## 2. Access Control Standard

| Control | Required operating practice | Evidence to retain |
| :--- | :--- | :--- |
| Individual identities | Each person uses an individual account; shared admin credentials are prohibited. | User/access export and access-review record. |
| Least privilege | Grant only the minimum role and only to the systems needed for the assigned duty. | Approved access request with role and expiry/review date. |
| Strong authentication | Enforce MFA or phishing-resistant authentication for privileged accounts whenever the provider supports it. | Provider configuration or access-review screenshot/export. |
| Time-bound access | Contractor, support, and emergency access has an expiry date or a dated removal task. | Access request and removal confirmation. |
| Separation of duties | The author of a material production change should not be the sole approver where staffing permits. | Change record with implementer and reviewer. |
| Offboarding | Revoke access promptly when employment, contract, or responsibility ends. | Offboarding checklist and access-removal record. |
| Quarterly review | Reconcile active users and roles across all critical systems. | Dated access-review log, reviewer, remediation actions. |

Critical systems include Cloudflare, Vercel, source control, database provider, Redis provider, R2/object storage, payment provider, email provider, domain registrar, monitoring/alerting, and the LinkForge administration console.

---

## 3. Access Request Workflow

1. **Request:** record the requester, business purpose, system, proposed role, data scope, approver, and expiry/review date.
2. **Approve:** the system owner verifies least privilege and conflicts of interest before granting access.
3. **Provision:** use a named identity and the lowest viable role. Never transmit passwords or recovery codes in tickets or chat.
4. **Validate:** confirm that the user can perform the required task and cannot access unnecessary functions or data.
5. **Review or remove:** review at the recorded date; renew only if the access remains justified.

Emergency access is permitted only to contain an active incident. Record the reason, systems accessed, actions taken, and removal/review result within one business day.

---

## 4. Change Classification

| Type | Examples | Approval and timing |
| :--- | :--- | :--- |
| Standard | Reversible, pre-approved low-risk change with an established runbook. | Follow the runbook and log execution. |
| Normal | Application release, schema migration, configuration change, billing catalog edit, DNS/domain change. | Written plan, peer review, rollback plan, scheduled window, post-change verification. |
| Emergency | Active security issue, outage mitigation, revoked credential, abuse containment. | Incident lead authorizes; document immediately and retrospectively review within two business days. |

---

## 5. Required Change Record

Every normal or emergency production change must record:

- a concise objective and systems affected;
- risk assessment, customer impact, and maintenance window;
- implementation steps, owner, and independent reviewer where possible;
- database migration and compatibility considerations;
- rollback plan with decision point;
- monitoring/verification steps and expected result;
- actual result, timestamps, incidents, and follow-up work.

Do not bundle unrelated changes. For redirect, authentication, payment, custom-domain, or data-retention changes, test the customer-facing flow in staging or an isolated production-safe path before general release.

---

## 6. Secrets and Recovery Material

- Store secrets only in approved provider secret stores or password managers with individual access and auditability.
- Never place keys, tokens, private certificates, backup credentials, recovery codes, or production database URLs in this repository, chat transcripts, screenshots, or issue descriptions.
- Rotate a credential after suspected exposure, staff departure, vendor compromise, or according to the system's risk-based schedule.
- Maintain at least two authorized recovery contacts for business-critical providers, while preventing any single recovery factor from becoming a shared secret.

---

## 7. Change Template

| Field | Record |
| :--- | :--- |
| Change ID / date |  |
| Type | Standard / normal / emergency |
| Owner / reviewer |  |
| Objective and affected systems |  |
| Risk and customer impact |  |
| Implementation window |  |
| Pre-change checks |  |
| Rollback trigger and steps |  |
| Verification and monitoring |  |
| Result / follow-up |  |
