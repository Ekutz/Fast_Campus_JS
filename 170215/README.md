## Database
> 기본적인 Query를 알아보고 ORM Lite를 이용한 DB 사용법을 알아본다

### Basic Query
> C(create)R(read)U(update)D(delete)

##### Create
- create table 테이블명 (컬럼명1 속성, 컬럼명2 속성);

```
ex)
create table bbs (
bbsno int            -- 숫자는 int, float
, title varchar(255) -- 숫자값 바이트의 문자열 입력시 사용
, content text       -- 대용량의 데이터 입력시 사용
, ndate datetime
);
```
```
id값 자동 증가 table)
bbsno int primary key auto_increment not null -- 자동증가
, title varchar(255) -- 숫자값 바이트의 문자열 입력시 사용
, content text       -- 대용량의 데이터 입력시 사용
, ndate datetime
);
```
##### Read
- select 불러올컬럼명1, 컬럼명2 from 테이블명 where 컬럼명 = 값

##### Update
- update 테이블명 set 변경할컬럼명1 = 값, 컬럼명2 = 값 where 컬럼명 = 값

```
ex)
update bbs set title='이순신' where bbsno = 2;
commit;
```

##### Delete
- delete from 테이블명 where 컬럼명 = 값;

```
ex)
delete from bbs where bbsno = 1;
commit;
```

##### Insert
- insert into 테이블명(컬럼명1, 컬럼명2) value(숫자값,'문자값');

```
ex)
INSERT INTO bbs (bbsno, title, content) VALUES(2, '타이틀', '내용입니다');
commit;
```

---

### ORM Lite
> 안드로이드 내부에 Database를 구성할 수 있도록 해주는 Library

### 기획 순서
1. gradle 추가
2. Helper Class 생성 및 Dao 선언
3. Main 에서 DB 연결
4. Dao의 Api를 이용하여 DB 사용

- [Log를 이용한 DB 제어 예제](https://github.com/Ekutz/170215_ORM)

