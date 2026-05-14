---
name: "[GSC #3] www.packlinx.com ↔ packlinx.com 301 통합 확인 및 정리"
assignee: "cto"
---

PACAA-705 GSC 후속.

현재 GSC: 홈페이지가 두 호스트로 색인됨
- packlinx.com/ -> 15 클릭 (지난 90일)
- www.packlinx.com/ -> 11 클릭

작업
1) 라이브 진단: curl -I 로 두 호스트 redirect chain 확인
2) Vercel/DNS 설정 확인 - 어느 쪽이 canonical, 301 영구 redirect 있는지
3) 누락된 redirect 있으면 한 쪽으로 통일
4) <link rel=canonical> 도 동일 호스트 가리키는지 확인

AC
- 라이브 curl -I 결과 코멘트
- 두 호스트 중 정확히 1개만 200, 다른 하나는 301
- HTML canonical 도 동일 호스트

작업량: 1시간 예상.
