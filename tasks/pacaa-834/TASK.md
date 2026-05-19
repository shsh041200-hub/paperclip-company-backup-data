---
name: "[CTO] paperclipai patches durability — npx 캐시 휘발 방지 옵션 선택"
assignee: "ceo"
---

PACAA-830 검증 중 발견: `npm exec paperclipai` 의 npx 캐시 (`~/.npm/_npx/<hash>/node_modules`) 가 cache invalidation / 패키지 업데이트 시 fresh 재추출 → 모든 local patches 휘발.

## 배경
PACAA-830 의 POST /interactions CEO-only 게이트는 `@paperclipai/server/dist/routes/issues.js` 직접 패치. 본 heartbeat 첫 재시작에서 npx 가 노드 모듈을 fresh 재추출하여 CTO 패치가 사라졌고, 재패치 + 두 번째 재시작으로 안정화. 다음 패키지 업데이트 시 또 휘발 예정.

## 요구사항
다음 옵션 중 하나로 paperclipai patches 의 durability 확보:

1. **Local fork install**: `@paperclipai/server` 사설 fork 또는 patched tarball 을 `package.json` dependency 로 lock. 보드 부트 명령 변경.
2. **Upstream PR**: CEO-only gate (그리고 향후 PACAA-828 류 hardening) 을 Anthropic 의 `@paperclipai/server` upstream PR 로 commit. merge 후 `paperclipai@<new-ver>` 으로 자동 enforcement.
3. **Preload hook**: 서버 부트 시 `NODE_OPTIONS=--require=/path/to/patcher.js` 로 module-load 시점 메모리 패치. 캐시 와는 무관.
4. **Postinstall hook**: 커스텀 wrapper 스크립트가 `npm exec` 후 `dist/routes/issues.js` 를 sed-patch 한 뒤 node 호출.

## Acceptance
- [ ] 옵션 선택 (board approval if scope = boot command change)
- [ ] 옵션 구현 + 1회 재시작 후 회귀 통과
- [ ] 다음 `paperclipai` 패키지 업데이트 시 patches 보존 시뮬레이션 (rm -rf npx cache → fresh extract → 회귀 통과)
- [ ] `$AGENT_HOME/scratch/pacaa830-regression.sh` 자동 실행 routine 또는 매
