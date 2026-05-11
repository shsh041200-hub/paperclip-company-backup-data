---
name: "[CMO] PACAA-507 Phase B2 — FAQ + 약관 부속서 + vendor 카드 hover surface (LC §0 한정 문구)"
assignee: "ceo"
---

## 배경

[PACAA-507](/PACAA/issues/PACAA-507) Phase B 보드 승인 (CEO=owner, 즉시 발의). [PACAA-509](/PACAA/issues/PACAA-509) Legal Counsel 자문 §0/§4-A 의 한정 문구 surface 4 location 권고 시행.

참조: `docs/legal/vendor-verification-criteria.md` (PACAA-510 머지 완료, main 합류).

## LC §0 한정 문구 (필수, 변경 금지)

> 본 표시(`정보 등록`)는 외부 공인 인증기관(예: KS, ISO, Korean Standards Association, 한국정보통신기술협회 등)이 발급한 인증이 아닙니다. Packlinx 가 자체적으로 운영하는 등록 절차에 따라, 객관적·실증 가능한 기준을 만족한 업체에 한해 부여되는 표시입니다.

## Acceptance (LC §4-A 4 surface)

| Surface | 노출 형태 | 우선순위 | 본 작업 범위 |
|---|---|---|---|
| FAQ ("`정보 등록`은 무엇인가요?") | 전체 본문 + §1~3 요약 + §0 한정 문구 | **P0** | ✅ CMO 단독 |
| 약관 부속서 (별표) | §0~3 전문 또는 docs/legal/ 링크 | **P0** | ✅ CMO 단독 |
| Footer | "Packlinx 자체 등록 기준 안내" 링크 → FAQ 항목 | P1 | ✅ CMO + FE 협업 (FE 위임 sub-task 발의 가능) |
| Vendor 카드 hover / `?` 아이콘 tooltip | §0 한정 문구 1줄 + FAQ 링크 | **P0** | ✅ CMO 카피 + FE implement (FE 위임 sub-task 발의) |
| 가이드 metaDescription | "검증된 업체" 표현 제거 | P0 | **이미 완료** ([PACAA-508](/PACAA/issues/PACAA-508) PR #57 머지) — skip |

### 작업 단계

1. FAQ 항목 추가 (현재 사이트 FAQ 페이지가 없으면 생성 — `app/faq/page.tsx` 또는 footer 의 "자주 묻는 질문" 라우트). "`정보 등록`은 무엇인가요?" 항목 + LC §1~3 요약 + §0 한정 문구.
2. 약관 부속서 — 약관 페이지 (`app/terms/` 등) 에 별표 "vendor 정
