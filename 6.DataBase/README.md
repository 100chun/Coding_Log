oracle DB 설치 (112? ver)
좌상단 +
생성

계정 우클릭 -> sql 워크시트 열기
좌 상단 화살표 (ctrl enter) : 라인 실행
그 옆 : 전체 실행

```
select * from USERTBL;
select * from USERTBL where name = '김경호';   -- where 조건은 가급적 primary key

select * from USERTBL where birthyear >= 1970 and height >= 182;
select * from USERTBL where birthyear >= 1970 or height >= 182;

select name, height from USERTBL where height between 180 and 183;

select name, height from USERTBL where addr in('경남', '전남', '경북');   -- 포함

select name, height from USERTBL where name like '김%';  -- keyword 검색, % (wildcard):길이 제한 없는 모든 문자 -> 김으로 시작만 하면 ok
select name, height from USERTBL where name like '_재범'; -- _ : 길이 제한이 있는 모든 문자 -> 재범 앞에 한 자리인 모든 글자
select name, height from USERTBL where name like '%경_';



select * from BUYTBL where amount <= 5;
select userid, prodname from BUYTBL where price between 50 and 500;
select * from BUYTBL where amount >= 10 or price >= 100;
select * from BUYTBL where userid like 'K%';
select * from BUYTBL where groupname = '서적' or groupname = '전자';
select * from BUYTBL where groupname in ('서적', '전자');
select * from BUYTBL where prodname = '책' or userid like '%W';

select * from USERTBL where height >= (select height from USERTBL where name = '김경호');   -- sub query
select * from USERTBL where birthyear >= (select birthyear from USERTBL where name = '임재범');
select * from USERTBL where height >= any (select height from USERTBL where addr = '경남');   -- return 값 여러개 -> any 붙여주기 -> 모두 적용 (or)
select * from USERTBL where height >= all (select height from USERTBL where addr = '경남');   -- return 값 여러개 -> all 붙여주기 -> 공통 사항 적용 (and)

select * from BUYTBL where price > (select price from BUYTBL where amount = 10);
select * from BUYTBL where amount > any (select amount from BUYTBL where userid like 'K%');
select * from BUYTBL where price > all (select price from BUYTBL where amount = 5);



create table TBL_BUY as select * from BUYTBL;   -- primary key는 복사 X
desc TBL_BUY;
select * from TBL_BUY;
select * from all_constraints where table_name = 'BUYTBL';

create table TBL_BUY2 as select * from BUYTBL where 1=2;
desc TBL_BUY2;
select * from all_constraints where table_name = 'TBL_BUY2';
select * from TBL_BUY2;

insert into TBL_BUY2 select * from BUYTBL;
select * from TBL_BUY2;

select name, mdate from USERTBL order by mdate;     -- 정렬 (기본-오름차순)
select name, mdate from USERTBL order by name desc;     -- 정렬 내림차순  
select name, mdate, height from USERTBL order by height desc, name asc;     -- 키 기준 내림차순 -> 중복 요소는 이름 오름차순
select distinct height from USERTBL order by height desc;

select * from USERTBL;
select rownum as RN, USERTBL .* from USERTBL; -- as : 별칭 지정 -> 행 번호에 별칭 rn 지정 -> usertbl의 모든 요소에
select * from (select rownum as RN, USERTBL .* from USERTBL) where RN >= 3;     -- 별칭 지정하면서 검색



select * from BUYTBL order by userid;
select * from BUYTBL order by price desc;
select * from BUYTBL order by amount, prodname desc;
select distinct prodname from BUYTBL order by prodname;
select distinct userid from BUYTBL;
select * from BUYTBL where amount >= 3 order by prodname desc;
create table CUsertbl as select * from USERTBL where addr in ('서울', '경기');
select userid, amount from BUYTBL order by userid;

select userid, sum(amount) as "구매총량" from BUYTBL group by userid;   -- userid 별 구매 총량 출력

select * from BUYTBL;
select groupname, sum(amount) as "구매총량" from BUYTBL group by groupname;       -- primary key는 제외해야함
select producname, sum(amount) as "구매총량" from BUYTBL group by prodname;

select userid, sum(amount * price) as "구매총액" from BUYTBL group by userid;
select userid, avg(amount * price) as "구매평균" from BUYTBL group by userid;
 
select count(*) from BUYTBL;    -- null 제외하고 count
select count(groupname) from BUYTBL;

select avg(amount) from BUYTBL;
select max(amount) from BUYTBL;
select min(amount) from BUYTBL;

select * from USERTBL where height = (select max(height) from USERTBL) or height = (select min(height) from USERTBL);
select * from BUYTBL where amount > (select avg(amount) from BUYTBL);

select trunc(avg(amount), 5) as "평균구매량" from BUYTBL;       -- 소숫점 자리수 제한

select userid, sum(amount) from BUYTBL group by userid;
select avg(height) from USERTBL;
select userid, amount from BUYTBL where amount = (select max(amount) from BUYTBL) or amount = (select min(amount) from BUYTBL);
select count(groupname) from BUYTBL;

select userid, sum(price * amount) as "총구매액" from BUYTBL group by userid having sum(price * amount) >= 100 order by "총구매액" desc;   -- gourp by의 조건절 having


select num, groupname, sum(price * amount) as "비용" from BUYTBL group by rollup(groupname, num);     -- groupname, num 기준으로 그룹화


select userid, prodname, sum(price*amount) as "비용" from BUYTBL group by prodname, userid;   -- userid가 기본키라서 기준에 추가 필요
select userid, prodname, sum(price * amount) as "비용" from BUYTBL group by rollup(prodname, userid) having sum(price * amount) >= 1000;
select userid, prodname, price from BUYTBL where price = (select max(price) from BUYTBL) or price = (select min(price) from BUYTBL);
select * from BUYTBL where groupname is null;
select * from BUYTBL where groupname is not null;
select * from BUYTBL where groupname != 'null';
select sum(amount) from BUYTBL group by rollup(prodname);



create table tmp(tidx number(10), name varchar(1000));
desc tmp;

create sequence tmp_seq START WITH 1
increment by 1
maxvalue 100
cycle nocache;

insert into tmp values(tmp_seq.nextval, 'a1');

select * from tmp;



create table TEST_01 (
    userid char(10) primary key,
    name char(10) not null
);

--desc TEST_01;
--select * from all_constraints where table_name = 'TEST_01' and constraint_type = 'P';
--select acc.constraint_name, acc.constraint_type,
--from all_cons_columns acc
--join user_cons_columns ucc
--on acc.constaint_name = ucc.constaint_name;

create table TEST_02 (
    userid char(10),
    name char(10) not null,
    primary key(userid)
);
select * from all_constraints where table_name = 'TEST_02' and constraint_type = 'P';
select * from all_cons_columns where table_name = 'TEST_02';

alter table TEST_01 drop primary key;   -- alter : 구조 변경
select * from all_constraints where table_name = 'TEST_01' and constraint_type = 'P';
select * from all_cons_columns where table_name = 'TEST_01';

alter table TEST_01 add constraint PK_USERID primary key(userid);






```
