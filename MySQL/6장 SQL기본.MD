### DB, TABLE, 열의 이름이 확실하지 않을 때 조회하는 방법

- 현재 서버에 어떤 DB,TABLE이 있는지 보기
    - SHOW DATABASES;
    - SHOW TABLE STATUS;
    - SHOW TABLES
- 테이블의 열이 무엇이 있는지 확인
    - DESCRIBE 테이블명; 또는 DESC 테이블명;
- 네비게이터로 확인 가능 하나 명령어르 알아두면 LINUX 명령어 모드에서 사용가능

## 특정 조건의 데이터만 조회

- WHERE절
    - SELECT 필드이름 FROM 테이블이름 WHERE 조건식;
- 관계 연산자의 사용
    - OR 연산자 : ‘...또는’
    - AND 연산자 : ‘...그리고’
    - 조건 연산자(=,<,> 등)와 관계 연산자(NOT,AND,OR등)를 조합하여 사용 가능
- BETWEEN, AND, IN, LIKE
    - 데이터가 숫자이고, 연속적인값 → BETWEEN
    - 이산적인값 → IN()
    - 문자열의 내용 검색 → LIKE(문자뒤에 %-무엇이든 허용, 한 글자와 매치 ‘-’ 사용)

## ANY/ALL/SOME, 서브쿼리

- 서브쿼리
    - 쿼리문 안에 또 쿼리문 있음
    - ex) 김경호보다 키가 크거나 같은 사람의 이름과 키 출력
    - select name, height from usertbl
    where height > ( select height from usertbl where name = '김경호');
    - 서브쿼리의 결과가 둘 이상이 되면 에러 발생
- ANY
    - 서브쿼리의 여러 개의 결과 중 한 가지만만족해도 가능
    - SOME은 ANY와 동일한 의미로 사용
    - =ANY(서브쿼리)는 IN(서브쿼리)와 동일한 의미
- ALL
    - 서브쿼리의 결과 중 여러 개의 결과를모두 만족해야 함
    

## 원하는 순서대로 정렬하여 출력

- ORDER BY절
    - 결과물에 대해 영향을 미치지는 않고 출력되는 순서를 조절
    - 기본적으로 오름차순(ASC), 내림차순은(DESC)
- 중복된 것은 하나만 남기는 DISTICT
    - 테이블의 크기가 클수록 효율적
    - 중복된 것은 1개씩만 보여줌
- 출력하는 개수를 제한하는 LIMIT
    - 상위 N개만 출력하는 ‘LIMIT N’구문 사용
    - MySQL부담 줄여줌
- 테이블을 복사
    - CREATE TABLE 새로운 테이블명 (SELECT 복사할 열 FROM 기존테이블)
    - PK나 FK같은 제약 조건은 복사 안돔

## GROUP BY 및 HAVING 그리고 집계 함수

- GROUP BY절
    - 그룹으로 묶어줌
    - 집계 함수와 함께 사용
        - 효율적인 데이터 그룹화
        - ex) 각 사용자 별로 구매한 개수를 합쳐 출력
        - SELECT userID, SUM(amount) FROM buytbl GROUP BY userID;
    - 읽기 좋게 하기 위해 별칭 AS 사용
    - SELECT userID AS ‘사용자 아이디’, SUM(amount)  AS ‘총 구매 개수’ FROM buytbl GROUP BY userID;
- 집계함수
    
    
    | 함수명 | 설명 |
    | --- | --- |
    | AVG() | 평균을 구한다. |
    | MIN() | 최소값을 구한다. |
    | MAX() | 최대값을 구한다. |
    | COUNT() | 행의 개수를센다(중복 1개만 인정) |
    | STDEV() | 표준편자를 구한다. |
    | VAR_SAMP() | 분산을 구한다. |
    - ex) SELECT AVG(amount) AS ‘평균 구매 개수’ FROM buytbl;
- Having 절
    - WHERE와 비슷한 개념으로 조건 제한, 집계 함수에 대해서 조건 제한
    - HAVING절은 꼭 GROUP BY절 다음에 나와야 함 (순서 바뀌면 안됨)
- ROLLUP
    - 총합 또는 중간 합계가 필요한 경우
    - GROUP BY절과 함께 WITH ROLLUP문 사용
        - ex) 분류별로 합계 및 그 총합 구하기
        
        ```sql
        SELECT num, groupName, SUM(price * amount) AS '비용'
        		FROM buytbl
        		GROUP BY groupName, num
        		WITH ROLLUP
        ```
