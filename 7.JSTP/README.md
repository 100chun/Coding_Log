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

* 선언문 <%!%> : 전체 영역에서 사용하는 멤버변수, 함수 선언 영역 (if, for)
* 표현식 <%=%> : 선언된 변수, 함수를 FrontEnd로 전달하는 영역 (화면 출력)
* 스크립틀릿 (Scriptlet) <%%> : Java 코드 사용 영역
  - 함수 선언 불가 : 함수 내에서 함수 선언 불가
```
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>  // 서버 전달 값
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
    <%= count() %>    // 표현식 -> 화면에 n 값 출력 (return n)
    <%


    %>
</body>
</html>
```

<%> : Scriptlet
<%!>
<%=>
request
js <-> jsp
