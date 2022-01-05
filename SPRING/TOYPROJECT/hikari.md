# hikari 연동

## 라이브러리 추가와 DataSource 설정

> [링크](https://mvnrepository.com/artifact/com.zaxxer/HikariCP)를 통해 porm.xml에 추가할 코드를 가져온다.

<img width="790" alt="스크린샷 2022-01-05 오후 10 39 23" src="https://user-images.githubusercontent.com/81155572/148226708-9b1a68b1-c76d-418e-bb39-55b7090e853e.png">


> root-context.xml 안에 <bean> 태그 작성한다.
~~~
<!-- Root Context: defines shared resources visible to all other web components -->
	<bean id="hikariConfig" class="com.zaxxer.hikari.HikariConfig">
		<property name="driverClassName" value="com.mysql.cj.jdbc.Driver"></property> 
		<property name="jdbcUrl" value="jdbc:mysql://localhost/root?serverTimezone=UTC"></property>
		<property name="username" value="username"></property>
		<property name="password" value="password"></property>
	</bean>

	<!-- Hikari -->
	<bean id="dataSource"
		class="com.zaxxer.hikari.HikariDataSource" destroy-method="close">
		<constructor-arg ref="hikariConfig"></constructor-arg>
	</bean>  
~~~

> 테스트 코드를 통해 연결확인
~~~
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("file:src/main/webapp/WEB-INF/spring/root-context.xml")
@Log4j
public class DataSourceTests {
	
	@Setter(onMethod_ = {@Autowired} )
		private DataSource dataSource;
		@Test
		public void testConnection() {
			
			
			try(Connection con = dataSource.getConnection()){
				log.info(con);
				
			} catch(Exception e ) {
				fail(e.getMessage());
			}
		}
}
~~~
  
> JUnit을 통한 실행 결과
<img width="1037" alt="스크린샷 2022-01-05 오후 10 50 18" src="https://user-images.githubusercontent.com/81155572/148228235-e3cadeb6-0311-45b9-8ae3-497122321071.png">

  
