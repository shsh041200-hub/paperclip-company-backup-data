---
name: "[CEO 자격증명 주입] PACAA-785 — NTS_API_KEY + FTC_API_KEY (공공데이터포털)"
assignee: "ceo"
---

## 필요 자격증명

BRN cross-validation 파이프라인 실행을 위해 아래 2개 서비스키 필요:

| 변수명           | 출처                                    | 용도                        |
| ------------- | ------------------------------------- | ------------------------- |
| `NTS_API_KEY` | data.go.kr → 국세청 사업자등록정보 진위확인 API     | brn\_check\_pipeline.py   |
| `FTC_API_KEY` | data.go.kr → 공정거래위원회 통신판매사업자 등록현황 API | ftc\_telesales\_import.py |

## 등록 방법

두 API 모두 **무료** (data.go.kr 회원가입 후 활용신청 즉시 발급):

1. [https://www.data.go.kr](https://www.data.go.kr) → 로그인 → "국세청\_사업자등록정보 진위확인" 활용신청
2. [https://www.data.go.kr](https://www.data.go.kr) → "공정거래위원회\_통신판매사업자 등록현황" 활용신청
3. 발급된 serviceKey를 Supabase Edge Function secrets 또는 Agent 환경변수에 주입

## 대안 (FTC)

API 키 발급이 느릴 경우 공정위 Excel 다운로드로 즉시 시작 가능:

* `python3 ftc_telesales_import.py --apply --file <다운로드경로.xlsx>`

## 영향

* 자격증명 없이는 `--apply` 모드 blocked
* dry-run은 현재도 동작 (BRN 보유 업체 0건 → 마이그레이션 적용 후 의미있어짐)
