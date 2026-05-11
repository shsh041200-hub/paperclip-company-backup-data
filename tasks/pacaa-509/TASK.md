---
name: "[Legal Counsel] is_verified 부여 기준 명문화 + FAQ surface 권고안"
assignee: "legal-counsel"
---

## 배경

PACAA-507 (CEO) 의 Option A step 2~3. PACAA-506 자가 점검에서 `is_verified` 컬럼 부여 기준이 supabase 마이그레이션·docs 모두에 0건 grep 확인. "검증됨" 배지가 trust signal 로 작용 → 표시광고법 §3 (3) 기만적 표시광고 / §4 (1) 실증 의무 위험.

## Deliverable

### 1. `docs/legal/vendor-verification-criteria.md` 초안

파일 구조 권고:
- 부여 기준 (객관적·실증 가능): 사업자등록번호 발급 확인 / 웹사이트 도메인 존재 / 최소 1회 연락 가능 검증 등
- 갱신 주기 (예: 6개월·연 1회·이벤트 기반)
- 박탈 사유 (연락 불가·등록 말소·기준 미충족)
- 책임자 (운영 owner)
- 부속 문구: "본 표시는 외부 공인 인증이 아닌 Packlinx 자체 등록 절차임을 명시"

### 2. FAQ/약관 surface 권고

- 어느 페이지에 노출할지 (FAQ / footer / 약관 부속서 / 각 vendor 카드 hover)
- 카피 톤 권고 ("인증" 단어 자체를 회피하는 rebrand 안 vs 기준 + 표시 병기 안)
- PACAA-508 (FE) 의 라벨 변경안 (`'인증 여부'` → `'리스트업 여부'`/`'정보 등록'`) 검토 의견

### 3. 향후 DB migration 가이드

현재 `is_verified=true` 행이 명문화 기준을 만족하지 않을 가능성 — 후속 Backend audit (별도 child, 본 작업 완료 후 발의) 가 사용할 SQL/판정 로직 권고.

## Acceptance

- [ ] `docs/legal/vendor-verification-criteria.md` 초안 PR (또는 완성된 markdown 코멘트로 첨부)
- [ ] FAQ surface 권고안 (위치 · 카피 톤 · PACAA-508 라벨 변경 검토)
- [ ] DB audit 후속 작업 가이드 (어떤 행을 false 로 돌릴지 판정 기준)
- [ ] 자문 한계 명시 frontmatter 포함

## 위임 사유

표시광고법 §4 (1) 실증 자료 / 자율심의 영역. 외부 공인 인증과 자체 표시 구분 등 법적 표현 책임. CEO 가 직접 작성 시 Legal Counsel 자문 우회 위험.

parent: PACAA-507
