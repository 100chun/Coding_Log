# JSP (10/18 ~
**환경 설정**          
[참고 자료](https://github.com/100chun/Coding_Log/tree/main/1.SW_Basic/02.MiddleWare_Basic)
1. Eclipse 설치 (Web, Java Developer ver)
2. Tomcat 설치
3. JDK 11.0.2 설치
4. Eclipse -> Help -> Install New Software -> ```http://download.emmet.io/eclipse/updates/``` 입력 -> 모두 설치
5. Install New Software -> ```https://github.com/angelozerr/tern.java/releases/tag/tern.java-1.2.1```의 파일 설치
6. Dynamic Web Project 생성 -> 우클릭 -> Configure -> Convert to Tern Project
* 저장 경로 : \workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\work\Catalina\localhost\01_JSP\org\apache\jsp\

**JSP (Java Server Pages) : 서버측에서 웹 페이지를 생성해 웹 브라우저로 전송 (동적 웹페이지 - 새로고침 시에 변화)**
**Servlet : 웹 요청과 응답의 흐름 단순화 (동적 웹페이지)**

* 선언문 <%! %> : 전체 영역에서 사용하는 멤버변수, 함수 선언 영역 (if, for 사용 불가)
* 표현식 <%= %> : 선언된 변수, 함수를 FrontEnd로 전달하는 영역 (화면 출력)
  - EL 표현식 (Expression Language) ${}: 값 표현 방식
* 스크립틀릿 (Scriptlet) <% %> : Java 코드 사용 영역
  - 함수 선언 불가 : 함수 내에서 함수 선언 불가
* 라이브러리 <%@ %> : 지정 Library 사용
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

기본 내장 객체_Scope
----------------------------
* Page -> Request -> Session -> Application
* Page (pageContext) : 한 JSP 페이지 (한 페이지 내에서만 값 공유)
* Request : HTTP가 요청하는 Parameter 값 추출
  1. HTTP : Form에 Input (Parameter) 작성 -> action으로 JSP에 전달
  2. JSP : Request를 이용하여 Parameter 값 추출
* Response : Parameter 값 HTTP에 재전달
  - Redirect : 지정 URL로 이동 (Parameter 추출 값 초기화)
  - Forward : 지정 URL로 이동 (Parameter 추출 값 유지) - Response 객체 X
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

    response.sendRedirect("02Scope.JSP");            // Response
    
%>

```
