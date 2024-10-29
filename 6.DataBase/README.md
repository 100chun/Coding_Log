# Database (10/17 ~ 10/18)
**Oracle 환경 설정**
1. Oracle DB 설치 (XE 11.2 ver)
2. 좌상단 + 버튼 -> 계정 생성
3. 생성 계정 우클 -> SQL 워크시트 열기
* Ctrol + Enter : Line 실행
* F5 : 스크립트 실행
![1](https://github.com/user-attachments/assets/8f2a71f2-2b79-4067-b721-cbc30d5449ee)

**CMD 환경 설정**
1. cmd 실행
2. sqlplus 입력
3. user-name : system
4. password : 1234
5. 명령어 실행
6. commit; 입력 <- 자동 저장 X
**Oracle <-> CMD 연동됨**

## Oracle 명령어
----------------
```
* create : 구조 생성
create table TEST_01 {
    userid char(8) not null primary key,           // 기본키
    name varchar(10) not null,                     // 빈 값 허용 X
    age int;
    foreign key (gender) references TEST(gender)   // 외래키 (열 명명) 참조 테이블 (열 정보) 
}
create table TEST_02 as selct * from TEST_01;      // TEST_01의 모든 요소를 가진 TEST_02 생성 (복사)

* alter : 구조 변경
alter table TEST_01 add(address varchar(45));      // 열 추가
alter table TEST_01 modify(address varchar(100));  // 열 변경
alter table TEST_01 rename column address to addr; // 열 이름 변경
alter table TEST_01 drop column address;           // 열 삭제

* constraint : 묶기
constraint TEST_pk primary key(userid, name);       // 기본키 2개 지정

* drop : 테이블 삭제
drop table TEST_02;                                // 테이블 삭제

* insert : 행(열의 값) 삽입
insert into TEST_01 values('LSG', '이승기', 35);  // 외래키 제외한 값 삽입
insert into TEST_01 values('SSG', '신세경', 28);  // not null X -> null 가능

* desc : 테이블 정보 조회
desc TEST;

* select : 행 정보 조회
[<, >, =, and, or, between, in, like]
select * from TEST_01;                             // TEST_01 테이블의 모든 행 조회
select name, age from TEST_01;                     // name, age 열 값 조회
select * from TEST_01 where age < 30;              // age의 값이 30 미만인 모든 행 조회
select * from TEST_01 where age between 25 and 32; // age 값이 25 ~ 32
select name from TEST_01 where name like '신%';    // 신으로 시작하는 모든 문자열
select * from TEST_01 where name like '_승_';      // 2자리가 승이고 총 3자리인 문자열
select * from TEST_01 where age in(20, 28);        // age 값이 20 또는 28
select * from TEST_01 where userid = 'LSG' and age = 35;
select * from TEST_01 where name like '%세_' or age = 28;

* () : 서브 쿼리
[any, all : 아무 값 만족 (or), 모든 값 만족 (and)]
select name, addr from TEST_01                     // name이 신세경인 행의 나이 미만의 나이를 가지는 행
where age < (select age from TEST_01 where name = '신세경');
select * from TEST_01
where age > any (select age from TEST_01 where userid = 'LSG')
selct addr : from TEST_01
where age = all (select age from TEST_01 where age >= 19);

* order by : 정렬
select name, age from TEST_01 order by name;     // name 순으로 오름차순 정렬 (default)
select addr from TEST_01 order by userid desc;   // userid 순으로 내림차순 정렬

* group by : 통합 정보
select name, age from TEST_01 group by addr;    // addr로 통합된 name age 정보 확인

* 계산
[sum, avg, max, min, trunc, count]
select gender, sum(age) from TEST_01 group by name;  // age의 합
```
<br>

## MVC
-----
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
* DAO (Data Access Object) : DB 조회, 활용  (Model - DB)
  - DB에 Query를 통해 CRUD 적용
**Transaction (TX) : 오류 발생 시에 실행 전으로 되돌리는 작업**
1. try, catch 구문 작성
2. auto Commit 해제
3. 본문 마지막에 commit
4. 오류 발생 시에 rollback

**DTO : 디폴트 생성자 + 모든 인자 생성자 + getter + setter + toString**
```
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

**DAO**
```
private static String url = "jdbc:mysql://localhost:3306/tmpdb";
private static String id = "root";
private static String pw = "1234";

private static Connection conn;
private static PreparedStatement pstmt;
private static ResultSet rs;		

public static List<BookDto> selectAll() throws SQLException{
    try {                               				// 오류 발생 가능 부분 -> catch에서 처리
	    Class.forName("com.mysql.cj.jdbc.Driver");			// DB 연결 드라이버 클래스 로드
	    conn = DriverManager.getConnection(url, id, pw);		// 커넥터에 서버 정보 저장
        conn.setAutoCommit(false);					// Auto Commit 해제 - TX

        // Insert
        pstmt = conn.prepareStatement("insert into tbl_book values(?, ?)");	// SQL 실행문
        pstmt.setLong(1, 12345);						// 1번째 물음표 값
        pstmt.setString(2, "채식주의자");					// 2번째 물음표 값
        pstmt.executeQuery();						        // 쿼리 실행

        // Select All
        pstmt = conn.prepareStatement("select * from tbl_book");
        rs.executeQuery();					// 쿼리 실행
        List<BookDto> list = new ArrayList();			// 정보 저장 목록
        BookDto dto = null;					// 정보 저장 객체 (if 문 밖에 선언)
        if (rs != null) {					// rs에 값이 있을 때 (Validation Check)
            while (rs.next()) {					// rs에 다음 값이 있는 동안
	        dto = new BookDto();				// 정보 저장 객체
                dto.setBookCode(rs.getLong("bookCode"));	// rs의 bookCode열 값 추출
                dto.setBookName(rs.getString("bookName"));	// rs의 bookName열 값 추출
                list.add(dto);					// 목록에 추출 객체 저장
            }
        }

        // Select (+ 조건)
        pstmt = conn.prepareStatement("select * from tbl_book where bookName = ?");
        pstmt.setString(1, "채식주의자");	// 찾고 싶은 정보의 조건
        rs.executeQuery();			// query 실행    
        int code = 0;				 // bookCode 저장 객체					
        while (rs != null) {			// next로 감싸지 않으면 rs값 추출 불가
            code = rs.getLong("bookCode");	// bookCode열 값 추출
        }    

        rs.close();		        // 사용 끝난 객체 닫기
        pstmt.close();                  // 사용 역순서로 닫기

        conn.commit();		        // 마지막에 commit - TX
        conn.close();
        } catch (Exception e) {		// 오류 e <- try에서 발생
	    conn.rollback();            // 오류 발생하면 초기화 - TX
	}
}	
```
<br>
