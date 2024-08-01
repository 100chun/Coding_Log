# 2. Middleware Basic (8/1 ~ )
```
* HardWare : PC의 부품    
* SoftWare
 1. System Software : WindowOS, Linux, macOS
 2. Application
```
* **MiddleWare : 하나의 시스템에서 앱을 동시에 실행, 연계시켜도 안정적으로 실행 가능 (Hardware + Software)**

**미들웨어 주요 기능**
|IT 자원 관리|서비스 플랫폼|네트워크 보안|분산 시스템|
|-|-|-|-|
|시스템 관리|IoT|네트워크 접근 제어|웹 앱 서버|
|SW 실행 관리|클라우드|보안 통신|연계 솔루션|
|네트워크 관리|UI/UX|침입 방지|실시간 처리|
|IT 서비스 관리|CND|사고 대응|TP 모니터|
|||보안 관리|분산 병렬 처리|



### JDK (JAVA Development Kit) 개발 환경 설정
---------------------------------------------

1. JDK 설치 (11 version)
   1. 환경 변수 설정
3. Tomcat 설치 (9 version)
   1. Java 설치 위치 연동
   2. Login : admin / 1234
   3. 마지막 체크 박스 : Run Apache Tomcat, Show readme 해제
5. Eclipse 설치 (Java and Web Developers package)
   1. File -> New -> Other -> Server -> Tomcat
   2. File -> New -> Dynamic Web Project -> Target Runtime : Apache Tomcat
   3. Tomcat Server 실행 -> 실행 중인 파일 더블 클릭 -> Overview -> Port Number 할당