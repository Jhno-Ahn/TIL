## 팩토리 메서드를 이용한 빈 생성

- 생성하려는 빈이 public 생성자가 없는 경우 팩토리 메서드를 이용해서 생성된 빈을 미리 연결한다.
- 생성자가 공연을 보여줄 무대는 하나 뿐이기 때문에 static으로 선언해야 한다.
- factory-method는 싱글톤 클래스가 아니더라도 정적 메서드로 객체를 생성하는 경우 사용가능

```xml
<bean id="stage" class="wiring.bean.Stage" factory-method="getInstance"/>
```

```java
public class Stage {
	private static Stage stage = new Stage();
	public static Stage getInstance() {
		return stage;
	}
}
```

## 싱글톤

### 싱글톤과 빈의 유효범위

- 컨테이너는 getBean() 메서드를 호출해서 빈을 가져오거나 빈을 와이어링 할 때 기본적으로 빈은 하나만 생성해서 항상 같은 인스턴스를 준다.

| 이름 | 유효범위 |
| --- | --- |
| singleton | 스프링 컨터이너당 하나의 인스턴스. 기본값. |
| prototype | 사용할 때마다 새 인스턴스 생성 |
| request | HTTP 요청당 하나의 인스턴스 . Spring MVC 같은 웹 환경에서만 유효 |
| session | HTTP 세션당 하나의 인스턴스.  Spring MVC 같은 웹 환경에서만 유효 |
| global-session | 전역 HTTP 세션당 하나의 인스턴스. 포클릿 환경에서만 유효 |

### 싱글톤 패턴

- 클래스의 인스턴스가 딱 1개만 생성되는 것을 보장하는 디자인 패턴이다.
- 해당되는 인스턴스에 대해서 statiac을 통해 최초 1번만 메모리를 할당시키며 이후 해당 인스턴스에 대한 호출이 생길 때 마다 최초로 생긴 인스턴스를 사용한다.
- 그래서 private를 사용해 객체 인스턴스를 2개 이상 새성하지 못하도록 막는다.

### 싱글톤 패턴의 사용하는 이유

- 메모리 측면에서 이점
- 최초 한번의 new 연산자를 통해 고정된 메모리 영역을 사용하기 때문에 추후 해당 객체에 접근할 때 메모리 낭비 방지, 속도 향상
- 다른 클래스 간에 데이터 공유가 쉽다.
- 인스턴스이기 때문에 다른 클래스의 인스턴스들이 접근하여 사용가능

### 싱글톤 패턴의 문제점

- 코드 자체가 많이 필요하다.
- 동시성 문제해결을 위해 syncronized 키워드를 사용해야 한다.
- 테스트하기 어렵다. 자원을 공유하고 있기 때문에 매번 인스턴스의 상태를 초기화시켜주어야한다.

## 빈의 초기화와 정리

- 빈을 초기화하거나 소멸시켜야 할 경우 정리할 필요할 경우가 있다.
- 초기화 이전에 로직을 실행하고 싶다면 init-method
- 제거되기 전에 어떤 로직을 실행하고 싶다면 destroy-method

```xml
<!-- 빈의 초기화 정리 -->
	<bean id="auditorium" class="wiring.bean.Auditorium" init-method="turnOn"
			destroy-method="turnOff"/>
```

```java
public class Auditorium {
	public void turnOn() {
		System.out.println("조명을 켠다");
	}
	public void turnOff() {
		System.out.println("조명을 끈다");
	}
}
```

## 자바 빈 프로퍼티의 주입

- 자바 빈 프로퍼티는 setter() getter() 메서드를 이용한다.
- 스프링은 세터 주입 방식을 제공

```xml
<!-- 프로퍼티 주입 -->
	<bean id="guitar" class="wiring.bean.Guitar"/>
	<bean id="piano" class="wiring.bean.Piano"/>
	<bean id="drum" class="wiring.bean.Drum"/>
	<bean id="hong" class="wiring.bean.Instrumentalist">
		<property name="song" value="Hello"/>
		<property name="instrument">
			<bean class="wiring.bean.Piano"/>
		</property>
	</bean>
```

```java
public class Instrumentalist implements Performer {
	private String song;
	private Instrument instrument;
	
	public void setInstrument(Instrument instrument) {
		this.instrument = instrument;
	}
	public void setSong(String song) {
		this.song = song;
	}
	
	public void perform() {
		System.out.println( song + "을 연주합니다. ");
		instrument.playing();
	
```

```java
public class Singer implements Performer {
	private String name; // xml에서 value 값
	private Song song;   // xml에서 ref 값
	
	//프로퍼티 주입을 위한 set메소드
	public void setName(String name) {
		this.name = name;
	}

	public void setSong(Song song) {
		this.song = song;
	}
	
	//기본 생성자
	public Singer() {}
	
	//생성자 오버로딩
	public Singer(String name, Song song) {
		this.name = name;
		this.song = song;
	}
	
	//Instrumentalist의 perform 추상메서드 완성
	public void perform() {
		song.singing();
	}
```

## 내부 빈 주입

- 빈을 공유하지 않고 자신만 사용할 경우 내부 빈을 생성해서 주입한다.
- 내부 빈은 재사용이 안되기 때문에 id는 선언해도 의미가 없다.
- 가독성이 떨어지는 문제가 생긴다.

```xml
<bean id=“객체명” class=“객체 타입”>
	<property name=“set 메서드” value=“값”/>
	<property name=“set 메서드”>
		<bean class=“객체 타입”/>
	</property>
</bean>
```

## p 네임스페이스를 이용한 와이어링

- <> 기호를 줄일 수 있다.
- 스키마 URI를 설정해야한다.

```xml
<bean id=“객체명” class=“객체 타입” p : set메드=“값” p : set메서드-ref=“빈 객체명”/>
<bean id="hong" class="wiring.bean.Instrumentalist"
		p:song="Hello" p:instrument-ref="guitar"/>
```

## 컬렉션 와이어링

| 이름 | 내용 |
| --- | --- |
| list | 값의 리스트에 사용. 중복 허용 |
| set | 값의 집합에 사용. 중복 없을 보장 |
| map | 키 - 값 쌍의 컬렉션의 사용. 키와 값의 타입에 제한 없음. |
| props | 키 - 값 쌍의 컬렉션의 사용. 키와 값이 모두 String |

```java
import java.util.Collection;

public class OneManBand implements Performer {
	private Collection<Instrument> instruments;
	public void setInstruments( Collection<Instrument> instruments ) {
		this.instruments = instruments;
	}
	public void perform() throws PerformanceException {
		for( Instrument instrument : instruments ) {
			instrument.playing();
		}
	}
}
```

```xml
<bean id="hong" class="wiring.bean.OneManBand">
		<property name="instruments">
			<set>
				<ref bean="piano"/>
				<ref bean="guitar"/>
				<ref bean="drum"/>
				<ref bean="guitar"/>				
			</set>
		</property>
	</bean>
```

## Map 형태

| 이름 | 내용 |
| --- | --- |
| key | 맵 엔트리의 키를 String 값으로 지정할 경우 |
| key-ref | 맵 엔트리의 키를 스프링 컨텍스트 내에 빈 레퍼런스로 지정할 경우 |
| value | 맵 엔트리의 값을 String 값으로 지정할 경우 |
| value-ref | 맵 엔트리의 값을 스프링 컨텍스트 내에 빈 레퍼런스로 지정할 경우 |

```java
import java.util.Iterator;
import java.util.Map;

public class TwoManBand implements Performer {
	private Map<String, Instrument> instruments;
	public void setInstruments( Map<String, Instrument> instruments ) {
		this.instruments = instruments;
	}
	public void perform() throws PerformanceException {
		Iterator<String> keys = instruments.keySet().iterator(); 
		while( keys.hasNext() ) {
			String key = keys.next();
			System.out.println( key + " : " );
			instruments.get(key).playing(); 
		}
	}
```

```xml
<bean id="hong" class="wiring.bean.TwoManBand">
		<property name="instruments">
			<map>
				<entry key="PIANO" value-ref="piano"/>
				<entry key="GUITAR" value-ref="guitar"/>
				<entry key="DRUM" value-ref="drum"/>
			</map>
		</property>
	</bean>
```
