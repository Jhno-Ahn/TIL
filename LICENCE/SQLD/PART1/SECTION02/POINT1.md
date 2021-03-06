### POINT1 : 정규화

> 정규화
> 

- 정규화는 **최소한의 데이터 중복, 최대한의 데이터 유연성, 데이터 일관성**을 위해 데이터를 분리하는 과정이다.
- 따라서 **데이터 중복을 제거**하고 **데이터 모델의 독립성을 확보**한다.
- 정규화를 통해 업무상 변화가 생겨도 **데이터 모델의 변경을 최소화** 할 수 있다.
    - 데이터 모델이 자주 변경되는 경우 정규화하는 것이 좋다.
- 제 1정규화부터 제 5정규화까지 있지만 보통 제 3정규화까지만 수행한다.

> 정규화와 이상현상
> 

<img width="459" alt="스크린샷 2022-02-18 오후 1 06 21" src="https://user-images.githubusercontent.com/81155572/154615603-a8cb3776-def2-4f06-a379-0ea5fa183d2e.png">


위의 왼쪽 테이블에서 새로운 직원 엔터티가 추가된다고 가정하자. 만약 그 직원의 부서 정보가 없으면 ‘부서코드'를 임의로 채워넣어야 한다. 즉 불필요한 정보를 꼭 추가해야 한다.

새로운 부서 엔터티도 마찬가지인데, 사원 정보가 없다고 해도 임의의 값으로 ‘사원번호'를 입력하지 않으면 추가할 수 없다.

이를 이상현상이라고 하며 이럴 때 테이블 분해(정규화)가 필요하다.

> 정규화의 절차(제 3정규화까지)
> 

| 정규화 절차 | 설명 | 함수적 종속성 |
| --- | --- | --- |
| 제 1정규화 | 속성의 원자성을 확보하며 PK를 설정 | 완전 함수 종속성 |
| 제 2정규화 | PK가 2개 이상의 속성으로 이루어진 경우, 부분 함수 종속성을 제거 | 부분 함수 종속성 |
| 제 3정규화 | PK를 제외한 칼럼 간 종속성 제거 = 이행 함수 종속성 제거 | 이행 함수 종속성 |
| BCNF | PK를 제외하고 후보키가 있는 경우, 후보키가 기본키를 종속시키면 분해한다. |  |

> 정규화와 함수적 종속성Functional Dependency
> 

<img width="400" alt="스크린샷 2022-02-18 오후 1 06 54" src="https://user-images.githubusercontent.com/81155572/154615638-0d6ce81f-9afb-4eec-83af-be7bbf4de03b.png">


정규화는 함수적 종속성을 근거로 한다. 함수적 종속성이란 데이터들이 어떤 기준값에 의해 종속되는 현상이다. 이 때 기준값을 결정자Determinant라고 하고, 종속되는 값을 종속자Dependent라고 한다.

1. 제 1정규화
- 사람 엔터티는 주민번호, 이름, 출생지, 주소라는 속성을 갖는다
    - 여기서 이름, 출생지, 주소라는 속성은 주민번호라는 속성에 종속된다.
- 어떤 사람의 주민번호가 신고되면 그 사람의 이름, 출생지, 주소가 생성되어 딱 하나의 유일한 값을 갖게 된다.
    - 즉, 주민번호가 이름, 출생지, 주소를 함수적으로 결정한다
    - 기호로 표시하면 , 주민번호 →(이름, 출생지, 주소)
- 이 예시는 X(주민번호)가 Y(이름, 출생지, 주소)를 함수적으로 종속한다. 이 때 X가 기본키가 되었다.
- 이렇게 기본키를 잡는 것이 제1정규화이다.
- 또, 이렇게 종속자가 PK에만 종속되는 것이 **완전 함수 종속성**이다.
- **릴레이션에 속한 모든 속성의 도메인이 원자 값으로만 구성되어 있으면 제 1정규형**에 속한다.

2. 제 2정규화
- 제 2정규화는 부분 함수 종속성을 제거하는 것이다.
- 부분 함수 종속성이란 PK가 2개 이상의 칼럼으로 이루어진 경우에만 발생한다. PK가 한 칼럼(위의 예시)이면 제 2정규화는 생략한다.
    
    <img width="457" alt="스크린샷 2022-02-18 오후 1 07 07" src="https://user-images.githubusercontent.com/81155572/154615653-42a2179b-5462-422c-997b-18a397b62fa5.png">

    

새로운 예시를 보자.

- PK인 회원 ID가 변경되면 이름도 변경된다.
    - 회원 ID가 이름을 함수적으로 종속하는 것이다.
- 이런 경우를 부분 함수 종속성이라고 하며 분해가 필요하다.
    
<img width="463" alt="스크린샷 2022-02-18 오후 1 07 24" src="https://user-images.githubusercontent.com/81155572/154615672-355e6e7a-d88c-4e0f-98c0-e4272f4129c7.png">

    
- 부분 함수 종속성을 제거하면 위와 같다.
    - 회원이라는 새로운 테이블이 도출되고 회원 ID가 PK가 된다.

3. 제 3정규화
- 제 3정규화는 **이행 함수 종속성**을 제거하는 것이다.
- 이는 PK를 제거한 칼럼 간 종속성이 발생하는 것으로, 제 1정규화와 제 2정규화를 거친 뒤 제 3정규화를 수행해야 한다.
    - 주식별자를 제외한 칼럼 간 종속성에 관한 것이므로, PK와 관련성이 가장 낮다.
- X,Y,Z의 3개 속성에서 X→Y, Y→Z라는 종속 관계일 경우, X→Z가 성립될 때를 말한다.
    
  <img width="378" alt="스크린샷 2022-02-18 오후 1 07 37" src="https://user-images.githubusercontent.com/81155572/154615690-045ef056-14cc-417d-823d-ba3fc306ca50.png">

    
- 이렇게 관리점이 관리점 코드에 종속되는 것이 이행 함수 종속성이다.

이를 분리해보자

<img width="471" alt="스크린샷 2022-02-18 오후 1 07 49" src="https://user-images.githubusercontent.com/81155572/154615708-f3f796ed-fb1c-4fd6-98b9-d0e27ecbf948.png">


- 제 3정규화를 수행하면 이렇게 관리점 테이블이 도출되고 관리점 코드가 기본키가 된다.

4. BCNF(Boyce-Codd Nolmalization Form)
- X→Y에서 , Y가 X의 부분집합(trivial FD)이거나 X가 릴레이션 R의 수퍼키일 경우이다.
