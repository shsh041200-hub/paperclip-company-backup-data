---
name: "[O2] 다중 API enrichment + LLM judge — top-3 + Kakao Local + Haiku 페이지 매칭 판정"
assignee: "ceo"
---

## 목적

PACAA-784 결정 (보드 2026-05-17): 크롤링 품질 약점 W1 (items\[0] only) / W2 (bigram 0.5 노이즈) / W4 (블랙리스트 부족) 해결.

## 작업

1. `naver_website_enrich.py` / `assoc_website_enrichment.py` 를 **top-3 결과 채택** 으로 변경
2. **Kakao Local Search API** 추가 (Naver 와 별도 소스, 카카오맵 디비)
3. **LLM judge** (Claude Haiku) 통합:
   * 각 후보 URL 의 메타 (title, description, og:site\_name) fetch
   * "이 페이지가 회사 '{name}' (주소: {addr}) 의 공식 웹사이트인가? Y/N + 신뢰도 0\~1" 프롬프트
   * 비용: vendor 1건당 약 1k input + 100 output tokens ≈ $0.0003 (Haiku 4.5)
4. bigram threshold 동적화: 음절 수 ≤ 2 면 strict (1.0), ≥ 4 면 0.5 유지
5. 호스트 블랙리스트 확장: 디렉토리/구인/언론 약 80개 도메인 추가

## Acceptance Criteria

* top-3 + Kakao + LLM judge 통합 dry-run 결과 (matched/false positive/false negative)
* O1 (parallel ticket) 과 audit 스키마 호환
* 월 운영비 ≤ $5 (Haiku) 산정 + 보고
* Naver/Kakao API 키는 환경변수, 코드에 하드코딩 금지

## 제약

* Legal P0-B 4-필드 제약 유지
* 일정: 4\~6일

## 부모 이슈

PACAA-784
