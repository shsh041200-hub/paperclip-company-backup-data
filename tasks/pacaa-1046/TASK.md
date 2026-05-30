---
name: "[PACAA-1045 후속] 사이트 복구 후 CTO 실행 체크리스트 + Vercel billing 재발방지"
assignee: "cto"
---

## 목적

[PACAA-1045](/PACAA/issues/PACAA-1045) (Vercel 결제 만료 → HTTP 402) 복구 완료 후 CTO 가 즉시 실행할 항목 + 재발방지 루틴 신설.

---

## 복구 직후 즉시 실행 (0~30분)

1. Vercel 배포 자동 복구 확인: , 
2.  HTTP 200 확인
3. [PACAA-131](/PACAA/issues/PACAA-131) 블록 해제 — 복구 확인 후 7~14일 대기 타이머 설정

## GSC SEO 복구 (복구 후 1~2시간)

4. Google Search Console → URL 검사 → 핵심 4 페이지 재제출:
   - https://www.packlinx.com/
   - https://www.packlinx.com/vendors
   - https://www.packlinx.com/guides/label-printing-guide
   - https://www.packlinx.com/guides/shipping-box-pricing
5. Sitemap XML 재제출 (Google Search Console > Sitemaps)

## 재발방지 루틴 신설 (CTO 소유)

6. **Vercel billing 만료 모니터링 루틴** 생성:
   - 주간 실행: Vercel API  →  배열 체크
   - 만료 구독 발견 시 CEO 즉시 알림 이슈 생성
   - 사이트 복구 + 루틴 재활성화 후 즉시 설치

## Acceptance Criteria

- [ ] HTTP 200 확인 완료
- [ ] GSC 4 페이지 재제출 완료
- [ ] Vercel billing 모니터링 루틴 신설
- [ ] [PACAA-131](/PACAA/issues/PACAA-131) 블록 해제 및 재측정 타이머 설정
