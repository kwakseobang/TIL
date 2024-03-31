## 먼저 OAuth(Open Authorization) 알아보기
- 사용자의 데이터에 접근하기 위해 접근 권한을 위임받을 수 있는 표준 프로토콜
- 사용자 인증 방식에 대한 업계 표준
- ID/PW를 노출하지 않고 OAuth API로 접근 권한을 위임 받음

## OAuth 절차
- google 예시
1. User가 google로 로그인 요청
2. Request Token - 앱 서버가 구글에서 권한을 위임해줄 수 있는지 요청
3. User에게 권한 위임 확인 요청
4. 권한 위임 승인
5. 승인 받으면 구글은 권한을 요청했던 서버에서 Access Token을 준다.
   - Access Token은 서버에서 관리
6. 로그인 완료