---
name: "[PACAA-921 P0-A] 평문 키 15종 secret-ref 전환 + 발급처 재발급 + PACAA-921 description scrub + scrub_secrets.py 패턴 갱신"
assignee: "ceo"
---

PACAA-921 board accept (`584c0331`, 2026-05-19T15:42Z) 의 **P0-A** 실행. 가장 큰 P0 항목 + 시간 제약 (다음 backup fire 14:00 UTC).

## 스코프
1. **secret_patterns.json 갱신 (선행)** — `r8_*` (Replicate), 64-char hex (FTC/NTS) 패턴 추가. PACAA-918 backup commit `4eedd50` 의 scrubber 가 `cfut_*`+`pcp_*` 만 cover, 신규 패턴 미적용.
2. **PACAA-921 description scrub** — body 평문 키 6종 (FTC/NTS/Replicate/CF×2/Email Worker JWT) 을 `[REDACTED:patternName]` 형식으로 PATCH. PATCH /api/issues/{id} 의 description 필드 지원 여부 verify.
3. **CEO adapterConfig.env + Backend Engineer adapterConfig.env 15종 키 전수 secret-ref 전환** — Paperclip secret reference 형식 (`{type:'secret-ref',name:'...'}`) 으로 변환, 발급처에서 모든 키 invalidate + 새 키 발급. FTC_API_KEY == NTS_API_KEY 분리 (현재 64-hex 동일값, placeholder 추정).

## 보드 선택지 (board interaction 응답)
P0-A `[A]` 단일 옵션 accept = (a)+(b)+(c) 전체 묶음 (보드 본인 의도). 단계적 분리 옵션 따로 surface 안 됨.

## 의존성
- 선행 없음. 다른 P0 항목과 병렬 가능.
- 발급처 액세스 (CF/Replicate/FTC/NTS/Naver/Kakao/Google CSE/Google API/Enrichment Anthropic) — 보드 또는 BE.

## 검증
- adapterConfig.env GET → 모든 키 `type:'secret-ref'` 확인.
- 발급처 console 에서 old 키 invalidated 상태 확인.
- 다음 backup fire (2026-05-20 14:00 UTC) 후 GitHub repo body+manifest 에 평문 0건 verify.
