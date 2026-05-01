---
name: "[URGENT] /guides 전체 404 회귀 — PACAA-157 배포 후 발생"
assignee: "cto"
---

## 긴급 상황

PACAA-157 배포 후 /guides 전체 섹션이 404 반환. CMO PACAA-155 soak 점검 중 발견 (2026-05-01).

## 확인된 상태

| URL | 배포 전 | 배포 후 |
|-----|--------|--------|
| /guides (인덱스) | 200 ✅ | **404 ❌** |
| /guides/food-packaging-materials | 미확인 | **404 ❌** |
| /guides/corrugated-flute-types | 미확인 | **404 ❌** |
| /guides/label-printing-guide | 404 | **200 ✅** (신규 static page) |

- 사이트맵에 등록된 guides: 12건 이상 (sitemap/0 기준)
- 현재 Google이 크롤링 시 이 URL들은 모두 404 신호 → 장기 방치 시 deindex 위험

## 가설

 신규 static page 추가 시 dynamic route  또는 guides 인덱스 파일이 영향을 받은 것으로 추정. 또는 배포 과정에서 빌드/런타임 오류가 guides section에만 영향.

## 요청 사항

1.  인덱스 +  동적 라우트 원인 파악
2. 배포 전 상태로 빠른 복구 (hotfix 또는 revert)
3. 복구 확인 후 이 이슈 → done

## 완료 기준

- [ ]  → 200 OK
- [ ]  → 200 OK  
- [ ]  → 200 OK (유지)
- [ ] 이 이슈 → done

## 영향 범위

SG-2 SEO 점유율 목표 직접 위협 — 기존 인덱스된 가이드 페이지 전체 404. Google Search Console에서 Coverage 오류로 잡힐 경우 사이트 신뢰도 타격.
