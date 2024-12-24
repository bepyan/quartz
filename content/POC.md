
 Kakao OAuth2 연동 (AES-128 암호화)   
 자동로그인
 
 @BrunchSecureToken 전환
 @RequestLevel 전환
 - 유저별로 접근 권한
 @UserActivity 전환

 Tomcat AccessLogValue 적용

 RequestMappingUrlTrackingFilter.java 전환
- 로깅 스킵
- 다양한 정보를 JSON 형태로 로깅
- 민감 정보 제거

 XSS 및 CSRF 대응 



**3차 POC** 1.06~1.24 

AOP → Middleware 전환 전략 수립
InternalNetwork Middleware 구현
UserActivity Log 연동
API 인증 연동 (글뷰 좋아요 연동)
인증 전략 워크샵
XSS 및 CSRF 영향 조사



**4차 POC**

  DDos 공격 대응 (bulkhead pattern)
  정상 부하 시나리오 테스트
  급격한 트래픽 증가 시나리오 테스트
  BFF 레이어 부하 테스트 (부하에 따른 API 요청 성능)
  시스템 성능 지표 파악 (메모리 누수 여부 확인)
