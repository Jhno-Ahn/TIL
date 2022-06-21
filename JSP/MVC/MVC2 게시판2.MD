## 메인페이지

### 메인페이지 뷰를 담당하는 main.jsp

- model1과 비교했을때, java코드들이 들어가는 부분들이 빠졌다.
- 제일 중요한 부분은 input폼에서 onclick했을때 loaction부분이 .jsp가 아니라 .do로 바뀐것을 확인할 수 있다.

```jsx
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
    
<%@ include file="setting.jsp" %>    
<link type="text/css" rel="stylesheet" href="<%=project%>/member/style_member.css">    
<script src="<%=project%>/member/script.js"></script>

<h2> <%=page_main%> </h2>

<%
	if( session.getAttribute( "memId" ) != null ) {
		// 로그인 된 상태
		%>
		<table>
			<tr>
				<th style="width:300px;"> <span><%=session.getAttribute( "memId" )%></span><%=msg_welcome%> 
			</tr>
			<tr>
				<th>
					<input class="inputbutton" type="button" value="<%=btn_modify%>"
						onclick="location='modifyForm.do'">
					<input class="inputbutton" type="button" value="<%=btn_delete%>"
						onclick="location='deleteForm.do'">
					<input class="inputbutton" type="button" value="<%=btn_logout%>"
						onclick="location='logout.do'">					
				</th>
			</tr>		
		</table>		
		<%
	} else {
		// 로그인 안 된 상태
		%>
		<form name="mainform" method="post" action="loginPro.do" onsubmit="return maincheck()">
			<table border="1">
				<tr>
					<th colspan="2">
						<%=msg_main%>
					</th>
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
						<input class="inputbutton" type="button" value="<%=btn_input%>"
							onclick="location='inputForm.do'">
					</th>
				</tr>
			</table>
		</form>
		<%		
	}
%>
```

### MainHandler.java

- model1이랑 비교했을때 기존에 jsp파일에 있던 자바 코드들이 Handler로 넘어왔다.
- 기존에 onclick을 통해 .jsp파일로 이동하는 방식에서 handler에서 처리한다.

```jsx
package handler;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class MainHandler implements CommandHandler {
	@Override
	public String process(HttpServletRequest request, HttpServletResponse reponse) throws Throwable {
				
		return "/member/main.jsp";
	}	
}
```

## 회원가입(input)

### 회원가입 view를 담당하는 inputForm.jsp 와 inputPro.jsp

- main과 마찬가지로 .jsp에서 .do로 변경

```jsx
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<%@ include file="setting.jsp" %>    
<link type="text/css" rel="stylesheet" href="<%=project%>/member/style_member.css">    
<script src="<%=project%>/member/script.js"></script>

<h2> <%=page_input%> </h2>

<form name="inputform" method="post" action="inputPro.do" onsubmit="return inputcheck()">
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
					onclick="location='main.do'">
			</th>
		</tr>
	</table>
</form>
```

```jsx
<%@page import="member.LogonDBBean"%>
<%@page import="java.sql.Timestamp"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<%@ include file="setting.jsp" %>    
<script src="<%=project%>/member/script.js"></script>

<h2> <%=page_input%> </h2>

<%
	int result = (Integer)request.getAttribute("result");
%>

<%
	if( result == 0 ) {
		%>
		<script type="text/javascript">
			<!--
			erroralert( inputerror );
			//-->
		</script>
		<%
	} else {
		response.sendRedirect( "loginForm.do" ); //.jsp에서 .do로 바뀐것을 확인
	}
%>
```

## 핸들러 InputFormHandler.java 와 InputProHandler.java

- 마찬가지로 기존에 있던 java코드들이 이쪽으로 넘어왔다.
- request요청을 통해 jsp단 경로로 리턴해준다.

```java
package handler;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class InputFormHandler implements CommandHandler {
	@Override
	public String process(HttpServletRequest request, HttpServletResponse reponse) throws Throwable {

		return "/member/inputForm.jsp";
	}
}
```

```java
package handler;

import java.sql.Timestamp;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import member.LogonDBBean;
import member.LogonDataBean;

public class InputProHandler implements CommandHandler {
	@Override
	public String process(HttpServletRequest request, HttpServletResponse reponse) throws Throwable {
		
		
		request.setCharacterEncoding( "utf-8" );
	
		LogonDataBean dto = new LogonDataBean();
		dto.setId(request.getParameter("id"));
		dto.setPasswd(request.getParameter("passwd"));
		dto.setName(request.getParameter("name"));
		dto.setJumin1(request.getParameter("jumin1"));
		dto.setJumin2(request.getParameter("jumin2"));
	
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
	
		dto.setReg_date( new Timestamp( System.currentTimeMillis() ) );
	
		LogonDBBean dao = LogonDBBean.getInstance();
		int result = dao.insertMember( dto );
		
		request.setAttribute("result", result);
		return "/member/inputPro.jsp";
	}

}
```
