# Object (9/26 ~ 

### Object Class : 모든 클래스가 상속 받는 최상위 부모 클래스
* Library : 자동 import (import.java.lang.* )
* 상속 : 자동 상속 (extends Object)
* 함수 오버라이딩 : 우클릭 -> Source -> Override/Implements Methods

```
* toString : 객체 정보 문자열로 출력
public String toString() {}           // 해쉬코드 대신 객체 정보 확인

* equals : 주소 값 비교
[String equals는 문자열 비교]
public boolean equals(Object obj) {}  // 주소 같으면 true

* hashoCode : 인스턴스의 저장 주소 반환
[hashcode는 객체 식별 코드]
public int hashCode() {}              // Object.equal -> hashcode equal
```

**Wrapper Class: 기본 객체를 참조 객체로 표현 가능한 클래스**
* 기본형 변수 (Primitive Type) : 비객체형 (null X)
* 참조형 변수 (Reference Type) : 기본형 변수를 제외한 나머지 변수 (클래스, 배열)

|기본형 변수|참조형 변수|
|-|-|
|byte|Byte|  
|char|Character|
|int|Integer|
|short|Short|
|long|Long|
|float|Float|
|double|Double|
|boolean|Boolean|

```
* import.java.lang.*                 // 자동 import

* Boxing : 기본형 변수를 참조형 변수로 표현
Integer Box = new Integer(10);      // 기본형 정수를 참조형으로 표현
Box = 50;

* UnBoxing : 참조형 변수로 표현된 값 기본형으로 되돌리기
[참조형 변수의 값 직접 변경 불가능]
int unbox = Box.intValue();         // 참조형 변수의 값 기본형 정수에 저장
unbox = unbox + 100;               
Box = unbox;                        // Boxing
```

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
```

## Generic
* 외부에서 클래스와 내부 변수 자료형 선언
* <> : 다이아몬드 연산자로 표현
 * Wrapper 자료형
 * Type 자료형 (범용적 자료형)

|기호|설명|
|-|-|
|T|Type (타입)|
|E|Element (요소-list)|
|K|Key (키-Map)|
|V|Value (값-Map)|
|N|Number (숫자)|

```
* <ex> : 임의의 자료형
class X {}
class Y extends X {}                // Y의 조상 타입만 가능
Y <X> ex = new ex<Y>(new Y());      // Y의 조상 X
Y <A> exA = new ex<A>(new A());     // 오류 발생

* <T> : Type 자료형
[Type 자료형은 암묵적 규칙 (임의의 자료형에 규칙 적용)]
Sample <K, V> map = new map<K, V>();     // 자료형 여러개 지정 가능
class map <K, V> {}

* <String> : wrapper 자료형
class wrap <W> {
  private <W> str;                      // Integer 자료형
  <W> apper() {return str;}
}
ArrayList <Interger> listInt = new ArrayList<Interger>(); 
```
* static
* final


**Collection : 자료 구조(Data Structure) 종류의 형태들을 자바 클래스로 구현한 모음집**
* List : 순서가 있는 목록 (중복 가능)
* Set : 순서가 없는 목록 (중복 불가)
* Map : 키-값으로 이루어진 순서가 없는 목록 (값만 중복 가능)



* final
* collection
* jdbc
* 람다스트림
* 클래스 다이어그램
* mvc

가볍게
socket, thread 가볍게, 디자인패턴
* generic
* list
* Swing
