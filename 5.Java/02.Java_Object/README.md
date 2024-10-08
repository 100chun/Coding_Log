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

**Collection : 자료 구조(Data Structure) 종류의 형태들을 자바 클래스로 구현한 모음집**
* List : 순서가 있는 목록 (중복 가능)
* Set : 순서가 없는 목록 (중복 불가)
* Map : 키-값으로 이루어진 순서가 없는 목록 (값만 중복 가능)


* static
* final




* final
* collection
* jdbc
* 람다스트림
* 클래스 다이어그램
* mvc

가볍게
socket, thread 가볍게, 디자인패턴
* Swing
