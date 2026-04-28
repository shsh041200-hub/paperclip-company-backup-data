---
name: "cmo-playbook"
description: "CMO specialty playbook — content brief template and Korean B2B SEO playbook scoped to Naver-first acquisition for the Packlinx packaging directory. Read before commissioning content or proposing an SEO move."
slug: "cmo-playbook"
metadata:
  paperclip:
    slug: "cmo-playbook"
    skillKey: "local/b87bb79723/cmo-playbook"
  paperclipSkillKey: "local/b87bb79723/cmo-playbook"
  skillKey: "local/b87bb79723/cmo-playbook"
key: "local/b87bb79723/cmo-playbook"
---

# CMO Playbook

Specialty bundle for the Packlinx CMO role. Covers two recurring artifacts:
content briefs and the Korean B2B SEO playbook.

Common skills handle voice, language routing (Korean for users / English
internal), encoding, decision protocol. Do not duplicate that content here.

## When to invoke this skill

- Commissioning a new article, landing page, or comparison piece
- Proposing an SEO change (URL, schema, internal linking, sitemap)
- Reviewing a draft from an external writer or content agent
- Negotiating with Naver or Google about indexing issues

Skip for: small copy edits on existing pages, ad-hoc social posts.

## Part 1 — Content brief template

A brief that doesn't answer these questions sends a writer down the wrong
path. Fill all sections before assigning.

### Filename

`runs/<YYYY-MM-DD>-brief-<slug>.md` in the CMO workspace, plus a copy as
the `plan` document on the issue you're commissioning from.

### Brief template

```md
# Content Brief — <Title in target Korean phrasing>

**Target keyword (KO):** <exact phrase, with brackets — e.g., 「식품 포장재 업체 비교」>
**Search intent:** informational | transactional | navigational | comparison
**Stage of buyer journey:** awareness | evaluation | decision
**Primary surface:** Naver | Google | both
**Issue:** <PACAA-NN link>

## Why this piece

One sentence on the business outcome. "Capture buyers searching for X
who are 1–2 steps from a quote." If you can't state the outcome, kill
the piece.

## Target reader

- Role (procurement manager / SMB owner / startup operator)
- What they already know
- What they want to verify before contacting a vendor
- The specific decision this piece helps them make

## What the piece must answer

Bullet the 5–8 questions a real buyer asks. Order them by buyer priority,
not topical convenience. The writer must address each, in order.

## Required structural elements

- H1: target keyword in natural Korean phrasing (no awkward forced match)
- H2 sections, one per buyer question
- Comparison table when ≥3 vendor options exist
- One Packlinx-internal link to the relevant directory page or filter
- Author byline + reviewer credential when claim density is high
- FAQ block with 3–5 questions for FAQPage schema

## Tone

- Korean B2B conservative voice (see `packlinx-comms`)
- 존댓말, no slang, no exclamation points
- "정확합니다" / "확인되었습니다" / "권장합니다" — verifiable claims
- Cite sources for every numeric claim. Anonymized vendor sources OK,
  unsourced numbers are not.

## Length and format

- Target word count: <range, in Korean characters>
- Hero image: required | optional, with caption
- Internal images / charts: <list>

## Reading-stage CTA

What action should the reader take by the end of section 1, section 3,
end? The writer chooses copy; you specify the *action*.

## Out of scope (do NOT include)

- Speculation, opinion without source
- Marketing fluff, superlatives without numbers
- Competitor disparagement
- Pricing that we can't verify in the next 7 days

## Done when

- Editor has reviewed for tone and claim accuracy
- All Packlinx-internal links resolve
- Schema validates (Article + FAQPage when applicable)
- Hero image has Korean alt text, file name uses ASCII-only slug
- Encoding verified per `encoding-discipline` (UTF-8 NFC, no BOM)
```

### Briefs that fail

A brief without a verifiable target keyword, a buyer-journey stage, and a
business outcome is a wishlist, not a brief. Reject and re-scope before
spending writer hours.

## Part 2 — Korean B2B SEO playbook

Default acquisition channel for Packlinx is **organic Korean search**, with
Naver as the primary surface and Google as the secondary. This section is
the per-decision filter.

### Naver vs Google split — what each rewards

| Surface | Rewards | Penalizes |
| --- | --- | --- |
| Naver | C-Rank (source authority over time), DIA (per-document quality), keyword in title + first 100 chars, internal references in 블로그 / 카페 ecosystem, 스마트블록 inclusion. | Thin pages, AI-generated text without human review, link-buying patterns. |
| Google | E-E-A-T signals (named author, credentials, freshness), structured data (Article, FAQ, Product), strong internal linking, Core Web Vitals, original research. | Doorway pages, duplicate content across vendors, slow LCP, broken hreflang. |

We optimize for both, but when the two conflict (rare), Naver wins for
buyer-intent queries — Korean B2B procurement starts on Naver.

### Per-piece SEO checklist

- [ ] Target keyword reproduced exactly in `<title>` and `<h1>`.
- [ ] Slug is ASCII (transliterated, kebab-case). Korean in URL hurts CTR
      in some surfaces and breaks log analysis.
- [ ] Meta description 70–120 Korean chars, includes keyword + buyer
      benefit.
- [ ] Internal links: at least one to a directory page, one to a related
      article, one to a vendor profile (if applicable).
- [ ] External links: only to authoritative sources (산업통상자원부, KS
      standards bodies, peer-reviewed). No reciprocal-link schemes.
- [ ] Structured data: Article + Organization always; FAQPage when there
      is an FAQ block; Product when describing a packaging spec.
- [ ] Open Graph + Twitter Card filled. Naver also reads OG.
- [ ] hreflang `ko-KR` set; do not auto-translate to English without a
      separate page.
- [ ] LCP target < 2.5s on 4G, INP < 200ms.
- [ ] Image alt text in Korean, file names ASCII.

### Site-wide rules

- One canonical URL per topic. Comparison pages + listicles must not
  cannibalize each other.
- Update timestamps honestly. `dateModified` should reflect substantive
  edits, not whitespace tweaks.
- Vendor profiles: each is a unique URL with unique copy. Do not template
  copy across vendors; that triggers Naver thin-content penalties.
- Robots.txt + sitemap.xml are first-class artifacts. Update sitemap on
  every publish.
- 301 (not 302) for permanent moves. Track redirect chains; > 1 hop is a
  bug.

### Naver-specific moves

- Register the domain on Naver Search Advisor on day 1.
- Submit sitemap and RSS to Naver. Resubmit on structural changes.
- Build a 블로그/카페 distribution loop only when the source post is
  evergreen — Naver's source authority compounds slowly.
- Avoid "Naver SEO consultants" who promise 1-week wins. They sell
  link schemes that get manually penalized.

### Refusal list

- Refuse to publish AI-generated drafts without a human Korean editor pass.
  C-Rank actively suppresses these.
- Refuse to template-stamp vendor profiles for SEO volume. Empty volume
  ≠ value, and vendors notice.
- Refuse paid-link or PBN tactics. One penalty resets months of work and
  is a one-way door.
- Refuse keyword stuffing in alt text or hidden divs.

## Self-check before commissioning or publishing

- [ ] Can I name the buyer this piece serves and the action they take next?
- [ ] Did the brief specify *the* keyword, not a topic?
- [ ] Have I checked the SERP for that keyword on Naver and Google to see
      what's already winning?
- [ ] Have I given the writer enough source material to make verifiable
      claims, or am I asking them to invent?
- [ ] Is the kill criterion defined (e.g., "no top-10 ranking after 90
      days → revisit")?
