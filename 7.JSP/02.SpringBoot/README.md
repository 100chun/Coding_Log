# SpringBoot (11/08 ~ )
**환경 설정** [참고 자료](https://github.com/100chun/Coding_Log/tree/main/1.SW_Basic/02.MiddleWare_Basic)
- SpringFramework : 자바 웹 애플리케이션 개발을 위한 경량형 오픈소스 프레임 워크
- lombok : 기계적인 코드 작성을 자동화하여 코드 다이어트를 해주는 Java 라이브러리
1. JDK 11.0.8 설치
2. Tomcat9 설치
3. SpringTool Eclpise Window (3.9.18 - win32-x86_64.zip) 설치
   * ```https://github.com/spring-attic/toolsuite-distribution/wiki/Spring-Tool-Suite-3```
   * C드라이브에 파일 압축 해제
   * STS.init 파일에 openFile 하단에 JDK 파일 경로, lombok 추가
    ```
    -vm
     C:\Program Files\Java\jdk-11.0.0.2\bin\javaw.exe
    -javaagent:lombok.jar
    ```
   * ```https://nirsa.tistory.com/405``` 파일 모두 다운로드
     1. workspace 경로 -> .metadata\.plugins\org.springsource.ide.eclipse.commons.content.core에 https-content.xml 추가
     2. workspace 경로 -> .metadata\.sts\content에 org.springframework.templates.mvc-3.2.2 압축 해제 파일 추가
4. STS 실행
   * Window -> Preferences -> Workspace, Files -> Encoding 언어 UTF-8 설정
   * Server -> Tomcat9 추가 -> port number 할당
   * Spring Legacy Project -> Spring MVC Project 선택 -> Configure templates -> spring-defaults 설치
   * pom.xml, web.xml 수정
5. Project -> Run As -> Maven clean -> Maven install
6. Project -> Maven -> Update Project -> Run As Apache Tomcat

**src -> pom.xml**
```
<properties>
  <!-- 자바 버전 변경 -->
  <java-version>11</java-version>          =
  <!-- springframework 버전 변경 (Maven Repository -> springframework -> Spring Core) -->
  <org.springframework-version>5.0.7.RELEASE</org.springframework-version> 
</properties>

<dependencies>
   <!-- loggin -->
  <dependency>
    <groupId>log4j</groupId>
    <!-- <scope>runtime</scope> 주석 처리 -->
  </dependency>

  <!-- Test -->
  <!-- J Unit Version 변경 --> 
  <dependency>
    <version>4.12</version>   <!-- Maven Compiler -->
  </dependency>

  <!-- workspace 한글 경로 포함 maven -> artifact -> xerces -> xercesImpl -->
  <dependency>
    <groupId>xerces</groupId>
    <artifactId>xercesImpl</artifactId>
    <version>2.12.2</version>
  </dependency>

  <!-- lombok -->
  <dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.34</version>
    <scope>provided</scope>
  </dependency>
		     
  <!-- https://mvnrepository.com/artifact/org.springframework/spring-test -->
  <dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-test</artifactId>
    <version>${org.springframework-version}</version>
    <scope>test</scope>
  </dependency>
</dependencies>

<plugins>
   <!-- Maven Compiler Version 변경 -->
   <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-compiler-plugin</artifactId>
      <version>3.5.1</version>
      <configuration>
         <source>${java-version}</source> <!-- 설정 자바 버전 -->
         <target>${java-version}</target>
      </configuration>
   </plugin>
</plugins>
 ```

**src -> main -> webapp -> WEB-INF -> web.xml**
```
<!-- 한글 변환 필터 시작 -->
<filter>
  <filter-name>encodingFilter</filter-name>
  <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
  <init-param>
    <param-name>encoding</param-name>
    <param-value>UTF-8</param-value>
  </init-param>
  <init-param>
    <param-name>forceEncoding</param-name>
    <param-value>true</param-value>
  </init-param>
</filter>
	
<filter-mapping>
  <filter-name>encodingFilter</filter-name>
  <url-pattern>/*</url-pattern>
</filter-mapping>  
```

## Spring Basic
**lombok Annotation**
* @Data : Getter + Setter + RequiredArgsConstructor + ToString
* @NoArgsConstructor : 기본 생성자
* @AllArgsConstructor : 모든 인자 생성자



* Mapping <- Servlet
* 
```
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Example {
   private int id;
   private String password;
}

```
@GetMapping("/ex")
@PostMapping("/ex")
