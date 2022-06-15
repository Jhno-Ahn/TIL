## 회원가입을 하는 inputForm.jsp

```jsx
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<%@ include file="setting.jsp" %>    
<link type="text/css" rel="stylesheet" href="<%=project%>/member/style_member.css">    
<script src="<%=project%>/member/script.js"></script>

<h2> <%=page_input%> </h2>

<form name="inputform" method="post" action="inputPro.jsp" onsubmit="return inputcheck()">
	<input type="hidden" name="check" value="0">
	<table border="1">
		<tr>
			<th colspan="2"> <%=msg_input%> </th>
		</tr>		
		<tr>
			<th> <%=str_id%> </th>
			<td> 
				<input class="input" type="text" name="id" maxlength="30" autofocus>
				<input class="inputbutton" type="button" value="<%=btn_confirm%>"
					onclick="confirm()"> 
			</td>
		</tr>
		<tr>
			<th rowspan="2"> <%=str_passwd%> </th>
			<td> <input class="input" type="password" name="passwd" maxlength="30"> </td>
		</tr>
		<tr>
			<td> <input class="input" type="password" name="repasswd" maxlength="30"> </td>
		</tr>
		<tr>
			<th> <%=str_name%> </th>
			<td> <input class="input" type="text" name="name" maxlength="30"> </td>
		</tr>
		<tr>
			<th> <%=str_jumin%> </th>
			<td> 
				<input class="input" type="text" name="jumin1" maxlength="6" style="width:50px;"
					onkeyup="nextjumin1()">
				- <input class="input" type="text" name="jumin2" maxlength="7" style="width:60px;"
					onkeyup="nextjumin2()">	
			</td>	
		</tr>
		<tr>
			<th> <%=str_tel%> </th>
			<td>
				<input class="input" type="text" name="tel1" maxlength="3" style="width:30px;"
					onkeyup="nexttel1()">
				- <input class="input" type="text" name="tel2" maxlength="4" style="width:40px;"
					onkeyup="nexttel2()">
				- <input class="input" type="text" name="tel3" maxlength="4" style="width:40px;"
					onkeyup="nexttel3()">
			</td>
		</tr>
		<tr>
			<th> <%=str_email%> </th>
			<td>
				<input class="input" type="text" name="email1" maxlength="15" style="width:100px;">
				@
				<select name="email2">
					<option value="0"> 직접입력 </option>
					<option value="daum.net"> 다음 </option>
					<option value="naver.com"> 네이버 </option>
					<option value="gmail.com"> 구글 </option>
					<option value="nate.com"> 네이트 </option>
				</select>
			</td>
		</tr>
		<tr>
			<th colspan="2">	
				<input class="inputbutton" type="submit" value="<%=btn_input%>">
				<input class="inputbutton" type="reset" value="<%=btn_cancel%>">
				<input class="inputbutton" type="button" value="<%=btn_input_cancel%>"
					onclick="location='main.jsp'">
			</th>
		</tr>
	</table>
</form>
```

## 회원가입폼의 로직을 실현하는 inputPro.jsp

- 자바빈 useBean을 이용하여 dto객체를 만든다. class는 member의 LogonDataBean을 받아온다.
- 이름은 dto로 설정하고 모든 객체를 이용할 수 있게 한다.
- tel은 모든 칸에 값이 있을 경우에는 “-”로 이어지게 만드는 로직 구현
- email은 직접입력, 선택입력으로 나누어 직접입력일 경우에는 email1만 작성, 선택입력일 경우에는 email1에 @와 email2 합치게 한다.
- 마지막단은 LogonDBBean 객체를 만들어서 만들어뒀던 insertMember메소드를 통해 계정을 생성한다.

```jsx
<%@page import="member.LogonDBBean"%>
<%@page import="java.sql.Timestamp"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<%@ include file="setting.jsp" %>    
<script src="<%=project%>/member/script.js"></script>

<h2> <%=page_input%> </h2>

<%
	request.setCharacterEncoding( "utf-8" );
%>
<jsp:useBean id="dto" class="member.LogonDataBean"/>
	<jsp:setProperty name="dto" property="*"/>
	<!-- id passwd name jumin1 jumin2 -->
	
<%
	String tel = null;
	String tel1 = request.getParameter( "tel1" );
	String tel2 = request.getParameter( "tel2" );
	String tel3 = request.getParameter( "tel3" );
	if( ! tel1.equals( "" ) && ! tel2.equals( "" ) && ! tel3.equals( "" ) ) {
		tel = tel1 + "-" + tel2 + "-" + tel3;
	}
	dto.setTel( tel );
%>	
<%
	String email = null;
	String email1 = request.getParameter( "email1" );
	String email2 = request.getParameter( "email2" );
	if( ! email1.equals( "" ) ) {
		if( email2.equals( "0" ) ) {
			// 직접입력
			email = email1;
		} else {
			// 선택입력
			email = email1 + "@" + email2;
		}
	}
	dto.setEmail( email );
%>	
<%
	dto.setReg_date( new Timestamp( System.currentTimeMillis() ) );
%>
<%
	LogonDBBean dao = LogonDBBean.getInstance();
	int result = dao.insertMember( dto );
	if( result == 0 ) {
		%>
		<script type="text/javascript">
			<!--
			erroralert( inputerror );
			//-->
		</script>
		<%
	} else {
		response.sendRedirect( "loginForm.jsp" );
	}
%>
```

## 회원가입시 중복체크를 위한 confirm.jsp

- 기존에 만들었던 check 메소드를 통해 확인
- LogonDBBean 객체를 만들어서, check메소드에 id값을 매개변수로 받아 정보를 확인
- result값이 0이면 아이디가 없는 것이므로 아이디 생성가능 창이, 값이 0이 아니면 아이디 값이 존재하는 것이니 다시한번 아이디를 입력받는 폼을 생성

```jsx
<%@page import="member.LogonDBBean"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<%@ include file="setting.jsp" %>    
<link type="text/css" rel="stylesheet" href="<%=project%>/member/style_member.css">    
<script src="<%=project%>/member/script.js"></script>

<h2> <%=page_confirm%> </h2>

<%
	String id = request.getParameter( "id" );
%>
<%
	LogonDBBean dao = LogonDBBean.getInstance();
	int result = dao.check( id );
	if( result == 0 ) {
		// 아이디가 없다
		%>
		<table border="1">
			<tr>
				<th style="width:300px;"> <span><%=id%></span><%=msg_confirm_o%>
			</tr>
			<tr>
				<th> 
					<input class="inputbutton" type="button" value="<%=btn_ok%>"
						onclick="setid( '<%=id%>' )"> 
				</th>
			</tr>		
		</table>
		<%
	} else {
		// 아이디가 있다
		%>
		<form method="post" name="confirmform" action="confirm.jsp" 
			onsubmit="return confirmcheck()">
			<table border="1">
				<tr>
					<th colspan="2"> <span><%=id%></span><%=msg_confirm_x%> </th>
				</tr>
				<tr>
					<th> <%=str_id%> </th>
					<td> <input class="input" type="text" name="id" autofocus> </td>
				</tr>
				<tr>
					<th colspan="2">
						<input class="inputbutton" type="submit" value="<%=btn_ok%>">
						<input class="inputbutton" type="button" value="<%=btn_cancel%>"
							onclick="window.close()">
					</th>
				</tr>
			</table>
		</form>
		<%
	}
%>
```
