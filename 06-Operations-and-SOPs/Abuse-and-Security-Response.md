# Standard Operating Procedure: Abuse & Security Response

---

**Document status:** target trust-and-safety procedure. The listed automation, inboxes, administrative routes, and response times must be confirmed from the deployed product and operating records before being described as active controls or contractual commitments.  
**Last reviewed:** 21 October 2026

---

## 1. Purpose & Guiding Principles

As a high-throughput link management and dynamic QR platform, LinkForge's shared redirect domains (`go.linkforge.site`) and custom edge infrastructure are critical operational assets. Preserving their clean reputation across global threat feeds (Google Safe Browsing, Spamhaus, Microsoft SmartScreen) is essential for customer campaign deliverability.

This Standard Operating Procedure (SOP) governs how LinkForge detects, investigates, and mitigates abusive links, malware distribution, phishing campaigns, and security vulnerabilities.

---

## 2. Ingestion Channels for Abuse Reports

LinkForge provides three intake vectors for security researchers, automated crawlers, and the general public:

1. **Public Abuse Form**: Accessible at [`/acceptable-use`](https://www.linkforge.site/acceptable-use) with automated Cloudflare Turnstile bot verification.
2. **REST Ingestion API**: Reported endpoint: `/api/abuse-reports`, with request validation and rate limiting. The source repository is not included here; confirm route availability, authentication, retention, and alerting before publication.
3. **Designated Security Inbox**: Direct reports sent to `abuse@linkforge.site`. Inbound emails trigger immediate automated alerts to platform administrators (`ABUSE_ALERT_EMAIL`).

---

## 3. Automated Threat Detection Pipeline

Before human review, links pass through real-time automated safety gates:

```
[ Link Creation / Update / Route Modification ]
                       │
                       ▼
         [ Google Web Risk Threat Scan ]
  - Scans destination URL against Google Web Risk API
  - Checks for:
      • MALWARE (Drive-by downloads, ransomware)
      • SOCIAL_ENGINEERING (Credential phishing)
      • UNWANTED_SOFTWARE (Bundled installers)
                       │
       ┌───────────────┴───────────────┐
       ▼                               ▼
[ Threat Confirmed ]           [ Clean Destination ]
- Instant rejection            - Short link saved
- User notified with error     - Edge cache populated
- Alert logged to safety queue
```

*Implementation note: prior internal documentation references a safety module. Retain a current code reference, test result, and vendor configuration record before describing the pipeline as active.*

---

## 4. Administrative Moderation SOP (`/admin/moderation`)

Platform moderators and administrators access the dedicated moderation queue inside the administrative portal:

### 4.1 Triage Lifecycle
Each report progresses through defined database statuses:
* **`OPEN`**: Newly received report awaiting initial human inspection.
* **`INVESTIGATING`**: Case assigned to a moderator; destination URL sandbox testing underway.
* **`RESOLVED`**: Abusive link suspended, destination permanently blacklisted, or reporter acknowledged.
* **`DISMISSED`**: Report reviewed and confirmed as benign, competitive harassment, or an uncorroborated claim.

### 4.2 Immediate Mitigation Actions
When investigating an active report:
1. **Analyze Destination**: Open the destination link in an isolated browser sandbox (never on an internal corporate network). Inspect for credential phishing login forms, deceptive branding, or automated payload downloads.
2. **Execute Link Suspension**:
   - In the moderation panel, click **"Suspend Link"**.
   - The platform immediately invalidates the Redis edge cache entry.
   - Any visitor accessing the link is redirected to a security warning interstitial stating: *"This link has been suspended due to violations of LinkForge Acceptable Use Policy."*
3. **Workspace Quarantine**:
   - If an account has generated multiple phishing links or high-velocity bot traffic, change the workspace status to `SUSPENDED`.
   - All active links belonging to the workspace are immediately deactivated.
4. **Internal Audit Documentation**:
   - Add a mandatory note (`POST /api/admin/abuse-reports/[id]/notes`) detailing the rationale, sandbox findings, and action taken for legal audit compliance.

---

## 5. False Positive Appeals & Reinstatement Protocol

Legitimate customers whose destinations are mistakenly flagged by threat intelligence feeds can appeal the suspension:

1. **Submission**: The account owner emails `support@linkforge.site` with the subject *"Appeal: Link Suspension - [Short Code]"*.
2. **Verification Requirements**:
   - Proof of destination ownership (e.g., DNS TXT verification or official business domain correspondence).
   - Clean scan report from independent reputation engines (VirusTotal, Google Search Console Security Issues).
3. **Appeal-review target**: Review within **4 business hours** where the reported support coverage permits. This is a target, not a guarantee or contractual SLA.
4. **Reinstatement Execution**:
   - The administrator removes the suspension in `/admin/moderation`.
   - The destination is whitelisted against false-positive triggers.
   - Redis edge cache is purged and repopulated.

---

## 6. Coordinated Vulnerability Disclosure & Safe Harbor

LinkForge actively welcomes responsible security vulnerability reports from independent researchers under our Coordinated Vulnerability Disclosure Policy:

* **Contact Channel**: Send findings to `abuse@linkforge.site` or `support@linkforge.site`.
* **Response targets**: Initial acknowledgement within **24 hours**; triage confirmation within **72 hours**. Confirm owner coverage and retain ticket evidence before publishing.
* **Safe Harbor Terms**: LinkForge will not initiate legal action against researchers who:
  - Act in good faith and avoid privacy violations, data destruction, or denial-of-service (DoS) attacks against our infrastructure.
  - Give our engineering team a reasonable window (minimum 30 days) to patch reported vulnerabilities before public disclosure.
  - Do not extort compensation or access user accounts without explicit permission.

---

## 7. Law Enforcement & Statutory Disclosures

LinkForge operates under the laws of the Republic of India:
* We do not provide customer metadata or account records to third parties without a valid, legally binding judicial order, court summons, or formal notice issued under the Bharatiya Nagarik Suraksha Sanhita (BNSS) / Information Technology Act, 2000.
* Emergency disclosures involving imminent risk of physical harm or child exploitation (CSAM) are escalated directly to the founder for immediate lawful compliance.

---

## 8. Evidence, Safeguards, and Review

For each abuse or vulnerability case, retain a minimal case record: report source, timestamps, affected link/workspace, classification, reviewer, evidence reference, action taken, customer notice, appeal outcome, and final disposition. Restrict access to need-to-know personnel and avoid storing raw malicious files or unnecessary reporter data in the case system.

Review monthly: reports received, time to triage, suspensions, appeals, false positives, repeat offenders, queue backlog, scan failures, and unresolved high-severity items. Test the suspension/appeal process at least quarterly using a controlled non-malicious destination.

Legal requests, preservation notices, CSAM, and credible threats to life require a documented escalation owner and qualified legal review. Do not promise disclosure, non-disclosure, or a response timeframe beyond what applicable law and the validated operating process require.
