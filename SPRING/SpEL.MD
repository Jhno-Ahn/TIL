## 표현식 와이어링 SpEL

- 런타임까지 어떤 값이 할당되는지 모르는 경우 런타임에 평가하는 표현식을 이용하여 빈의 프로퍼티나 생성자 인자에 값을 할당하는 스프링 표현식 언어
- ID로 빈을 참조하는 기능
- 메서드 호출과 객체의 프로퍼티 액세스
- 값의 수학 관계 그리고 논리 연산
- 정규 표현식 매칭
- 컬렉션 처리

- Main 클래스

```java
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class SqELTest {
	public static void main(String[] args) {
		ApplicationContext ctx 
			= new ClassPathXmlApplicationContext("/wiring/spel/ApplicationContext.xml");
		Prop prop = (Prop) ctx.getBean("prop");
		System.out.println("값은 : " + prop.getStr());
	}
}
```

- Prop클래스

```java
public class Prop {
	private String str;
	public void setStr(String str) {
		this.str = str;
	}
	public String getStr() { 
		return str;
	}
}
```

- xml

```xml
<bean id="prop" class="wiring.spel.Prop">
		<property name="str" value="롱길롱"/>
</bean>
```
