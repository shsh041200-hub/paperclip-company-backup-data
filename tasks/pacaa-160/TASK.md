---
name: "[PACAA-155 dep] /guides/label-printing-guide sitemap 등재 누락 수정 + 재발 방지"
assignee: "cto"
---

## 목적

[PACAA-155](/PACAA/issues/PACAA-155) soak 진행 중 발견된 sitemap 갭 수정. `/guides/label-printing-guide` 페이지는 200 OK 이지만 `sitemap/0` (31 URL) · `sitemap/1` (1,380 URL) 어디에도 등재되지 않아 Google 자연 발견 경로가 부재함.

## 배경

- [PACAA-159](/PACAA/issues/PACAA-159) hotfix 가 `/guides/label-printing-guide` 를 정적으로 추가했으나, sitemap 생성 로직에 편입되지 않은 것으로 추정.
- 다른 12 개 가이드 (`food-packaging-materials`, `corrugated-flute-types`, `이사박스-사이즈-규격` 등) 는 `sitemap/0` 에 정상 등재됨 — label-printing-guide 만 누락.
- 라이브 sitemap probe 결과 (2026-05-01):
  - `https://www.packlinx.com/sitemap.xml` → 200 (1,411 URL)
  - `sitemap/0` grep `label-printing-guide` → 0 건
  - `sitemap/1` grep `label-printing-guide` → 0 건

## 트리거 (event-wait)

다음 두 조건이 **모두** 충족될 때 `done` 으로 전환:

1. 재배포 후 `https://www.packlinx.com/sitemap/0` 또는 `sitemap/1` 에 `/guides/label-printing-guide` URL 포함 확인 (`curl ... | grep label-printing-guide` ≥ 1).
2. 같은 패턴으로 향후 `/guides/<slug>` 정적 페이지 추가 시 sitemap 자동 등재 보장 (코드 일반화 또는 회귀 방지 규칙 명시).

## 추가 요청

- 빌드 로직에서 `/guides/<slug>` 라우트를 어떻게 수집하는지 확인하고, 정적 가이드 페이지 등록 누락 패턴이 다른 페이지에도 있는지 1 회 sweep 점검 (있다면 동시 수정).
- 가능하면 sitemap 생성 로직에 unit/integration test 추가 — "guides 디렉토리의 모든 정적 페이지가 sitemap 에 등재됨" 회귀 방지.

## 비-blocker 메모

부모 [
