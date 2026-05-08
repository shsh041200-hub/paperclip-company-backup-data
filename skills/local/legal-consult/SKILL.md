---
name: "legal-consult"
description: "Standard procedure for calling Legal Counsel — how to obtain Korean legal advisory on decisions with legal exposure. Domains: PIPA / 표시광고법 / 통신판매업 / copyright·trademark / terms. Pair with the SG-1~4 trigger rules."
slug: "legal-consult"
metadata:
  paperclip:
    slug: "legal-consult"
    skillKey: "local/04cb0580f6/legal-consult"
  paperclipSkillKey: "local/04cb0580f6/legal-consult"
  skillKey: "local/04cb0580f6/legal-consult"
key: "local/04cb0580f6/legal-consult"
---

# Legal Consult — Legal Counsel call procedure

## Who uses this

Every Packlinx agent. Use when handling decisions, actions, or artifacts with legal exposure (PIPA / 표시광고법 / 통신판매업 / copyright·trademark / terms-of-service).

## Recognising the call trigger

### Mandatory surface — pre-consult required (PACAA-240)

The 4 surfaces below are **hard-gated**: no merge / publish without a prior Legal Counsel consult. The same trigger list is embedded into CMO / Backend / Frontend AGENTS.md as a double fallback — if you read either source, you get the same rule.

1. **Site-external content publishing** (CMO owner) — new blog / guide / landing / social posts visible outside packlinx.com. (표시광고법 / copyright / 통신판매업)
2. **New vendor data field exposure** (Backend + Frontend co-owners; **change originator** triggers the consult) — schema additions, new API fields, or new UI surfaces that expose vendor info (esp. 통신판매업 / contact / identifiers / internal labels). (PIPA §15·§17, 표시광고법 §3, 통신판매업 §13)
3. **SEO keyword list with possible third-party trademarks** (CMO owner) — keyword candidates / meta / anchors / internal links that could embed external company / brand / registered marks. (Trademark §108)
4. **New measurement / tracking tool introduction** (Backend + Frontend co-owners; **change originator** triggers the consult) — Plausible / GA / GTM / Sentry / Pixel / self-built event pipeline / cookies / local-storage / fingerprint collection. (PIPA + 정보통신망법 §50-7)

When Backend and Frontend are both owners (surfaces 2 and 4), the **change originator** calls; the counterpart cites the response. One-side-only consult = SOP miss. Owner ambiguity → CEO routing.

### Other SG triggers (per-SG SOUL.md / `goal_skills/sg{2,4}_*.md`)

- **SG-1 (Vendor coverage):** adding vendor info fields / exposing identification info / correction-deletion channels (PIPA)
- **SG-2 (SEO):** using third-party content, images, logos (copyright) / third-party trademarks (trademark) / advertising labels (표시광고법)
- **SG-3 (Measurement infra):** introducing Plausible / analytics (PIPA + cookie consent) / behavioural-data forms
- **SG-4 (Vendor self-action):** changes to terms / privacy policy / claim·edit·intent form data items

If a trigger match is missed, Legal Counsel issues a retroactive consultation in the Monday 09:30 KST routine — but calling at trigger time is safer. Misses on the 4 mandatory surfaces above are SOP violations and counted in the 2026-06-01 SOP-effectiveness review (kill criterion: misses > calls → SOP redesign).

## Call procedure

1. **Create a PACAA child issue:**
   ```
   POST /api/companies/{companyId}/issues
   {
     "title": "[법률 자문] {one-line question}",
     "description": "{context: which SG / which decision. concrete question. decision deadline}",
     "assigneeAgentId": "54623669-64c6-402d-b87b-c0b8ebae3940",
     "parentId": "{calling issue id}",
     "goalId": "{calling goal id}",
     "priority": "{calling priority — usually medium}"
   }
   ```
2. **Wait for the response.** Legal Counsel wakes on call (heartbeat off — wakeOnDemand). Response time is typically < 1 heartbeat.
3. **Quote the response.** Legal Counsel responses always carry the disclaimer block — when quoting in a decision comment, include it **verbatim**. Do not truncate or summarize.

## Disclaimer (auto-attached to responses)

```
---
⚠️ 자문 한계 명시:
이 자문은 참고용이며 법적 책임 면제를 보장하지 않습니다.
사고 발생 시 면책 사유로 사용될 수 없습니다. Packlinx 보드는
외부 변호사 자문 미도입을 결정한 상태이며, 모든 법적 리스크는
Legal Counsel 자문에 의존합니다.
---
```

This block is baked into Legal Counsel SOUL.md (§4) + this skill (double fallback). The caller must not truncate it.

## Out-of-Korea law detection

If the question drifts into GDPR / CCPA / Japan APPI / US labor law / international tax etc., Legal Counsel explicitly refuses + escalates to the CEO. The caller waits for the CEO decision.

## Response quality bar

- Risk grade stated (`낮음` / `중간` / `높음` / `금지` — i.e., low / medium / high / prohibited)
- Applicable law cited at the article level
- Responses that punt with "talk to legal" are rejected — Legal Counsel is the legal team
- If the disclaimer is missing, the response is invalid → request a rewrite

## Call cost + post-hoc audit

Within paperclip subscription budget. Estimated call frequency ~3-5 / week. PACAA-101 §5.8 deferred row keeps an 8-week spot-check (5 consultations + 8 weeks OR 2026-06-25 backstop) — board + CEO audit advisory quality after the fact. If quality is judged insufficient, the external-counsel trigger is renegotiated.
