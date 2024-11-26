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
* Spring Bean : Spring 프로그램이 관리하는 자바 객체 (외부 라이브러리)
* Context : Bean이 담긴 컨테이너
  * web.xml : servlet, root eontext의 경로 설정
  * servlet-context.xml (공유 X) : View, url-controller 요청과 관련된 Bean 설정
  * root-context.xml (공유 O) : Servoce, Dao, DB 같은 백엔드 Bean 설정


**Annotation : 실행 시에 특정 기능을 하는 주석**
* @ComponentScan : Bean을 탐색해 content.xml에 자동 추가
* @Component : 직접 작성한 class를 Bean으로 등록
* @Bean : 외부 라이브러리 클래스를 Bean으로 등록
* @Autowired : 속성 생성자에 자동 Bean 주입 (Dao, Service)
* @Configuration :  @Autowired로 호출 가능한 Config 파일
* @Service : MVC Service 등록
* @Controller : MVC Controller 등록 (View Return)
* @RestController : View에 응답하지 않는 Controller 등록 (method Return)
* @RequestMapping : 처리 method, 응답 방식 등록

**lombok Annotation**
* @Data : Getter + Setter + RequiredArgsConstructor + ToString
* @NoArgsConstructor : 기본 생성자
* @AllArgsConstructor : 모든 인자 생성자
```
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Example {
   private int id;
   private String password;
}

```

## Mapping

#### REST
* Representational State Transfer : Resource (URI) + Verb (HTTP Method) + Representations
* Mapping : URI로의 요청을 특정 함수와 연결하기 위해 사용
**Controller + HTTP Method**
```
@RequestMapping("/home") 	// 공통 경로
public class HomeController {

* GET : 서버의 데이터 획득 (Select)
@GetMapping("/getHome")		// URI
private void GetHome() {	// Verb
    log.info("GET");		// Representations
}

* POST : 서버에 데이터 추가 (Insert)
@PostMapping("/postHome")
private void PostHome {}

* PUT : 서버의 데이터 수정 (Update - 전체)
@PutMapping("/putHome")
private void PutHome {}

* Patch : 서버의 데이터 수정 (Update - 일부)
@PatchMapping("/patchHome")
private void PatchHome {}

* Delete : 서버의 데이터 삭제 (Delete)
@DeleteMapping("/deleteHome")
private void DeleteHome {}
```

SQL Mapper (MyBatis)
-------------------
* MyBatis Framework : JDBC 기능, 자바 객체와 SQL 매핑기능 제공

1. Mapper.java + Dao
```
*HomeMapper.java
@Mapper		// MyBatis Mapper Annotation
public interface HomeMapper {
    @Insert(value="insert into tbl_home values(#{id}, #{pw}, #{name})")
    public int Insert(HomeDto dto);
}
```

2. Mapper.xml + Mapper.java + Dao
```
* Mapper.xml
<mapper namespace="com.example.ex01.domain.mapper.HomeMapper">    // Mapper.java 경로
    <update id="Update_xml" parameterType="com.example.ex01.domain.dto.HomeDto">  // dto 경로
        update tbl_memo set id=#{id}, pw=#{pw}, where name=#{name}   	  // dto의 객체 #{}
    </update>
</mapper>

* HomeMapper.java
public int Update_xml(MemoDto memoDto);    // Mapper.xml의 함수 선언
```



** Transaction : 데이터 베이스의 작업 단위**
 - 작업 중 비정상적 종료 시에 작업 전으로 반환
 - Commit : 작업 마지막에 작성하는 전체를 실행하는 함수
 - Rollback : 예외 문에 작성하는 작업 전으로 되돌리는 함수
**Config**
```
@Autowired  
private DataSource dataSource;

@Bean    // TxManager 추가
public DataSourceTransactionManager transactionManager() {
    return new DataSourceTransactionManager(dataSource);
}
```

**Service**
```
@Transactional(rollbackFor = SQLException.class) 	// default 특정 유형의 에러 발생 시에 롤백
public boolean memoAddTx(MemoDto memoDto) throws Exception {
    int result = memoDao.insert(memoDto);
    return result>0;
}
```



**AOP**
- Aspect-Oriented Programming : 관점 지향 프로그래밍
- 프로그램을 핵심, 부가적 기능으로 나누어 모듈화
aop?
file, up, download (fiolder create)
crud axios
intercreptor

listener
handling
schedule
security
동기 비동기
