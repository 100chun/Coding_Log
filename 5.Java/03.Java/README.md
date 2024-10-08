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

----------------------------------------------
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
