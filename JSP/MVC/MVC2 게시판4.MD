## 업데이트

### 업데이트 view 담당하는 modifyForm.jsp, modifyView.jsp, modifyPro.jsp

```jsx
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<%@ include file="setting.jsp" %>    
<link type="text/css" rel="stylesheet" href="<%=project%>/member/style_member.css">    
<script src="<%=project%>/member/script.js"></script>   

<h2> <%=page_modify%> </h2>

<form name="passwdform" method="post" action="modifyView.do" onsubmit="return passwdcheck()">
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
					onclick="location='main.do'">
			</th>
		</tr>
	</table>
</form>
```

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
	int result = (Integer) request.getAttribute( "result" );
%>
<%
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
		LogonDataBean dto = (LogonDataBean) request.getAttribute( "dto" );
		%>
		<form name="modifyform" method="post" action="modifyPro.do" 
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
							onclick="location='main.do'">
					</th>
				</tr>				
			</table>
		</form>
		
		
		<%
	}
%>
```

```jsx
<%@page import="member.LogonDBBean"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<%@ include file="setting.jsp" %>    
<script src="<%=project%>/member/script.js"></script>   

<h2> <%=page_modify%> </h2>

<%
	int result = (Integer) request.getAttribute( "result" );
%>
<%
	if( result == 0 ) {
		// 수정 실패
		%>
		<script type="text/javascript">
			<!--
			alert( modifyerror );
			//-->
		</script>
		<meta http-equiv="refresh" content="0; url=main.do">
		<%
	} else {
		// 수정 성공
		response.sendRedirect( "main.do" );
	}
%>
```

## ModifyFormHandler, ModifyProHandler, ModifyViewHandler

```java
package handler;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class ModifyFormHandler implements CommandHandler {
	@Override
	public String process(HttpServletRequest request, HttpServletResponse reponse) throws Throwable {
	
		return "/member/modifyForm.jsp";
	}
}
```

```java
package handler;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import member.LogonDBBean;
import member.LogonDataBean;

public class ModifyProHandler implements CommandHandler {
	@Override
	public String process(HttpServletRequest request, HttpServletResponse reponse) throws Throwable {
		
		LogonDataBean dto = new LogonDataBean();
		dto.setPasswd( request.getParameter( "passwd" ) );
		
		dto.setId( (String) request.getSession().getAttribute( "memId" ) );
	
		String tel = null;
		String tel1 = request.getParameter( "tel1" );
		String tel2 = request.getParameter( "tel2" );
		String tel3 = request.getParameter( "tel3" );
		if( ! tel1.equals( "" ) && ! tel2.equals( "" ) && ! tel3.equals( "" ) ) {
			tel = tel1 + "-" + tel2 + "-" + tel3;
		}
		dto.setTel( tel );
	
		String email = null;
		String email1 = request.getParameter( "email1" );
		String email2 = request.getParameter( "email2" );
		if( ! email1.equals( "" ) && ! email2.equals( "" ) ) {
			email = email1 + "@" + email2;
		}
		dto.setEmail( email );
	
		LogonDBBean dao = LogonDBBean.getInstance();
		int result = dao.modifyMember( dto );
		
		request.setAttribute( "result", result );
		
		return "/member/modifyPro.jsp";
	}
}
```

```java
package handler;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import member.LogonDBBean;
import member.LogonDataBean;

public class ModifyViewHandler implements CommandHandler {
	@Override
	public String process(HttpServletRequest request, HttpServletResponse reponse) throws Throwable {

		String id = (String) request.getSession().getAttribute( "memId" );
		String passwd = request.getParameter( "passwd" );	

		LogonDBBean dao = LogonDBBean.getInstance();
		int result = dao.check( id, passwd );
			
		request.setAttribute( "result", result );
		
		if( result != 0 ) {
			LogonDataBean dto = dao.getMember( id );
			request.setAttribute( "dto", dto );
		}
		
		return "/member/modifyView.jsp";
	}
}
```
