# SQL 고급

## MySQL에서 지원하는 데이터 형식의 종류

- Data Type으로 표현
    - 데이터 형식, 데이터형, 자료형, 데이터 타입등 다양하게 불림
- 데이터 형식에 대한 이해가 필요한 이유
    - SELECT문 더욱 잘 활용
    - 테이블의 생성 효율적으로 하기 위해 필요
- MySQL에서 데이터 형시의 종류는 30개 정도 : JSON
    - 중요하고 자주 쓰는 형식에 대해 중점 학습
- 숫자 데이터 형식
    
    ![1](https://user-images.githubusercontent.com/81155572/168587909-33bb8a4f-96ad-4dc6-bfd8-9128c73c045d.png)

- 문자 데이터 형식
    
    ![2](https://user-images.githubusercontent.com/81155572/168587919-ae2142e7-d28c-470b-929c-efcfccd46df9.png)

- 날짜와 시간 데이터 형식
    
    ![3](https://user-images.githubusercontent.com/81155572/168587925-c2034151-0318-4078-acbd-12f914d694c0.png)

- 기타 데이터 형식
    
    ![4](https://user-images.githubusercontent.com/81155572/168587940-5bedea5a-14dc-430d-aaac-5c80aa623dd1.png)

- LONGTEXT, LONGBLOB
    - 대량의 데이터를 저장하기 위해 지원
    - 4기가의 파일을 하나의 데이터로 저장 가능
    - LONGTEXT - 큰 텍스트 파일
    - LONGBLOB - 동영상 파일과 같은 큰 바이너리 파일

## 변수의 사용

- Workbench를 재시작까지는 유지, 재시작하면 소멸
- 변수의 선언과 값의 대입 형식

```sql
SET @변수이름 = 변수의 값; -- 변수의 선언 및 값 대입
SELECT @변수이름 ;         -- 변순의 값 출력

SET @myVar = 5;
SET @myVar2 = 3.5;

SELECT @myVar + @myVar2;
```

## 데이터 형식과 형 변환

- 데이터 형식 변환 함수
    - CAST(), CONVERT() 함수를 가장 일반적으로 사용
    - 데이터 형식 중에서 가능한 것은 BINARY, CHAR, DATE, DATETIME, ....UNSIGNED INTEGER
    - 함수 사용법
    
    ```sql
    형식 : 
    CAST (expression AS 데이터형식[(길이)]
    CONVERT (expression , 데이터형식[(길이)]
    -------
    
    SELECT CAST(AVG(amount) AS SINGED INTEGER) AS '평균 구매 개수'
    		FROM buytbl;
    
    SELECT CONVERT(AVG(amount), SINGED INTEGER) AS '평균 구매 개수'
    		FROM buytbl;
    ```
    
- 암시적 형변환
    
    ```sql
    SELECT '100' + '200'; -- 문자와 문자를 더함(정수로 변환연산)
    SELECT CONCAT('100','200'); -- 문자와 문자를 연결(문자로 처리)
    SELECT CONCAT(100, '200'); -- 정수와 문자를 연결(정수가 문자로 변환처리)
    SELECT 1 > '2mega'; -- 정수인 2로 변환되어서 비교
    SELECT 0 = 'mega2'; -- 문자는 0으로 변환됨
    
    #실행결과
    300
    100200
    100200
    0
    1
    ```
    

## MySQL 내장 함수

- 제어 흐름 함수
    - NULLIF(수식1, 수식2)
        - 수식1과 수식2가 같으면 NULL을 반환, 다르면 수식1을 반환
    - CASE ~ WHEN ~ ELSE ~ END
        - CASE는 내장 함수는 아니며 연산자로 분류
        - 다중 분기에 사용
        
        ```sql
        SELECT CASE 10
        		WHEN 1  THEN '일';
        		WHEN 5  THEN '오';
        		WHEN 10 THEN '십';
        		ELSE '모름'
        	END AS 'CASE연습';
        -------
        CASE 뒤의 값이 10이므로 세 번째 WHEN이 수행되어 '십'이 반환
        만약, 해당사항 없으면 ELSE문 반환
        ```
        
    - 문자열 함수
        - 문자열 조작, 활용도 높음
        - ASCII코드 - SELECT ASCII(’A’), CHAR(65)
        - CAHR(숫자) - 숫자의 아스키 코드값의 해당하는 문자 반환
        - LENGTH
            - 할당된 BIT크기 또는 문자 크기 반환
            - CHAR_LENGTH는 문자 ㅐ수 반환
            - LENGTH는 할당된 Byte 수 반환
        - Concatenation
            - CONCAT(문자열1, 문자열2...), CONCAT_WS(구분자, 문자열1, 문자열2....)
                - CONCAT : 문자열을 이어줌
                - CONCAT_WS : 구분자와 함께 문자열을 이어주는 역할
                
                ```sql
                SELECT CONCAT_WS('/', '2025','01','01');
                
                #결과
                2025/01/01 반환
                ```
                
        - ELT() : 위치번째에 해당하는 문자열 반환
        - FIELD() : 찾을 문자열의 위치를 찾아 반환, 없으면 0
        - FIND_IN_SET() : 찾을 문자열을 문자열 리스트에서 찾아 위치 반환( 콤마로 구분하고 공백 없어야 함)
        - INSTR() : 기본 문자열에서 부분 문자열 찾아 그 시작 위치 반환
        - LOCATE()는 INSTR()와 동일하지만 파라미터의 순서가 반대
## 피벗의 구현

- 피벗(Pivot) 이란?
    - 한 열에 포함된 여러 값 출력, 이를 여러 열로 변환하여 테이블 반환식 회전, 필요하면 집계까지 수행

## JSON 데이터

- 웹과 모바일 응용프로그램 등과 데이터 교환하기 위한 개방형 표준 포맷
- 속성(KEY) 과 값(VALUE)으로 쌍을 이루며 구성
- JavaScript 언어에서 파생
- 특정한 프로그래밍 언어에 종속되어 있지 않은 독립적인 데이터 포맷
- 포맷이 단순하고 공개되어 있기에 거의 대부분의 프로그래밍 언어에서 쉽게 읽거나 쓸 수 있음

## 조인(Join)

- 두 개 이상의 테이블을 서로로 묶어서 하나의 결과 집합으로 만들어 내는 것
- INNER, OUTER, CROSS, SELF 조인이 있다.
- 데이터베이스의 테이블
    - 중복과 공간 낭비를 피하고 무결성을 위해서 여러 개의 테이블로 분리 저장
    - 1대 다 관계 보편적

## INNER JOIN(내부 조인)

- 조인 중에서 가장 많이 사용되는 조인
    - 대개의 업무에서 조인은 이너조인 사용
    - 일반적으로 JOIN이라고 하는 것은 이너조인임
    
    ```sql
    SELECT <열 목록>
    FROM <첫 번째 테이블>
    		INNER JOIN <두 번째 테이블>
    		ON <조인될 조건>
    [WHERE 검색조건]
    ```
    

## OUTER JOIN(외부 조인)

- 조인의 조건에 만족되지 않는 행까지도 포함시키는 것
- LEFT OUTER JOIN
    - 왼쪽 테이블의 것은 모두 출력되어야 한다로 이해
- RIGHT OUTER JOIN
    - 오른쪽 테이블의 것은 모두 출력되어야 한다로 이해

```sql
SELECT <열 목록>
FROM <철 번째 테이블(LEFT 테이블)>
<LEFT | RIGHT | FULL > OUTER JOIN <두 번째 테이블(RIGHT 테이블)>
	ON <조인될 조건>
[WHERE 검색조건];
```

## CROSS JOIN(상호 조인)

- 한쪽 테이블의 모든 행들과 다른 쪽 테이블의 모든 행을 조인시키는 기능
- 크로스조인의 결과 개수 = 두 테이블 개수를 곱한 개수
    
    ![스크린샷 2022-05-18 오후 4.34.00.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fecc443a-e250-4a60-b324-22bbb44814be/스크린샷_2022-05-18_오후_4.34.00.png)
    
- 테스트로 사용할 많은 용량의 데이터를 생성할 때 주로 사용
- ON 구문 사용 x
- 대량의 데이터를 생성하면 시스템이 다운되거나 디스크 용량이 모두 찰 수 있어COUNT(*) 함수로 개수만 카운트

```sql
SELECT COUNT(*) AS '데이터 개수'
	FROM employees
		CROSS JOIN titles;
```

## SELF JOIN(자체 조인)

- 자기 자신과 자기 자신이 조인한다는 의미
- 조직도와 관련된 테이블

## IF..ELSE

- 조건에 따라 분기
- 한 문장 이상 처리되어야 할때 BEGIN.. END로 묶어주기

```sql
형식 :
IF <부울 표현식 > THEN
	SQL문장1
ELSE
	SQL문장2
END IF;
```

## CASE

- 조건에 따라 분기
    - 다중 분기
    - 조건에 맞는 WHEN이 여러 개더라도 먼저 조건이 맞는 WHEN이 처리됨
    - 점수로 성적을 판단하는 경우처럼 여러 단계로 분기 될 때 사용

## WHILE/ITERATE/LEAVE

- WHILE문
    - 다른 언어의 WHILE과 동일 개념
    - 참인 동안 반복되는 반복문
    
    ```sql
    형식 : 
    WHILE <부울 식> DO
    	SQL 명령문들..
    END WHILE;
    ```
    
    - ITERATE문을 만나면 WHILE문으로 이동해서 다시 비교 (CONTINUE와 동일 개념)
    - LEAVE문을 만나면 WHILE문 빠져나옴(BREAK 동일 개념)

## 오류 처리

- 형식 : DECLARE 액션 HANDLER FOR 오류조건 처리할문장;
- 액션
    - 오류 발생 시에 행동 정의
    - CONTINUE와 EXIT 둘 중 하나 사용, CONTINUE가 나오면 제일 뒤에 처리할문장 부분이 처리
- 오류 조건 : 어떤 오류를 처리할 것인지를 지정
    - MySQL의 오류 코드 숫자가가 오거나 SQLSTATE’상태코드’, SQLEXCEPTION 등이 올 수 있음

```sql
CREATE PROCEDURE errorProc()
BEGIN
	DECLARE CONTINUE HANDLER FOR 1146 SELECT '테이블 없음' AS '메시지';
	SELECT * FROM noTable; -- noTable은 존재하지 않는 테이블
END
CALL errorProc();
```

## 동적 SQL

- PREPARE문
    - SQL문을 실행하지는 않고 미리 준비만 해놓음
- EXECUTE문
    - 준비한 쿼리문 실행
    - 실행 후에는 DEALLOCATE PREFARE로 문장 해제
