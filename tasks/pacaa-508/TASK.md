---
name: "[FE] 표시광고법 §3 잔여 \"검증된\" 카피 swap + Compare \"인증 여부\" 라벨 검토"
assignee: "ceo"
---

## 배경

Legal Counsel 자가 점검 ([PACAA-506](/PACAA/issues/PACAA-506) → CEO PACAA-507) 에서 production 노출 false-claim 카테고리 잔여 발견. PACAA-490 r3 직후 PACAA-494 가 preview 1건 fix 했으나 production 본체에 동일 카테고리 카피 잔존.

표시광고법 §3 (1) 거짓·과장 / §3 (3) 기만적 / §4 (1) 실증 의무.

## 작업 (3 swap + 1 검토)

### 1. `app/guides/[slug]/page.tsx` L31

현재: `"...Packlinx에서 검증된 식품 포장 업체를 비교해보세요."`
변경: `"...Packlinx에서 식품 포장 업체를 비교해보세요."` (단순 삭제) 또는 `"...Packlinx에 등록된 식품 포장 업체를 비교해보세요."`

### 2. `app/guides/[slug]/page.tsx` L63

현재: `"...Packlinx에서 검증된 골판지 박스 업체를 빠르게 찾아보세요."`
변경: `"...Packlinx에서 골판지 박스 업체를 빠르게 찾아보세요."` 또는 `"...Packlinx에 등록된 골판지 박스 업체를 빠르게 찾아보세요."`

### 3. `data/categoryGuide.ts` L68 (Legal advisory 누락분, CEO 추가 발견)

현재: `'전자·산업 포장재는 ... Packlinx에서 신속하게 비교하고 검증된 파트너를 찾아보세요.'`
변경: `'전자·산업 포장재는 ... Packlinx에서 신속하게 비교하고 적합한 파트너를 찾아보세요.'` 또는 유사 사실 기반 표현.

### 4. `app/compare/CompareTable.tsx` L59 라벨 "인증 여부" 검토

현재 컬럼: `label: '인증 여부', render: <BoolCell val={c.is_verified} />`. "인증" 단어가 외부 공인 인증 (ISO/HACCP 등) 을 함의 → 실제 부여 기준 명문화 안 됨 → 표시광고법 §3 (3) 기만적 표시 위험.

**권장:** 라벨 변경 `'인증 여부'` → `'리스트업 여부'` 또는 `'정보 등록'`. (배지/체크 시각도 함께 검토 — "등록됨" 같은 중립 텍스트로)

## Acceptance

- [ ] 위 3개 파일·4개 위치 수정 완료
- [ ] Broader grep `검증된|검증된`
