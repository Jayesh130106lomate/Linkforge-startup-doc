# Documentation Standards and Review Policy

**Applies to:** every document in this repository  
**Repository owner:** LinkForge Technologies  
**Last reviewed:** 21 October 2026  
**Review cadence:** quarterly, and before any material public, contractual, security, or pricing change

---

## 1. Purpose

This repository is the internal source of truth for LinkForge's company, product, technical, commercial, legal, and operating documentation. It makes three things unambiguous:

1. what is evidenced and current;
2. what is an internal operating statement that still needs verification; and
3. what is planned rather than available today.

It is not a substitute for signed customer agreements, live product configuration, source-code review, legal advice, tax advice, or financial records.

---

## 2. Required Claim Labels

| Label | Meaning | Where it may be used |
| :--- | :--- | :--- |
| **Verified** | Supported by an attached official record, a dated system export, a signed agreement, or a reproducible test. | Facts, legal registration details, measured performance, live plan limits. |
| **Operational statement** | Reported internal operating practice. It has an owner but the supporting evidence is not stored here. | SOPs, architecture descriptions, host inventory. |
| **Target** | A goal, design objective, or non-contractual service target. | Latency, uptime, recovery goals, response-time targets. |
| **Planned** | Not yet released or contractually available. | Roadmap, future integrations, hiring. |
| **Needs confirmation** | Material information is missing, stale, or contradictory. | Tax status, vendor regions, legal-policy versions, live pricing. |

Do not use words such as *guaranteed*, *compliant*, *certified*, *unlimited*, *always*, or *never* unless the exact scope and proof are recorded in the [Verification Register](Verification-Register.md).

---

## 3. Document Control Requirements

Every substantive document must include, near the top or in a linked register:

- a named business owner;
- the date last reviewed;
- the source or evidence type for material claims;
- clear separation of current state, targets, and roadmap; and
- links that work when the repository is cloned or viewed on GitHub.

Update the document and the [Verification Register](Verification-Register.md) together when a claim changes. Never replace an official record; add a newer record alongside it and note the supersession.

---

## 4. Evidence Rules

### Acceptable evidence

- Government-issued certificates and filings.
- Signed contracts, policies, Data Processing Agreements (DPAs), and approved terms.
- Read-only exports from a live system, dated and redacted where necessary.
- A reproducible release check, architecture diagram, or source-code commit from the relevant product repository.
- Vendor documentation for a vendor capability. This proves the vendor's offering, not that LinkForge has enabled it.

### Evidence handling

- Keep original documents in their native format under the appropriate restricted folder.
- Do not store credentials, access tokens, production URLs with secrets, personal financial details, or raw customer data here.
- Store a redacted export where a complete record would expose personal data.
- Record the evidence date, owner, and storage location. If a document contains an expiry date, add a review reminder before it expires.

---

## 5. Writing Rules

- Use a relative Markdown link, never a local `file:///` URL.
- State units and scope: for example, `target first response within 12 business hours`, rather than `12 hours`.
- Distinguish a response target from a resolution target and an availability target from a contractual SLA.
- Do not turn product design into a legal conclusion. “Cookieless” does not by itself establish GDPR, CCPA/CPRA, or DPDP compliance.
- Do not publish customer, revenue, conversion, uptime, security-certification, or performance claims without dated evidence.
- Keep public-facing statements narrower than internal operating claims until they have legal and technical approval.

---

## 6. Review Cycle and Change Process

| Trigger | Required action | Accountable owner |
| :--- | :--- | :--- |
| Product release or configuration change | Update feature status, limits, architecture, and customer-facing copy. | Product / Engineering owner |
| Pricing, billing, or tax change | Reconcile live catalog, invoices, refund terms, and pricing documentation. | Finance / Commercial owner |
| New vendor or data flow | Update sub-processor register, data inventory, privacy policy, and security review. | Privacy / Engineering owner |
| Security incident or material outage | Update the incident record; revise the affected SOP and control evidence. | Incident lead |
| Quarterly review | Reconfirm open items, retired claims, owners, and review dates. | Repository owner |

Emergency operational changes may be made immediately to restore service. They must be documented retrospectively within two business days, including reviewer and rollback notes.

---

## 7. Minimum Records Still Needed

The documents in this repository are stronger when accompanied by the following restricted records:

1. approved Terms of Service, Privacy Policy, Acceptable Use Policy, refund/cancellation policy, and DPA, each with version and effective date;
2. current product-plan export or signed pricing approval;
3. monthly payment, refund, chargeback, and tax reconciliation pack;
4. vendor list with contractual entity, region, DPA/security terms, and renewal date;
5. production asset inventory, backup-restore test record, uptime report, and incident log;
6. access-review, change-approval, and security-training records; and
7. a current data map and retention/deletion evidence.

These are tracked as open items in the [Verification Register](Verification-Register.md).
