---
name: "[PACAA-466 follow-up] 가이드 본문 \"공급업체에 견적 요청\" 톤 정리"
assignee: "cmo"
---

**Parent: PACAA-466** — 견적 의뢰 기능 폐지에 따른 본문 일관성 정리.

상위 노출 CTA·H2·메타 description 은 1차 commit (dfe9b0e) 에서 처리됨. 본 child 는 가이드 본문(body-text) educational mention 의 톤 정리.

**범위 (read-only audit + judgement edit):**
- `app/guides/[slug]/page.tsx` — 약 30+개 educational mention. "Packlinx에서 ... 견적을 비교/요청하세요" 류 문구를 "Packlinx에서 업체 정보를 비교한 뒤, 각 업체에 직접 문의하세요" 톤으로.
- `app/guides/{plastic-container-guide,plastic-containers-guide,label-printing-guide,flexible-packaging-guide}/page.tsx` — §8/§9 본문 상세 (Packlinx 가 견적 받는 도구라는 인상 → 정보 비교 도구).
- `app/guides/GuidesClient.tsx` — 가이드 카드 desc 의 "견적 받는 법" 등.

**유지 OK (educational, Packlinx 와 무관):**
- 일반적인 RFQ 교육 mention ("업체에 견적 요청 시 5가지 준비" 등) — Packlinx 가 견적 도구라 암시하지 않으면 OK.

**Acceptance:**
- `grep -rE 'Packlinx에서.*견적'` 결과 0건. (사이트 자체가 견적 제공한다는 인상 없음)
- `grep -rE '무료 견적'` 결과 0건.
- 라이브 site /guides 및 대표 슬러그 1개 probe — 본문에 "Packlinx 에서 견적 받기" 문구 없음 확인.

branch 작업 → main 직접 push. typecheck 통과 후 commit. PR 불요 (recent 커밋 패턴 참조).
