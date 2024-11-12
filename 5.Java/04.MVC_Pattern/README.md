# MVC Pattern
**Model View Controller**
* 어플리케이션의 역하을 세 부분으로 나눈 소프트웨어 디자인 패턴
* Model : 데이터 처리 함수, 형식 정의
  * DTO : 정 객체 정의
  * DAO : DB 정보 관리 (SQL문 - CRUD)
* View : Model의 정보 (-> Controller)를 User에게 전달
* Controller : View의 입력을 Model에 전달하고 다시 View에 반영 (중간 다)
   * Service : 복잡한 Controller의 로직들을 캡슐화하는 역할

**View - JSP**
```
// JoinController에게 POST방식으로 입력받은 정보 전달
<form action="${pageContext.request.contextPath}/join}" method="POST" >
    <input name="id" />
    <input name="pw" />
    <input type="submit" value="회원 가입" />
</form>
```

**DTO**
```
@Data
@Builder
@NoArgsConstructor
@AllArgsConstructor
public class JoinDto {
    private String id;
    private String pw;
}
```

**DAO**
```
public class JoinDao {
    @Autowired
	  private DataSource dataSource;

    Connection conn;
    PreparedStatement pstmt;
    ResultSet rs;
	
	  public int insert(JoinDto dto) {
        pstmt = conn.prepareStatement("insert into tbl_memo values(?, ?)");
		    pstmt.setString(1, dto.getId());
		    pstmt.setString(2, dto.getPw());
		
		    int result =  pstmt.executeUpdate();

		    rs.close();
		    pstmt.close();
		    return result;
	  }
}
```

**Config**
```
@Bean
public DataSource dataSource() {
    HikariDataSource dataSource = new HikariDataSource();

    dataSource.setDriverClassName("com.mysql.cj.jdbc.Driver");
    dataSource.setJdbcUrl("jdbc:mysql://localhost:3306/bookdb");
    dataSource.setUsername("admin");
    dataSource.setPassword("1234");
    
    return dataSource;
}
```

**Service**
```
public class JoinServiceImpl {
    @Autowired
	  private JoinDao dao;

	  public boolean JoinRegistration(JoinDto dto) {
        int result = dao.insert(dto);

        return result > 0;
	  }
}
```

**Controller**
```
@Controller
@RequestMapping("/join") 
@Slf4j      // lombok 사용
public class JoinController {

    @Autowired
  	private JoinServiceImpl JoinServiceImpl;

    @GetMapping("/add")
	      public void join_get() {
		    log.info("GET /join/add...");
	  }
	  @PostMapping("/add")
	  public void join_post(@ModelAttribute @Valid MemoDto memoDto,BindingResult bindingResult,Model model) {
        log.info("POST /join/post..." + joinDao);
		
		    if(bindingResult.hasErrors()) {
			      for(FieldError error : bindingResult.getFieldErrors()) {				
				    log.info("Error Field : " + error.getField()+" Error Msg : " + error.getDefaultMessage());
				    model.addAttribute(error.getField(),error.getDefaultMessage());
        }
		}
}
```
