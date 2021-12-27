# 스프링 프레임워크의 간략한 역사

프레임워크는 말 그대로 '뼈대나 근간을 이루는 코드들의 묶음'이다.
중요한 점은 이 뼈대가 왜 필요한지에 대한 것이다.

개발자는 각 개객인의 능력 차이가 큰 직종이고, 따라서 개발자 구성에 따라 프로젝트의 결과 역시 큰 차이를 낳는다.
프레임 워크는 바로 이런 상황을 극복하기 위한 코드의 결과물이다.
프레임워크를 이용한다는 의미는 프로그램의 기본 흐름이나 구조를 정하고, 모든 팀원이 이 구조에 자신의 코드를 추가하는 방식으로 개발하게 된다.

프레임워크의 최대의 장점은 개발에 필요한 구조를 이미 코드로 만들어 놓았기 때문에, 회사의 입장에서는 프레임워크를 사용하면 일정한 품질이 보장되는 결과물을 얻을 수 있고,
개발자의 입장에서는 개발 시간을 단축할 수 있습니다.

# 스프링의 주요 특징
1. POJO 기반의 구성
2. 의존성 주입을 통한 객체 간의 관계 구성
3. AOP(Aspect-Oriented-Programming) 지원
4. 편리한 MVC 구조
5. WAS의 종속적이지 않은 개발 환경

### POJO 기반의 구성
스플링은 관계를 구성할 때 별도의 API등을 이용하지 않는 POJO(Plain Old Java Object)의 구성만으로 가능하도록 제작되어 있다.
쉽게 말해서 Java 코드를 이용해서 객체를 구성하는 방식을 그대로 스프링에서 사용할 수 있다.

이것이 중요한 이유는 코드를 개발할 때 개발자가 특정한 라이브러리나 컨테이너 기술에 종속적이지 않다는 것을 의미하기 때문이다.
-> 가장 일반적인 코드를 작성하므로 생상선 유리, 코드 테스트 또한 유연하게 가져갈 수 있음.

### 의존성 주입과 스프링
의존성은 하나의 객체가 다른 객체 없이 제대로 된 역할을 할 수 없다는 것을 의미한다.

주입은 말 그대로 '밀어 넣는 것'을 의미.

- 스프링은 'ApplicationContext'라는 존재가 필요한 객체들을 생성하고, 필요한 객체들을 주입하는 역할을 해 주는 구조이다.
- 스프링을 이용하면 개발자들은 기존의 프로그래밍과 달리 객체와 객체를 분리해서 생성하고, 이러한 객체들을 엮는(wiring)작업을 하는 형태의 개발을 하게 된다.
- 스프링에서는 ApplicationContect가 관리하는 객체들을 빈(Bean)이라는 용어로 부르고, 빈과 빈 사이의 의존관계를 처리하는 방식으로 XML설정, 어노테이션 설정, Java설정 방식을 이용할 수 있다.
