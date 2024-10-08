10/8
**시각 표현**
* Date : 일회용 날짜 표현
* Calender : 실시간 날짜 표현
* Time : 시간 표현
```
* Date
[getYear, getMonth, getHours, getMinutes, getSeconds, getTime]
Date date = new Date();
System.out.println(date);
System.out.println(date.getDay());          // 일~토 (0~6)

* Calender
import java.util.Calender;
Calender cal = new Calender();
[YEAR, MONTH, HOUR, MINUTE, SECOND]
System.out.println(cal.DAY_OF_MONTH+1);     // 0부터
System.out.println(cal.DAY_OF_WEEK);        // 일~토 (1~7)
```
          
## Exception
* Error : 프로그램 코드로 처리 불가능한 오류 (메모리 부족)
* Exception (예외) : 프로그램 코드로 처리 가능한 오류 (다른 자료형)
  * Checked : 오류 발생 시점 확인 가능 -> 예외 처리 필수
  * Unchecked : 오류 발생 시점 확인 불가능 -> 예외 처리 선택

```
* throw : 예외 전가
[throw : 특정 부분에 전가, throws : 상위 메소드로 전가]
public static void main(String[] args) throws Exception {}

* try, catch : 예외 처리 구문 작성
try{                       // 에러 발생 가능 코드
  System.out.println(str);
}
catch(Exception e) {       // 에러 처리 코드 (오류종류 오류명명)
  System.out.println("해당 문자열 오류가 발생");
  e.pritnStackTrace();     // 오류 출력
}
finally{                   // 최종 실행 코드
  System.out.println("예외 처리 종료");
}
```

## Lambda Stream
----------------
* Lambda Expression : 매서드의 이름, 반환값을 생략해 간략화시킨 형태 (익명 함수)
* Stream : 데이터 타입과 무관한 처리를 도와주는 API

```
* lambda
int max (int a, int b) {  // 일반 함수식
  return a + b;
}
(a, b) -> {a + b}         // 람다식

* filter() : 조건문에 해당하는 데이터 추출
list.stream().filter(i->i.getNumber() > 10)

* map() : 각 요소에서 특정 속성 값만 추출
list.stream().map(i -> i.getId())

* reduce() : 계산식
list.stream().reduce(0, (a,b) -> {a+b}) // 람다스트림 (0은 초기값)

* sorted() : 정렬
list.stream().map((a,b), -> {a - b})  // 람다스트림
```

* jdbc
* 클래스 다이어그램
* mvc

가볍게
socket, thread 가볍게, 디자인패턴
* Swing

* Socket : TCP/IP 기반 네트워크 통신에서 데이터 송수신의 마지막 접점
* Server : 데이터를 송신자
* Client : 데이터 수신자
* Buffer : 데이터 이동에 필요한 바이트, 문자 변환자
