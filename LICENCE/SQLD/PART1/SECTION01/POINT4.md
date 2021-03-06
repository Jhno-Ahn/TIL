### POINT4: 속성

> 정의
> 

<img width="485" alt="스크린샷 2022-01-24 오후 12 57 25" src="https://user-images.githubusercontent.com/81155572/150719735-2e70b371-f5e3-4c58-b801-f3a204bfc7bf.png">


속성은 ‘업무에서 필요로 하는 인스턴스로 의미상 더 이상 분리되지 않는 최소의 데이터 단위’이다.

> 특징
> 
1. 속성은 해당 업무에서 필요하고 관리하고자 하는 정보이다.
2. 정규화 이론을 근거로 주식별자에 함수적으로 종속된다. 즉 기본키가 변경되면 속성 값도 변경된다.
3. 한 속성은 한 개의 값만 가진다. 한 속성에 다중값이 있을 경우 별도의 엔터티를 이용하여 분리한다.
4. 속성명은 데이터 모델에서 유일하게 사용하되, 속성값은 중복될 수 있다.

> 분류
> 

<img width="508" alt="스크린샷 2022-01-24 오후 12 57 37" src="https://user-images.githubusercontent.com/81155572/150719751-6a02a69c-54ee-42f0-a0ea-d37d46e3f62c.png">


1. 특성에 따른 분류
- 기본 속성
    - 비즈니스 프로세스에서 도출되는 본래의 속성
    - 코드성 데이터, 엔터티 식별을 위한 일련 번호, 다른 속성을 계산하거나 다른 속성의 영향을 받아 생성된 속성을 제외한 모든 속성은 기본 속성이다.
    - 업무로부터 분석한 속성이라도 이미 업무상 코드로 정의한 속성은  기본 속성이 아니다.
    - 회원 ID, 이름, 계좌번호, 주문 일자, 이자율, 원금, 예치 기간 등
- 설계 속성
    - 데이터 모델링 과정에서 속성을 새로 만들거나 변형하여 도출된 속성
    - 유일한 값을 부여한다.
    - 상품코드, 지점 코드, 예금분류 등
- 파생 속성
    - 다른 속성에 의해 만들어지는 (계산되는)속성이다
    - 합계, 평균, 이자 등

2. 엔터티 구성방식(분해 여부)에 따른 분류

엔터티를 식별할 수 있는 속성을 PK 속성, 다른 엔터티와의 관계에서 포함된 속성을 FK 속성, 엔터티에 포함되고 PK/FK에 포함되지 않은 속성을 일반 속성이라 한다. 속성은 그 세부 의미를 쪼갤 수 있는지에 따라 나뉜다.

<img width="471" alt="스크린샷 2022-01-24 오후 12 57 59" src="https://user-images.githubusercontent.com/81155572/150719781-23ed5f9a-0877-4bc1-bd71-abc53a943440.png">


1. 단일 속성
- 하나의 의미로 구성된 것
- 회원 ID, 이름, 나이, 성별 등
2. 복합 속성
- 여러 개의 의미가 있는 것
- 주소(시, 구, 동, 번지와 같은 세부 속성으로 구성) 등
3. 다중값 속성
- 속성에 여러 개의 값을 가질 수 있는 것
- 다중값 속성은 엔터티로 분해되므로 1차 정규화를 하거나 별도의 엔터티를 만들어 관계로 연결해야 한다
- 상품 리스트, 자동차의 색상(차 지붕, 차체, 외부의 색 별로 색이 다를 수 있음) 등

> 엔터티, 인스턴스, 속성, 속성값의 관계
> 

한 개의 엔터티는 두 개 이상의 인스턴스가, 두 개 이상의 속성을 갖는다.

- 예를 들면 사원은 이름, 주소, 전화번호, 직책 등을 가질 수 있다. 사원이라는 엔터티에 속한 인스턴스들의 성격을 구체적으로 나타내는 것이 속성이며 각각의 인스턴스는 속성의 집합이다. 한 속성은 하나의 인스턴스에만 존재할 수 있다. 속성은 관계로 기술될 수 없고 자신이 속성을 가질 수도 없다.
- 엔터티 내 하나의 인스턴스 속 한개의 속성은 한 속성값만 가질 수 있다.
- 사원의 이름은 홍길동, 주소는 서울시, 전화번호가 1234, 직챙이 대리라고 할 때 이름, 주소, 전화번호, 직책은 속성이고 홍길동, 서울시, 1234, 대리는 속성값이다. 따라서 속성값 각각은 엔터티가 가지는 속성들의 구체적 내용이다.
- 속성명은 직원 엔터티의 이름, 고객 엔터티의 이름과 각 엔터티별로 동일한 속성명을 상용하여 데이터 모델의 일관성을 가지는 것이 좋다(X)
- 전체 데이터 모델에서 유일성을 확보하는 것이 좋다(O)

ex) 학생이 대학교에 입학하기 위해서는 주민번호, 이름, 나이를 입력해야 한다.

엔터티 : 학생, 입학 / 속성 : 주민번호, 이름, 나이

> 도메인이란?
> 

도메인은 각 속성은 가질 수 있는 값의 범위이다.
