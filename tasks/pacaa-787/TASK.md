---
name: "[O3 사전] Playwright 직접 크롤링 법적 자문 — robots.txt / 저작권 / PIPA §15-2"
assignee: "legal-counsel"
---

## 목적
PACAA-784 결정 (보드 2026-05-17 answered): O3 (업체 웹사이트 HTML 직접 크롤링) 진행 가부를 Legal 자문으로 확정.

## 자문 요청 사항
1. **robots.txt 준수 시** 한국 B2B 업체 웹사이트의 공개 정보 (회사명·주소·전화·취급 품목·이메일) HTML 크롤링이 법적으로 허용되는가?
2. 저작권법상 단순 사실 정보(회사 정보) 추출의 적법성 (DB 권 vs fair use)
3. **PIPA §15-2** (개인정보보호법 — 개인사업자의 영업용 연락처) 적용 여부 — 4-필드 (이름·전화·주소·카테고리) + 제품/서비스 추가 가능 한도
4. **통신판매업 등록자**의 공개 의무 정보를 어디까지 활용 가능한가
5. 차단 사이트 (robots.txt Disallow / IP 차단) 우회 절대 금지 — 우리 정책 baseline 확인
6. Cache/저장 정책: 크롤한 HTML 원본 보관 기한·삭제 의무

## Acceptance Criteria
- 5개 질문 각각에 대해 "허용/조건부 허용/금지" + 근거 조항 + 우리 적용 가이드라인
- O3 진행 시 의무 가드 리스트 (예: User-Agent 명시, robots.txt 캐시, opt-out 즉시 적용, 분기당 1회 재크롤 한도 등)
- 위반 시 페널티 견적

## 컨텍스트
- 현재 우리는 Naver Open API 만 사용 (HTML 직접 fetch 0건)
- 두 번째 PC 분산 워커 검토 중 (O3 채택 시에만 활용)

## 부모 이슈
PACAA-784
