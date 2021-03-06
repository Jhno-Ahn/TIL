# 기술면접준비

## PROGRAMING
> 프로그램이란?
> 
- 컴퓨터가 사람 일을 할 수 있도록 해 주는 것
- 컴퓨터에 처리되는 작업의 순서를 논리적으로 명령어로 작성하는 것

> JAVA언어의 장점은?
> 
- 객체지향형 프로그래밍 언어
- 독립적인 플랫폼
- 높은 이식성과 바이트 코드
- 라이브러리 지향성과 보안성
- 멀티 스레드와 가상머신

> 객체지향 언어(Object Oriented Language)의 장점과 등장한 배경
> 
- 코드의 재사용성이 높다
- 코드의 관리가 용이하다
- 제어자와 메서드를 이용해 데이터를 보호하고, 올바른 값을 유지하며, 코드의 중복을 제거해 오작동을 방지

> Primitive Type과 Reference Type이란?
> 
- Primitive Type은 변수에 값 자체를 저장하며, Reference Type은 메모리상에 객체가 있는 위치를 저장한다.
- Primitive Type의 종류는 boolean, byte, char, short, int, float, long, double 총 8가지이며,  Reference Type의 종류는 클래스타입, 인터페이스타입, 배열타입, 열거타입이다.

> 배열과 컬렉션의 차이점은?
> 
- 배열은 단 하나의 자료형만 저장이 가능하고, 컬렉션은 복수의 자료형을 저장할 수 있다.
- 배열은 고정된 크기이고, 컬렉션은 가변적 크기이다.

> 다형성이란?
> 
- 여러 가지 데이터를 다룰 수 있는 특성을 뜻함.
- 조상 클래스의 인스턴스를 이용하여 자손타입의 클래스를 다룬다거나, 메서드 오버롣ㅇ을 통하여 동일 이름의 메서드를 이용하여 다양한 형태의 파라미터를 다루는 것을 뜻한다.

> 멀티 쓰레드의 장단점은?
> 
- 두 가지 이상의 작업을 동시에 실행 할 수 있어 자원을 효율적으로 이용할 수 있으나, dead lock 및 동기화에 대한 철저한 검증이 필요하다.

> 자바에서 멀티쓰레드를 구현하는 방법은?
> 
- Thread 클래스를 상속한다. 단일 상속만 된다는 단점이 있다.
- Runnable 인터페이스를 상속한다. 다중 상속이 된다는 장점이 있다.

> Java 콜렉션의 대표 인터페이스는?
> 
- List
    - 순서가 있는 데이터의 집합으로 데이터의 중복을 허용한다.
    - 구현클래스 → ArrayList, LinkedList, Stack, Vector
- Set
    - 순서를 유지하지 않는 데이터의 집합으로 데이터의 중복을 허용하지 않는다.
    - 구현클래스 → HashSet, TreeSet
- Map
    - 키와 값의 쌍으로 이루어진 데이터의 집합으로 순서는 유지되지 않으며, 키는 중복으로 허용하지 않고, 같은 값은 중복을 허용한다.
    - 구현클래스 → HashMap, TreeMap, HashTable, Properties

> 컬렉션에서 제네릭이 추가된 이유는?
> 
- 컬렉션은 복수개의 데이터 타입 요소값이 저장되다 보니 원하는 자료형 타입 요소값을 추출하기 어렵다.
- 그러므로 지정한 자료형 타입 한가지만 저장하기 위해서 나온 것이 제네릭이다.

> 접근제어자의 종류와 특성
> 
- private → 같은 클래스 내에서만 접근 가능
- default → 같은 패키지 내에서만 접근 가능
- protected → 같은 패키지 내에서, 그리고 다른 패키지의 자손클래스에서 접근 가능
- public → 접근제한x
- public > protected > default > private

> Wrapper 클래스란?
> 
- Primitive 타입으로 표현할 수 있는 간단한 데이터를 객체로 만드는 기능을 지원하는 클래스를 뜻한다.
- byte → Byte
- short → Short
- int → Integer
- long → Long
- char → Character
- float → Float
- double → Double
- boolean → Boolean

> 추상클래스란?
> 
- 미완성 설계도이며, 미완성 메서드(추상메서드)를 포함하고 있는 클래스이다.
- 인스턴스를 생성할 수 없으며, 상속을 통해 자손클래스에 의해서만 완성된다.

> 인터페이스란?
> 
- 일종의 추상클래스
- 추상메서드를 갖지만, 추상클래스와 달리 일반 메서드 또는 멤버변수를 가질 수 없고, 오직 추상메서드와 상수만을 멤버로 가지며 그 외의 요소는 허용하지 않는다.
- 인터페이스로부터만 상속을 받을 수 있으며, 클래스와는 달리 다중상속이 가능하다.

> 인터페이스를 사용하는 이유는?
> 
- 다형성을 구현하기 위해서 사용
    - 같은 인터페이스를 구현하는 클래스들은 실행하는 객체가 인터페이스를 통하여 다른 객체를 사용할 수 있도록 하여 **클래스간의 결합도를 낮추고 응집도를 높힐 수 있음.**
    - 예로 스프링에서 DI(의존성 주입) 등에서 **다형성을 구현하고 결합도를 낮추기 위해 사용**
- 양식역할 : 규칙에 맞게 구현하도록 표준을 제시하고 클래스들이 메서드를 빠짐 없이 재정의 하도록 한다.

> 자바의 GUI에서의 스윙과 AWT의 차이점?
> 
- AWT는 운영체제가 갖고 있는 각 컴포넌트를 이용한다. 즉, 운영체제에 종속적인 GUI로서 운영체제 종류에 따라 화면에 출력되는 모양이 약간씩 다르다.
- 스윙은 운영체제가 갖고 있는 GUI를 사용하지 않고 자바 가상머신의 Swing 패키지를 직접 사용해 구현한다. 따라서, 운영체제가 서로 달라도 동일한 화면을 출력하게 한다.
- 스윙은 AWT보다 세련되고 다양한 GUI를 제공해주기 때문에 자바 어플 GUI개발에서는 AWT보다는 스윙을 더 많이 사용한다.

> 가비지 콜렉터(Garbage Collector)란?
> 
- 동적 할당된 메모리 가운데 더 이상 사용할 수 없게 된 영역을 자동으로 해제한다.
- 프로그래머가 동적으로 할당한 메모리 영역을 완벽하게 관리할 필요 x
- 이러한 작업은 백그라운드 섭스를 통해 자동으로 이뤄짐

> 컬렉션 List 인터페이스를 구현한 ArrayList 컬렉션 클래스란?
> 
- 가변적 크기이다.
- 순차적으로 요소 값을 저장한다.
- 중복 요소 값을 허용한다.

> 자바의 메모리 구조는?
> 

| 코드영역 |
| --- |
| 데이터영역(전역변수, static 변수) |
| Heap 영역(사용자의 동적할당) |
| Stack 영역(지역변수 매개변수) |
- out of memory 는 어느 메모리 부족?
    - heap 메모리 부족
    

> 메서드 오버로딩과 오버라이딩 설명
> 
- 오버로딩 → 메소드 이름은 같지만 매개변수의 개수나 데이터 형식을 다르게 정의하는 것
- 오버라이딩 → 기존에 있는 메소드를 재정의하는 것으로 매개변수의 개수나 데이터 형식이 같아야 한다.

> Exception?
> 
- 프로그램의 비정상적인 종료나 중단을 막을 수 있다.
- RuntimeException과 그 외의 Exception으로 나눌 수 있다.

> 동기화란
> 
- 하나의 자원을 여러 태스크가 사용하려 할 때에, 한 시점에서 하나의 태스크만이 사용할 수 있도록 하는 것

> 프로세스와 쓰레드의 차이점
> 
- 프로세스 → 실행중인 프로그램, 자원과 쓰레드로 구성
- 쓰레드 → 프로세스 내에서 실제 작업을 수행하는 단위, 모든 프로세스는 하나 이상의 쓰레드를 가지고 있다.
- 다중 쓰레드 → 하나의 프로세스(프로그램)에 하나 이상의 쓰레드를 생성 실행

> OSI 7계층
> 
> <img width="721" alt="스크린샷 2022-01-06 오후 12 17 30" src="https://user-images.githubusercontent.com/81155572/148323008-886b7480-5c1a-4fa5-a728-5f2ea1c9d720.png">


