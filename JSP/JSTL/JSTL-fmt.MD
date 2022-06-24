- JSTL 국제화 지역화 태그로 다국어 문서를 처리할 때 유용하고,
날짜와 숫자 형식을 다룰 때 사용된다.

```jsx
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt" %>

<h2> JSTL - fmt </h2>

<fmt:requestEncoding value="utf-8"/>
<form method="post" action="fmt.jsp">
	<table border="1">
		<tr>
			<th> 이름 </th>
			<td> <input type="text" name="name"> </td>
			<th> <input type="submit" value="전송"> </th>
		</tr>
	</table>
</form>    
<br>
이름 : ${param.name} <br>
<br><br>

<c:set var="num" value="${1234.5678}"/>
<fmt:formatNumber value="${num}"/> <br>
<fmt:formatNumber value="${num}" type="number"/> <br> 
<fmt:formatNumber value="${num}" type="percent"/> <br> <!-- 뒤에 퍼센트 표시 -->
<fmt:formatNumber value="${num}" type="currency"/> <br> <!-- 화폐 표시 -->
<fmt:formatNumber value="${num}" type="number" pattern="00,000.0000"/> <br> <!-- 숫자에 패턴 추가 -->
<fmt:formatNumber value="${num}" type="currency" currencySymbol="$"/> <br> <!-- 화폐단위 설정 -->
<br>

<c:set var="now" value="<%=new java.util.Date()%>"/>
<fmt:formatDate value="${now}"/> <br> <!-- 현재 날짜(디폴트) -->
<fmt:formatDate value="${now}" type="time"/> <br> <!-- 현재 시간 -->
<fmt:formatDate value="${now}" type="date"/> <br> <!-- 현재 날짜 -->
<fmt:formatDate value="${now}" type="both"/> <br> <!-- 날짜와 시간 둘 다 표시 -->
<fmt:formatDate value="${now}" type="time" pattern="HH:mm:ss"/> <br> <!-- 시간 표시 패턴 설정 -->
<fmt:formatDate value="${now}" type="date" pattern="yyyy-MM-dd"/> <br> <!-- 날짜 표시 패턴 설정 -->
```
