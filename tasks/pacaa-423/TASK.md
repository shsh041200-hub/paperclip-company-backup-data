---
name: "PACAA-420 v1 목업 정적 배포 — /mockups/guide-v2/{index,detail}.html"
assignee: "frontend-engineer"
---

## 목적
PACAA-420 (가이드 페이지 UI 개선) 보드 검수용 **HTML 목업 v1** 두 개를 packlinx.com 정적 경로에 배포해 보드가 브라우저로 직접 확인할 수 있게 하는 게 전부다.

**구현이 아니라 배포만.** 실제 가이드 페이지 코드는 절대 건드리지 말 것. 이 목업이 보드 OK 받은 뒤에 별도 implementation child 로 분리될 예정.

## 산출물
배포 후 라이브 접근 가능해야 함:
- `https://www.packlinx.com/mockups/guide-v2/index.html` — 가이드 인덱스 페이지 목업
- `https://www.packlinx.com/mockups/guide-v2/detail.html` — 가이드 상세 페이지 목업 (canonical template, 골판지 박스 업체 선정 가이드 콘텐츠로 채움)

## 배포 방법 (Next.js public/ 정적 파일)
1. `pkging-platform` repo 에서 브랜치 만들기 — `feat/pacaa-420-mockup-v1`
2. 디렉토리 생성: `public/mockups/guide-v2/`
3. 아래 두 파일을 그대로 복사:
   - `public/mockups/guide-v2/index.html` ← 본 description 의 첫 번째 코드블록 그대로
   - `public/mockups/guide-v2/detail.html` ← 이 issue 첫 번째 코멘트 코드블록 그대로
4. **robots/sitemap 등재 금지** — 검수용이므로 노출 차단. 그냥 정적 파일만 두고 끝낼 것 (Next.js public/ 은 sitemap 자동 생성에 안 잡히므로 별도 조치 불필요).
5. PR 만들고 보드 머지 → Vercel 자동 배포 → 두 URL 200 확인
6. 두 URL 200 확인되면 본 issue 코멘트로 라이브 URL 보고 → CEO 가 보드 interaction 발사

## acceptance
- [ ] PR 머지 + Vercel deploy 성공
- [ ] `curl -I https://www.packlinx.com/mockups/guide-v2/index.html` → 200
- [ ] `curl -I https://www.packlinx.com/mockups/guide-v2/detail.html` → 200
- [ ] 두 페이지 브라우저 렌더링 정상 (스타일 깨짐 없음
