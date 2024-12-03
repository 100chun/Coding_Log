# SpringBoot
**환경설정**
1. JDK 21.0.2 설치
2. Tomcat 9 설치
3. IntelliJ Community 설치
4. start.spring.io
    1. Packagin : War, Java : 21
    2. Dependencies : Web, lombok
    3. EXPLORE -> Download -> Demo 폴더
5. Workspace -> Demo 폴더 삽입 -> demo(project 명) -> cmd -> ```idea .```
6. File -> Settings -> Gradle
    *  Build and run using : IntelliJ
    *  Run tests using : IntelliJ
    *  Gradle JVM : JDK 21
7. Project -> Open Module Settings
    * Project -> SDK : 21
    * SDKs -> JDK home Path : jdk-21
8. build-gradle (== pom.xml)
    ```
    dependencies {
        implementation 'org.springframework.boot:spring-boot-starter-web'
        compileOnly 'org.projectlombok:lombok'
        annotationProcessor 'org.projectlombok:lombok'
        //providedRuntime 'org.springframework.boot:spring-boot-starter-tomcat'
        testImplementation 'org.springframework.boot:spring-boot-starter-test'
        //JSP
        implementation 'org.apache.tomcat.embed:tomcat-embed-jasper' // 추가
  	    //JSTL
  	    implementation 'jakarta.servlet:jakarta.servlet-api' //스프링부트 3.0 이상
  	    implementation 'jakarta.servlet.jsp.jstl:jakarta.servlet.jsp.jstl-api' //스프링부트 3.0 이상
  	    implementation 'org.glassfish.web:jakarta.servlet.jsp.jstl' //스프링부트 3.0 이상
    }
    ```
9. src -> main -> resource -> application.properties
   ```
   spring.application.name=demo
   #Tomcat Server Port Setting
   server.port=8080
   #UTF-8 Setting
   spring.servlet.filter.encoding.filter-name=encodingFilter
   spring.servlet.filter.encoding.filter-class=org.springframework.web.filter.CharacterEncodingFilter
   spring.servlet.filter.encoding.init-param.encoding=UTF-8
   spring.servlet.filter.encoding.init-param.forceEncoding=true
   spring.servlet.filter.encoding.url-pattern=/*
    ```
****



RESULTFUL API
 공공데이터 포털 자료 이용법
   thymeleaf
    leaflet
   map
   -marker, popup 
   kakao map, login
   naver
   (getmapping -> )

security
   principal details
   oauth2








# Security

### OAuth2 Client (Open Authorization)
* 웹사이트 서드파티 어플리케이션(Google, Kakao)을 통해 인증권한을 획득 가능한 프로토콜
* Provicer : 로그인을 시도하는 서드파티 어플리케이션
* Authorization Code : Client의 권한요청에 반환되는 코드
* Access Token : 권한획득 자격증명 (짧은 만료 기간 -> 재로그인)
* Refresh Token : Access Token 재발급 가능 

**User -> Client 선택 -> Authorization Server -> Resource Server**
|행위자|정의|
|-|-|
|User, Owner|웹 사이트 사용자, 소유자|
|User-Agent|사용 브라우저|
|Client|서드파티 어플리케이션 서버|
|Authorization Server|인증, 권한 부여 서버 (Authorization Code, Access Token)|
|Resource Server|사용자의 개인 정보 저장 Client 서버 (Client는 Token을 통해 정보 획득)|

**환경 설정 (kakao)**
1. Kakao Developer에 애플리케이션 추가
2. 카카오 로그인 활성화
3. 사용 도메인으로 Web 플랫폼 등록 (http://localhost:8080)
4. 로그인 Redirect URI 등록 (http://localhost:8080/api/v1/oauth2/kakao)
5. 로그아웃 Redirect URI 등록 (http://localhost:8080/login)
6. Client Secret 코드 생성, 확성화
7. Scope (사용 개인정보) 설정
**application.properties**
```
spring.security.oauth2.client.registration.kakao.client-id=                                                          // Kakao Develper 등록 후에 얻은 Client Id
spring.security.oauth2.client.registration.kakao.client-secret=                                                      // 보안을 위해 활성화한 Client Secret 값
spring.security.oauth2.client.registration.kakao.client-authentication-method=client_secret_post                     // OAuth2 인증 방식 (Http Post 방식으로 전달)
spring.security.oauth2.client.registration.kakao.redirect-uri=http://localhost:8080/login/oauth2/code/kakao          // 인증 후에 인증 코드 전달 URL
spring.security.oauth2.client.registration.kakao.authorization-grant-type=authorization_code                         // authorization_code 인증 방식
spring.security.oauth2.client.registration.kakao.scope=profile_nickname,profile_image,account_email                  // 사용 Scope
spring.security.oauth2.client.registration.kakao.client-name=Kakao                                                   // Client 이름 정의
spring.security.oauth2.client.kakao.logout.redirect.uri=http://localhost:8080/login                                  // 로그아웃 후의 Redirect 경로

#KAKAO PROVIDER
spring.security.oauth2.client.provider.kakao.authorization-uri = https://kauth.kakao.com/oauth/authorize
spring.security.oauth2.client.provider.kakao.token-uri = https://kauth.kakao.com/oauth/token
spring.security.oauth2.client.provider.kakao.user-info-uri = https://kapi.kakao.com/v2/user/me
spring.security.oauth2.client.provider.kakao.user-name-attribute = id
```
