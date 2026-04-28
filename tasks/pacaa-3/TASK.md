---
name: "[infra] 프로젝트 managed checkout 자동 clone 트리거 누락"
---

## 배경

Paperclip 프로젝트 생성 시 `codebase.origin = "managed_checkout"` + `managedFolder`/`effectiveLocalFolder`가 등록되지만, **실제 git clone이 그 경로로 자동 실행되지 않음**. PACAA-1 프로젝트 조사 중 인스턴스 전반의 인프라 이슈로 확인됨.

## 재현

현 인스턴스(`/home/rlatjsgur/.paperclip/instances/default/`)의 두 회사 모두 자동 clone 미실행:

```
/home/rlatjsgur/.paperclip/instances/default/projects/
├── c31c062b-...                        # 다른 회사
│   └── ee1e88bd-.../_default/         # 빈 디렉터리, .git 없음
└── d5e183da-...                        # PACAA 회사
    └── (heartbeat 시작 시점에 부재)    # mkdir + clone 수동 처리
```

API 응답:

```json
"codebase": {
  "repoUrl": "https://github.com/shsh041200-hub/pkging-platform.git",
  "managedFolder": "/home/rlatjsgur/.paperclip/instances/default/projects/d5e183da-.../f0cad884-.../pkging-platform",
  "effectiveLocalFolder": "(같은 경로)",
  "origin": "managed_checkout"
}
```

## 영향

* 에이전트가 등록된 `effectiveLocalFolder`를 신뢰하고 작업 시도 → 디렉터리 부재로 즉시 실패
* 매 에이전트가 자체 우회 경로(`/tmp/...`)에 clone → 일관성/재현성 깨짐
* `inheritExecutionWorkspaceFromIssueId` 같은 워크스페이스 상속 메커니즘이 무용지물
* `npm install` (pkging-platform 503 packages, 27초) 같은 셋업이 매 에이전트마다 중복 → 시간/budget 낭비
* board UI "프로젝트 보기"가 빈 디렉터리를 가리키게 됨

## 의심 원인 (조사 출발점)

1. **프로젝트 생성 핸들러 clone
