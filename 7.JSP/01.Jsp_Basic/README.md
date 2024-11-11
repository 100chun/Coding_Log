# JSP (10/18 ~ 11/07)

**환경 설정**  [참고 자료](https://github.com/100chun/Coding_Log/tree/main/1.SW_Basic/02.MiddleWare_Basic)
1. Eclipse 설치 (Web, Java Developer ver)
2. Tomcat 설치
3. JDK 11.0.2 설치
4. Eclipse -> Help -> Install New Software -> ```http://download.emmet.io/eclipse/updates/``` 입력 -> 모두 설치
5. Install New Software -> ```https://github.com/angelozerr/tern.java/releases/tag/tern.java-1.2.1```의 파일 설치
6. Dynamic Web Project 생성 -> 우클릭 -> Configure -> Convert to Tern Project
* 저장 경로 : ```\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\work\Catalina\localhost\01_JSP\org\apache\jsp\```

**JSP (Java Server Pages) : 서버측에서 웹 페이지를 생성해 웹 브라우저로 전송 (동적 웹페이지 - 새로고침 시에 변화)**         
**Servlet : 웹 요청과 응답의 흐름 단순화 (동적 웹페이지)**
* 라이브러리 <%@ %> : 지정 Library 사용
* 선언문 <%! %> : 전체 영역에서 사용하는 멤버변수, 함수 선언 영역 (if, for 사용 불가)
* 표현식 <%= %> : 선언된 변수, 함수를 FrontEnd로 전달하는 영역 (화면 출력)
  - EL 표현식 (Expression Language) ${}: 값 표현 방식
* 스크립틀릿 (Scriptlet) <% %> : Java 코드 사용 영역
  - 함수 선언 불가 : 함수 내에서 함수 선언 불가

```
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>  // 서버 전달 값
<%@ import="java.util.*, java.sql.*" %>    // java.util, java.sql의 모든 Library 사용 가능
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
    <%!                // 선언문
        int n = 0;
        public int count() {
            n++;
            return n;
        }
    %>
    <%                 // 스크립틀릿
        while (n < 5)
            count();
    %>
    N : <%= n %>       // 표현식 -> N : 4
    N : ${n}           // EL 표현식 -> N : 4
</body>
</html>
```

### 기본 내장 객체_Scope
* Page < Request < Session < Application
* Page (pageContext) : 한 JSP 페이지 (한 페이지 내에서만 값 공유)
* Request : HTTP가 요청하는 Parameter 값 추출 (Client -> Server)
  1. HTTP : Form에 Input (Parameter) 작성 -> action으로 JSP에 전달
  2. JSP : Request를 이용하여 Parameter 값 추출
  - Forward : 지정 URL로 이동 (Parameter 추출 값 유지)
* Response : Parameter 값 HTTP에 재전달 (Server -> Client)
  - Redirect : 지정 URL로 이동 (Parameter 추출 값 초기화)
* Session : 한 Browser (Chrome, Safari) 내어서만 값 공유
* Application : 모든 값 공유

**HTML**
```
<form action="01Scope.JSP">                  // Form 정보 JSP로 전달
    <input type="text" name="username" />    // username Parameter 입력
    <input type="text" name="password" />    // password Parameter 입력
    <button>전송</button>
</form>
```

**JSP**
```
<%
    System.out.println(pageContext);    // Page
    pageContext.getRequest();           // 큰 범위 객체 사용 가능

    String name = request.getParameter("username");  // Request
    String ps = request.getParameter("password");    // password Parameter의 값 추출
    String ser = request.getServerName();            // 사용자 명 추출 (localhost)

    request.getRequestDispatcher("02Scope.jsp").forward(request, response);  // Forward : 전달하며 값 유지
    response.sendRedirect("02Scope.jsp");                                    // Redirect : 이동하며 값 초기화    
%>
```

### Cookie
* Server -> Client
* 웹 브라우저가 보관하고 있는 데이터, 웹 서버에 요청을 보낼 때 함께 전송 (ID 저장)
* 문자열 데이터 저장 (최대 4Kbyte)
* 최대 300개의 쿠키 저장 -> 초과 시에 미사용 쿠키부터 삭제
* Domain당 20개까지 사용 가능
```
    Cookie cookie = new Cookie("Cok_Key", "Cok_Val");    // 쿠키 선언 : 키 - 값 형태
    cookie.setMaxAge(30);                                // 유효 시간 30s -> 30초 뒤 새로고침 -> 값 사라짐
    response.addCookie(cookie);                          // 쿠키 전달
```

# Servlet
---------
**Servlet : 클라이언트의 요청을 처리하고 그 결과를 반환하는 기술**
*  Cient -> HttpRequest -> WAS(tomcat) -> ServletGet -> ServletPost -> HttpResponse -> Client
* 동적 웹페이지에서 수행
* HTML의 요청에 응답

**JSP1 - 정보 입력**
```
<body>  <!-- 정보 처리 Servlet 경로 -->
    <form action="${pageContext.request.contextPath}/servlet1.do" method="post">
        <input type="text" name="userid" /> <br>
        <input type="password" name="password" /> <br>
        <input type="submit" value="회원가입" /> <br>
    </form>
</body>
```

**Servlet1 - 정보 처리**
```
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;

@WebServlet("/servlet1.do")                    // 서블릿 이름 명명 = /Test
public class ServletTest extends HttpServlet {
    @Override      // 초기화 함수
    public void init() thrwos ServletException {}
    @Override      // 정보를 받아올 JSP 위치 - Forward로 전달
    public void doGet(HttpServletRequest req, HttpServletResponse resp) {
        req.getRequestDispatcher("/WEB-INF/Test.jsp").forward(req, resp);
    }
    @Override      // 정보를 반환할 Servlet or JSP 위치
    public void doPost(HttpServletRequest req, HttpServletResponse resp) {
        String id = req.getParameter("userid");        // JSP에서 가져온 값
        Stirng pw = req.getParameter("password");
        HttpSession session = req.getSession();        // Servlet 내장 객체 - 정보 저장
        session.setAttribute("userid", id);            // session에 Key, Value 형태로 정보 저장
        session.setAttribute("password", pw);
        resp.sendRedirect(req.getContextPath() + "/JSP2.jsp);    // 반환할 경로 (/main.do로 명명된 Servlet)
    }
    @Override    // 삭제 함수
    public void destroy() {}
}
```

**JSP2 - 반환 정보 출력**
```
<body>
    ID : ${userid} <br> 
    PW : ${password} <br>
</body>
```

### Filter
**Filter : 요청, 반환 사이에서 정보 처리**
* ClientReq -> Filter -> ServletReq -> ServletResp -> Filter -> ClientResp
* Servlet 처리 전, 후에 작업 추가 - Servlet에 따라 선택적 실행
```
@WebFilter("/.do")    // .do 형태의 servlet에 모두 적용 (/* : 모든 servlet)
public class filter implents Filter {
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {}
    @Override
    public void doFilter(ServletRequest req, ServletResponse resp, FilterChain chain)
            throws Exception {
        req.setCharacterEncoding("UTF-8");                   // request에서 적용
        chain.doFilter(req, resp);      // 다른 filter로 전달 = filter1 -> filter2 -> filter2 -> filter1
        resp.setContentType("text/html;" charset=UTF-8");    // response에서 적용
}
```

### Listner
**Listner : 특정 이벤트가 발생하면 실행**
```
@WebListner()
public class ServletContextListner implements ServletContextListner {
    @Override
    public void contextInitia   
}
```

### web.xml
**Web Application Deployment Descriptor : Servlet, Filter의 URL 정보 처리**
* mapping -> 파일에 annotation 추가 불필요 (@WebServlet(), @WebFilter())
```
* Default Servlet : Servlet Mapping 처리가 되지 않은 Servlet 처리
<web-app>
    <servlet>
        <servlet-name>default</servlet-name>
        <servlet-class>org.apache.catalina.servlets.DefaultServlet</servlet-class>
        <init-param>
            <param-name>debug</param-name>
            <param-value>0</param-value>
        </init-param>
        <init-param>
            <param-name>listings</param-name>
            <param-value>false</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>default</servlet-name>
        <url-pattern>/resources/*</url-pattern>    <!-- 정적 자원 요청에 대한 URL 패턴 지정 -->
    </servlet-mapping>

<!-- Servlet -->
    <servlet>
        <servlet-name>test.do</servlet-name>      // == @WebServlet(/test.do)
      	<servlet-class>Servlet.Servlet</servlet-class>  // class 경로
    </servlet>
    <servlet-mapping>
        <servlet-name>test.do</servlet-name>     // == @WebServlet(/test.do) 
        <url-pattern>/</url-pattern>
    </servlet-mapping>

<!-- Filter -->
    <filter>
      	<filter-name>UTF8</filter-name>
      	<filter-class>Filter.UTF8_Encoding</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>UTF8</filter-name>
      	<url-pattern>/*</url-pattern>
    </filter-mapping>
</web-app>
```
