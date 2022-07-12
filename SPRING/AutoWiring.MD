- 어플리케이션이 커질수록 <bean> 객체가 많아져서 XML 설정도 늘어남.
- 오토와이어링은 스프링이 자동으로 빈 종속 객체를 할당하도록 한다.
- 오토디스커버리는 스프링이 빈으로 설정해야 하는 클래스를 직접 알아낸다.
- 오토와이어링과 오토디스커버리를 함께 사용하면 XML양을 줄일 수 있다.

# 빈 프로퍼티  오토 와이어링

- 프로퍼티에 할당할 빈 레퍼런스가 명확한 경우 스프링은 오토 와이어링을 제공한다.

| 이름 | 내용 |
| --- | --- |
| byName | 해당 빈 프로퍼티와 일치하는 이름(또는 ID)을 갖는 빈 정의가 발견되는 경우 해당 빈이 없으면 아무 일도 하지 않는다. |
| byType | 해당 빈 프로퍼티와 일치하는 타입을 가지는 빈 정의가 발견되는 경우 해당 빈이 없으면 아무 일도 하지 않는다. |
| constructor | byType과 유사하지만 해당 프로퍼티를 설정하기 위한 생성자가 존재하는 경우 |
| autodetect | constructor 오토와이어링을 먼저 적용한 후 실패하면 byType을 적용 |

![image](https://user-images.githubusercontent.com/81155572/178458855-e3aa4a67-ea10-45ae-8ea3-22709ef48d34.png)

  
## byName

- Bean의 이름에 따라 객체 종속성을 주입.
- 이 경우 속성과 빈 이름이 같아야 한다.
- 내부적으로 setter 메서드 호출

```xml
	<bean id="piano" class="wiring.auto.Piano"/>
	<bean id="guitar" class="wiring.auto.Guitar"/>
	<!-- hong의 autowire을 byName으로 설정하고 id 값 drum를 instrument으로 변경 -->
	<bean id="instrument" class="wiring.auto.Drum"/>
	<bean id="hong" class="wiring.auto.Instrumentalist" autowire="byName">
		<property name="song" value="Hello"/>
	</bean>

-------------------------------------------------------

	<bean id="hello" class="wiring.auto.Hello"/>
	<!-- singer의 autowire을 byName으로 설정하고 id 값 bounce를 song으로 변경 -->
	<bean id="song" class="wiring.auto.Bounce"/>
	<bean id="singer" class="wiring.auto.Singer" autowire="byName">
		<property name="name" value="조용필" />
	</bean>
```

## byType

- 프로퍼티에 할당 가능한 타입인지에 따라서 적용
- byType으로 바뀌면 instrument 프로퍼티에는 빈의 클래명이 instrument인 빈이 오토 와이어링 된다.
- 단 상속이 적용된 하위 클래스까지 가능하다.
- 단점으로는 같은 클래스의 빈이 두 개 이상이면 스프링은 선택할 수 없기 떄문에 예외를 발생

```xml
<!-- 오토 와이어링 -->
<bean id="piano" class="wiring.autowiring.Piano"/>
<bean id="kenny" class="wiring.autowiring.Instrumentalist" autowire="byType">
<property name="song" value="Jingle Bells"/>
</bean>
```

### primary

- 선택을 위해 오토와이어링에 사용될 빈에 primary 속성을 사용.
- 기본값이 true이기 때문에 사용하지 않을 빈에 모두 false를 적어 주어야 한다.
