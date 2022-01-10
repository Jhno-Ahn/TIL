# DATABASE

> 데이터베이스 종류는?
> 
1. Hirearchical Data Base : IMS/DB, HDB
2. NetWork DataBase
3. Relational DB, OR(Relatioanal, Object) DB
- 대형 Oracle, DB2, Sysbase, Informix
- 소형 MS-SQL, My SQL, PostgresSQL
- 기타 MongoDB
4. OODB(Object Oriented DataBase)

> Oracle과 MySQL의 차이는?
> 
- Oracle → 대용량처리에 적합, UNIX, Linux 메인프레임 등에서 사용, DB관리자 별도
- MySQL → 5000만건 미만의 데이터 주로 PC, UNIX 시스템에서 사용, 보통 개발자가 DB관리
- SQL의 80~90%가 비슷하지만
    - MySQL에 없는 Oracle 명령어 : varchar2, nvl, nvl2, sequence, decode, outer join에서 + 등
    - Oracle에 없는 MySQL 명령어 : autoincrement, show, ifnull 등
    

> 데이터베이스 언어(Database Language)란
> 
- 데이터베이스를 구축하고 이용하기 위한 데이터베이스 시스템과의 통신수단이다.
    - DDL(Data Definition Language) → DB를 구축하거나 수정할 목적으로 사용하는 언어
        - CREATE, ALTER, DROP
    - DML(Data Manipulation Language) → 사용자가 데이터를 처리할 수 있게하는 도구로써 사용자와 DBMS간의 인터페이스를 제공
        - SELECT, INSERT, DELETE, UPDATE
    - DCL(Data Control Language) → 데이터의 무결성, 보안 및 권한 제어, 회복 등을 하기 위한 언어
        - COMMIT, ROLLBACK, GRANT, REVOKE

> 제약사항(Constraint)
> 

컬럼에 대한 속성 형태로 정의하지만 엄연히 오라큰 데이터베이스 객체 중 하나이며 데이터 무결성을 보장하기 위한 용도로 사용.

- Not Null
    - 컬럼 생성시 지정하지 않으면 default로 Null이 허용 가능하게 되어 있다. 이를 방지하기 위함.
        - ex ) name varchar2(10) NOT NULL;
- Primary key
    - 기본키이다. Null 값을 갖지 못하고, 중복된 값도 가질 수 없다. 즉, UNIQUE와 NOT NULL을 동시 정의한 것과 같다.
        - ex ) bno number primary key;
- Foreign Key
    - 외래키이다. 이 외래키로 지정된 컬럼은 반드시 다른 테이블의 “Primary Key(기본키)”와 참조 관계를 가지게 되고 외래키로 지정된 컬럼은 참조관계를 가진 테이블의 기본키에 있는 값만을 가질 수 있다. 즉, Null값은 허용하되, 참조하고 있는 테이블의 기본키에 있는 값만 입력될 수 있다.
        - ex ) constraints 외래키명 foreign key references 참조테이블명
- Unique
    - 중복이 허용되지 않도록 데이터를 넣어야 하는 경우 사용.
        - ex) bno number UNIQUE;
- Default
    - 아무런 값을 입력 하지 않았을 때, 디폴트로 설정한 값이 입력되도록 하는 것.
- Check
    - Mysql enum 데이터 타입과 비슷한 효과로, 입력될 수 있는 데이터의 종류를 제한 할 수 있다.
        - bno number primary key CHECK (bno between 1 and 10) 으로 하면 1~10 값만 가능

> 색인(index)
> 
- 색은(index)은 내용을 미리 목록으로 만들어 놓고 찾고자 하는 내용을 검색하는 시간을 줄이기 위한 것
- 검색성능을 향상시키기 위한 것으로 정보에 빨리 접근할 수 있도록 소재를 표시해주고, 자료의 유무 확인, 신속한 이용을 하게 한다.
- 색인(index)이 많으면 조회 속도는 빠르지만 입력/수정/삭제의 속도는 떨어진다.

> 트랜잭션(transaction)
> 
- 데이터베이스 관리 시스템 또는 유사 시스템에서 상호작용의 단위로 논리적 작업단위(LUW, Logical Units of Work)이다.
- 유사 시스템이란 트랜잭션이 성공과 실패가 분명하고 상호 독립적이며, 일관되고 믿을 수 있는 시스템을 의미.
- 데이터베이스 시스템은 각각의 트랜잭션에 대해 원자성(Atomicity), 일관성(Consistency), 고립성(Isolation), 영구성(Durability)을 보증한다. 이 성질을 첫 글자를 따 ACID라고 한다.

> 커밋(Commit)과 롤백(Roll Back)
> 
- Commit → 처리결과의 영구적 반영을 시행한다.
- RollBack → 결과를 취소, 트랜잭션의 처음 시점으로 되돌린다.

> CRUD
> 

| 이름 | 조작 | SQL |
| --- | --- | --- |
| Create | 생성 | INSERT |
| Read(Retreieve) | 읽기 | SELECT |
| Update | 갱신 | UPDATE |
| Delete(Destroy) | 삭제 | DELETE |

> 커서(Cursor)
> 
- 커서는 일련의 데이터에 순차적으로 액세스 할 때 검색 및 “현재 위치”를 포함하는 데이터 요소이다.
- Declare → Open → Fetch → Empty → Close
