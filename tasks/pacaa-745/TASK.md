---
name: "[회의 PACAA-737] vendor 모델 분류 표현 — FE V1 UI 분기 wireframe 자문"
assignee: "frontend-engineer"
---

**FE Engineer 자문 청구** — V1 UI 분기 (PACAA-737 vendor 모델 분류 회의).

---
## CEO 1차 안 — Vendor 모델 분류 표현 (PACAA-737 V1 보강)

**보드 결정 (2026-05-16)**: V1 채택. Vendor 두 모델 구분 표현 신규 작업.

**두 모델 정의 (보드 메시지)**:
- **Model A — 기업 거래 전문**: 통신판매업 신고 X + 회사 홍보용 사이트 + 초대량 B2B 위주. 영업 = 오프라인/전화/이메일 견적.
- **Model B — 샘플·소량부터 가능**: 통신판매업 신고 O + 웹에서 샘플/소·대량 거래 + 정보·이미지 풍부. 영업 = 웹 + 오프라인 혼합.

**V1 페이지 표현 방식 (1차 draft)**:
1. **상단 배지** (vendor name 옆): "기업 거래 전문" 또는 "샘플·소량부터 가능"
2. **거래 방식 박스** (사업자 박스 옆/아래 신설):
   - A: "거래 방식: 초대량 B2B 위주 — 견적 문의 권장"
   - B: "거래 방식: 샘플·소량부터 가능 — 웹 카탈로그/직접 견적"
3. **CTA 차별** (sticky):
   - A: "견적 문의" 단일 (전화/카톡/이메일)
   - B: "샘플 요청" + "견적 문의" 2-CTA
4. **분류 데이터 출처**: 통신판매업 신고번호 DB 필드 (1차) + vendor 옵트인 폼 (선택, BE 작업)

**ANTI (memory `feedback_vendor_telesales_registration_signal.md` baked, 위반 시 reject)**:
- Model A 를 "위험/미신고/주의" 라벨 금지
- 둘 다 동등 "다른 거래 모델" 로 표현 (평가 등급 X)
- "신고 안 한 곳 위험" 카피 금지
- 분류는 buyer 정보 보충용, vendor 등급 아님

---
## FE 검토 질문 (V1 UI 분기)

1. **wireframe**: 배지/거래방식박스/CTA 분기 UI 스케치 (모바일/데스크탑) — 간단 텍스트 wireframe OK.
2. **컴포넌트 위치**: V1 (`/internal/vendor-redesign/v1/[slug]`) 현재 구조에서 어느 컴포넌트에 추가? (page.tsx + 신규 component 트리 제안)
3. **데이터 prop 설계**: `vendorModel: 'A' | 'B' | 'un
