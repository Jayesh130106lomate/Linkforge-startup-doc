# Product Overview: LinkForge SaaS

---

**Document status:** reported product scope. Validate feature availability, plan entitlements, and operational behaviour against a dated release and the live product before making a customer commitment.  
**Last reviewed:** 21 October 2026

---

## 1. Product Description & Purpose

**LinkForge** is a multi-tenant SaaS application that brings campaign link management, smart destination routing, dynamic vector QR codes, creator bio pages, and privacy-focused analytics into a single, cohesive workflow.

It serves as the day-to-day link operations hub for marketing teams and agencies that deploy and manage client traffic across paid advertising, printed collateral, social media, and offline events.

---

## 2. Core Feature Modules

### 2.1 Branded URL Shortener & Link Operations
- **Custom Slugs & Aliases**: Create branded, memorable short links on the shared platform domain or your own verified custom domains.
- **UTM Campaign Builder**: Automatically attach standard UTM parameters (`utm_source`, `utm_medium`, `utm_campaign`, `utm_term`, `utm_content`) to destination URLs.
- **Access Protection & Cloaking**: Protect sensitive links with passwords or unlock gates without exposing raw target destinations.
- **Link Scheduling & Expiration**: Set automatic activation and expiration dates; expired links route visitors to an accountable fallback URL.
- **Tagging & Organization**: Group and filter links by client, campaign, or marketing channel.

### 2.2 Dynamic Vector QR Code Studio
- **Dynamic Target Editing**: Update the destination URL at any time without reprinting packaging, flyers, or business cards.
- **Vector & High-Resolution Export**: Download production-ready QR codes in SVG, PNG, and PDF formats for commercial printing.
- **Visual Customization**: Customize colors, corner square (eye) styling, and embed company logos with built-in error-correction tolerance.
- **Dedicated Scan Analytics**: Track offline print scans separately from direct browser clicks.

### 2.3 Smart Link Routing Engine
- **Device & OS Targeting**: Route visitors to specific destination URLs based on their operating system (iOS, Android, Windows, macOS, Linux). Ideal for mobile app promotions.
- **Geographic Routing**: Send visitors to country-specific storefronts or localized pages based on their country.
- **Referrer Routing**: Deliver specialized landing pages depending on where the visitor clicked the link.
- **Fallback Guarantees**: Every rule includes a default fallback URL to ensure visitors never land on a broken link.

### 2.4 Creator Bio Link Pages ("Link in Bio")
- **Drag-and-Drop Page Builder**: Arrange links, social icons, text cards, and headers using intuitive drag-and-drop reordering powered by `@dnd-kit`.
- **Custom Themes**: Choose from pre-designed color palettes or customize fonts, card borders, and backgrounds.
- **Custom Domain Attachment**: Connect creator bio pages directly to custom root domains or subdomains.
- **Page-Level Analytics**: Review page views, link clicks, and individual block click-through rates (CTR).

### 2.5 Custom Branded Domains
- **Cloudflare for SaaS Integration**: Simple CNAME-based setup pointing to `cname.linkforge.site`.
- **Automated SSL/TLS Certificates**: Automatic certificate provisioning and renewal.
- **Real-Time Verification**: DNS verification checks and diagnostic feedback in the dashboard.

### 2.6 Cookieless, Privacy-Safe Analytics
- **Cryptographic IP Anonymization**: Visitor IPs are hashed immediately with SHA-256 and a secret server pepper (`IP_HASH_PEPPER`). Raw IP addresses are never permanently saved.
- **Cookie-minimised tracking design**: The documented design avoids persistent analytics cookies and hashes IP-derived identifiers before storage. Legal obligations and consent requirements require separate review for the applicable deployment and jurisdiction.
- **Bot & Spider Filtering**: Automatically detects and filters web crawlers and automated bots to keep click counts accurate.
- **Detailed Breakdowns**: Reports by country, city, referrer, device, browser, operating system, and UTM parameters.
- **Private CSV Exports**: Asynchronous CSV report generation processed by background workers without silent row truncation.

---

## 3. User Personas & Use Cases

```
┌────────────────────────────────────────────────────────────────────────┐
│                        LinkForge Target Personas                       │
└────────────────────────────────────────────────────────────────────────┘
          │                                  │
          ▼                                  ▼
┌──────────────────┐               ┌──────────────────┐
│ Digital Agencies │               │ Content Creators │
└──────────────────┘               └──────────────────┘
  • Multi-client workspaces          • Mobile bio landing pages
  • Branded custom domains           • Link-in-bio monetization
  • Dynamic print QR codes           • Social click attribution
  • Campaign export reports          • Clean custom aesthetics
```

### Use Case 1: Agency Print & Packaging Campaigns
An agency prints QR codes on 10,000 product packages for a retail launch. When the landing page needs an update a month later, the team updates the destination inside LinkForge without having to recall or reprint physical packaging, while tracking scan counts by city and device.

### Use Case 2: Multi-Platform App Promotion
A performance marketer runs ads across social platforms for a mobile app. A single smart link directs iPhone users to the App Store, Android users to Google Play, and desktop visitors to a web product demo.

### Use Case 3: Creator Campaign Aggregation
A creator consolidates YouTube videos, podcast episodes, newsletter signups, and sponsor links onto a branded bio page (`bio.creatorbrand.com`), monitoring weekly click-through rates across each link.

---

## 4. Current Status & Known Operational Boundaries

- **Reported deployment status**: Early-stage production deployment. This repository contains no deployment record or release evidence; confirm before publishing this status.
- **Redirect performance objective**: The architecture is designed to use Cloudflare Workers and Redis caching for a sub-50ms redirect target. A target is not a measured or contractual guarantee.
- **Operational Boundaries**:
  - **Payment and billing**: The commercial documentation describes a Dodo Payments integration. Confirm live checkout, invoices, taxes, renewals, cancellations, and refunds with a dated reconciliation before selling it as available.
  - **Public API**: Internal REST routes are reported, but public documentation, customer key management, supported use cases, rate limits, and support terms are not yet published.
  - **Enterprise identity**: Managed enterprise SSO (SAML/Okta) is planned, not available unless a release record says otherwise.

### Before a Feature Is Sold or Announced

Confirm the following for the exact plan and deployment environment: customer-visible UI, entitlement rule, success and failure path, analytics effect, data retention, support ownership, rollback path, and published policy impact. Record the result in the [Verification Register](../00-Governance/Verification-Register.md).

---

## 5. Document Cross-References

- For the detailed feature status breakdown and roadmap priorities, see [Features and Roadmap](Features-and-Roadmap.md).
- For documented pricing and entitlements, see [Pricing and Revenue](../04-Business-Growth/Pricing-and-Revenue.md).
- For reported architecture and data flow, see [Architecture and Tech Stack](../03-Technology/Architecture-and-Tech-Stack.md).
