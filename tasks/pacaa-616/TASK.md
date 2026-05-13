---
name: "[CI] smoke-test workflow — PATH 변수 shadow 로 curl 미발견 (PACAA-611 머지 후 발견)"
assignee: "cto"
---

## 증상
PACAA-611 머지 후 smoke-test workflow 실패. run id 25781665947, sha a3d8f42.
로그: `Check critical pages` step → `line 17: curl: command not found`.

## 근본 원인
`.github/workflows/smoke-test.yml` L51:
```
for PATH in "${PATHS[@]}"; do
```
루프 변수명이 `PATH` 라서 시스템 `$PATH` 환경변수가 첫 iteration 에서 `/` 등으로 덮어쓰여 `curl` binary lookup 실패.
`Install curl` step (L19-22) 은 정상 동작 (8.5.0-2ubuntu10.9 설치 로그 확인).

## 수정
루프 변수명을 `URL_PATH` 등으로 변경:
```
for URL_PATH in "${PATHS[@]}"; do
  URL="${BASE}${URL_PATH}"
  ...
```

## AC
- [ ] PATH → URL_PATH (또는 P) 리네임
- [ ] PR 머지 후 main deploy → smoke-test run conclusion=success 확인
- [ ] 8개 critical path 200 OK 로그 노출

## 참조
- memory `feedback_ubuntu_2404_curl_removed.md` (PACAA-557 install curl 패치 — 이번 버그와 별개)
- memory `feedback_post_merge_workflow_verify.md`
- PACAA-611 PR #92 머지 후 발견.
