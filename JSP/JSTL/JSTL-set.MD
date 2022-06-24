- 태그를 사용하기 위해서 상단에 링크를 작성
- taglib prefix는 core(c)로 uri는 "http://java.sun.com/jsp/jstl/core"로 작성

```jsx
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
    
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>

<h2> JSTL - core - set / remove </h2>

<%
	int a = 10;
%>

scriptlet : <%out.println(a);%><br>
expression : <%=a%><br>
EL : ${a}<br>
<br>

<!-- c 변수명을 a로, 값을 10으로 설정  -->
<c:set var="a" value="10"/>

<!-- EL태그로 a값 출력 -->
EL : ${a}<br> 

<!-- c:out태그로 a출력 -->
out : <c:out value="a"/><br> 
<!-- c:out태그로 a의 값 출력 -->
out : <c:out value="${a}"/><br> 

<!-- 변수명을 b로, 값을 abc로 설정 -->
<c:set var="b" value="abc"/><br>
<c:set var="b" value="${'abc'}"/><br> <!-- 위랑 동일, 이 방법을 더 많이 사용 -->
<c:set var="b" value='${"abc"}'/><br> <!-- 따옴표 쌍따옴표 안 밖 바꿔줘도 가능 ㅇㅇ
 하지만 안쪽이나 바깥 둘 중 한곳만 주면 안됨. -->
b : ${b}<br>
<br>

<!-- 변수명을 c로 값을 10으로 설정  -->
<c:set var="c">
	10 <br> 
</c:set>

<!-- 변수명을 f로  값을 문자열 ABC로 설정 -->
<c:set var="f">
	${"ABC" }<br> 
</c:set>
f : ${f} <!-- f 출력 (ABC) -->

<%
	int g = 20; /* 변수 g를 20으로 초기화 */
%>
<!-- 변수명 g로, 값은 자바코드에서 설정한 g값(20)으로 설정 -->
<c:set var = "g" value="<%=g%>"/> 
g : ${g}<br> 
<c:remove var="g"/> <!-- g변수 지움 -->
g : ${g}<br>

<!-- Date를 import하여 사용 -->
<jsp:useBean id="h" class="java.util.Date"/>
date : ${h}<br>
<c:set var="i" value="<%=new java.util.Date() %>"/>
date : ${i}<br>
 <!-- Random을 import하여 사용 -->
<c:set var="r" value="<%=new java.util.Random() %>"/>
r : ${r.nextInt(45)+1 }<br>
```
