## 회원탈퇴 폼

```jsx
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
    
<%@ include file="setting.jsp" %>    
<link type="text/css" rel="stylesheet" href="<%=project%>/member/style_member.css">    
<script src="<%=project%>/member/script.js"></script>   

<h2> <%=page_delete%> </h2>

<form method="post" name="passwdform" action="deletePro.jsp" onsubmit="return passwdcheck()">
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
					onclick="location='main.jsp'">		
			</th>
		</tr>
	</table>
</form>
```

## 회원탈퇴 폼

```jsx
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
    
<%@ include file="setting.jsp" %>    
<link type="text/css" rel="stylesheet" href="<%=project%>/member/style_member.css">    
<script src="<%=project%>/member/script.js"></script>   

<h2> <%=page_delete%> </h2>

<form method="post" name="passwdform" action="deletePro.jsp" onsubmit="return passwdcheck()">
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
					onclick="location='main.jsp'">		
			</th>
		</tr>
	</table>
</form>
```

## 회원가입폼의 로직을 구현하는 deletePro.jsp

- id와 passwd 변수를 만들어 session과 request를 통해 memId와 passwd를 저장
- LogonDBBean 객체를 만들어 check메소드에 id값과 passwd를 매개변수로 받아 result에 저장
- 값이 0이라면 비밀번호가 다른것, 0이 아니면 정보가 같기 때문에 deleteMember메소드 실행

```jsx
<%@page import="member.LogonDBBean"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
    
<%@ include file="setting.jsp" %>    
<script src="<%=project%>/member/script.js"></script>   

<h2> <%=page_delete%> </h2>

<%
	String id = (String) session.getAttribute( "memId" );
	String passwd = request.getParameter( "passwd" );
%>
<%
	LogonDBBean dao = LogonDBBean.getInstance();
	int result = dao.check( id, passwd );
	if( result == 0 ) {
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
		result = dao.deleteMember( id );
		if( result == 0 ) {
			// 탈퇴 실패
			%>
			<script type="text/javascript">
				<!--
				alert( deleteerror );
				//-->
			</script>
			<meta http-equiv="refresh" content="0; url=main.jsp">
			<%
		} else {
			// 탈퇴 성공
			session.removeAttribute( "memId" );
			response.sendRedirect( "main.jsp" );
		}
	}
%>
```
