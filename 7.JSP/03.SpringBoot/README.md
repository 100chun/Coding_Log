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
