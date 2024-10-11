10/8


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




mvc
view (요청) -> FrontController - execute -> BookController (파라미터 확인 -> 유효성 체크 -> 서비스 실행) -> BookService (요청자 확인 -> BookDao (tbl CRUD)
FC _> SC -> Service -> Dao -> tbl

EndPoint          ServiceNumber          parameter                    return
/book                    add(0)          BookDto                    boolean
/book                    Update(1)          BookDto                    boolean
/book                    Delete(2)          BookDto                    boolean
/book                    select(3)          BookDto                    bookDto
/book                    selectAll(4)          x                     list<BookDto>                   
