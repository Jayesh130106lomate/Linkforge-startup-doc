# Registration and Compliance: LinkForge Technologies

---

**Document status:** the Udyam certificate fields are verified from the preserved PDF. Tax, privacy, vendor, policy, trademark, and service-level content is an operating record or planned position requiring the evidence in the [Compliance Action Register](Compliance-Action-Register.md).  
**Last reviewed:** 21 October 2026  
**Important:** this document is not legal or tax advice.

---

## 1. Legal Entity & Operating Structure

The preserved Udyam certificate identifies the enterprise as `LINKFORGE` and prints the registration fields below. It does not itself evidence the legal trading name “LinkForge Technologies”, current GST status, customer policies, or vendor contracts:

| Legal Parameter | Verified Startup Record |
| :--- | :--- |
| **Enterprise name on certificate** | **`LINKFORGE`** |
| **Legal trading name used in this repository** | LinkForge Technologies *(needs an authoritative tax, bank, or other record before external reliance)* |
| **Legal form / proprietor** | Sole proprietorship / Jayesh Lomate *(reported internal information; retain supporting record for due diligence)* |
| **Operating location / public contacts** | Pune, Maharashtra; `legal@linkforge.site`; `hello@linkforge.site` *(reported contacts; verify ownership and response coverage before publication)* |

---

## 2. MSME / Udyam Government Registration

LinkForge holds an official Udyam Registration Certificate issued by the Ministry of Micro, Small and Medium Enterprises (MSME), Government of India:

| Registration Parameter | Official Registration Detail |
| :--- | :--- |
| **Udyam Registration Number** | **`UDYAM-MH-24-0085874`** |
| **Date of Incorporation / Registration** | **1 February 2026 (01/02/2026)** |
| **Date of Business Commencement** | **5 February 2026 (05/02/2026)** |
| **Date of Udyam Registration** | **6 February 2026 (06/02/2026)** |
| **Enterprise Name on Certificate** | **`LINKFORGE`** |
| **Name of Registered Unit(s)** | `LinkForge` |
| **Enterprise Classification** | **Micro Enterprise** *(Classified for Year 2025-26 on 06/02/2026 and Year 2026-27 on 14/04/2026)* |
| **Major Activity on Record** | **Trading** *[For availing benefits of Priority Sector Lending (PSL) ONLY]* |
| **Social Category of Entrepreneur** | General |
| **Registered Address on Certificate** | • **Flat/Door/Block**: Hipparga Rava<br>• **Premises/Building**: Hipparga Rava<br>• **Village/Town**: Hipparga Rava<br>• **Block**: Hipparga Rava<br>• **Road/Street**: Lohara<br>• **City**: Pune<br>• **District**: Osmanabad, Pin: 413608<br>• **State**: Maharashtra |
| **Address Discrepancy Note** | The certificate lists Lohara (located in Osmanabad/Dharashiv district) alongside Pune as the city. This entry reflects the official government certificate as printed and is noted for routine portal reconciliation. |
| **Official Email on Certificate** | `jayeslomate@gmail.com` |
| **District Industries Centre (DIC)** | Osmanabad, Maharashtra |
| **MSME Development Office** | MSME-DFO Mumbai, Maharashtra |
| **National Industry Classification (NIC)** | • **`62012`**: Web-page designing (Activity: Services)<br>• **`63121`**: Operation of web portals that use search engines to generate and maintain extensive databases of internet addresses and content in an easily searchable format (Activity: Services)<br>• **`62099`**: Other information technology and computer service activities n.e.c (Activity: Services) |
| **Certificate Document** | The original, official 2-page PDF certificate is stored at [Certificates/UDYAM-MH-24-0085874-LinkForge-Udyam-Registration-Certificate.pdf](Certificates/UDYAM-MH-24-0085874-LinkForge-Udyam-Registration-Certificate.pdf). |

---

## 3. Tax & Regulatory Status

- **PAN & GSTIN:** The Udyam certificate does not establish an active GSTIN, registration exemption, PAN status, or filing requirement. Confirm the actual business model, turnover, supply location, and registration position with a qualified Indian tax adviser; keep the decision and review date in the [Compliance Action Register](Compliance-Action-Register.md).
- **Payment-provider / Merchant-of-Record role:** Dodo Payments publishes Merchant-of-Record services, but LinkForge's executed agreement, account configuration, invoice issuer, refund/chargeback responsibilities, and tax allocation must be verified from the actual records. Do not assume that a payment-provider capability resolves LinkForge's own tax or legal obligations.

---

## 4. Privacy, Data Protection & Regulatory Compliance

The product documentation describes privacy-oriented technical practices. Whether those practices meet a specific legal requirement depends on the deployed data flows, contracts, customer role, locations, and applicable law. Complete the evidence in the [Compliance Action Register](Compliance-Action-Register.md) before describing the service as compliant.

### 4.1 General Data Protection Regulation (GDPR - EU/UK)
- **Data minimisation (design intent):** collect only data needed for link routing, account operations, support, security, and reporting. The actual field inventory, legal basis, and retention need to be documented and reviewed.
- **Cookies and consent:** the documented design avoids persistent analytics cookies. Confirm every first- and third-party script, cookie, embedded service, and jurisdiction-specific consent requirement before making a public statement about banners or consent.
- **IP-derived data:** the documented design hashes IP-derived identifiers with a server-side secret. Confirm proxy, application, logging, monitoring, and vendor behaviour before stating that raw IP addresses are never retained.
- **Deletion and rights requests:** confirm the customer deletion flow, backup expiry, export, identity verification, and statutory handling process before promising a specific right or timeframe.

### 4.2 California Consumer Privacy Act (CCPA)
- **Sale/share restrictions (policy target):** the intended policy is not to sell or rent customer or visitor personal data. An approved policy and vendor/data-flow review are required before publishing this statement.
- **Browser privacy signals:** confirm detection, treatment, and policy disclosure for Do Not Track (DNT) and Global Privacy Control (GPC) signals before asserting that they are honoured.

---

## 5. Sub-Processor & Third-Party Vendor Data Register

The following is a reported vendor architecture inventory, not a completed legal sub-processor register. Verify contractual entity, processing role, data categories, storage/processing locations, DPA, security terms, and review date for every enabled vendor:

| Vendor / Provider | Entity & Jurisdiction | Function in Architecture | Data Processed & Storage Region |
| :--- | :--- | :--- | :--- |
| **Cloudflare, Inc.** | United States (Global Edge) | Anycast DNS, Edge Workers, Cloudflare for SaaS, R2 object storage, Turnstile bot protection | Anonymized request headers, visitor country codes, encrypted edge cookies, public assets; Global edge network. |
| **Vercel, Inc.** | United States | Next.js web application and dashboard serverless hosting | Authenticated user session data, application API requests, dashboard traffic; US / Global serverless regions. |
| **Managed PostgreSQL Provider** | United States / Regional Cloud | Primary relational database | User credentials (Argon2 hashed), workspace data, link configurations, aggregated analytics rollups; Regional cloud data centers. |
| **Managed Redis Provider** | United States / Regional Cloud | Ephemeral in-memory caching and BullMQ job broker | Edge redirect cache keys, API rate-limiting token buckets, temporary click event buffers; Ephemeral storage. |
| **Resend, Inc.** | United States | Transactional email delivery service | User email addresses, authentication codes, password reset tokens, security notifications; United States. |
| **Dodo Payments, Inc.** | Jurisdiction/regions to confirm from executed agreement | Reported Merchant-of-Record and payment service | Customer billing and subscription data as configured. Dodo publishes PCI DSS information; this is a vendor claim, not a LinkForge certification, and the enabled scope must be verified. |
| **Google LLC** | United States | Google Web Risk threat scanning & Google OAuth | Target destination URLs submitted for safety scanning, user Google OAuth profile tokens; United States. |

---

## 6. Platform Legal Policies & Governance

The following routes and contents are reported from prior documentation. Before relying on them, archive the live copy, record its version/effective date, obtain required approval, and update the policy register in the [Compliance Action Register](Compliance-Action-Register.md):

### 6.1 Terms of Service (`/terms`)
- **Required contents:** operating entity, account ownership, acceptable use, subscription/renewal, cancellation/refund, limitation of liability, dispute process, and effective date.
- **Verification need:** no signed or archived policy version is held in this repository.

### 6.2 Privacy Policy (`/privacy`)
- Must accurately describe deployed data collection, IP/logging behaviour, cookies, vendor/sub-processor list, customer/visitor rights channels, retention, and contact information.

### 6.3 Acceptable Use Policy & Abuse Reporting (`/acceptable-use`)
- **Required contents:** prohibited conduct, reporting channel, investigation standard, suspension/appeal process, and lawful notice handling.
- **Verification need:** confirm public reporting route, scanner coverage, moderator access, notice templates, and appeal ownership.

### 6.4 Service Level Agreement (SLA)
- Any availability target, exclusion, measurement method, support scope, and credit remedy must be explicitly stated in the signed customer agreement. The operational 99.9% target is not independently evidenced or a binding commitment in this repository.

---

## 7. Trademark & Intellectual Property (IP) Strategy Tracker

To protect the LinkForge brand equity in India and international SaaS markets, the business follows this IP registration roadmap:

### 7.1 Target Trademark Classes (India - CGPDTM)
- **Class 9**: Downloadable software, mobile applications, computer programs for link redirection, dynamic QR generation, and analytics data visualization.
- **Class 42**: Software-as-a-Service (SaaS), cloud computing services, hosting website links, URL shortener platforms, and online non-downloadable marketing software.

### 7.2 Filing Preparation & Concession Status
- **Potential fee category:** IP India lists a lower TM-A filing fee for an individual, startup, or small enterprise. Confirm the applicant/category, document evidence, classes, and current fee immediately before filing; do not assume eligibility solely from this register.
- **Specimen of Use**: Live marketing website screenshots, production dashboard captures, and domain registration WHOIS records dating back to incorporation (February 2026).

### 7.3 Trademark Filing Progress Table

| Mark & Type | Target Class(es) | Filing Stage | Official App Number | Current Status |
| :--- | :--- | :--- | :--- | :--- |
| **LinkForge** *(Word Mark)* | Class 9, Class 42 | Pre-filing Search Completed | Pending Filing | Ready for formal filing |
| **LinkForge Logo** *(Device Mark)* | Class 9, Class 42 | Vector Asset Finalized | Pending Filing | Asset prepared for submission |

---

## 8. Coordinated Vulnerability Disclosure Policy (VDP)

LinkForge values the contributions of the security research community in identifying potential vulnerabilities in our web surfaces and edge network.

### 8.1 Reporting Channel & Guidelines
- Security researchers who discover potential vulnerabilities are requested to email **`abuse@linkforge.site`** or **`legal@linkforge.site`** with detailed reproduction steps.
- **Safe Harbor**: LinkForge will not pursue legal action against researchers who act in good faith, avoid privacy violations, prevent service disruption, and give LinkForge reasonable time to remediate issues before public disclosure.
- **Out of Scope**: Distributed Denial of Service (DDoS), social engineering, automated credential stuffing, and spamming.

### 8.2 Vulnerability-Response Targets
- **Initial acknowledgement target:** within 24 hours of submission.
- **Triage/validation target:** within 72 hours of report receipt.
- **Remediation target:** prioritise critical findings for expedited remediation; do not promise a fixed patch date unless it is supported by staffing, testing, and customer-impact assessment.

These targets must be reviewed against the active on-call/support model and are not a bug-bounty, safe-harbour, or contractual commitment without an approved policy.

---

## 9. Outstanding Compliance & Administrative Actions

1. **Udyam Address Portal Check**: Cross-check the Udyam portal to resolve the Pune / Osmanabad district notation and confirm whether an amended certificate is required.
2. **GST Registration Review**: Confirm the current registration threshold and other registration triggers for the actual supply model with a qualified Indian tax adviser; monitor the relevant turnover and transaction conditions using that advice.
3. **Trademark Application Submission**: Submit formal online applications for the "LinkForge" word mark under Classes 9 and 42 utilizing the MSME statutory fee concession.
4. **Approved Policy Archive**: Store current and superseded versions of the Terms, Privacy Policy, Acceptable Use Policy, cancellation/refund policy, and DPA with approval/effective dates.
5. **Data and Vendor Evidence:** Complete the data map, vendor DPA/region review, deletion test, and access-control evidence in the [Compliance Action Register](Compliance-Action-Register.md).
