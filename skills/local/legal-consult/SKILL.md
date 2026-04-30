---
name: "legal-consult"
description: "Legal Counsel 호출 표준 절차 — 법적 우려가 있는 결정에서 한국 법률 자문을 받는 절차. PIPA / 표시광고법 / 통신판매업 / 저작권·상표권 / 약관 영역. SG-1~4 trigger 룰과 함께 사용."
slug: "legal-consult"
metadata:
  paperclip:
    slug: "legal-consult"
    skillKey: "local/04cb0580f6/legal-consult"
  paperclipSkillKey: "local/04cb0580f6/legal-consult"
  skillKey: "local/04cb0580f6/legal-consult"
key: "local/04cb0580f6/legal-consult"
---

# Legal Consult — Legal Counsel 호출 표준 절차

## 누가 사용하는가

Packlinx 모든 에이전트. 법적 우려 (PIPA / 표시광고법 / 통신판매업 / 저작권·상표권 / 약관) 가 있는 결정 / 행동 / 산출물을 다룰 때.

## 호출 트리거 인지

각 SG 별 구체 trigger 는 SOUL.md (Backend/CTO) 또는 `goal_skills/sg{2,4}_*.md` 에 박혀 있다. 요약:

- **SG-1 (Vendor coverage):** vendor 정보 필드 추가 / 식별 정보 노출 / 정정·삭제 채널 (PIPA)
- **SG-2 (SEO):** 외부 콘텐츠·이미지·로고 사용 (저작권) / 타사 상표 (상표권) / 광고 라벨링 (표시광고법)
- **SG-3 (측정 인프라):** Plausible/analytics 도입 (PIPA + 쿠키 동의) / 행동 데이터 폼
- **SG-4 (Vendor self-action):** 약관·처리방침 변경 / claim·edit·intent 폼 데이터 항목

trigger 매칭 인지 못한 경우 Monday 09:30 KST routine 에서 Legal Counsel 이 회고 자문 발행 — 그래도 trigger 시점 호출이 안전하다.

## 호출 절차

1. **PACAA child issue 생성:**
   ```
   POST /api/companies/{companyId}/issues
   {
     "title": "[법률 자문] {간단한 질문 한 줄}",
     "description": "{컨텍스트: 어느 SG / 어느 결정. 구체 질문. 의사결정 데드라인}",
     "assigneeAgentId": "54623669-64c6-402d-b87b-c0b8ebae3940",
     "parentId": "{본 작업 issue id}",
     "goalId": "{본 작업 goal id}",
     "priority": "{본 작업 priority — 보통 medium}"
   }
   ```
2. **응답 대기.** Legal Counsel 은 호출 시 wake (heartbeat off — wakeOnDemand). 응답 시간 < 1 heartbeat 통상.
3. **응답 인용.** Legal Counsel 응답 본문에는 항상 디스클레이머 블록이 부착되어 있다 — 자기 결정 코멘트에 인용 시 **그대로 포함**, 절단·요약 금지.

## 디스클레이머 (응답에 자동 부착되어 도착)

```
---
⚠️ 자문 한계 명시:
이 자문은 참고용이며 법적 책임 면제를 보장하지 않습니다.
사고 발생 시 면책 사유로 사용될 수 없습니다. Packlinx 보드는
외부 변호사 자문 미도입을 결정한 상태이며, 모든 법적 리스크는
Legal Counsel 자문에 의존합니다.
---
```

이 블록은 Legal Counsel SOUL.md (§4) + 본 스킬 양쪽에 박혀 있다 (이중 fallback). 호출자는 절단 금지.

## 한국 외 법률 영역 감지

질문이 GDPR / CCPA / 일본 APPI / 미국 노동법 / 국제 세무 등으로 이탈할 경우 Legal Counsel 은 명시적으로 회피 + CEO 에 escalation 한다. 이 경우 호출자는 CEO 결정을 기다린다.

## 응답 품질 기대치

- 위험 등급 (낮음 / 중간 / 높음 / 금지) 명시
- 적용 법률 조항 단위 인용
- "법무팀과 상의하세요" 식 책임 회피 응답 거부됨 — Legal Counsel 본인이 그 법무팀
- 디스클레이머 누락 시 응답 무효 → 재작성 요청

## 호출 비용 + 사후 검증

paperclip subscription 한도 내. 호출 빈도 ~3-5회/주 추정. PACAA-101 §5.8 deferred row 에 8주 spot-check (자문 5건+8주 OR 2026-06-25 backstop) — 자문 품질 보드+CEO 가 사후 audit. 부족 판단 시 외부 변호사 트리거 도입 재논의.
