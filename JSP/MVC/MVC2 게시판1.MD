## 매핑을 위한 web.xml

- 서블릿과, 서블릿 매핑은 Controller로 설정
- 서블릿 클래스는 control 패키지의 Cotroller 클래스 → control.Controller
- init-param의 name 은 configFile로, value값은 WEB-INF폴더의 handler.properties파일로 설정
- 서블릿매핑의 urt-pattern은 *.do로 설정해 .do로 되어 있는것은 모두 사용

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
xmlns="http://xmlns.jcp.org/xml/ns/javaee"
 xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee 
http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  <display-name>MemberEx</display-name>
  <welcome-file-list>
    <welcome-file>index.html</welcome-file>
    <welcome-file>index.htm</welcome-file>
    <welcome-file>index.jsp</welcome-file>
    <welcome-file>default.html</welcome-file>
    <welcome-file>default.htm</welcome-file>
    <welcome-file>default.jsp</welcome-file>
  </welcome-file-list>
  
	<servlet>
		<servlet-name>Controller</servlet-name>
		<servlet-class>control.Controller</servlet-class>
		<init-param>
			<param-name>configFile</param-name>
			<param-value>WEB-INF/handler.properties</param-value>
		</init-param>
	</servlet>
	<servlet-mapping>
		<servlet-name>Controller</servlet-name>
		<url-pattern>*.do</url-pattern>
	</servlet-mapping>
	  
</web-app>
```

## 핸들러를 사용해 컨트롤러 조회를 위한 handler.properties

- *.do라는 요청이 들어오면 각각에 맞는 컨트롤러를 조회한다.
- ex) [main.do](http://main.do) 요청이 들어오면, handler패키지의 MainHandler 클래스를 조회한다

```java
# handler.properties
/main.do=handler.MainHandler
/loginForm.do=handler.LoginFormHandler
/loginPro.do=handler.LoginProHandler
/logout.do=handler.LogoutHandler
/deleteForm.do=handler.DeleteFormHandler
/deletePro.do=handler.DeleteProHandler
/modifyForm.do=handler.ModifyFormHandler
/modifyView.do=handler.ModifyViewHandler
/modifyPro.do=handler.ModifyProHandler
/inputForm.do=handler.InputFormHandler
/inputPro.do=handler.InputProHandler
/confirm.do=handler.ConfirmHandler
```

## 인터페이스 CommanHandler.java

- 다른 핸들러들을 사용하기 위한 인터페이스

```java
package handler;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public interface CommandHandler {
	public String process( HttpServletRequest request, HttpServletResponse reponse )
		throws Throwable;
}
```

## 컨트롤러 Controller.java

```java
package control;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.util.HashMap;
import java.util.Iterator;
import java.util.Map;
import java.util.Properties;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletConfig;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import handler.CommandHandler;
import handler.DefaultHandler;

//HttpServlet을 상속받는다.
public class Controller extends HttpServlet {
	
	//Map을 통해 String과 CommandHandler를 담는다.
	private Map<String, CommandHandler> handlerMap 
		= new HashMap<String, CommandHandler> ();

	//ServletConfig을 매개변수로 받는 init 메소드
	public void init( ServletConfig config ) throws ServletException {
		String configFile = config.getInitParameter( "configFile" );
		String path = config.getServletContext().getRealPath( "/" );
		String filename = path + "/" + configFile;
		Properties prop = new Properties();
		FileInputStream fis = null;
		
		try {
			fis = new FileInputStream( filename );
			prop.load( fis );
			Iterator<Object> keys = prop.keySet().iterator();
			while( keys.hasNext() ) {
				String command = (String) keys.next();
				String handlerName = prop.getProperty( command );
				Class<?> handlerClass = Class.forName( handlerName );
				CommandHandler handler = (CommandHandler) handlerClass.newInstance();
				handlerMap.put( command, handler );
			}			
		} catch( FileNotFoundException e ) {
			e.printStackTrace();
		} catch( IOException e ) {
			e.printStackTrace();
		} catch( ClassNotFoundException e ) {
			e.printStackTrace();
		} catch( IllegalAccessException  e ) {
			e.printStackTrace();
		} catch( InstantiationException e ) {
			e.printStackTrace();
		}		
	}	

	public void doProcess( HttpServletRequest request, HttpServletResponse response ) 
		throws ServletException, IOException {
		
		String command = request.getRequestURI();
		if( command.indexOf( request.getContextPath() ) == 0 ) {
			command = command.substring( request.getContextPath().length() );
		}
		
		CommandHandler handler = handlerMap.get( command );
		if( handler == null ) {
			handler = new DefaultHandler();
		}
		String viewPage = null;
		
		try {
			viewPage = handler.process( request, response );
		} catch( Throwable e ) {
			e.printStackTrace();
		}
		
		RequestDispatcher dispatcher = request.getRequestDispatcher( viewPage );
		dispatcher.forward( request, response );		
	}	

	public void doGet( HttpServletRequest request, HttpServletResponse response )
		throws ServletException, IOException {
		doProcess( request, response );
	}

	public void doPost( HttpServletRequest request, HttpServletResponse response ) 
		throws ServletException, IOException {
		doProcess( request, response );
	}
	
} // class
```
