---
name: "legal-counsel-playbook"
description: "Legal Counsel specialty playbook — Korean compliance checklist (PIPA, e-commerce act, fair trade, advertising) and takedown drafting template for the Packlinx packaging directory. Read before any legal-facing artifact or compliance review."
slug: "legal-counsel-playbook"
metadata:
  paperclip:
    slug: "legal-counsel-playbook"
    skillKey: "local/82aac25510/legal-counsel-playbook"
  paperclipSkillKey: "local/82aac25510/legal-counsel-playbook"
  skillKey: "local/82aac25510/legal-counsel-playbook"
key: "local/82aac25510/legal-counsel-playbook"
---

# Legal Counsel Playbook

Specialty bundle for the Packlinx Legal Counsel role. Covers a Korean
compliance checklist scoped to the directory's actual exposure surface,
and a drafting template for outbound takedown / cease-and-desist /
response letters.

This skill is **operational, not professional legal advice**. For matters
that cross into licensed-attorney territory (litigation, regulator
hearings, contract disputes with material exposure), escalate to a
licensed Korean attorney. The board approves engagement.

Common skills handle voice, language routing, encoding, and decision
protocol. Do not duplicate that content here.

## When to invoke this skill

- Reviewing a privacy-related change (data collection, cookies, third-
  party processors)
- Drafting Terms of Service / Privacy Policy / vendor agreements
- Receiving or sending a takedown / cease-and-desist letter
- Handling a regulator inquiry (KFTC, KCC, 식약처, 개인정보보호위원회)
- Reviewing marketing claims for unfair-advertising risk
- Responding to a personal-data subject request (PIPA Article 35 +)

## First principle

**The Korean packaging market runs on trust. One verified-vendor lie or
one mishandled data subject request ends the company.** Legal posture
isn't a checklist that lives next to the product — it's the product's
floor.

## Part 1 — Korean compliance checklist

Scoped to the laws that actually apply to a Korean B2B directory. Not a
substitute for license-holder advice on edge cases.

### Personal Information Protection Act (PIPA — 개인정보보호법)

Triggers: any collection of personal information from buyers, vendors,
or employees. This is the hot zone for a directory.

**Mandatory artifacts:**

- [ ] Privacy Policy (개인정보처리방침) — public-facing, Korean,
      conforming to PIPA Article 30. Linked from every page footer.
- [ ] Per-purpose consent (목적별 동의) at collection time. Bundled
      consent ("동의합니다") for multiple purposes is not lawful.
- [ ] Retention period for each data category, stated explicitly.
      Default: delete on retention expiry, not "indefinite."
- [ ] Data Subject Rights process (열람, 정정, 삭제, 처리정지) —
      response within 10 days of request.
- [ ] Data breach notification process — to subjects + 개인정보보호
      위원회 within 72 hours of discovery, where threshold met.
- [ ] Cross-border transfer disclosure if any processor is overseas
      (e.g., Vercel, Supabase US regions). Subject consent + listed in
      privacy policy.

**Common pitfalls:**

- Collecting 주민등록번호 (resident registration number) without legal
  basis. **Almost never permissible** for a B2B directory. Use 사업자
  등록번호 instead.
- Collecting "just in case" data that's not tied to a stated purpose.
  PIPA penalizes excess collection.
- Using personal data for purposes not in the consent. Re-consent
  required for new purposes.
- Vendor employee personal data (담당자 phone, email): treat as personal
  data subject to PIPA, not as "company data."

### Act on Promotion of Information and Communications Network Use
(정보통신망법)

Triggers: outbound marketing communications (email, SMS, KakaoTalk).

- [ ] Opt-in (사전 동의) before sending marketing communications. Korea
      is opt-in, not opt-out.
- [ ] Sender disclosure: "(광고)" prefix in subject line for marketing
      emails. Failure to prefix is per-message penalty.
- [ ] Clear unsubscribe at the bottom, in Korean, one-click.
- [ ] Quarterly opt-in confirmation for retained marketing consents
      (every 2 years; track per subject).
- [ ] No marketing communications between 21:00–08:00 unless explicit
      time-window consent.

### Act on Consumer Protection in Electronic Commerce (전자상거래법)

Triggers: any e-commerce activity. Note: a B2B directory that doesn't
process payments is largely outside the consumer-protection scope, but
becomes in-scope the moment we add buyer payment flows.

- [ ] Business identification disclosure (법인명, 대표자, 사업자등록
      번호, 통신판매업 신고번호 if applicable, 주소, 전화) on every
      page footer.
- [ ] Refund / cancellation policy disclosure if any paid transactions.
- [ ] Receipt / contract-confirmation flow for any paid vendor service.

### Monopoly Regulation and Fair Trade Act (공정거래법) +
Indication and Advertising Act (표시·광고법)

Triggers: any claim about vendors or buyers, any comparison content, any
"recommended" or "verified" badge.

- [ ] No false / exaggerated claims about vendors. "Verified" badge
      requires the verification per `coo-playbook` Step 1.
- [ ] No comparative claims that misrepresent competitors.
- [ ] Sponsored content or paid placement clearly labeled. Mixing
      organic and paid in the same surface without labeling is per-
      surface penalty.
- [ ] Materially-influencer-relevant claims (영향력 있는 표시·광고)
      require evidence on file.

### Sector-specific (식품의약품안전처, 환경부, 산업통상자원부)

For food-contact, medical, or hazardous-substance packaging vendors:

- [ ] Vendor's claims about food-contact safety require KFDA approval
      number on file. Do not publish without it.
- [ ] Hazardous-material claims (e.g., medical-grade, lab-grade)
      require regulatory documentation.
- [ ] Eco-claims (친환경, 생분해, 재활용) — under 환경표지 rules,
      require certification number, not just self-claim.

**Refusal:** any vendor claim in these regulated categories without
documentation does not get published. The COO holds the documentation;
Legal Counsel verifies authenticity.

### Employment and contractor (when applicable)

For any human or contractor working on Packlinx:

- [ ] Written contract (근로계약서 or 용역계약서). No verbal-only
      agreements.
- [ ] Tax forms (원천징수영수증, 사업소득 신고).
- [ ] Personal data of contractors handled per PIPA.

This is solo-operated for now, but the moment we engage a freelance
designer, writer, or developer, this section activates.

### Ongoing-operation hygiene

- [ ] Annual compliance review — at minimum: privacy policy, consent
      flows, vendor agreement template, regulator-letter file.
- [ ] Regulator inquiry log — every letter received, date, response,
      outcome. Retained 5 years.
- [ ] Counsel-of-record relationship — a licensed Korean attorney
      retained for escalations. Identify and engage before the first
      regulatory inquiry, not after.

## Part 2 — Takedown / cease-and-desist drafting template

For outbound letters from Packlinx (we are the requester, e.g., asking a
third party to take down infringing content) and for response letters
(we received a takedown request). For inbound takedown handling
*operations*, see `coo-playbook` Part 2 — this section is the legal
artifact, not the workflow.

### Outbound takedown letter — template (Korean, formal)

```
[수신: <상대방 회사명 / 담당자>]
[발신: Packlinx 운영팀]
[일자: <YYYY년 MM월 DD일>]

제목: <대상 콘텐츠> 관련 게시 중단 요청 — <간단한 사유 카테고리>

1. 발송인 정보
   - 회사명: Packlinx
   - 사업자등록번호: <사업자등록번호>
   - 주소: <주소>
   - 담당자: <이름>, <직함>, <연락처>

2. 대상 콘텐츠
   - URL: <정확한 URL>
   - 콘텐츠 설명: <어떤 콘텐츠인지 1~2문장>
   - 게시일: <확인된 게시일 또는 발견일>

3. 게시 중단 요청 사유
   - 권리 근거: <상표권 / 저작권 / 영업비밀 / 명예훼손 / 부정경쟁 등 — 명시>
   - 권리 보유 증빙: <등록번호, 첨부 자료>
   - 법적 근거 조항: <해당 법령과 조항>
   - 요청 내용: 본 콘텐츠의 게시 중단 및 향후 동일·유사 콘텐츠 게시 금지

4. 회신 요청
   - 회신 기한: 본 통지 수령일로부터 <N>영업일 이내
   - 회신 방법: 본 메일 회신 또는 <연락처>
   - 게시 중단 확인 시 후속 조치 종결, 무회신 또는 거부 시 추가 법적
     절차를 검토할 수 있음을 안내드립니다.

5. 첨부
   - <증빙 자료 목록>

본 통지는 향후 절차에서 사용될 수 있습니다.

Packlinx 운영팀 드림
```

**Drafting rules:**

- Lead with the legal basis, not the emotion. "X 권리를 침해하고 있어"
  rather than "very disappointed."
- Cite specific URLs. Vague "your content" gets ignored.
- State a deadline. Open-ended requests are easy to deprioritize.
- Avoid threats you won't follow through on. Implied legal action only
  if Legal Counsel + CEO have agreed it's on the table.
- Send via a verifiable channel (e.g., 내용증명 우편 for high-stakes).
  Email-only for low-stakes; document send + receipt.

### Response letter — template (Korean, formal)

When Packlinx receives a takedown request and we're either complying or
declining.

#### Compliance response

```
[수신: <상대방>]
[발신: Packlinx 운영팀]
[일자: <YYYY년 MM월 DD일>]

제목: 게시 중단 요청 처리 안내 — <티켓 번호>

귀하께서 <YYYY년 MM월 DD일> 발송하신 게시 중단 요청 (대상 URL:
<URL>)을 검토하였습니다.

귀하께서 제시하신 <권리 근거>에 따라 해당 콘텐츠의 게시를 <YYYY년
MM월 DD일>자로 중단 처리하였음을 안내드립니다.

* 처리 결과: 해당 URL은 410 응답으로 전환되었으며, 검색 색인 제거
  요청이 함께 진행되었습니다.
* 향후 동일·유사 사례 발생 시 신속한 처리를 위해, 추가 신고가 있을
  경우 본 티켓 번호를 함께 알려주시면 감사하겠습니다.
* 본 처리는 귀하의 청구를 인정하는 것으로, 향후 법적 분쟁 시 자료로
  활용될 수 있습니다.

문의 사항은 본 메일 회신 또는 <연락처>로 부탁드립니다.

Packlinx 운영팀 드림
```

#### Decline response

Use only when COO + Legal Counsel have agreed the request lacks merit
or evidence.

```
[수신: <상대방>]
[발신: Packlinx 운영팀]
[일자: <YYYY년 MM월 DD일>]

제목: 게시 중단 요청 검토 결과 안내 — <티켓 번호>

귀하께서 <YYYY년 MM월 DD일> 발송하신 게시 중단 요청 (대상 URL:
<URL>)을 검토한 결과, 아래 사유로 해당 요청을 수용하기 어렵다는
점을 안내드립니다.

* 사유: <구체적 사유 — 권리 입증 부족 / 사실 일치 / 표현의 자유
  범위 등>
* 검토 근거: <법령 또는 정책>
* 추가 자료 제출 시 재검토: 귀하께서 <어떤 자료>를 추가로 제출
  해주시면 다시 검토하여 회신드리겠습니다.

본 회신은 본 시점의 자료를 기반으로 한 검토 결과이며, 향후 추가
자료 또는 법적 절차에 따라 변경될 수 있습니다.

문의 사항은 본 메일 회신 또는 <연락처>로 부탁드립니다.

Packlinx 운영팀 드림
```

**Drafting rules:**

- State the decision clearly in the first body paragraph. Don't bury it.
- Cite the specific reason and the legal/policy basis. Vague decline =
  invitation to escalate.
- Always offer the "additional evidence → re-review" path. It's both
  fair and reduces escalation pressure.
- Don't apologize for declining a legitimately frivolous request. An
  apology is read as weakness and breeds repeat requests.
- For decline, CEO + Legal Counsel sign-off required before send.
  Compliance can ship under Legal Counsel + COO sign-off.

### Logging and retention

Every outbound or response letter:

- [ ] Saved as PDF (signed, dated) in the legal artifact store.
- [ ] Indexed against the takedown ticket from `coo-playbook`.
- [ ] Retained 5 years minimum, longer if the matter is unresolved.
- [ ] Forwarded summary to the CEO within 24 hours of send.

## Refusals

- Refuse to draft or send any letter that misrepresents Packlinx's
  legal position.
- Refuse to ship a privacy policy or ToS that doesn't accurately
  describe what we collect and why.
- Refuse to bypass per-purpose consent for "marketing convenience."
- Refuse to publish vendor claims in regulated categories without
  documentation on file.
- Refuse to handle anything that crosses into licensed-attorney
  territory without engaging counsel of record. State the limit
  clearly to the requester.

## Self-check before sending or approving

- [ ] Is the legal basis specific (statute + article + facts), not
      vague?
- [ ] Is every claim in the letter verifiable from documents on file?
- [ ] Has the CEO seen anything that's a one-way door (lawsuit,
      regulator response, public-statement)?
- [ ] Is the artifact retained per the 5-year rule?
- [ ] If a Korean attorney audited this tomorrow, would the trail
      support our position?
