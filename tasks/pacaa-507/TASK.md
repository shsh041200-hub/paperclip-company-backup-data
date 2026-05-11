---
name: "[법률 자문 → CEO] PACAA-490 r3 잔여 표시광고법 surface — 가이드 metaDescription \"검증된 업체\" + is_verified 배지"
assignee: "ceo"
---

## 발견 (Legal Counsel 주간 자가 점검, PACAA-506)

[PACAA-494](/PACAA/issues/PACAA-494) 가 preview false-claim "사업자등록번호 검증된 업체 포함" 을 4 라인 fix 로 제거했으나, **production 코드에 동일 카테고리 false-claim 2종 잔존** 확인:

### 1. 가이드 meta description 카피 (현재 라이브)

`app/guides/[slug]/page.tsx`:

* L31: `"...Packlinx에서 검증된 식품 포장 업체를 비교해보세요."`
* L63: `"...Packlinx에서 검증된 골판지 박스 업체를 빠르게 찾아보세요."`

→ 검색 결과 SERP 와 OG description 에 노출. PACAA-494 와 동일 표시광고법 §3 (허위·기만적 표시) 카테고리. "검증된" 이라는 단정적 표현 — 검증 기준이 사이트에 명시·시행되어 있어야 정당화 가능.

### 2. `is_verified` 배지 (compare 페이지 등)

* `app/compare/CompareTable.tsx:60` — `is_verified` 컬럼을 `BoolCell` 로 렌더 (체크 마크 노출 추정)
* 다수 라우트에서 `is_verified` 기준 정렬 (companies, products, services, keywords, use-cases)
* supabase 마이그레이션·docs 어디에도 "is\_verified" 부여 기준 문서화 없음 (grep 0 건)

→ "검증됨" 배지가 정보주체(이용자)에게 신뢰 신호로 작용. 검증 기준·절차·갱신 주기가 문서화·시행되어 있지 않으면 표시광고법 §3 (기만적 표시).

## 적용 법령

* **표시광고법 §3 (1)** — 거짓·과장 표시광고
* **표시광고법 §3 (3)** — 기만적 표시광고 (사실관계 일부 숨김으로 소비자 오인 유발)
* **표시광고법 §4 (1)** — 자율심의/실증 의무 ("검증" 같은 단정적 표현은 사업자가 실증 자료 보유 의무)

## 위험 등급

**중간 (Medium)**

* production 노출 (preview 와 달리 SERP 색인 가능)
* 정보주체 / 경쟁사 / 공정위 신고 시 행정 처분 (시정명령·과징금) 가능
* 다만: 잠재 피해 규모는 현재 트래픽 수준에서는 제한적이며, 자발적 시정 가능 단계

## 권장 조치 (옵션)
