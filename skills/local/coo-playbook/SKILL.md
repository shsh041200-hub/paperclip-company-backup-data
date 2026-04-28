---
name: "coo-playbook"
description: "COO specialty playbook — vendor onboarding SOP and takedown procedure pointer for the Packlinx packaging directory. Read before onboarding a new vendor or handling a takedown request."
slug: "coo-playbook"
metadata:
  paperclip:
    slug: "coo-playbook"
    skillKey: "local/ad66b86163/coo-playbook"
  paperclipSkillKey: "local/ad66b86163/coo-playbook"
  skillKey: "local/ad66b86163/coo-playbook"
key: "local/ad66b86163/coo-playbook"
---

# COO Playbook

Specialty bundle for the Packlinx COO role. Covers two recurring operational
artifacts: the vendor onboarding SOP and the takedown procedure.

Common skills handle voice, encoding, decision protocol, and company context.
Do not duplicate that content here.

## When to invoke this skill

- Onboarding a new vendor onto the directory
- Receiving a takedown request (vendor, third party, regulator)
- Reviewing vendor-data quality issues
- Updating either SOP

## Part 1 — Vendor onboarding SOP

The directory's value is **verified vendor density in the right categories**.
An empty directory is worse than no directory; a directory full of
unverified vendors is worse than empty. This SOP encodes the floor.

### When this SOP applies

- Inbound vendor signup (vendor self-served)
- Outbound vendor recruitment (we contacted them)
- Vendor profile import from a partner list

### Step 0 — Pre-check (before any data entry)

- [ ] Vendor business registration number (사업자등록번호) provided.
- [ ] Verified format (10 digits, valid checksum). Reject malformed.
- [ ] Vendor category fits the directory's current scope. If not, either
      add the category (CEO decision) or politely decline.
- [ ] No active dispute or takedown record on the vendor.

### Step 1 — Identity verification

- [ ] Business registration looked up via 국세청 / 공공데이터 portal.
      Match name, address, status (active / closed / suspended).
- [ ] Active status confirmed within last 30 days. Reject closed or
      suspended.
- [ ] Industry code matches our category mapping. Mismatch → flag for
      review, do not auto-publish.
- [ ] Domain ownership verified (DNS TXT record, email at the vendor's
      domain, or signed letter). At least two of three.

### Step 2 — Profile content

- [ ] Vendor name in Korean (legal name) + display name (if different).
- [ ] At least one product / service category claim, with evidence.
- [ ] Capabilities: production volume, lead time, MOQ. Numeric where
      possible. "큼 / 빠름 / 유연" without numbers is rejected.
- [ ] Certifications listed: FSSC 22000, ISO 9001, KS marks — each
      requires a document upload or a regulator-portal link.
- [ ] Contact channel: at least one verifiable phone + one verifiable
      email at the verified domain.
- [ ] Address geocoded. Map pin matches the address.

### Step 3 — Content quality pass

- [ ] No duplicate copy stamped from another vendor (run similarity check
      against existing profiles). Threshold: < 60% similarity.
- [ ] Korean copy passes editorial pass (see `packlinx-comms` voice rules
      for user-facing surfaces).
- [ ] Images: vendor-supplied or verified-stock. No copyrighted
      third-party imagery without license. Image filenames ASCII.
- [ ] No pricing claims that we can't verify within 7 days.

### Step 4 — Publish decision

- **Auto-publish allowed when:** all of Steps 0–3 pass clean, no flags,
  no manual-review tags.
- **Manual review required when:** any flag, any cert claim that lacks a
  document, any category mismatch.
- **Reject when:** Step 0 fails, identity verification fails, or duplicate
  copy detected at > 60% similarity.

### Step 5 — Post-publish observation window

- 7 days of "verified — recently added" badge.
- Daily check for: takedown signals, contact-form abuse, profile edits
  that re-introduce rejected content.
- After 7 days, badge transitions to standard "verified" if no issues.

### Audit trail

Every step logs to the vendor's audit record:

- Who acted (agent or board member)
- What changed (field-level diff)
- Why (link to evidence)
- When (timestamp, UTC + KST)

The audit trail is the legal artifact when a dispute arises. Treat it as
production data, not internal notes.

### Refusals

- Refuse to publish a vendor who fails identity verification, regardless
  of how complete the rest of the profile is.
- Refuse to accept "verification pending — we'll add it later." Either
  it's verified or it isn't.
- Refuse vendor pressure to bypass any step. The directory's trust is
  the moat; one fake vendor erodes it permanently.
- Refuse to onboard direct competitors of Packlinx as vendors. Conflict
  of interest disclosure required, CEO sign-off, or decline.

## Part 2 — Takedown procedure

A takedown request is a high-priority, time-bounded operation. Mishandling
a legitimate request is a legal exposure; mishandling a fraudulent one
erodes vendor trust. Both fail loudly.

### Categories (different procedures per category)

| Category | Examples | Default response window |
| --- | --- | --- |
| **Vendor self-takedown** | Vendor wants their profile removed | 48h, no questions |
| **Trademark / IP** | Brand owner claims unauthorized use | 7d, evidence-gated |
| **Defamation / false claims** | Vendor or third party claims false content | 14d, escalate to LegalCounsel |
| **Regulatory** | KFTC / KCC / 식약처 letter | 24h acknowledgement, deadline per letter |
| **Personal data (PIPA)** | Individual requests removal of personal info | 5d, evidence-gated |

### Universal first 60 minutes

Whatever the category:

1. **Acknowledge receipt** within 1h via the requestor's channel.
   Confirm: who they are, what they request, evidence they've sent.
2. **Open a takedown ticket** with priority = high, assign per category.
   Link to the affected vendor profile / page.
3. **Snapshot the disputed content** (full HTML, screenshots, image
   files) into the takedown ticket as attachments. This is the legal
   record of what existed at request time.
4. **Notify chain of command:** CEO + LegalCounsel cc'd on the ticket.

Do **not** remove content in the first 60 minutes unless the request is a
self-takedown or regulatory letter with a same-day deadline. Premature
removal eliminates evidence and may not be required.

### Decision matrix

- **Clearly valid request** (self-takedown, regulatory letter, signed
  trademark notice with registration number) → execute removal, log,
  notify requester within window.
- **Plausible but unverified** → hold content live, request specific
  evidence, set deadline = window minus 24h. If no evidence by deadline,
  decline in writing with reason.
- **Frivolous or harassing** (no evidence, repeat fraudulent requests,
  competitor pretending to be brand owner) → decline, log pattern,
  notify LegalCounsel for repeat-offender file.

### Removal mechanics

When removing:

- [ ] Replace page with a tombstone (HTTP 410) explaining "removed at
      request" — no detail on requester.
- [ ] Update sitemap.xml to drop the URL.
- [ ] Submit removal in Naver Search Advisor + Google Search Console.
- [ ] Clear caches (Vercel + Cloudflare if applicable).
- [ ] Log removal in vendor audit trail with the takedown ticket link.
- [ ] Email the vendor (if not the requester) with the action taken,
      reason category, and how to appeal.

### After-action review

For every takedown that reaches removal: write a 1-paragraph after-action
in the takedown ticket. What happened, how long it took, what the next
similar request should learn. This is how the SOP gets sharper over time.

### Escalation triggers

Pull LegalCounsel in immediately when:

- The request is from a regulator (any 부 / 청 / 위원회).
- The request alleges criminal liability (사문서위조, 사기, 명예훼손).
- A second request arrives on the same vendor within 30 days.
- The request asks for action outside our jurisdiction.

Pull the CEO in when:

- A removal would substantially affect a top-50 vendor.
- A pattern of takedowns suggests a category-level issue (we're publishing
  a class of content that keeps getting flagged).

## Self-check before publishing a vendor or actioning a takedown

- [ ] Can I point to evidence for every claim on this vendor's profile?
- [ ] If a regulator audited this onboarding tomorrow, would the audit
      trail satisfy them?
- [ ] On takedown: am I within the response window, and is the requester
      acknowledged?
- [ ] Have I logged the action in a way the next COO heartbeat can pick
      up cleanly?
