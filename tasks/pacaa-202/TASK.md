---
name: "[PACAA-198 soak] 플라스틱 용기·병 가이드 GSC 첫 인덱싱 + 2주 성과 확인"
assignee: "cmo"
---

## 목적

[PACAA-198](/PACAA/issues/PACAA-198) Phase D 발행 후 2주 soak 리뷰.

## 트리거 (event-bound)

GSC에서 `/guides/plastic-container-guide` 첫 impression 발생 후 14일 경과 시 실행.

## 확인 항목

1. **GSC 색인 상태:** URL 검사 → "URL이 Google에 등록됨" 확인
2. **GSC 쿼리 데이터:**
   - 타겟 키워드 노출: 「플라스틱 용기 종류」 「PET 병 제작」 「플라스틱 통 업체」
   - Impressions / Clicks / Average Position
3. **Naver 색인:** Naver Search Advisor URL 검사 결과
4. **내부 링크 클릭:** Plausible에서 `/guides/plastic-container-guide` → `/plastic-containers` 카테고리 전환율 확인

## Kill criterion 평가

발행 후 90일 이내 Naver top 30 미진입 + Google top 50 미진입 → 키워드 교체 or 재구조화 결정.
이 리뷰 시점 기준 90일 데드라인: **2026-07-31**

## Done when

- [ ] GSC 쿼리 데이터 스크린샷 첨부
- [ ] Naver 색인 상태 확인
- [ ] Plausible 클릭 데이터 확인
- [ ] 다음 액션 결정 (최적화 / kill / 유지) 이유 포함

## Related

- 발행 이슈: [PACAA-198](/PACAA/issues/PACAA-198)
- Phase C soak 선례: [PACAA-187](/PACAA/issues/PACAA-187)
