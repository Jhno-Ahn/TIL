# 8장 테이블과 뷰

## 제약조건

- 제약조건이란?
    - 데이터의 무결성을 지키기 위한 제한된 조건 의미
    - 특정 데이터를 입력 시 어떤한 조건을 만족했을 때에 입력되도록 제약
        - 동일한 아이디로 다시 회원가입이 안되는 것
    - 데이터무결성을 위한 제약조건
    - PRIMARY KEY
    - FOREIGN KET
    - UNIQUE
    - CHECK
    - DEFAULT
    - NULL 값 허용
- 기본 키(PRIMARY KEY)
    - 테이블에 존재하는 많은 행의 데이터를 구분할 수 있는 식별자
    - 중복이나 NULL 값이 입력될 수 없음(회원아이디, 학번)
    - 기본 키로 생성한 것은 자동으로 클러스터형 인덱스 생성
    - 테이블에서는 기본 키를 하나 이상 열에 설정 가능
        
        ```sql
        create table usertbl
        	(userid char(8) not null,
        	name varchar(10) not null,
        	birthyear int not null,
        	constraint primary key pk_usertbl_userid(userid) -- 기본키 생성방법
        ```
        
- 외래 키(Foreign Key)
    - 두 테이블 사이의 관계 선언하여 무결성 보장
    - 설정하면 다른 테이블에 의존
    - 기준 테이블의 열은 반드시 PRIMARY KEY이거나 UNIQUE 제약 조건 설정 되어 있어야 함
    - ON DELETE CASCADE 또는 ON UPDATE CASCADE
        - 기준 테이블의 데이터가 변경되었을 때 외래 키 테이블도 자동으로 적용되도록 설정
    
    ```sql
    #생성 방법 1
    CREATE TABLE usertbl
    	(userid char(8) not null PRIMARY KEY,
    	name varchar(10) not null,
    	birthyear int not null);
    
    CREATE TABLE buytbl
    	(num int AUTO_INCREMENT not null PRIMARY KEY,
    	userid char(8) not null,
    	prodName char(8) not null,
    	FOREIGN KEY(userid) REFERENCES usertbl(userid) --외래키 참조
    );
    
    #생성 방법 2 - ALTER TABLE
    CREATE TABLE buytbl
    	(num int AUTO_INCREMENT not null PRIMARY KEY,
    	userid char(8) not null,
    	prodName char(8) not null,
    );
    ALTER TABLE buytbl
    	ADD CONSTRAINT FK_userTBL_buyTBL
    	FOREIGN KEY(userid)
    	REFERENCES usertbl(userid);
    ```
    

- UNIQUE 제약조건
    - 중복되지 않는 유일한 값을 입력해야 하는 조건
    - PRIMARY KEY와 비슷하나 UNIQUE는 NULL 값 허용
        - NULL은 여러 개가 입력되어도 상관 없음
- CHECK 제약 조건
    - 입력되는 데이터를 점검하는 기능
    - 키(HEIGHT) 제한 마이너스(-)값이 들어올수 없도록,
    - 출생년도에 1800년도 이런게 들어오지 못하게
- DEFAULT 정의
    - 값 입력하지 않았을 때 자동으로 입력
- NULL 값 허용
    - NULL 값 허용하려면 NULL을, 허용하지 않으려면 NOT NULL을 사용
    - PRIMARY KEY(unique + not null)가 설정된 열에는 생략하면 자동으로 NOT NULL
    - NULL 값은 ‘아무 것도 없다’ 라는 의미, 공뱁(’’)이나 0과 다름

## 테이블 압축

- 대용량 테이블의 공간 절약
- create table compressTBL(emp_no VARCHAR(14)) **ROW_FORMAT = COMPRESSED;**

## 임시 테이블

- CREATE **TEMPORARY** TABLE [IF NOT EXISTS] 테이블 이름
- 세션 내에서만 존재(닫히면 삭제)
- 생성한 클라이언트에서만 접근 가능
- 삭제 시점
    - DROP TABLE로 직접 삭제
    - 워크벤치, 클라이언트 종료시 삭제
    - 서비스 재시작

## 테이블 삭제

- DROP TABLE 테이블이름;
- 외래 키 제약 조건의 기준 테이블은 삭제할 수가 없음
    - 먼저 외래 키가 생성된 외래 키 테이블을 삭제해야 함
        - 구매 테이블이 존재하는데 회원 테이블을 삭제 할 수 없음, 구매 테이블 삭제가 선행 되어야 함
- 동시에 여러 테이블 삭제 가능
    - DROP TABLE 테이블1, 테이블2, 테이블3

## 테이블 수정

- ALTER TABLE
    - 테이블에 추가,변경,수정,삭제 모두 사용
    - 기본적으로 가장 뒤에 추가
    - 순서를 지정하려면 제일 뒤에 FIRST 또는 ALTER 열 이름 지정
    
    ```sql
    #추가
    ALTER TABLE usertbl
    	ADD homepage VARCHAR(30) -- 열 추가
    			DEFAULT 'www.naver.com' -- 디폴트 값
    			NULL; -- NULL 허용
    
    #삭제
    ALTER TABLE usertbl
    	DROP COLUMN mobile1;
    
    #데이터형식 변경
    ALTER TABLE usertbl
    	CHANGE COLUMN name uName VARCHAR(20) NULL;
    
    #제약 조건 추가 및 삭제
    ALTER TABLE usertbl
    	DROP PRIMARY KEY;
    ```
    

## 뷰(view)

- 일반 사용자 입장에서 테이블과 동일하게 사용하는 개체
- 뷰의 장점
    - 보안에 도움(사용자가 중요한 정보에 바로 접근하지 못함)
    - 복잡한 쿼리 단순화(긴 쿼리를 뷰로 작성, 뷰를 테이블처럼 사용가능)

```sql
create view v_usertbl
as
	select userid, name, addr from usertbl;
--------

create view v_userbuytbl
as
select u.userid, u.name, b.prodName, u.addr, 
CONCAT(u.mobile1, u.mobile2) as '연락처'
from usertbl u
	inner join buytbl b
	on u.userid = b.userid;

#실행
select * from v_userbuytbl where name = '김범수';
```

<img width="726" alt="스크린샷 2022-05-17 오후 3 27 56" src="https://user-images.githubusercontent.com/81155572/168754983-e867fc5f-1c8e-4d72-8c7d-e300df2ba8c2.png">

## 테이블스페이스 개녕

- 물리적인 공간을 뜻함
- 데이터베이스는 논리적 공간
- 테이블스페이스를 지정하지 않은 경우, 시스템 테이블스페이스에 테이블 저장됨
- 시스템 변수 innodb_data_file_path에 관련 내용 저장됨

## 성능 향상을 위한 테이블스페이스 추가

- 소용량의 데이터를 사용하는 경우에는 고려하지 않아도 되나 대용량의 데이터를 운영할 경우에는 성능 향상을 위해 테이블스페이스의 분리를 적극 고려
