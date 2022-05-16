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
