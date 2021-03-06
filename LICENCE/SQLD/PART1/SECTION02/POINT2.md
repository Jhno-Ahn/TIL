### POINT2 : 정규화와 성능

> 정규화의 문제점
> 
- 정규화는 데이터 중복성을 제거한다.
    - 그래서 데이터 모델의 유연성을 높이고 성능 향상에 도움이 되낟.
- 하지만 데이터 조회select 시 조인join을 유발한다.
    - 그래서 CPU, 메모리 사용량이 크다.
- 이런 부분은 반정규화를 적용해서 해결한다.

예시를 들어보자

<img width="311" alt="스크린샷 2022-02-18 오후 3 14 34" src="https://user-images.githubusercontent.com/81155572/154628278-13284082-64e4-47ee-92c3-42ffb335a42f.png">


- A 테이블의 칼럼이 계속 증가하면 어쨌든 조인은 최소화되므로 조회 성능은 좋아진다.
- 하지만 너무 많은 칼럼이 추가되면 DBMS의 입출력 단위인 블록의 크기를 넘어서게 되어, 한 행을 읽기 위해 여러 블록을 읽어야 한다.
    - 따라서 I/O량이 증가되고 성능이 떨어진다.
- 이럴 때 반정규화가 필요하다.
