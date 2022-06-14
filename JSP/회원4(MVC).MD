## 계정의 정보를 변경하기 위해 정보 입력받는 modifyForm.jsp

- 정보변경 페이지로 가기 위해서 비밀번호를 입력받아야 하는 폼
- onsubmit으로 passwdcheck()함수를 사용해 비밀번호를 확인

```jsx
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<%@ include file="setting.jsp" %>    
<link type="text/css" rel="stylesheet" href="<%=project%>/member/style_member.css">    
<script src="<%=project%>/member/script.js"></script>   

<h2> <%=page_modify%> </h2>

<form name="passwdform" method="post" action="modifyView.jsp" onsubmit="return passwdcheck()">
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
				<input class="inputbutton" type="submit" value="<%=btn_mod%>">
				<input class="inputbutton" type="button" value="<%=btn_mod_cancel%>"
					onclick="location='main.jsp'">
			</th>
		</tr>
	</table>
</form>
```

## 정보를 변경하는 폼인 modifyView.jsp

- 마찬가지로 id와 passwd 객체를 만들어 session과 request를 통해 “memId”와 “passwd”를 얻어와 저장
- LogonDBBean 객체를 만들어 check메서드를 통해 id,passwd를 매개변수로 받아 result에 저장
- result값이 0이면 비밀번호가 다른것이고,  값이 다른 경우에는 비밀번호가 같다.
- 인증이 된 경우에는 변경할 수 있는 폼이 주어진다.
- tel과 email 같은 경우에는 나누어서 입력을 하기 때문에 각각 “-”와 “@”로 구분(split)지어 배열객체로 만들어 입력받게 한다.

```jsx
<%@page import="java.text.SimpleDateFormat"%>
<%@page import="member.LogonDataBean"%>
<%@page import="member.LogonDBBean"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<%@ include file="setting.jsp" %>    
<link type="text/css" rel="stylesheet" href="<%=project%>/member/style_member.css">    
<script src="<%=project%>/member/script.js"></script>   

<h2> <%=page_modify%> </h2>    

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
		LogonDataBean dto = dao.getMember( id );
		%>
		<form name="modifyform" method="post" action="modifyPro.jsp" 
			onsubmit="return modifycheck()">
			<table>
				<tr>
					<th colspan="2"> <%=msg_modify%> </th>
				</tr>
				<tr>
					<th> <%=str_id%> </th>
					<td> &nbsp;<%=dto.getId()%> </td>
				</tr>
				<tr>
					<th rowspan="2"> <%=str_passwd%> </th>
					<td>
						<input class="input" type="password" name="passwd" maxlength="30"
							value="<%=dto.getPasswd()%>">
					</td>
				</tr>
				<tr>
					<td>
						<input class="input" type="password" name="repasswd" maxlength="30"
							value="<%=dto.getPasswd()%>">
					</td>
				</tr>
				<tr>
					<th> <%=str_name%> </th>
					<td> &nbsp;<%=dto.getName()%> </td>
				</tr>
				<tr>
					<th> <%=str_jumin%> </th>
					<td> &nbsp;<%=dto.getJumin1()%> - <%=dto.getJumin2()%> </td>
				</tr>
				<tr>
					<th> <%=str_tel%> </th>
					<td>
						<%
						String tel = dto.getTel();
						if( tel == null || tel.equals( "" ) ) {
							%>
							<input class="input" type="text" name="tel1" maxlength="3"
								style="width:30px">
							- <input class="input" type="text" name="tel2" maxlength="4"
								style="width:40px">
							- <input class="input" type="text" name="tel3" maxlength="4"
								style="width:40px">		
							<%
						} else {
							String t[] = tel.split( "-" );
							%>
							<input class="input" type="text" name="tel1" maxlength="3"
								style="width:30px" value="<%=t[0]%>">
							- <input class="input" type="text" name="tel2" maxlength="4"
								style="width:40px" value="<%=t[1]%>">
							- <input class="input" type="text" name="tel3" maxlength="4"
								style="width:40px" value="<%=t[2]%>">								
							<%							
						}
						%>
					</td>
				</tr>
				<tr>
					<th> <%=str_email%> </th>
					<td>
						<%
						String email = dto.getEmail();
						if( email == null || email.equals( "" ) ) {
							%>
							<input class="input" type="text" name="email1" maxlength="15"
								style="width:100px">
							@
							<input class="input" type="text" name="email2" maxlength="15"
								style="width:100px">	
							<%
						} else {
							String e[] = email.split( "@" );
							%>
							<input class="input" type="text" name="email1" maxlength="15"
								style="width:100px" value="<%=e[0]%>">
							@
							<input class="input" type="text" name="email2" maxlength="15"
								style="width:100px" value="<%=e[1]%>">
							<%						
						}
						%>
					</td>
				</tr>
				<tr>
					<th> <%=str_reg_date%> </th>
					<td>
						<%
						SimpleDateFormat sdf = new SimpleDateFormat( "yyyy-MM-dd HH:mm" );
						%>
						&nbsp;<%=sdf.format( dto.getReg_date() )%>
					</td>
				</tr>
				<tr>
					<th colspan="2">
						<input class="inputbutton" type="submit" value="<%=btn_mod%>">
						<input class="inputbutton" type="reset" value="<%=btn_cancel%>">
						<input class="inputbutton" type="button" value="<%=btn_mod_cancel%>"
							onclick="location='main.jsp'">
					</th>
				</tr>				
			</table>
		</form>
		
		
		<%
	}
%>
```

## 정보수정 로직을 수행하는 modifyPro.jsp

- tel과 email같은 경우는 나누어서 정보를 입력받았기 때문에, 다시 합쳐주는 로직을 구현
- 마지막은 이전과 마찬가지로 LogonDBBean 객체를 만들어 modifyMember 메소드를 통해 dto객체를 매개변수로 받아 result에 저장.
- 값이 0이면 수정실패, 값이 0이 아니라면 정보수정성공하고 main.jsp로 이동

```jsx
<%@page import="member.LogonDBBean"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<%@ include file="setting.jsp" %>    
<script src="<%=project%>/member/script.js"></script>   

<h2> <%=page_modify%> </h2>

<jsp:useBean id="dto" class="member.LogonDataBean"/>
	<jsp:setProperty name="dto" property="*"/>
	<!-- passwd -->
<%
	dto.setId( (String) session.getAttribute( "memId" ) );
%>	
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
	if( ! email1.equals( "" ) && ! email2.equals( "" ) ) {
		email = email1 + "@" + email2;
	}
	dto.setEmail( email );
%>
<%
	LogonDBBean dao = LogonDBBean.getInstance();
	int result = dao.modifyMember( dto );	
	if( result == 0 ) {
		// 수정 실패
		%>
		<script type="text/javascript">
			<!--
			alert( modifyerror );
			//-->
		</script>
		<meta http-equiv="refresh" content="0; url=main.jsp">
		<%
	} else {
		// 수정 성공
		response.sendRedirect( "main.jsp" );
	}
%>
```
