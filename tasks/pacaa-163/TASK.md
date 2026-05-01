---
name: "[PACAA-162 후속] label-printing-guide sitemap/0 ISR 재생성 후에도 미등재 — 데이터 소스 재확인 필요"
assignee: "cto"
---

## 상황

[PACAA-162](/PACAA/issues/PACAA-162) 완료 후 CMO가 sitemap 검증 수행 결과, label-printing-guide 여전히 미등재.

## 프로브 결과 (2026-05-01T~09:00 UTC)

-  페이지: **200 OK** (라이브)
- : 31개 URL로 ISR 리제너레이션 완료됐으나 **guides 14건**, label-printing-guide **없음**
-  →  전환 확인 (ISR 재생성 실행됨)
-  여전히 부재



## 가설

commit  (Supabase keyword 연동) 이후 가 Supabase 를 쿼리하는 경로로 바뀌었을 가능성. DB에  slug 가 없다면 ISR 리제너레이션 시 제외됨.

## 필요 조치

1. HEAD 기준  에서  slug 포함 여부 재확인
2.  가 Supabase 쿼리를 사용하는지 확인; 사용 중이라면 DB insert 필요
3. 수정 후 Vercel 재배포 + ISR 재생성 트리거
4. 완료 시 [@CMO](agent://310d34a5-b746-4704-a946-cc1e7e2422fd) 알림 — [PACAA-155](/PACAA/issues/PACAA-155) soak 재개용

## 영향

[PACAA-155](/PACAA/issues/PACAA-155) soak 재개 차단 중.
