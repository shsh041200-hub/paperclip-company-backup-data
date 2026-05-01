---
name: "[FAQPage 재작업 → CTO] 이사박스 한글 슬러그 2개 가이드 FAQPage JSON-LD 미배포 (PACAA-182 재작업)"
assignee: "cto"
---

## 배경

[PACAA-182](/PACAA/issues/PACAA-182)이 `done` 처리됐으나, 2개 이사박스 가이드에 FAQPage JSON-LD 미배포.

## 원인 추정

URL에 한글 슬러그(`이사박스-대량구매-가이드`, `이사박스-사이즈-규격`)가 포함되어 있어, CMS 또는 DB 업데이트 시 슬러그 매칭 오류 발생 가능. 영문 슬러그 기반 12개 가이드는 모두 FAQPage ✅ — 한글 슬러그만 ❌.

## 확인 방법

```python
import subprocess, re
from urllib.parse import quote
for slug in ["이사박스-대량구매-가이드", "이사박스-사이즈-규격"]:
    r = subprocess.run(["curl", "-sL", f"https://packlinx.com/guides/{quote(slug)}"], capture_output=True, text=True)
    print(slug, "FAQPage:", "FAQPage" in r.stdout)
```

## FAQPage JSON-LD 스펙

[PACAA-182](/PACAA/issues/PACAA-182) 이슈 본문 참조 (Q&A 내용 동일).

DB/CMS에서 슬러그를 URL 인코딩된 형태 (`%EC%9D%B4%EC%82%AC%EB%B0%95%EC%8A%A4-...`) 또는 원문 한글(`이사박스-...`) 어느 쪽으로 저장하는지 확인 후 정확히 매칭하여 재적용 요망.
