---
name: "[Surface 3 시정] 키워드 50건 표시광고법·상표법 회고 시정"
assignee: "backend-engineer"
---

## 컨텍스트

[PACAA-241](/PACAA/issues/PACAA-241) Surface 3 회고 자문 결과(risk 중간) 후속 시정.

자문 원문: 본 parent issue 댓글 `Surface 3 — SEO 키워드 50건` 참조.

## 시정 항목

### 1) `test-keyword` 행 즉시 삭제 (위험 `높음`)
`supabase/migrations/20260508_keyword_pages_seed.sql` 의 `test-keyword` 행은 description 이 "국내 **최고**의..." 로 시작 — 표시광고법 §3 1항 1호(허위·과장) trigger. 운영 가치도 없는 테스트 키워드이므로 즉시 제거.

- 새 마이그레이션: `DELETE FROM keyword_pages WHERE slug = 'test-keyword';`
- 라우팅 / sitemap / 캐시에서도 제거.

### 2) 공통 description 3-구문 사실 부합 조정 (위험 `중간`, 49건)
모든 description 의 "**제조사 직접 연결, 가격 투명화, 신뢰 기반 매칭**" 문구를 사실에 부합하도록 조정.

- "제조사 직접 연결" — 등재 vendor 가 모두 제조사인 경우만 유지. 도매·중개상이 섞여 있다면 "**제조사·도매업체 비교**" 등으로 표현 변경.
- "가격 투명화" — 견적 매칭 모델이라 사전 가격 공개가 없다면 "**견적 비교**" 로 변경.
- "신뢰 기반 매칭" — 인증·심사 근거가 없다면 "**업체 비교 매칭**" 등 사실적 표현으로 변경.

→ Backend Engineer 가 CMO 와 상의 후 표준안 1개 채택 → 49건 일괄 PATCH.

### 3) `우체국택배박스-가격` slug 정비 (위험 `중간`)
"우체국택배" 는 우정사업본부 등록 서비스표(상표법 §108) + 표시광고법 §3 1항 3호(기만) 동시 trigger.

옵션 (택 1):
- (A) slug·title·description 에서 "우체국" 단어 제거 → `택배박스-가격` 등으로 통합 / redirect
- (B) "**우체국택배 규격 호환 박스 — 일반 제조사 비교**" 식으로 호환 표현 명시 + description 에 "우정사업본부 공식 인증 상품 아님" 고지

권장: (A) — 가장 안전.

## Acceptance

- [ ] `test-keyword` 행 DB 삭제 + 마이그레이션 comm
