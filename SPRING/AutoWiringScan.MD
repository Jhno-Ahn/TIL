# 오토 디스커버리

- <context:annotation-config>는 대부분의 <property><construct-arg>를 제거할 수 있지만 여전히 <bean>을 선언해야 한다.

## <context:component-scan>

- <context:component-config> 대신 사용해서
- 그 기능을 모두 수행하며 여기에 더해 자동으로 빈을 발견하도록 설정한다.

```xml
<!-- <context:annotation-config /> -->
<context:component-scan base-package="autoWiring.scan"/>
```

## 오토 디스커버리 빈 애너테이션

| 애너테이션 | 내용 |
| --- | --- |
| @Component | 범용 스테레오타입 애너테이션은 클래스가 스프링 컴포넌트임을 나타낸다. |
| @Controller | 클래스가 스프링 MVC 컨트롤러를 정의함을 나타낸다. |
| @Repository | 클래스가 데이터 저장소를 정의함을 나타낸다. |
| @Service | 클래스가 서비스를 정의함을 나타낸다. |
- 명시적으로 선언한 빈을 제거해도 된다.
- 지정한 패키지를 스캔할 때 @Component() 애너테이트를 만나면 자동으로 빈을 드옭해준다.
- 카멜 케이싱 클래스 이름으로 생성된다.

## 컴포넌트 - 스캔 필터링

- <context:include-filter>와 <context:exclude-filter>서브 엘리멘트를 추가하여 스캔을 조정할 수 있다.
- @Component() 등록을 제거해도 된다.

| 이름 | 내용 |
| --- | --- |
| annotation | 클래스에 지정한 애너테이션이 적용됐는지 여부, expression 애트리뷰트에는 애너테이션 이름을 적용한다. |
| assignable | 클래스가 지정한 타입으로 할당 가능한지의 여부, expression 애트리뷰트에는 클래스 타입 이름을 적용한다. |
| aspectj | 클래스 이름이 AspectJ의 표현식에 일치하는지 여부, expression 애트리뷰트에는 AspectJ의 표현식을 저용한다. |
| custom | org.springframeword.core.type.TypeFilter의 커스텀 구현체를 사용, expression 애트리뷰트에 지정한다. |
| regex | 클래스 이름이 정규 표현식에 일치하는지 여부, expression 애트리뷰트에는 정규표현식을 정용한다. |

### <context:include-filter>

- 모든 클래스를 빈으로 자동 등록한다.
- 대부분 assignable 사용
- expresstion에는 인터페이스 경로

```xml
<context:component-scan base-package="wiring.autowiring">
	**<context:include-filter type="assignable" expression="wiring.autowiring.Instrument"/>**
</context:component-scan>
```

### <context:exclude-filter>

- 등록하지 말아야할 클래스를 알려준다.
- @Skiplt 애너테이션과 유사

```xml
<context:component-scan base-package="wiring.autowiring">
	<context:include-filter type="assignable" expression="wiring.autowiring.Poem"/>
	<context:exclude-filter type="assignable" expression="wiring.autowiring.Flower"/>
</context:component-scan>

---------------------------

<context:component-scan base-package="wiring.autowiring">
	<context:include-filter type="assignable" expression="wiring.autowiring.Instrument"/> <context:exclude-filter type="assignable" expression="wiring.autowiring.SkipIt"/>
</context:component-scan>
```

# 스프링의 자바 기반 설정 사용

- XML 기반의 객체 생성 대신 자바 고유의 기능을 사용할 수 있다.
- 최소한의 XML 설정은 필요하다.
- <context:component-scan>이 @Configuration 애너테이션이 적용된 클래스를 찾아 자동으로 빈으로 등록한다.
