---
name: "텔레그램 외부 알림 — 포맷 모듈 분리 + notify-telegram.py 분류 매핑 + dry-run"
assignee: "backend-engineer"
---

## 부모 이슈 / 사인오프

- 부모: [PACAA-106](/PACAA/issues/PACAA-106) — plan v1 (revision `998029a3-acfb-41d3-b421-199a10d3380e`) 보드 사인오프 완료 (interaction `1096ae43-3ac4-43b3-b386-ba87af0c5ec7` accepted, 2026-04-30).
- 본 이슈는 plan §3 마이그레이션 5단계의 **단계 1·2·5** 실행 + dry-run/sample fire 산출까지 담당. 단계 3·4 (PACAA-53/54 hub 디스크립션) 는 보드 피드백 통과 후 본격 도입 단계에서 별도 위임 예정.

## 산출물 (이 이슈)

1. **신규 파일** `tools/board-visibility/_telegram_format.py` — 본문 템플릿 빌더 + 첨부 빌더 + 자가검수 함수.
2. **수정 파일** `tools/board-visibility/notify-telegram.py` — 분류 매핑(A/B/C) + 새 빌더 사용 + `--dry-run` / `--sample={action|approval|choice}` 플래그 추가.
3. **신규 섹션** `packlinx-comms/SKILL.md` — "Board-facing Telegram output (PACAA-106)" 섹션 (plan §1 본문 그대로 박는다).
4. **검증 산출물** — `--dry-run --sample=action` 출력 텍스트 + 첨부 .txt 본문을 본 이슈 코멘트에 붙여 CEO 검토 요청.

산출물 4 통과 후 CEO 가 합성 액션 알림 1회 실발사 → 보드 모바일 피드백 → 본격 도입.

## 본문 템플릿 (plan §1 발췌, 구현 기준)

### A. 액션 알림

```
[액션] {보드가 무엇을 해야 하는지, 한 줄}
이유: {왜 필요한지, 한 줄}
막히는 일: {진행 안 되면 멈추는 작업, 한 줄}
상세: {첨부 파일명}
```

### B. 승인 요청

```
[승인] {무엇을 승인하는지, 한 줄}
승인 시: {한 줄 영향}
거절 시: {한 줄 영향}
상세: {첨부 파일명}
```

인라인 버튼: `✅ 승인` / `❌ 반려`.

### C. 선택지 요청

```
[선택] {무엇을 결정하는지, 한 줄}
1) {선택지 1} — {한 줄 영향}
2) {선택지 2} — {한 줄 영향}
3) {선택지 3}
