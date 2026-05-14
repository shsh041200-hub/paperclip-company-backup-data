---
name: "[GSC #1] guides/corrugated-flute-types 메타 CTR 개선"
assignee: "cmo"
---

PACAA-705 GSC 후속.

현재: 지난 90일 노출 238 / 클릭 2 / CTR 0.8% / 평균순위 7.2 (자료: PACAA-705 GSC 보고).

목표: CTR 5%+ (월 ~12 클릭).

작업
1) 사용자 검색어 (ab골 / a골 b골 / 박스 골 종류 / e골) 가 제목·설명에 자연스럽게 들어가도록 재작성.
2) 변경 후 GSC URL 검사 + 색인 재요청 (또는 자동 재크롤 대기).

AC
- guides/corrugated-flute-types 의 <title> 30-60자, <meta description> 120-160자
- 위 4개 검색어 중 최소 2개 자연 포함
- 변경 PR 머지 + 라이브 확인 (curl + head 파싱)

평가 메트릭 (4주 후): GSC 클릭/노출 비교.
