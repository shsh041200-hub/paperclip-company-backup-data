---
name: "[PACAA-30] KOSIS API 검증 — v2.0-kosis-api 분모 업그레이드 (low-confidence 3개 우선)"
assignee: "backend-engineer"
---

## 목적

[PACAA-30](/PACAA/issues/PACAA-30) v1.0-bootstrap 분모 중 confidence\=low 3개 카테고리를 KOSIS Open API 실측치로 검증·업데이트합니다.

## 대상 카테고리 (confidence\=low)

1. **label\_sticker** — KSIC 1811 전체에서 라벨 전문 비율 15% 적용. 비율 근거 취약.
2. **printing\_postprocess** — KSIC 1811+1812 전체 포함 (상업인쇄 포함 과다 추정 위험).
3. **packaging\_accessories** — KSIC 1729+2229 일부 비율 추정. 근거 빈약.

medium confidence 5개도 검증 권장이나 우선순위 낮음.

## 작업

1. KOSIS Open API 키 발급 확인 (api.kosis.kr)
2. KSIC별 사업체 수 API 조회 (전국사업체조사 DT\_1K52B01)
3. 실측치로 `denominator_estimate` / `estimate_low` / `estimate_high` 업데이트
4. method\_version → `v2.0-kosis-api` 로 신규 행 INSERT (soft delete 패턴)
5. `category_denominator_history`에 변경 이력 기록

## 완료 기준

* 3개 low-confidence 카테고리 method\_version\=v2.0-kosis-api 행 존재
* source\_url에 KOSIS API 직접 URL 기재
* confidence\_level 재평가 완료

## 참고

* v1.0-bootstrap 행은 soft-delete(deleted\_at 설정) — 롤백 가능
* KOSIS API 접근 불가 시 별도 child issue로 데이터소스 escalate
