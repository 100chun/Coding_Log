oracle DB 설치 (112? ver)
좌상단 +
생성

계정 우클릭 -> sql 워크시트 열기
좌 상단 화살표 (ctrl enter) : 라인 실행
그 옆 : 전체 실행

## Database (10/17 ~ )
**환경 설정**
1. Oracle DB 설치 (XE 11.2 ver)
2. 좌상단 + 버튼 -> 계정 생성
3. 생성 계정 우클 -> SQL 워크시트 열기
* Ctrol + Enter : Line 실행
* F5 : 스크립트 실행
![1](https://github.com/user-attachments/assets/8f2a71f2-2b79-4067-b721-cbc30d5449ee)

**Oracle 명령어**
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
