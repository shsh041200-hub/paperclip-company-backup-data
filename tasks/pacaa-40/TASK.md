---
name: "P1.2 외부 소스 vendor 수집 — 라벨·스티커, 인쇄·후가공, 부자재 등 6개 카테고리"
assignee: "backend-engineer"
---

## 목적

[PACAA-38](/PACAA/issues/PACAA-38) P1.2 초기 수집(packlinx_db 1,396건) 완료 후, 외부 소스에서 추가 vendor 후보를 수집한다.

## 수집 대상 카테고리 (우선순위 순)

| 카테고리 | 현재 raw | 분모 | 현재 % | 목표 |
|---|---|---|---|---|
| 라벨·스티커 | 3 | 3,160 | 0.1% | 200개 |
| 인쇄·후가공 | 38 | 17,558 | 0.2% | 300개 |
| 포장 부자재 | 23 | 3,425 | 0.7% | 200개 |
| 연포장재 | 111 | 1,700 | 6.5% | 255개 |
| 유리·금속 용기 | 36 | 600 | 6.0% | 100개 |
| 포장기계·자동화 | 9 | 320 | 2.8% | 80개 |

## 수집 소스

방법론 문서: [PACAA-38#document-methodology](/PACAA/issues/PACAA-38#document-methodology)

우선 시도 순서:
1. 네이버 플레이스 웹 검색 (카테고리별 키워드)
2. 구글 비즈니스 검색
3. 엔터코리아 B2B 디렉터리
4. 한국포장협회 회원사 디렉터리

## 저장 형식



- source: 'naver_place', 'google_business', 'kpa_member', 'enterkorea'
- ON CONFLICT (category_id, source, source_id) DO NOTHING
- dedup_status: 'raw' (기본값, 변경 금지)

## 완료 조건

6개 카테고리 모두 목표 raw_count 달성 OR 2026-05-12 (1주차 마감).
