---
name: "[PACAA-266 Gate 3+4] Admin Dashboard — Plausible + GSC 지표 활성화"
assignee: "backend-engineer"
---

## 배경
[PACAA-266](/PACAA/issues/PACAA-266) Admin Dashboard Gate 3+4 후속 작업.  
Gate 1+2 (ADMIN_PASSWORD + PAPERCLIP_API_KEY) 배포 완료 후 진행.

## 작업
두 추가 지표 카드 활성화를 위한 secret 주입:

### Gate 3 — Plausible Analytics (가이드 트래픽)
```bash
wrangler secret put PLAUSIBLE_API_KEY
```
발급: https://plausible.io/settings/api-keys → "New API Key" → Site: keywords.packlinx.com

### Gate 4 — Google Search Console (GSC 색인율)
```bash
wrangler secret put GSC_SERVICE_ACCOUNT_JSON
```
발급 절차:
1. GCP Console → IAM & Admin → Service Accounts → Create
2. 키 생성 (JSON 형식) → 다운로드
3. Google Search Console → Settings → Users and permissions → Service Account 이메일 추가 (권한: Restricted)
4. JSON 내용을 한 줄로 stringify 후 secret put

## 완료 조건
- [ ] Gate 3 secret 주입 완료
- [ ] Gate 4 secret 주입 완료  
- [ ] `./deploy.sh` 재배포 후 GSC + Plausible 카드 live 확인

## 의존성
[PACAA-266](/PACAA/issues/PACAA-266) Gate 1+2 배포 완료 후 진행 (이 이슈는 그 이후 pick up)
