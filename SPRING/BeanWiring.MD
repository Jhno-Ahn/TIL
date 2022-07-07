## BeanWiring의 정의

- 스프링은 객체가 자신의 일을 하기 위해서 다른 객체를 직접 찾거나 생성할 필요가 없다.
- 컨테이너가 협업할 객체를 직접 제공한다.
- 이러한 객체간의 연관관계 형성 작업이 종속객체 주입(DI) 이를 와이링이라고 한다.

## 빈 선언

![image](https://user-images.githubusercontent.com/81155572/177775730-5f7a7bf0-8a58-4b37-8557-c2f9e130b08b.png)


## 인터페이스 구현

```java
public interface Performer { // 공연자
	//공연하다. (추상메서드) , PerfomanceException으로 예외 던져줌
	public void perform() throws PerformanceException;
}
```

## 예외처리 클래스

- Exception 을 상속받는 PerformanceException
- 어떤 예외가 올 지 모르기 때문에 모든 예외를 처리해주는 Exception을 사용

```java
public class PerformanceException extends Exception {
	
}
```

## 메인 클래스

```java
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class BeanWiringTest {
	public static void main( String[] args ) throws PerformanceException {
//		// 강한 결합
//		Juggler kim = new Juggler();
//		kim.perform();
//		
//		// 느슨한 결합
//		Performer hong = new Juggler();
//		hong.perform();
		
		// DI 종속 객체 주입
		ApplicationContext ctx
			//xml에서 객체를 만들어 받아 쓰기 위해
			= new ClassPathXmlApplicationContext( "/wiring/bean/ApplicationContext.xml" );
		// getBean통해 받아오면 Object로 반환되기 때문에, 형변환 해주어야 함.
		Performer hong = (Performer) ctx.getBean( "hong" );
		hong.perform();		
		
		
		// 연습용
		Performer singer = (Performer) ctx.getBean( "singer" );
		singer.perform();
	}
}
```

## 빈 선언

- Performer(공연자)를 상속받는 Juggler(저글링하는 공연자) 클래스 생성

```java
public class Juggler implements Performer {
	private int beanBags = 3;

	// 기본 생성자
	public Juggler() {}
	
	// 생성자 오버로딩
	public Juggler( int beanBags ) {
		this.beanBags = beanBags;
	}	
	
	// Performer에 있는 추상 메서드 perform을 여기서 상황에 맞게 완성시켜줌.
	public void perform() throws PerformanceException {
		System.out.println( beanBags + "개를 저글링합니다." );
	}
}
```

- Performer(공연자)를 상속받는 Singer(가수) 클래스 생성

```java
public class Singer implements Performer {
	private String name; // xml에서 value 값
	private Song song;   // xml에서 ref 값
	
	//기본 생성자
	public Singer() {}
	
	//생성자 오버로딩
	public Singer(String name, Song song) {
		this.name = name;
		this.song = song;
	}
	
	//Performer인터페이스에 있는 perform 추상메서드 완성.
	public void perform() throws PerformanceException {
			song.singing();
			System.out.println(name);
	}
}
```

- Performer를 상속받는 Juggler를 상속받는 PoeticJuggler 클래스

```java
public class PoeticJuggler extends Juggler {
	// 같은 클래스 안에서 그냥 사용 가능 시인 인터페이스
	private Poem poem; 
	
	// 기본생성자
	public PoeticJuggler() {}
	
	// 생성자 오버로딩
	public PoeticJuggler( int beanBags, Poem poem ) {
		super( beanBags ); // 부모클래스의 생성자로 던져라
		this.poem = poem;
	}
	
	// Performer에 있는 perform 추상 메서드 완성
	public void perform() throws PerformanceException {		
		super.perform(); // 부모쪽에서 처리
		poem.recite(); // 시인이 시낭송
	}
}
```

## 객체 주입

### 생성자를 이용한 주입

- 생성자를 이용해서 주머니의 개수를 늘린다.

```xml
<!-- DI -->
	<bean id="lee" class="wiring.bean.Juggler"/>
	
	<!-- 생성자 Wiring -->
	<bean id="park" class="wiring.bean.Juggler">
		<constructor-arg value="5"/>
	</bean>
	
	<!-- 시 객체  -->
	<bean id="flower" class="wiring.bean.Flower"/>
	<bean id="picnic" class="wiring.bean.Picnic"/>
	
	<!-- 공연자 객체 -->
	<bean id="hong" class="wiring.bean.PoeticJuggler">
		<constructor-arg value="7"/> <!-- value는 기본형 타입일 때 사용  -->
		<constructor-arg ref="flower"/>  <!-- ref 값은 interface나 클래스형 타입 -->
	</bean>
	
	<!-- 가수 객체 -->
	<bean id ="hello" class="wiring.bean.Hello"/>
	<bean id="singer" class="wiring.bean.Singer">
		<constructor-arg value ="조용필"/> <!-- value는 기본형 타입일 때 사용  -->
		<constructor-arg ref ="hello"/> <!-- ref 값은 interface나 클래스형 타입 -->
	</bean>
```

## 객체 레퍼런스 주입

### 시낭송 인터페이스

```java
package wiring.bean;

public interface Poem {
	public void recite();
}
```

### Song(노래) 인터페이스

```java
public interface Song {
	public void singing();
}
```

### 주입할 객체

- Poem(시) 인터페이스를 상속받은 Flower 클래스

```java
public class Flower implements Poem {
	String str = "내가 그의 이름을 불러주기 전에는\r\n" + 
			"그는 다만\r\n" + 
			"하나의 몸짓에 지나지 않았다.\r\n";
	public void recite() {
		System.out.println( "Flower : " + str );
	}
}
```

- Song(노래) 인터페이스를 상속받는 Hello 클래스

```java
public class Hello implements Song {
	private String str = "네 눈빛을 보면 꽤 낯 가려 보여\r\n" + 
			"자존심도 좋지만 난 너 생각뿐야\r\n" + 
			"Ah~ 손끝만 스쳐도 그댄 벌써 나를 알아보리\r\n" + 
			"Ah~ 우린 운명이라고 나의 느낌이 말해주지";
	public void singing() {
		System.out.println( "Hello : " + str );
	}
}
```
