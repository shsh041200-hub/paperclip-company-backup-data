---
name: "Backup pipeline: permanent secret scrubber + rotation tracking"
assignee: "backend-engineer"
---

PACAA-657 (2026-05-13)에서 처음 발견: 회사 export(.paperclip.yaml)가 이슈 코멘트 본문을 그대로 dump하면서 production secrets 5종이 노출. 오늘 push는 GitHub push protection이 막아 public repo는 안전. CEO가 임시 scrubber로 redact 후 push 완료 (commit eb8872d).

## 후속 작업

### 1. 영구 scrubber 통합
- `$AGENT_HOME/backup-work/scrub_secrets.py` 의 패턴을 `write_export.py` 의 commit 직전 단계에 통합.
- 새 secret 패턴 발견 시 추가하기 쉽도록 외부 JSON config로 분리.
- write_export.py 가 redaction 수를 stdout에 보고 → PACAA-### 백업 close-out 코멘트에 자동 포함.

### 2. 노출된 토큰 rotation 추적
2026-05-01 PACAA-168/190/266 코멘트에 plaintext로 박힌 secrets:
- Cloudflare API 토큰 3건 (`cfut_Cl103Sa...`, `cfut_iS4HL6rs9...`, `cfut_jjIllQuMD...`)
- Paperclip Worker JWT (`pcp_13897a46bb...`)
- GitHub 웹훅 시크릿 (`1e38fcfe5f38...` 64-hex)
- 파운더 대시보드 비밀번호 (`packlinx.com/admin`)

2026-05-01 메모에 "weekly rotate ~2026-05-08 만료" 라고 적혀있어 대부분 이미 rotate 된 것으로 추정. 보드가 각 토큰의 현 유효성을 확인하고 미rotate 토큰은 즉시 rotate.

### 3. DB redaction (선택)
원본 코멘트의 토큰을 DB에서 `[REDACTED-<type>]`로 교체하면 향후 export 자체에 secret 없음 → scrubber는 defense-in-depth. CEO 권한 밖일 수 있어 보드 판단.

## DoD
- [ ] write_export.py 가 scrub_secrets 통합되어 push 전 자동 적용
- [ ] secret 패턴 config 외부화
- [ ] 노출된 5종 토큰 rotation 상태 board 확인 (이슈 코멘트로 보고)
- [ ] (선택) PACAA-168/190/26
