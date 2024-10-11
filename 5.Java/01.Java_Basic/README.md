# Java_Basic (9/7 ~ 9/24)

**Github - Eclipse 연동**
* Eclipse -> Github
  1. Eclipse에서 Java Project 생성
  2. Java Project -> Team -> Share
  3. Window -> Show View -> Other -> Git Repositories, Git Staging
  4. Github -> New Repository -> add Readme 해제 -> Repository HTTPS 복사
  5. Git Repositories -> Java Project -> Remote -> Create Remote -> Github Repository Link와 연결
                     
* Github -> Eclipse
  1. Import -> Project from git -> Clone URL
<br>
 
**Java : C언어 (절차 지향)와 C++언어 (객체 지향)를 기반으로 하는 객체지향 프로그래밍 언어, 소프트웨어 플랫폼**
 * Class 영역 : 객체 지향 문법 적용 단위
 * Method (함수) : 작업 수행에 필요한 코드들을 묶어서 실행하는 단위
 * Main Method : 최초 실행 함수
 * Library Method : 미리 만들어져 제공되는 함수
 * Custom Method : 사용자 정의 함수
```
package Ch00.C00;				// 패키지 명 : Class 위치 (Ch00 -> C00 -> HelloWorld)
public class HelloWorld {			// 클래스 영역 : 파일명과 동일
    public static void main(String[] args) {	// 메서드 영역 : Main	
	void Func() {int c = 3 + 5;}		// 사용자 정의 함수
    }
}
```
<br> 

**표준 입출력**
* 그래픽 문자 ("") : 일반적 문자
* 비그래픽 문자 ("\\") : 문자의 역할을 하는 비일반적 문자    
* 서식 문자 : 서식에 사용되는 비일반적 문자

|비그래픽||서식||
|-|-|-|-|
|\n|줄바꿈|%d|10진수|
|\t|tab(8칸) 공백|%f|실수|
|\b|백스페이스|%c|단일 문자|
|\ |특수 기호 (\\")|%s|문자열|

```
* print : 표준 출력 장치
System.out.print("Hello World");		// 그래픽 문자

* println : 표준 출력 장치 + 줄바꿈
System.out.println("Hello \t World");		// 비그래픽 문자

* printf : 표준 출력 장치 + 서식 문자 사용
System.out.printf("Today is %d day \n", 28);	// 서식 문자, 비그래픽 문자
```
<br>

**진수**
* 2진수 : 두 수 (0, 1)만 이용하는 체계
* 10진수 -> 2진수 (8bit = 00000000)
  1. 10진수를 2로 나눌 수 없을 때까지 나누기		(56 -> 28,0 14,0 7,0 3,1 1,1)
  2. 마지막 몫을 배치					(1)
  3. 마지막 몫에 가까운 순서부터 나머지들을 배치		(1/11000)
  4. 남는 자리수 만큼 앞에 0 배치				(00/1/11000  =>  00111000)
* 2의 보수 : 8bit의 첫 자리는 보수 자리
  1. 2진수의 0, 1 배치 반전				(00111000 -> 11000111)
  2. +1							(11000111 + 1 -> 11001000)
```
10진수		2진수			2의 보수
0 		00000000		10000000 = -128				
1		00000001		11111111
3		00000011		11111101
7		00000111		11111001
15		00001111		11110001
31		00011111		11100001
63		00111111		11000001
127		01111111		10000001
```
<br>

## 자료형
--------
* 수 (data) : 선 저장 -> 후 처리
* 변수 : 개발자의 유지 보수 측면에서 바뀔 가능성이 있는 가변수	(아파트 주민)
* 변수명 : 저장되어 있는 변수 공간에 접근하기 위한 문자 주소	(아파트 주소)
* 자료형 : data의 데이터 유형을 제한하고 저장하는 예약어		(아파트 유형)
  
|자료형|크기|값 범위|
|-|-|-|
|byte|1byte|-128 ~ 127|
|short|2byte| -32768 ~ 32767|
|char|2byte|0 ~ 65535|
|int(표쥰형)|4byte|-21억 ~ 21억|
|long|8byte|980경|
|float|4byte|10 <sup>-7<sub>|
|double|8byte|10 <sup>-16<sub>|
|String|문자열|

```
* byte < short = char < int < long < float < double
* 정의 : 4byte 정수만 저장되는 공간 형성 -> 공간에 100 저장 -> 저장 공간에 이름 부여

byte  bn;		// 선언
bn = 100;		// 초기화
short sn = -500;	// 정의 : 선언 + 초기화
char cn = 'A'; 		// 문자 -> 아스키코드
int n = 10000000;
long ln = 5000000000000;

float fn = 1.123456;
double dn = 5.123456789123456789;

String str = "문자열";
```
<br>

**자료형 변환**
* 자동 형변환 (암시적) : 컴파일러에 의한 자동 형변환
  - 작은 자료형에서 큰 자료형으로 형변환
* 강제 형변환 (명시적) : 프로그래머에 의한 강제 형변환
  - 큰 자료형에서 작은 자료형으로 형변환 -> 데이터 손실 발생
```
byte n = 100;
n = (int) 500;		// 자동 형변환
n = (byte) -100;	// 강제 형변환

byte n1 = 100;
int n2 = 200;
int result = n1 + n2;	// 연산식의 n2 : int 
//n1 = (byte) -100;	  -> 연산식의 가장 큰 자료형인 int로 자동 형변환 -> 에러

System.out.println("문자열1" + "문자열2");	// 문자열1문자열2
System.out.println("문자열" + '!');		// 문자열!

double dvalue = 3.14;
String str = Strign.valueOf(dvalue);		// "3.14"
String str = dvalue + "";			// "3.14"
//str = dvalue;					// 문자열로 형변환 필요 -> 에러
```
<br>

**Scanner : 키보드로 값을 입력받는 생성자**
* nextInt, nextLong : 정수형 입력
* nextFloat, nextDouble : 실수형 입력
* next : 문자열 입력 - 공백 포함 불가능 (공백 입력 -> 다른 문자열로 인식)
* nextLine : 문자열 입력 - 공백 포함 가능 (공백 입력 -> 같은 문자열로 인식)
```
import java.util.Scanner;			// Scanner Library 추가
public class Main {
    public static void main(String[] args) {
	Scanner sc = new Scanner(System.in);	// Scanner 객체의 자료형 sc

	int n = sc.nextInt();			// 2 3.14  -> n, d 동시 입력 가능
	double d = sc.nextDouble();		// n = 2, d = 3.14

	String s1 = sc.next();			// 문자열1 문자열2 -> s1, s2
	String s2 = sc.next();			// s1 = 문자열1, s2 = 문자열2

	sc.nextLine();				// 초기화하기 (한 줄 띄어주기) <- nextLine의 공백, 엔터 인식 방식 차이
	String str = sc.nextLine();		// str = 문자열3
    }	
}
```
<br>

## 연산자
--------
```
* 기본 산술 연산자
[+, -, *, /, % : 더하기, 빼기, 곱하기, 나누기-몫, 나누기-나머지]

* 복합 대입 연산자 (대입 + 산술)
[+=, -=, *=]
a += 10;				// a = a + 10;

* 비교 연산자
[==, !=, <, >]
a = 5; b = 10;
a == 5;					// 값이 동등한 경우
a <= b;					// 이하인 경우
a != b;					// 값이 다른 경우 (느낌표가 앞에 위치)

* 논리 연산자
[&&, || : 조건 모두 true면 true, 조건 중 최소 하나 true면 true]
(a < b) && (a > 15);			// true	(조건이 flase면 이 후 조건 계산 x -> false)
(b != 5) || (a != 5);			// true (조건이 true면 이 후 조건 계산 x -> true)

* 논리 부정 연산자
[=! : 연산자 의미 반전 (느낌표기 뒤에 위치)]
boolean flag = true;			// flag == true;
flag =! flag;				// flag == false;
	
* 증감 연산자
[++, -- : 변수 앞에 위치 -> 전치 연산, 변수 뒤에 위치 -> 후치 연산]
a = 5; b = 10;
c = a++ + ++b;				// a = 6, b = 11, c = 17
c = a-- - b--;				// a = 4, b = 9, c = 15

* 삼항 연산자
[선언 = 조건 ? 참 : 거짓]
a = 3;
String 거짓 = (a != 0) || (a >5) ? "참" : "거짓";
```
<br>

**흐름 제어문**
```
* if : 위쪽부터 조건에 맞는 1개만 실행
[if, else if, else : 첫 조건식, 첫 조건식이 false인 n번재 조건식, 모든 조건식이 false 경우]
int a = 3;
if (a == 3) 		// 첫 조건식 (필수)
    a = 5;
else if (a > 5) {	// 선택적
    a = 8;
}
else			// 선택적
    a = 10;

* switch : 값이 맞는 1개만 실행
[case n, default, break]
case 1 : n = 1;
    System.out.println("n = 1");
    break;			// switch문에서 빠져나가는 break
case 2 : n = 2;
    System.out.println("n = 2");
    break;
default				// case에 없는 기본값
    System.out.println("n = 0");

* while : 조건에 맞는 동한 반복 실행
[while, do while : 조건에 맞으면 실행, 무조건 1번은 실행]
int n = 0;
while (n <= 3) {		// n이 3이하인 동안 반복
    n++;
}

* for : 특정 횟수 동안 반복 실행
for(int i = 0; i < 10; i++) 	// 1줄이면 {} 생략 가능
    System.out.println(i);	


* continue : 반복문의 처음으로 돌아감
for (int i = 0; i < 10; i++) {
    if (i == 5)
        continue;		// i == 5면 하위 부분 스킵
    System.out.println(i);	// 0, 1, 2, 3, 4, 6, 7, 8, 9,
}

* break
[break, break Exit : 해당 반복문만 종료, 종료하는 부분 선택 가능]
Exit : 
for (int i = 0; i < 10; i++) {
    if (i == 5)
        break;			// i == 5면 반복문 그만
    System.out.println(i);	// 0, 1, 2, 3, 4
}
break Exit;
```
<br>

## Class
--------
* 객체 (Object) : 속성, 기능을 가지는 프로그램 단위
  - 속성 (Attribute) : 객체만의 고유한 값 (변수로 저장)
  - 기능 (Method) : 객체가 수행할 수 있는 행동 (함수로 구현)

* 클래스 (자료형) ; 동일한 종류의 객체에 필요한 메모리 공간 제공 (변수, 함수)
   * default : 같은 패키지 내에서만 접근 가능 (기본 접근 제한자) 
   * public : 접근 제한 X
   * private : 해당 클래스 내에서만 접근 가능 
   * protected : 같은 패키지, 타 패키지의 자식 클래스에서 접근 가능
   * static : 한 번만 생성되며 모든 인스턴스가 공유
   * final : 한 번만 생성되며 값 변경 불가능 (상수)

* 메모리 영역
  1. Stack 영역 : {} 내에 생성되는 공간 (int, double)
  2. Heap 영역 : 객체 저장 영역 (new 예약어)
  3. Class 영역 (Method 영역) : 공유 메모리 영역 (static, 생성자, 일반 메서드)
  * EX) SCanner sc = new Scanner(System.in);
    1. Scanner sc : Stack - Scanner 클래스 자료형으로 정의된 참조 변수 sc
    2. new : Heap - 영역에 객체 저장
    3. Scanner() : Class - 객체에 초기값 부여를 위한 생성자 메서드

* *오버로딩 (OverLoading) : 매개변수의 수, 자료형에 따라 같은 이름의 다른 생성자 호출*
```
* Default (동일 package 내에 생성)
class C01Person {					// 클래스 생성
    String name;
    int age;
    String addr;
}
C01Person hong = new C01Person();			// 참조 변수 생성
hong.name = "홍길동";
hong.age = 44;
hong.addr = "서울";
System.out.printf("%s, %d, %s \n", hong.name, hong.age, hong.addr);

* 매개변수 생성자 (Parameter Constructor) 
class C02Person {
    String name;
    int age;
    C02Person () {
        name = null;		age = 0;		// defualt 생성자 (매개변수 X)
    }
    C02Person (String name) { 				// 오버로딩
        this.name = name;	age = 0;		// C02Person의 name = this.name으로 구분
    }
    C02Person (int age) {
        this(null, age);				// 마지막 생성자 호출 (축약 기능)
    }
    C02Person (String name, int age) {
        this.name = name;	this.age = age;
    }
    C02Person (String ...str) { 			// 가변 인자 : 매개변수 값을 String 형태의 배열로 저장
        name = str[0];		age = str[1];	
    }
}

* Private : 외부에서 접근이 불가능 -> 값을 출력, 입력하기 위한 방법 : Getter, Setter
class C03Person {
    private name;
    public String getName() {return this.name)}			// 기존 name 반환
    public void setName(String name) {this.name = name;}	// 기존 name = 입력 name
}
```
<br>

**배열 (Array) : 같은 타입의 데이터를 연속된 공간에 순서대로 나열한 자료 구조**
```
byte[3] arr;		// index 3개
int arr2[5];		// index 5개

arr = {1, 2, 3};
arr[0] = 5;		// arr = {5, 2, 3}

* 얕은 복사 : 주소 값 복사
arr2 = arr1;

* 깊은 복사 : 값 복사
for (int i = 0; i < 3; i++) 
    arr2[i] = arr[i];	// arr2 = {5, 2, 3}
```
