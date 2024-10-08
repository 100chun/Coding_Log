# Object (9/26 ~ 
## 상속
-------
**상속 (Inheritance) : 기존 클래스를 재활용하여 새로운 클래스 작성**
* 부모 클래스 (Super Class) / 자식 클래스 (Sub ClasS) : 자식 클래스는 부모 클래스의 객체, 메서드 사용 가능
* 업캐스팅 (UpCasting) : 부모 클래스 참조 변수를 하위 클래스에 연결 (자동형변환)
  - 자식 클래스 객체 사용 X -> DownCasting 필요 / 오버라이딩된 메소드 사용 O
* 다운캐스팅 (DownCasting) : 부모 클래스 참조 변수의 하위 클래스 객체 사용을 위한 강제형변환
  - 자식 클래스 객체 사용 O
* 오버라이딩 (OverRiding) : 상속 받은 메서드의 내용 변경 (재정의) -> 다형성

```
class Super {
	int a;
	void A() {
		a = 10;
	}
}
class Sub extends Super { 	// Super 클래스 상속
	int b;
	void A() {		// OverRiding
		a = 20;		// 상속 받은 객체 a 사용 가능
	}
	void B() {
		b = 50;
	}
}

public static void main(String[] args) {
	Super obj1 = new Super();
	obj1.A();		
	// obj1.B();		// 자식 클래스의 메서드 -> Err

	Sub obj2 = new Sub();
	obj2.A();		// 부모 클래스 메서드
	obj2.B();

	Super obj3 = new Sub();	// UpCasting <- 부모 클래스 obj3를 자식 클래스로 확장 (자동 형변환)
	obj3.A();		// a = 20 <- OverRiding된 자식 클래스 메서드 호출 (Method 구조는 공유 메모리인 Class 영역에 저장)
	// obj3.B();		// UpCasting 상태에서 자식 클래스 메서드 사용 불가 -> DownCasting 필요

	Sub obj4 = (Sub) obj3;	// DownCasting <- 부모 클래스 obj3를 자식 클래스로 변환 (강제 형변환)
	obj4.A();
	obj4.B();		// 자식 클래스의 메서드 사용 가능
}
```

**추상**
* 추상 메소드 (abstract method) : 자식 클래스에서 오버라이딩해야 사용 가능한 클래스
* 추상 클래스 (abstract class) : 하나 이상의 추상 메소드를 포함하는 클래스
  - 규격화 (하위 클래스에 강제성 부여)
  - 설계 단계 추후 작업 가능
* 인터페이스 (Interface) : 동일한 메소드만 가지는 추상 클래스
  - 하위 클래스에 오버라이딩 강제성 부여
  - 코디 길이 증가 / 결합도 감소
    
```
* 추상 클래스
abstract class Super {					// 추상 클래스 선언
	int n;
	void n() {
		n = 15;
	}
	abstract void func();				// 추상 메소드 선언 (인스턴스 X)
}
class Sub1 extends Super {
	int a;
	Sub1(int a) {this.a = a;}
	void func() {					// 자식 클래스에서 오버라이딩
		a += 10;
		System.out.println("a : " + a);
	}
}
class Sub2 extends Super {				// extends 다중 상속 X 
	int b;
	Sub2(int b) {this.b = b;}
	void func() {					// 자식 클래스에서 오버라이딩
		b--;
		System.out.println("b : " + b);
	}
}

* 인터페이스
interface Parent {					// interface 클래스 선언 == 부모 클래스
	int NUM1 = 100;					// public static fianl 형태의 수 = 고정된 값 (객체 생성 X)
	int NUM2 = 200;
	void method1();
	void method2(int num);
}
class Son1 implements Parent {				// implments 클래스 선언 == 자식 클래스
	int num1;
	int num2;
	public void method1() {				// public으로 작성
		num1 = NUM2;
		System.out.println("num1 : " + num1);
	}
	public void method2(int num) {
		num2 = num;
		System.out.println("num2 : " + num2);
	}
}
class Son2 extends Super implements Parent {		// extends, interface 동시 사용 가능 (extends 다음 interface)
	int num3;
	int num4;
	int num5;
	public void method1() {				// Parents method
		num3 = 120;
		System.out.println("num3 : " + num3);
	}
	public void method2(int num) {			// Parents method
		num4 = num - NUM2;
		System.out.println("num4 : " + num4);
	}
	void func() {					// Super method
		num5 = NUM1 + NUM2;
		System.out.println("num5 : " + num5);
	}	
}

class main {
	public static void Abstract(Super abs) {	
		abs.func();
	}
	public static void Interface(Parent inter) {	
		inter.method1();
		inter.method2(500);
	}
	public static void main(String[] args) {
//		 Super obj = new Super();		// 추상 클래스는 객체 생성 불가
		Sub1 obj2 = new Sub1(1);		// 자식 클래스는 객체 생성 가능
		Sub2 obj3 = new Sub2(2);		// 자식 클래스는 객체 생성 가능
		Super obj4 = (Super) obj3;		// UpCasting으로 부모 클래스 객체 생성

		Abstract(new Sub1(10));
		Abstract(new Sub2(5));
		
		Son2 ob = new Son2();			
		Interface(new Son1());			// Parent method - interface
		Interface(new Son2());			// Parent method - interface
		ob.func();				// Super method - abstract
	}
}
```
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
