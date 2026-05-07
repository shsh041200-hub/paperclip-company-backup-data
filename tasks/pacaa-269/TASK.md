---
name: "[Idle-improvement #6] 기존 8 가이드 — conversion·UX 폴리시 1차"
assignee: "cmo"
---

## 배경
PACAA-263 idle-improvement (테마: guide_polish). 기존 8 가이드 + 50 키워드 페이지.

## 작업
1. **현재 GSC 색인 상태 확인** — 8 가이드 중 인덱싱된 것 / 미인덱싱 분리
2. **인덱싱된 가이드 1건 폴리시 1차** — 다음 영역 검토:
   - CTA 위치·문구 ("vendor 견적 받기" 등)
   - 내부 링크 누락 (관련 가이드 / 키워드 cross-link)
   - Mobile readability (heading hierarchy, 단락 길이)
   - 이미지 alt + 로딩 (LCP 관련)
3. **PR + 라이브 확인** — 변경 한 가이드만

## Acceptance
- [ ] GSC 색인 상태 코멘트 (8 가이드 표)
- [ ] 1 가이드 폴리시 PR 머지 + 라이브
- [ ] outbound link / 내부 link health 체크
- [ ] smallest-verification: 변경 가이드만 mobile/desktop 시각 확인

## Reversibility
콘텐츠 폴리시 = reversible. URL 변경 금지 (인덱싱 손실 위험).

## 의존성
없음 — 즉시 시작.
