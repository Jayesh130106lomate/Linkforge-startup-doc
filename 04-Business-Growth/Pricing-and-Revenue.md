# Pricing and Revenue: LinkForge

---

**Document status:** commercial proposal and internal entitlement reference. Prices, payment methods, discounts, tax treatment, and limits must be reconciled with the live checkout, payment-provider account, and published terms before customer use.  
**Last reviewed:** 21 October 2026

---

## 1. Commercial Pricing Strategy

LinkForge's documented commercial model is freemium SaaS with regional purchasing-power pricing for domestic and international markets. This section describes the intended offer; it is not proof of the current checkout catalog.

The intended checkout design uses **Dodo Payments** as Merchant of Record, subject to the executed agreement and live account configuration:
- **India Region (`IN`)**: Billed in Indian Rupees (₹ INR) supporting UPI, domestic debit/credit cards, and netbanking.
- **Rest of World Region (`ROW`)**: Billed in US Dollars (\$ USD) supporting major international credit cards and digital wallets.

---

## 2. Documented Subscription Plans Matrix

The annual amounts below are approximately **16.7% lower** than twelve monthly payments. Confirm any discount representation against the live product catalog before publication.

### Pricing by Region

| Plan Tier | India (Monthly) | India (Annual) | Global (Monthly) | Global (Annual) | Target Audience |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Free** | ₹0 | ₹0 | \$0 | \$0 | Testing, evaluation, individual links |
| **Starter** | ₹149 / mo | ₹1,490 / yr *(₹124/mo eq.)* | \$4.50 / mo | \$45 / yr *(\$3.75/mo eq.)* | Solo creators, freelancers |
| **Pro** | ₹799 / mo | ₹7,990 / yr *(₹666/mo eq.)* | \$24 / mo | \$240 / yr *(\$20/mo eq.)* | Small marketing teams, growth brands |
| **Business** | ₹3,499 / mo | ₹34,990 / yr *(₹2,915/mo eq.)* | \$79 / mo | \$790 / yr *(\$65.83/mo eq.)* | Full-service marketing agencies |

---

## 3. Comprehensive Plan Entitlements & Limits

The following table is the documented entitlement proposal. A versioned live-plan export or automated entitlement test is required before it can be described as the exact production configuration.

| Feature / Limit | Free Tier | Starter Tier | Pro Tier | Business Tier |
| :--- | :--- | :--- | :--- | :--- |
| **Active Short Links** | 10 | 125 | 1,250 | 5,000 *(expandable)* |
| **Custom Branded Domains** | 0 | 1 | 5 | 12 *(expandable)* |
| **Dynamic QR Code Campaigns** | 2 | 7 | 35 | 100 *(expandable)* |
| **Smart Routing Rules (per link)** | 0 (Disabled) | 0 (Disabled) | 8 rules | 16 rules *(expandable)* |
| **Creator Bio Pages** | 1 page | 2 pages | 15 pages | 45 pages |
| **Max Blocks per Bio Page** | 8 blocks | 15 blocks | 60 blocks | 100 blocks |
| **Bio Page Branding Removal** | No (LinkForge logo) | Yes | Yes | Yes |
| **Bio Page Custom Themes** | No | Yes | Yes | Yes |
| **Monthly Tracked Events** | 1,000 | 7,500 | 50,000 | 250,000 *(expandable)* |
| **Raw Event Retention** | 7 days | 30 days | 90 days | 365 days |
| **Aggregated Data Retention** | 30 days | 90 days | 365 days | 730 days |
| **Advanced Analytics & CSV Export** | No | No | Yes | Yes |
| **Two-Factor Auth (Email 2FA)** | No | Yes | Yes | Yes |
| **Daily AI Copilot Credits** | 20 credits | 50 credits | 250 credits | 1,000 credits |
| **Bulk CSV Link Import** | Disabled | 1,000 rows / import (10/day) | 5,000 rows / import (50/day) | 25,000 rows / import (200/day) |
| **Customer Support Tier** | Community Support | Standard Support | Priority Support | Dedicated Support |
| **Target Resolution Time** | 72 hours | 24 hours | 4 hours | 1 hour (critical issue) |

> **Commercial boundary:** high-volume expansions, support response, retention, and service credits are available only when they are documented in the current customer contract or order form. The values in this document are not a standalone contractual offer.

---

## 4. Expansion Revenue & Add-On Catalog

The intended add-on catalogue allows resource scaling without a full tier upgrade. Confirm availability, price, tax, renewal, and cancellation behaviour before sale:
- **Additional Custom Domains**: Monthly add-on slots for agencies managing extra client domains.
- **Active Link Packs**: Incremental link volume allocations.
- **Creator Bio Page Packs**: Additional bio landing page slots.
- **Event Tracking Buffer**: 10% grace buffer enforced on event limits before redirects pause, allowing uninterrupted campaign operation.

---

## 5. Billing Infrastructure & Provider

- **Payment-provider role:** Dodo Payments publishes Merchant-of-Record services, but LinkForge's account configuration and contractual allocation of responsibility must be retained as evidence.
- **Tax and invoicing:** Tax collection/remittance and invoice issuer must be confirmed from the executed payment agreement and a redacted live invoice. Merchant-of-Record support does not remove the need for LinkForge to confirm its own Indian tax obligations.
- **Webhook handling:** Signature verification, idempotency, retries, reconciliation, and manual recovery should be demonstrated by a dated test/reconciliation record before being treated as production controls.
- **Entitlement Promotion Engine**:
  - The platform includes a promotional coupon system (`model Promotion`) allowing marketing campaigns to provide trial extensions or temporary plan discounts.
  - Super Administrators can issue temporary time-bounded promotional entitlements (`model WorkspaceEntitlement`) with mandatory audit reason logging.

---

## 6. Current Revenue & Traction Status

- **Monetization Status**: **Early-Stage SaaS; Revenue Figures Not Yet Verified**.
- **Customer Acquisition**: LinkForge has acquired its first registered user following initial product testing and outreach.
- **Financial Metrics**:
  - To maintain factual accuracy, **no estimated or placeholder revenue figures are documented**.
  - Current revenue ledgers, active paying subscriber counts, and churn rates will be formally documented once verified against actual payment gateway statements.
  - End-to-end checkout, payment reconciliation, and subscription renewal flows are currently undergoing final operational validation before scaling commercial customer acquisition.

---

## 7. Commercial Operating Records Still Required

Maintain a monthly reconciliation pack with the following fields: catalog version, gross collections, refunds, chargebacks, failed renewals, tax shown on invoices, provider fees, active paid subscriptions, entitled workspaces, and exceptions/manual adjustments. The pack should identify the preparer, reviewer, period close date, and links to source exports.

Before changing any price or limit, record: affected region, currency, effective date, existing-customer treatment, tax display, cancellation/refund treatment, checkout test, communication plan, and owner. Link the change to the [Verification Register](../00-Governance/Verification-Register.md).
