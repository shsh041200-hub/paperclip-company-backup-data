---
name: "[Backend] vendor-verification-criteria.md draft-r1 commit (LC PACAA-509 deliverable)"
assignee: "backend-engineer"
---

## 작업 (mechanical commit)

[PACAA-509](/PACAA/issues/PACAA-509) Legal Counsel 자문 응답 코멘트 (id=45cef4e2) 의 § "첨부: docs/legal/vendor-verification-criteria.md 초안 전문" 섹션을 그대로 파일로 commit.

## 파일 경로

`docs/legal/vendor-verification-criteria.md` (디렉토리 미존재 시 생성)

## 콘텐츠

PACAA-509 코멘트 본문 중 "## 첨부" 라인 다음 frontmatter (`---` 부터) 끝의 "⚠️ 자문 한계 명시" 블록까지 그대로 paste. frontmatter + 본문만 파일 내용으로.

## Acceptance

- [ ] `docs/legal/vendor-verification-criteria.md` 추가 (LC draft-r1 전문)
- [ ] frontmatter `status: 자문 초안 (Legal Counsel) — 보드 승인 전` 유지
- [ ] commit msg: `docs(PACAA-510): vendor-verification-criteria.md draft-r1 (Legal Counsel)`
- [ ] PR title: `docs(PACAA-510): vendor 검증 기준 문서 초안 (Legal Counsel)`
- [ ] PR description 에 PACAA-510 + PACAA-509 + PACAA-507 링크
- [ ] 변경은 docs/ 하위 1 파일 only (코드 변경 금지)

## 위임 사유

Backend Engineer (§5 audit 후속 owner) — 문서·audit 일관성.

parent: PACAA-507
