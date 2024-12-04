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


# Thymeleaf
* 컨트롤러의 전달 데이터를 이용해 동적 화면 생성
* 순수 HTML 구조 (Natural Template) -> 수정 시 서버 재가동 불필요
* Server X : 웹은 타임리프 속성(th:) 인식 불가 -> 순수 HTML 구조
* Server O : HTML 속성을 타임리프 속성으로 대체 -> 동적 HTML          

|문법|정의|활용|
|-|-|-|
|@{URL}|URL 링크 표현식|th:href="@{/css/bootstrap.min.css}"|
리터럴
https://jddng.tistory.com/223
```
<html lang="en" xmlns:th="http://www.thymeleaf.org/">    // 타임리프 사용
    <body>
        Name : <span th:text="${name}></span>            // th: = 타임리프 구문
    </body>
</html>

```















# Security
* Security : 홈페이지에 인증 권한을 빠르게 추가 가능한 프레임워크
* Authentication : User의 인증 정보 (getPrincipal(), getCredentials())
  * principal : User 정보에 대한 인터페이스 (getName())
  * credential : Principal에 접근을 위한 암호
  * grantedAuthority : User의 권한 인터페이스 (ROLE_USER, ROLE_ADMIN)

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
// Kakao Develper 등록 후에 얻은 Client Id
spring.security.oauth2.client.registration.kakao.client-id=
// 보안을 위해 활성화한 Client Secret 값                                                          
spring.security.oauth2.client.registration.kakao.client-secret=
// OAuth2 인증 방식 (Http Post 방식으로 전달)                                                      
spring.security.oauth2.client.registration.kakao.client-authentication-method=client_secret_post
// 인증 후에 인증 코드 전달 URL                     
spring.security.oauth2.client.registration.kakao.redirect-uri=http://localhost:8080/login/oauth2/code/kakao
// authorization_code 인증 방식          
spring.security.oauth2.client.registration.kakao.authorization-grant-type=authorization_code
// 사용 Scope
spring.security.oauth2.client.registration.kakao.scope=profile_nickname,profile_image,account_email
// Client 이름 정의                  
spring.security.oauth2.client.registration.kakao.client-name=Kakao
// 로그아웃 후의 Redirect 경로            
spring.security.oauth2.client.kakao.logout.redirect.uri=http://localhost:8080/login                                  

#KAKAO PROVIDER
// authorization URL
spring.security.oauth2.client.provider.kakao.authorization-uri = https://kauth.kakao.com/oauth/authorize
// token URL
spring.security.oauth2.client.provider.kakao.token-uri = https://kauth.kakao.com/oauth/token
// 사용자 개인정보 획득 URL
spring.security.oauth2.client.provider.kakao.user-info-uri = https://kapi.kakao.com/v2/user/me
// id Attribute를 통하여 사용자 식별
spring.security.oauth2.client.provider.kakao.user-name-attribute = id
```


## JWT Token
**Jason Web Token : 기본 Cookie가 아닌 Json으로 정보를 저장하는 Web Token**
* Header + Payload + Signature로 구성 = hhhh.pppp.ssss
 * Header(헤더) : Signature 해싱을 위한 알고리즘 정보 저장 (검증)
    * typ : 토큰의 타입 = JWT
    * alg : 서명용 알고리즘
    * kid : 서명 키 식별 값
 * Payload(정보) : 실 사용 정보 저장
    * claim : 속성 (Key - Value)
    * claim set : 여러 개의 속성들
* Signature(서명) : 인코딩, 검증에 필요한 암호화 코드
         
**Login_JWT**
```
* Token 속성 정의
public class TokenKey {
    private String grantType;
    private String accessToken;
    private String refreshToken;}

* JWT 설정
public class JwtProperties {
    public static final int EXPIRATION_TIME = 60000;                   // 토큰 만료 시간
    public static final String COOKIE_NAME = "JWT-AUTHENTICATION"; }   // 토큰 명

* 서명 암호 코드 생성
public class SignGenerator {
    public static byte[] genSign() {
        SecureRandom secureRandom = new SecureRandom();    // 난수 생성 객체
        byte[] signBytes = new byte[256/8];                // 256 바이트 배열 생성
        secureRandom.nextBytes(signBytes);                 // 배열에 난수 삽입
        return signBytes;                                  // 서명용 배열 반환
    }    
}

* JWT Access, Refresh 토큰 생성 - 서명에 헤더, 내용 추가 
public Tokenkey genJwt(Authentication authentication) {
    String authorities = authentication.getAuthorities().stream()    
        .map(GrantedAuthority::getAuthority)                        // 권한 명 추출
        .collect(Collectors.joining(","));                          // 추출 권한 집합 (ROLE_USER, ROLE_ADMIN)
    long now = (new Date()).getTime();                              // 현재 시각 객체
    // AccessToken 생성
    Data accessTokenExpire = new Data(now + JwtProperties.EXPIRATION_TIME);        // 현재+설정 만료시간=만료 기한
    String accessToken = Jtws.builder()                    // JWT 객체 생성
        .setSubect(authentication.getName())               // 토큰 주체 설정 = 사용자명
        .claim("username", authentication.getName())       // 데이터 추가
        .claim("auth", authorities)    
        .claim("provider", userDto.getProvider())
        .setExpiration(accessTokenExpire)                 // 만료 기한
        .signWith(key, SignatureAlgorithm.HS256)          // 서명 알고리즘
        .compact();                                       // Token 생성
    // RefreshToken 생성
    String refreshToken = Jwts.builder()
        .setExpiration(new Date(now + 86400000))          // 24시간 후까지
        .signWith(key, SignatureAlgorithm.HS256)
        .compact();
    return TokenKey.builder()             
        .grantType("Bearer")            // Bearer Type : Authorization header type
        .accessToken(accessToken)       // 생성 accessToken
        .refreshToken(refreshToken)     // 생성 refreshToken
        .build();                       // 객체 반환
}

* JWT 토큰 복호화, 검증
public Authentication getAuthentication(String accessToken) {
    Claims claims = parseCliams(accessToken);                            // accessToken을 복호화한 claims 객체
    Collection< ? extends GrantedAuthority> authorities =                // GrantedAuthority의 문자열
        Arrays.stream(claims.get("auth").toString().split(","))          // , 로 구분된 것을 분리하여
            .map(auth -> new SimpleGrantedAuthority(auth))               // Map 생성
            .collect(Collectors.toList());
}

* Security.Config : JWT Filter 추가
http.addFilterBefore(new JwtFilter(userRepository, jwtTokenProvider), BasicAuthenticationFilter.class);

```
