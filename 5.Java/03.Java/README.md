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















## MVC
**MVC (Model View Controller) : 사용자 인터페이스, 데이터 논리 제어에 사용되는 소프트웨어 디자인 패턴**
* Model : 데이터, 비지니스 로직 관리
  - 데이터 저장 (요청에 따른 변경 후에 수신)
* View : 레이아웃, 화면 처리
  - 저장 정보 없이 출력만 담당 (요청에 따른 변경 후에 수신)
* Contoller : 모델, 뷰에 명령 전달 (중간 다리)
  - 모델, 뷰의 변경 모니터링
  - Front Controller : Client의 요청에 맞는 Controller 호출
  - Sub Controller : 실제 서비스 처리
 
* DTO (Data Transfer Object) : 계층간의 데이터 교환 객체 (View - Controller)
  - Client와 직접 통신에 이용 (RequestDto + ResponseDto)
```
DTO : 디폴트 생성자 + 모든 인자 생성자 + getter + setter + toString
public class BookDto {
    private long bookCode;
    private String bookName;
    private String isbn;
    // 생성자
    public BookDto() {}              // 디폴트 생성자
    public BookDto(long bookCode, String bookName, String isbn) {
        super();
        this.bookCode = bookCode;    // 모든 인자 생성자
        this.bookName = bookName;
        this.isbn = isbn;
    }
    // Getter, Setter
    public int getBookCode() {
        return bookCode;
    }
    public void setBookCode(long bookCode) {
        this.bookCode = bookCode;
    }
}
```
* DAO (Data Access Object) : DB 조회, 활용  (Model - DB)
  - DB에 Query를 통해 CRUD 적용
* Service : 비지니스 로직 처리 (Controller - Model - DB)




Connection Pool
Transaction
refactor extract interface
