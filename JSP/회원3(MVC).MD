## 로그인을 하는 loginForm.jsp

- loginForm또한 loginPro.jsp를 통해 구동

```jsx
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<%@ include file="setting.jsp" %>    
<link type="text/css" rel="stylesheet" href="<%=project%>/member/style_member.css">    
<script src="<%=project%>/member/script.js"></script>    

<h2> <%=page_login%> </h2>

<form name="mainform" method="post" action="loginPro.jsp" onsubmit="return maincheck()">
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

## 로그인을 구현하는 loginPro.jsp

- id와, passwd 객체를 만들어 request 요청을 통해 loginForm에서 id와 passwd를 받아온다.
- LogonDBBean 객체를 통해 만들었던 check메소드에 id와 passwd를 매개변수로 받아
- 아이디가 없는경우, 비밀번호가 다른경우, 비밀번호가 같은경우를 나누어 처리

```jsx
<%@page import="member.LogonDBBean"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
    
<%@ include file="setting.jsp" %>    
<script src="<%=project%>/member/script.js"></script>    

<h2> <%=page_login%> </h2>

<% 
	String id = request.getParameter( "id" );
	String passwd = request.getParameter( "passwd" );
%>
<%
	LogonDBBean dao = LogonDBBean.getInstance();
	int result = dao.check( id, passwd );
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
		response.sendRedirect( "main.jsp" );
	}
%>
```

## 로그아웃을 처리하는 logout.jsp

- removeAttribute를 통해 session에서 없애주고
- sendRedirect를 통해 main.jsp로 이동시킨다.

```jsx
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<%@ include file="setting.jsp" %>  
<h2> <%=page_logout%> </h2>

<%
	session.removeAttribute( "memId" );
	response.sendRedirect( "main.jsp" );
%>
```
