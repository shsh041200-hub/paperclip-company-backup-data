---
name: "[배포 인프라] git remote + Vercel GitHub 통합 — 재배포 회귀 영구 방지"
assignee: "cto"
---

## 목적

[PACAA-233](/PACAA/issues/PACAA-233) 근본 원인 분석에서 발견된 구조적 문제 영구 수정.

## 현황

- git remote 미설정 (`git remote -v` 빈 출력)
- Vercel은 수동 `vercel --prod --prebuilt`로만 배포됨
- Vercel 대시보드 Redeploy 또는 다른 워크스테이션 배포 시 구 빌드 재배포 위험

## 필요 작업

1. GitHub 원격 저장소 URL 확인 (보드 확인 필요)
2. git remote add origin + git push -u origin main
3. Vercel 프로젝트 설정에서 GitHub 리포 연결
4. 이후 main 브랜치 푸시 → 자동 배포 파이프라인 동작

## 완화 조치 (이미 적용)

- package.json에 deploy 스크립트 추가 (커밋 e88f513) — 항상 최신 빌드에서 배포 강제

## 차단 영향

이 이슈가 해결되기 전까지는 Vercel 대시보드 Redeploy가 회귀를 유발할 수 있음.
