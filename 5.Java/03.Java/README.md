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
list.stream().map((a,b), -> {a - b})  	// 람다스트림
```
## MVC
------
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
    // 생성자
    public BookDto() {}              // 디폴트 생성자
    public BookDto(long bookCode, String bookName) {
        super();
        this.bookCode = bookCode;    // 모든 인자 생성자
        this.bookName = bookName;
    }
    // Getter, Setter
    public int getBookCode() {
        return bookCode;
    }
    public void setBookCode(long bookCode) {
        this.bookCode = bookCode;
    }
    public int getBookName() {
        return bookName;
    }
    public void setBookName(long bookName) {
        this.bookName = bookName;
    }
    //toString
    @Override
    public String toString() {
        return "BookDto [bookCode=" + bookCode + ", bookName=" + bookName + "]";
    }	
}
```
* DAO (Data Access Object) : DB 조회, 활용  (Model - DB)
  - DB에 Query를 통해 CRUD 적용
```
// SQL DB CONN DATA
private static String url = "jdbc:mysql://localhost:3306/tmpdb";
private static String id = "root";
private static String pw = "1234";
	
private static Connection conn;
private static PreparedStatement pstmt;
private static ResultSet rs;		

public static List<BookDto> selectAll() throws SQLException{
    Class.forName("com.mysql.cj.jdbc.Driver");				// DB 연결 드라이버 클래스 로드
    conn = DriverManager.getConnection(url, id, pw);			// 커넥터에 서버 정보 저장

    // Insert
    pstmt = conn.prepareStatement("insert into tbl_book values(?, ?)");	// SQL 실행문
    pstmt.setLong(1, 12345);						// 1번째 물음표 값
    pstmt.setString(2, "채식주의자");					// 2번째 물음표 값
    pstmt.executeQuery();						// 쿼리 실행

    // Select All
    pstmt = conn.prepareStatement("select * from tbl_book");
    rs.executeQuery();						// 쿼리 실행
    List<BookDto> list = new ArrayList();			// 정보 저장 목록
    BookDto dto = null;						// 정보 저장 객체 (if 문 밖에 선언)
    if (rs != null) {						// rs에 값이 있을 때 (Validation Check)
        while (rs.next()) {					// rs에 다음 값이 있는 동안
	    dto = new BookDto();				// 정보 저장 객체
            dto.setBookCode(rs.getLong("bookCode"));		// rs의 bookCode열 값 추출
            dto.setBookName(rs.getString("bookName"));		// rs의 bookName열 값 추출
            list.add(dto);					// 목록에 추출 객체 저장
        }
    }

    // Select (+ 조건)
    pstmt = conn.prepareStatement("select * from tbl_book where bookName = ?");
    pstmt.setString(1, "채식주의자");		// 찾고 싶은 정보의 조건
    rs.executeQuery();				// query 실행
    int code = 0;				// bookCode 저장 객체					
    while (rs != null) {			// next로 감싸지 않으면 rs값 추출 불가
        code = rs.getLong("bookCode");		// bookCode열 값 추출
    }

    rs.close();			// 사용 끝난 객체 닫기
    pstmt.close();              // 사용 역순서로 닫기
    conn.close();
```
Connection Pool
Transaction
refactor extract interface
* Socket : TCP/IP 기반 네트워크 통신에서 데이터 송수신의 마지막 접점
* Server : 데이터를 송신자
* Client : 데이터 수신자
* Buffer : 데이터 이동에 필요한 바이트, 문자 변환자
