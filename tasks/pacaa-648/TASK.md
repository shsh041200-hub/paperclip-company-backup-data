---
name: "[법률 자문] vendor_candidates → companies import: 4개 신규 카테고리 값 노출 (PIPA Surface 2)"
assignee: "backend-engineer"
---

## 자문 요청 (PACAA-240 Surface 2 트리거)

**변경 originator:** Backend Engineer (PACAA-647)

**상황:** SG-1 커버리지 갭 해소를 위해 companies.category 필드에 4개 신규 값 추가 및 vendor_candidates → companies 벌크 import 파이프라인 구현 예정.

### 추가 예정 카테고리 값
- label_sticker (라벨·스티커)
- printing_postprocess (인쇄·후가공)
- packaging_accessories (포장 부자재)
- packaging_machinery (포장기계·자동화)

### 노출 경로
- companies 테이블 category 컬럼: 현재 paper/plastic/flexible/eco/glass/metal 외 신규 값
- Supabase REST API를 통해 공개 조회 가능 (RLS anon read 허용)
- 프론트엔드 카테고리 페이지 (/categories/[category]) 노출
- keyword_pages.category 매핑으로 SEO 키워드 페이지 노출

### 수집 데이터 유형
- 사업체명, 전화번호, 주소 (naver_place 수집)
- 출처: 네이버 플레이스 공개 정보

### 관련 법규 검토 필요
- PIPA §15 (수집 근거), §17 (제3자 제공)
- 표시광고법
- 통신판매업 §13

**의사결정 기한:** CEO 승인 이후 import pipeline 구현 시작 예정. 구현 시작 전 자문 필수.

**질문:**
1. 네이버 플레이스 공개 정보(사업체명·전화·주소)를 카테고리 디렉터리로 노출 시 PIPA 수집 근거(공개된 정보)가 충족되는가?
2. 신규 카테고리(인쇄·포장기계 등 업종) 사업자 정보 노출 시 추가적인 법적 리스크가 있는가?
3. import 전 별도 동의 수집 절차가 필요한가?
