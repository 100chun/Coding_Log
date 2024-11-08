# SpringBoot (11/08 ~ )
**환경 설정**
1. JDK 11.0.8 설치
2. Tomcat9 설치
3. SpringTool Eclpise Window (3.9.18) 설치
```https://github.com/spring-attic/toolsuite-distribution/wiki/Spring-Tool-Suite-3```(win32-x86_64.zip)
  * C드라이브에 파일 압축 해제
  * STS.init 파일에 openFile 하단에 JDK 파일 경로 추가
  ```
   -vm
   C:\Program Files\Java\jdk-11.0.0.2\bin\javaw.exe
  ```
  * ```https://nirsa.tistory.com/405``` 파일 모두 다운로드
    1. workspace 경로 -> .metadata\.plugins\org.springsource.ide.eclipse.commons.content.core에 https-content.xml 추가
    2. workspace 경로 -> .metadata\.sts\content에 org.springframework.templates.mvc-3.2.2 파일 추가
4. STS 실행
  * Window -> Preferences -> Workspace, Files -> Encoding 언어 UTF-8 설정
  * Server -> Tomcat9 추가 -> port number 할당
  * Spring Legacy Project -> Spring MVC Project 선택 -> Configure templates -> spring-defaults 설치

  **pon.xml**
  ```
<properties>
	<java-version>11</java-version>          <!-- 자바 버전 변경 -->
  <!-- springframework 버전 변경 (Maven Repository -> springframework -> Spring Core) -->
	<org.springframework-version>5.0.7.RELEASE</org.springframework-version> 
</properties>

<dependencies>
  <!-- Test -->
  <dependency>
	  <version>4.12</version>   <!-- Maven Compiler -->
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
  <plugin>
    <configuration>
      <source>${java-version}</source>
      <target>${java-version}</target>
    </configuration>
  </plugin>
</plugins>
  ```











web xml +
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
  <!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.34</version>
    <scope>provided</scope>
</dependency>


pom의 depedencies
spring test
		     <!-- https://mvnrepository.com/artifact/org.springframework/spring-test -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-test</artifactId>
    <version>${org.springframework-version}</version>
    <scope>test</scope>
</dependency>



- library lombok 실행 > 경로 install
- > controller + @Slf4j -> log.info("") - 로깅 가능
