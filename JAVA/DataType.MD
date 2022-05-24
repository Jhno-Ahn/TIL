## 변수의 메모리 사용

- 기본 타입 변수 → 실제 값을 변수 안에 저장
- 참조 타입 변수 → 주소를 통해 객체 참조

## JVM이 사용하는 메모리 영역

- OS에서 할당 받은 메모리 영역을 세 영역으로 구분
    - 메소드 영역
        - JVM 시작할 때 생성
        - 로딩된 클래스 바이트 코드 내용을 분석 후 저장
        - 모든 스레드가 공유
    - 힙 영역
        - JVM 시작할 때 생성
        - 객체, 배열 저장
        - 사용되지 않는 객체는 Garbage Collector가 자동 제거
    - JVM 스택
        - 스레드 별 생성
        - 메소드 호출할 땜다 Frame을 스택에 추가(push)
        - 메소드 종료하면 Frame 제거(pop)

## 참조변수의  ==, ≠ 연산

- 변수의 값이 같은지 다른지 비교
    - 기본 타입 : byte, char, short, int, long, float, double, boolean
        - 의미 : 변수의 값이 같은지 다른지 조사
    - 참조 타입 : 배열, 열거, 클래스, 인터페이스
        - 의미 : 동일한 객체를 잠초하는지 다른 객체를 참조하는지 조사
        

## null과 NullPointException

- null(널)
    - 변수가 참조하는 객체가 없을 경우 초기값으로 사용 가능
    - 참조 타입의 변수에만 저장가능
    - null로 초기화된 참조 변수는 스택 영역 생성
- ==, ≠ 연산 가능
- NullPointException의 의미
    - 예외(Exception)
        - 사용자의 잘못된 조작이나 잘못된 코딩으로  인해 발생하는 프로그램 오류
    - NullPointException
        - 참조변수가 null 값을 가지고 있을 때

## String 타입

- 문자열을 저장하는 클래스 타입

```java
String name;
name = "우리흥";
String hobby = "football";

//name, hobby -> stack영역
//"우리흥", "football" -> 힙영역
```

- 문자열 리터럴 동일하다면 String  객체 공유

```java
String name1 = "우리흥";
String name2 = "우리흥";

//name1, name2 -> 스택
//"우리흥"-> 힙
//name1,name2 둘 다 "우리흥"을 가르킴(공유)
```

- new 연산자를 이용한 String 객체 생성
    - 힙 영역에 새로운 String 객체 생성
    - String 객체체를 생성한 후 번지 리턴

```java
String name1 = new String("우리흥");
String name1 = new String("우리흥");

//name1(스택) -> "우리흥"(힙)
//name2(스택) -> "우리흥"(힙)
//우리흥이 2개 만들어져서 name1과 name2가 각각 하나씩 가르킴
```

## 배열이란?

- 같은 타입의 데이터를 연속된 공간에 저장하는 자료구조
- 각 데이터 저장 위치는 인덱스 부여해 접근
- 중복된 변순 선언 줄이기 위해 사용
- 반복문 이용해 요소들을 쉽게 처리

## new 연산자로 배열 생성

- 배열 생성시 값 목록을 가지고 있지 않음
- 향후 값들을 저장할 배열을 미리 생성하고 싶을 경우

```java
데이터타입[] 변수 = new 타입[길이];
------
타입[] 변수 = null;
변수 = new 타입[길이];
------
int[] intArray = new int[5];
```

## 배열 복사

- 배열은 한 번 생성하면 크기 변경 불가
- 더 많은 저장 공간이 필요하다면 보다 큰 배열을 새로 만들고 이전 배열로부터 항목 값들을 복사
- for문 이용
- System.arrayCopy() 메소드 이용
- Arrays 클래스 이용

## 열거 타입

- 한정된 값만을 갖는 데이터 타입
- 한정된 값은 열거 상수로 정의

```java
public enum 열거타입이름{...} 
// 파일 이름과 동일한 이름으로 선언 (첫 글자 대문자)

public enum Week { MONDAY, TUESDAY.....}
public enum LoginResult {LOGIN_SUCCESSS,...}
// 열거 상수 이름은 관례적으로 모두 대문자로 작성
// 다른 단어가 결합된 이름일 경우 관례적으로 밑줄로 연결
```
