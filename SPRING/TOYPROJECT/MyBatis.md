# 맥 스프링 MyBatis 연동

## MyBatis
Mybatis는 흔히 'SQL 매핑 프레임워크'로 분류되는데, Mybatis 장점으로는
- 자동적으로 Connection close() rksmd
- Mybatis 내부적으로 PreparedStatement 처리
- #{prop}와 같이 속성을 지정하면 내부적으로 자동 처리
- 리턴 타입을 지정하는 경우 자동으로 객체 생성 및 ResultSet 처리

---

## MyBatis 관련 라이브러리 추가

MyBatis와 mybatis-spring을 사용하기 위해서 pom.xml 파일에 추가적인 라이브러리들을 설정해야 한다.

<img width="751" alt="스크린샷 2022-01-05 오후 11 41 28" src="https://user-images.githubusercontent.com/81155572/148240765-578a78ca-3a78-4fb8-9ece-355e46f47c7e.png">

---

## SQLSessionFactory

SQLSession을 통해 Connection을 생성하거나 원하는 SQL을 전달하고, 결과를 리턴 받는 구조로 작성.

root-context.xml 에서 작성.

<img width="930" alt="스크린샷 2022-01-05 오후 11 49 50" src="https://user-images.githubusercontent.com/81155572/148240854-e38744bf-6a96-4378-b70c-b75d6d04b705.png">

---

## 테스트 코드를 통해 확인

기존 테스트 코드에 추가한다
~~~
@Setter(onMethod_= {@Autowired} )
	private SqlSessionFactory sqlSessionFactory;
		
	@Test
	public void testMyBatis() {
		try(SqlSession session = sqlSessionFactory.openSession();
		Connection con = session.getConnection();
		) {
			log.info(session);
			log.info(con);
		} catch (Exception e) {
			fail(e.getMessage());
		}
	}
~~~

testMyBatis()는 설정된 SqlSessionFactory 인터페이스 타입의 SqlSessionFactoryBean을 이용해서 생성하고, 이를 이용해 Connection까지를 테스트한다.

정상적으로 실행된다면 아래와 같은 로그가 출력된다.

<img width="978" alt="스크린샷 2022-01-06 오전 12 06 29" src="https://user-images.githubusercontent.com/81155572/148241065-41d13008-d0ef-4c93-9a3c-63662e1b55d6.png">
