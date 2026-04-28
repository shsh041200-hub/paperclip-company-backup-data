---
name: "head-of-sales-playbook"
description: "Head of Sales specialty playbook — outbound script library and pricing-negotiation checklist for Korean B2B vendor and buyer outreach at Packlinx. Read before sending an outbound or negotiating a price."
slug: "head-of-sales-playbook"
metadata:
  paperclip:
    slug: "head-of-sales-playbook"
    skillKey: "local/4ca38b3f7e/head-of-sales-playbook"
  paperclipSkillKey: "local/4ca38b3f7e/head-of-sales-playbook"
  skillKey: "local/4ca38b3f7e/head-of-sales-playbook"
key: "local/4ca38b3f7e/head-of-sales-playbook"
---

# Head of Sales Playbook

Specialty bundle for the Packlinx Head of Sales role. Covers outbound
scripts (Korean, by audience and channel) and a pricing-negotiation
checklist scoped to Korean B2B norms.

Common skills handle voice, language routing (Korean for users / English
internal), encoding, and decision protocol. Do not duplicate.

## When to invoke this skill

- Sending an outbound message (cold or warm) to a vendor or buyer
- Replying to an inbound inquiry that touches pricing
- Negotiating contract terms, fees, or discounts
- Reviewing a draft outbound from another role
- Writing to a partner channel (associations, trade groups)

## First principle

**The Korean packaging market is traditional and relationship-driven.**
Pushy / scripty Western SaaS outbound fails here. Earn standing through
specificity, third-party references, and patience. Speed comes after
trust, not before.

## Part 1 — Outbound script library

All scripts are Korean (per `packlinx-comms` language routing). Use
존댓말, no slang, no exclamation points, no superlatives without numbers.

### Channel rules

| Channel | Use for | Don't use for |
| --- | --- | --- |
| 이메일 (work email) | First-touch with vendors and procurement leads | High-volume cold blasts |
| 전화 | Confirming interest after email reply, urgent issues | First-touch (cold call has very low success in Korean B2B) |
| 카카오톡 비즈니스 | Confirmed contacts only, ongoing relationships | Cold outreach (filtered as spam) |
| 카카오 비즈채널 | Vendor-side notifications when they've opted in | Anything cold |
| LinkedIn | Decision-makers at modern SMBs, not legacy manufacturers | First-touch with traditional vendors |
| Trade events / 박람회 | In-person trust-building, longest path but highest yield | Direct sale on the day |

### Script — Vendor cold outbound (Korean email)

Use for first-touch to a target vendor we want on the directory.

```
제목: Packlinx 디렉토리 등재 안내 — <업체명>님 카테고리 추천

<업체명> <담당자 직함>님께,

안녕하세요. Packlinx 운영팀의 <이름>입니다.

저희는 한국 포장 산업의 정확한 정보를 한 곳에 정리하는 B2B 디렉토리
서비스를 운영하고 있습니다. <업체명>님의 <구체적 카테고리> 분야 정보를
검토하던 중, 디렉토리에 등재드리는 것이 적합하다고 판단되어 연락드립니다.

* <업체명>님의 <인증/제품/거점> 정보를 정확히 반영해 검색 결과 상단에
  노출되도록 도와드리며, 현재 등재 비용은 부과되지 않습니다.
* 이미 <비교 가능한 산업군 / 인접 카테고리>의 <N>개 업체가 등재되어 있어,
  같은 카테고리 검색 트래픽에서 직접 비교 노출됩니다.
* 등재 진행은 <간단한 절차 — 사업자등록증, 인증서, 담당자 연락처 확인>로
  이루어지며, 영업일 기준 <N>일 소요됩니다.

검토 후 회신 부탁드립니다. 추가 자료가 필요하시면 언제든지 답장 주시면
바로 보내드리겠습니다.

감사합니다.

<이름> 드림
Packlinx 운영팀 | <연락처> | <웹사이트 URL>
```

**Hygiene:**
- Subject line: name the recipient's company explicitly + state the
  reason for contact. Generic subjects ("협업 제안") get ignored.
- Body: 1 paragraph why-now, 3 bullets value, 1 paragraph next step.
- Sign-off: 드림 (formal). Phone + URL in signature.
- No tracking pixels. No "did you see my last email?" follow-ups.

### Script — Vendor warm follow-up (Korean email)

After initial reply expressing interest, before onboarding.

```
제목: Packlinx 등재 진행 — 다음 단계 안내

<업체명> <담당자 직함>님께,

안녕하세요. 회신 주셔서 감사합니다. 등재 진행을 위해 아래 자료를
공유해 주시면 검토 후 영업일 기준 <N>일 내로 등재가 완료됩니다.

1. 사업자등록증 사본
2. 보유 중이신 인증서 (FSSC 22000, ISO 9001, KS 등 해당 항목)
3. 담당자 연락처 — 전화 + 이메일 (확인 가능한 도메인)
4. 카테고리 / 주요 제품 정보 — 가능한 경우 카탈로그 PDF

자료는 <보안 업로드 URL> 또는 본 메일에 회신으로 보내주시면 됩니다.
수령 즉시 검토 시작하며, 추가 확인이 필요한 경우 따로 연락드리겠습니다.

감사합니다.

<이름> 드림
```

### Script — Buyer cold outbound (Korean email)

Use for first-touch with procurement leads at companies we believe will
benefit from the directory.

```
제목: <구매 담당 직함>님께 — 포장재 비교 검색 도구 안내

<회사명> <담당자 직함>님께,

안녕하세요. Packlinx의 <이름>입니다.

귀사가 <카테고리 / 산업>에 종사하는 점을 고려해 안내드립니다. 저희는
한국 포장 업체 정보를 카테고리별·인증별·생산지역별로 비교 검색할 수 있는
디렉토리를 운영하고 있습니다.

* 등재 업체는 모두 사업자 정보·인증·연락처가 검증된 상태입니다.
* 검색 무료, 등록 불요. 필요한 정보를 즉시 비교하실 수 있습니다.
* 견적 문의는 디렉토리 내 업체 프로필을 통해 직접 진행하실 수 있습니다.

지금 사용 중이신 검색 채널과 비교해 보시고, 의견 주시면 감사하겠습니다.
서비스 문의는 본 메일 회신 또는 <연락처>로 부탁드립니다.

감사합니다.

<이름> 드림
Packlinx 운영팀 | <연락처> | <웹사이트 URL>
```

### Script — Inbound reply (Korean email)

Buyer or vendor reaches out with a question.

```
제목: Re: <원 메일 제목>

<상대 직함>님께,

안녕하세요. 문의 주셔서 감사합니다.

<문의 내용 요약 1줄>에 대해 답변드립니다.

* <답변 핵심>
* <뒷받침 자료 / 링크>
* <다음 단계가 있다면 명확히>

추가 질문이 있으시면 언제든지 회신 부탁드립니다.

감사합니다.

<이름> 드림
```

**Reply timing:** within 4 work hours. Korean B2B expects faster reply
than Western markets; > 24h reply is read as low interest.

### Script anti-patterns (refuse to send)

- Generic "Hi {{first_name}}" templating that doesn't actually
  personalize. Korean recipients spot this immediately and screen out.
- Subject lines starting with "Quick question" or "?" — looks like
  spam.
- "Last chance" / "limited offer" pressure language. Inappropriate for
  Korean B2B and damages standing.
- Mass-CCing or BCCing multiple unrelated vendors on the same email.
  Privacy violation and reputation killer.
- English-only outbound to Korean vendors (unless their site/contact
  page is English-only and clearly indicates that preference).

## Part 2 — Pricing-negotiation checklist

Pricing in Korean B2B is rarely a one-shot transaction. It's a
relationship signal. The pricing decision is also a positioning
decision; treat it as such.

### Before any pricing conversation

- [ ] **Know the segment.** Vendor (paying for premium placement?
      certification verification? lead routing?), buyer (always free at
      this stage — confirmed?), partner (different terms entirely).
- [ ] **Know the floor.** What's the lowest price we'd accept and still
      cover the cost of serving them? Below that, walk.
- [ ] **Know the ceiling.** What's the most we could ask for without
      damaging the relationship? Above that, you're trading future
      goodwill for current revenue — bad trade at our stage.
- [ ] **Know the alternative.** What does the customer's BATNA look
      like? Word-of-mouth referrals? Existing directories? In-house
      sourcing? Knowing this shapes the pitch.
- [ ] **Know the policy.** Has this segment seen this price before? Are
      we offering a price that contradicts an earlier published number?
      Consistency matters more than optimization at our stage.

### During the conversation

- [ ] **Anchor on value, not cost.** Lead with the outcome ("X
      additional verified leads / month") before the number. Korean B2B
      buyers respond to specifics, not abstractions.
- [ ] **Single price first.** Don't open with three-tier menus on a
      first conversation. Tier menus are for buyers in evaluation
      mode, not first-touch.
- [ ] **Silence after stating the number.** Korean negotiation
      respects pause. Resist filling the silence with discount offers.
- [ ] **Document the asks.** If they request a discount, ask
      specifically why ("if you can share the constraint, I can think
      about how to meet it"). Vague discount requests get vague
      answers.
- [ ] **Don't promise on the call.** "I'll need to confirm with the
      operations side and get back to you within <N> business days."
      This both signals diligence and gives you space to think.

### Discount discipline

- Discounts are **time-bounded** (e.g., first-90-day promotion), **role-
  bounded** (e.g., trade-association member), or **volume-bounded**
  (e.g., 10+ profile bulk). Never open-ended.
- Every discount is documented with a reason in the contract. "As a
  goodwill gesture" is not a reason — it normalizes free.
- Discount requests beyond standard tiers escalate to CEO before being
  granted. Pricing concessions are positioning decisions.

### Refusal triggers (walk-away signals)

Walk away — politely — when:

- The customer demands an exclusivity that excludes competitors from
  the directory. The directory's value depends on density.
- The customer demands editorial control over how their or competitors'
  profiles are presented. Editorial integrity is non-negotiable.
- The customer's payment terms are unilateral (e.g., 90+ day net,
  retroactive discounts) and they refuse to negotiate.
- The conversation reveals intent to use Packlinx as a marketing
  surface for falsified or unverified claims.

State the refusal cleanly: "이번에는 함께하기 어려울 것 같습니다.
이유는 <짧은 설명>입니다. 추후 변경 사항이 있으면 다시 연락드리겠습니다."
Don't apologize for the refusal; don't soften it into a maybe.

### Post-conversation

- [ ] Log the conversation in the CRM (vendor / buyer record). Date,
      participants, asks, decisions, follow-up date.
- [ ] If a discount was granted: link to the contract clause and the
      reason.
- [ ] If walked away: log the trigger so we recognize the pattern next
      time.
- [ ] Schedule the follow-up before closing the loop. "I'll get back to
      you" without a calendar entry usually means you won't.

## Refusals

- Refuse to send mass un-personalized cold outbound at scale. It poisons
  the domain reputation and the brand.
- Refuse to misrepresent vendor verification status to win a sale.
- Refuse to grant exclusivity or editorial control as part of a pricing
  negotiation.
- Refuse to commit to terms outside written policy without CEO
  sign-off.
- Refuse to use buyer / vendor data for outbound to a third party.
  Privacy is non-negotiable.

## Self-check

- [ ] Is the recipient name and context specific enough that this email
      couldn't be sent to anyone else?
- [ ] Did I open with the why-now, not the pitch?
- [ ] If pricing came up: do I know the floor, ceiling, and BATNA?
- [ ] Did I document the conversation and the next-step calendar entry?
- [ ] Is anything I'm sending inconsistent with what we said publicly?
