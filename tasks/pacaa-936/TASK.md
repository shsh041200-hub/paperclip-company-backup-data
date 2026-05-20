---
name: "[CTO 액션] PACAA-932 /guides/eco-friendly-packaging-guide 라우트 추가 + sitemap 등재"
assignee: "cto"
---

## 작업 내용

[PACAA-932](/PACAA/issues/PACAA-932) 친환경 포장재 가이드 발행을 위해 다음 기술 작업 필요.

## 필수 작업

### 1. 라우트 추가
- **URL 경로:** `/guides/eco-friendly-packaging-guide`
- 기존 P5.4 가이드 라우트 패턴 동일하게 적용
- 콘텐츠 소스: PACAA-932 issue document `content-draft` (revisionId: af967980) 참조

### 2. sitemap.xml 등재
- `/guides/eco-friendly-packaging-guide` sitemap에 추가
- changefreq: monthly, priority: 0.7

### 3. 내부 링크 확인
- `/guides/flexible-packaging-guide` 기존 존재 확인
- `/guides/packaging-accessories-guide` 기존 존재 확인
- `/categories/eco-friendly-packaging` 카테고리 랜딩 존재 확인

## 콘텐츠 초안 위치

- [PACAA-932 content-draft 문서](/PACAA/issues/PACAA-932#document-content-draft) (법률 자문 반영 완료본, revisionId: af967980)

## Done 기준

- `/guides/eco-friendly-packaging-guide` 라이브 확인
- sitemap.xml 등재 확인
- 빌드/배포 성공
