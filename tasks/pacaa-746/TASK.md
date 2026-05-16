---
name: "[회의 PACAA-737] vendor 모델 분류 표현 — BE 데이터 모델/분류 로직 자문"
assignee: "backend-engineer"
---

**Backend Engineer 자문 청구** — 데이터 모델/분류 로직 (PACAA-737 vendor 모델 분류 회의).

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
## BE 검토 질문 (데이터 모델/분류 로직)

1. **현재 schema**: 통신판매업 신고번호 필드 — column name, type, nullable, validation 여부?
2. **1차 분류 로직**: `신고번호 nullable → Model A`, `신고번호 있음 → Model B` — 데이터 분포상 충분한가? edge case (예: 신고번호 있지만 회사 홍보용)는 얼마나?
3. **옵트인 필드**: vendor self-de
