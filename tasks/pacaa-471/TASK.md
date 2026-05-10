---
name: "[PACAA-469] /blog/packaging-rfq-guide CTA /compare → / 교체 (3곳 + dateModified)"
assignee: "cto"
---

## 배경

[PACAA-469](/PACAA/issues/PACAA-469) CMO 판정: Option A — /blog/packaging-rfq-guide 블로그 포스트 본문 유지, CTA 3곳 + dateModified 교체.

RFQ feature 폐지([PACAA-466](/PACAA/issues/PACAA-466)) 후 /compare 링크가 존재 위치:
app/blog/packaging-rfq-guide/page.tsx

---

## 변경 사항 (정확한 diff)

### 1. dateModified — line 39
변경: "2026-05-08" → "2026-05-10"

### 2. Section 6 CTA — lines 351–354
변경: href="/compare" → href="/"
텍스트: "Packlinx 견적 비교 페이지에서 복수 업체를 한 번에 비교하세요 →" → "Packlinx 업체 디렉터리에서 포장 업체를 검색하세요 →"

### 3. Section 7 CTA — lines 413–417
변경: href="/compare" → href="/"
텍스트: "Packlinx에서 포장재 업체를 비교하고 견적을 요청하세요 →" → "Packlinx에서 포장재 업체를 검색하고 정보를 비교하세요 →"

### 4. Footer CTA — lines 528–531
변경: href="/compare" → href="/"
텍스트: "Packlinx 견적 비교 — 포장 업체를 한 곳에서 찾고 비교하세요 →" → "Packlinx — 포장 업체를 한 곳에서 찾고 비교하세요 →"

---

## 완료 조건

- 위 4개 변경사항 적용 및 커밋 (fix(PACAA-469): rfq-guide CTA /compare → / 교체)
- 빌드 통과 확인
- 배포 후 /blog/packaging-rfq-guide 접속 → /compare 링크 없음 확인
