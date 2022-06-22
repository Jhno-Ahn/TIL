## 로그인

### 로그인 view를 담당하는 loginForm.jsp, loginPro.jsp

```jsx
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<%@ include file="setting.jsp" %>    
<link type="text/css" rel="stylesheet" href="<%=project%>/member/style_member.css">    
<script src="<%=project%>/member/script.js"></script>    

<h2> <%=page_login%> </h2>

<form name="mainform" method="post" action="loginPro.do" onsubmit="return maincheck()">
	<table>
		<tr>
			<th colspan="2"> <%=msg_login%> </th>
		</tr>
		<tr>
			<th> <%=str_id%> </th>
			<td> <input class="input" type="text" name="id" maxlength="30" autofocus> </td>
		</tr>	
		<tr>
			<th> <%=str_passwd%> </th>
			<td> <input class="input" type="password" name="passwd" maxlength="30"> </td>
		</tr>
		<tr>
			<th colspan="2">
				<input class="inputbutton" type="submit" value="<%=btn_login%>">
				<input class="inputbutton" type="reset" value="<%=btn_cancel%>">
			</th>
		</tr>
	</table>
</form>
```

```jsx
<%@page import="member.LogonDBBean"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
    
<%@ include file="setting.jsp" %>    
<script src="<%=project%>/member/script.js"></script>    

<h2> <%=page_login%> </h2>

<%
	int result = (Integer) request.getAttribute( "result" );
	String id = (String) request.getAttribute( "id" );
%>

<%
	if( result == -1 ) {
		// 아이디가 없다
		%>
		<script type="text/javascript">
			<!--
			erroralert( iderror )
			//-->
		</script>
		<%
	} else if( result == 0 ) {
		// 비밀번호가 다르다
		%>
		<script type="text/javascript">
			<!--
			erroralert( passwderror )
			//-->
		</script>		
		<%
	} else {
		// 비밀번호가 같다
		session.setAttribute( "memId", id );
		response.sendRedirect( "main.do" );
	}
%>
```

### 로그인 Java단을 담당하는 LoginFormHandler, LoginProHandler

- 다른 Formhandler와 마찬가지로 member의 .jsp파일을 리턴한다.

```java
package handler;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class LoginFormHandler implements CommandHandler {
	@Override
	public String process(HttpServletRequest request, HttpServletResponse reponse) throws Throwable {
		return "/member/loginForm.jsp";
	}
}
```

```java
package handler;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import member.LogonDBBean;

public class LoginProHandler implements CommandHandler {
	@Override
	public String process(HttpServletRequest request, HttpServletResponse reponse) throws Throwable {
		
		//id와 passwd객체 request.getParameter를 통해 생성
		String id = request.getParameter( "id" );
		String passwd = request.getParameter( "passwd" );
		
		//LogonDBBean 연결하여 객체 생성 후 check메소드를 사용해 result에 값 저장 
		LogonDBBean dao = LogonDBBean.getInstance();
		int result = dao.check( id, passwd );
		
		request.setAttribute( "result", result );
		request.setAttribute( "id", id );
		
		return "/member/loginPro.jsp";
	}
}
```

## 회원탈퇴

### 탈퇴 view를 당하는 deleteForm.jsp, deletePro.jsp

```java
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
    
<%@ include file="setting.jsp" %>    
<link type="text/css" rel="stylesheet" href="<%=project%>/member/style_member.css">    
<script src="<%=project%>/member/script.js"></script>   

<h2> <%=page_delete%> </h2>

<form method="post" name="passwdform" action="deletePro.do" onsubmit="return passwdcheck()">
	<table>
		<tr>
			<th colspan="2"> <%=msg_passwd%> </th>
		</tr>
		<tr>
			<th> <%=str_passwd%> </th>
			<td> <input class="input" type="password" name="passwd" maxlength="30" autofocus> </td>
		</tr>		 
		<tr>
			<th colspan="2">
				<input class="inputbutton" type="submit" value="<%=btn_del%>">		
				<input class="inputbutton" type="button" value="<%=btn_del_cancel%>"
					onclick="location='main.do'">		
			</th>
		</tr>
	</table>
</form>
```

```java
<%@page import="member.LogonDBBean"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
    
<%@ include file="setting.jsp" %>    
<script src="<%=project%>/member/script.js"></script>   

<h2> <%=page_delete%> </h2>

<%
	int resultCheck = (Integer) request.getAttribute( "resultCheck" );
%>
<%
	if( resultCheck == 0 ) {
		// 비밀번호가 다르다
		%>
		<script type="text/javascript">
			<!--
			erroralert( passwderror );
			//-->
		</script>
		<%
	} else {
		// 비밀번호가 같다
		int result = (Integer) request.getAttribute( "result" );
		if( result == 0 ) {
			// 탈퇴 실패
			%>
			<script type="text/javascript">
				<!--
				alert( deleteerror );
				//-->
			</script>
			<meta http-equiv="refresh" content="0; url=main.do">
			<%
		} else {
			// 탈퇴 성공
			session.removeAttribute( "memId" );
			response.sendRedirect( "main.do" );
		}
	}
%>
```

### 회원탈퇴 java단을 담당하는 DeleteFormHandler.java , DeleteProHandler.java

```java
package handler;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class DeleteFormHandler implements CommandHandler {
	@Override
	public String process(HttpServletRequest request, HttpServletResponse reponse) throws Throwable {
	
		return "/member/deleteForm.jsp";
	}
}
```

```java
package handler;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import member.LogonDBBean;

public class DeleteProHandler implements CommandHandler {
	@Override
	public String process(HttpServletRequest request, HttpServletResponse reponse) throws Throwable {
	
		String id = (String) request.getSession().getAttribute( "memId" );
		String passwd = request.getParameter( "passwd" );

		LogonDBBean dao = LogonDBBean.getInstance();
		int resultCheck = dao.check( id, passwd );
		
		request.setAttribute( "resultCheck", resultCheck );
		
		if( resultCheck != 0 ) {
			int result = dao.deleteMember( id );
			request.setAttribute( "result", result );
		}
		
		return "/member/deletePro.jsp";
	}
}
```
