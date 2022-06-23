## EL(Expression Language)

- 값을 표현하는데 사용되는 새로운 스크립트 언어로 JSP 기본 문법을 보완하여 표현식 보다 편리하게 값을 출력할 수 있다.
- null값에 관대하고, 형변환을 자동으로 해준다. Object를 본래 형으로 자동으로 처리해준다.
- 장점
    - 코드가 간결해진다.
    - JSP코드가 제외되어 코드 분석이 보다 쉬워진다.
    - 태그들과의 조화가 쉬워진다.

| 표현 언어 기본 객체 |  설명 |
| --- | --- |
| pageContext | JSP의 page 기본 객체와 동일 |
| pageScope | pageContext 기본 객체에 저장된 속성의 <속성, 값> 매핑을 저장한 Map 객체 |
| requestScope | request.getAttribute().request 기본 객체에 저장된 속성의 <속성, 값> 매핑을 저장한 Map 객체. 유일하게 생략가 |
| sessionScope | session.getAttribute().session 기본 객체에 저장된 <속성, 값> 매핑을 저장한 Map 객체 |
| applicationScope | application.getAttribute().session 기본 객체에 저장된 <속성, 값> 매핑을 저장한 Map 객체 |
| param | request.getParameter(). 요청 파라미터의 <파라미터 이름, 값> 매핑을 저장한 Map 객체 |
| paramValues | request.getParameterValues(). 요청 파라미터의 <파라미터 이름, 값 배열> 매핑을 저장한 Map 객체 |
| header | request.getHeader(). 요청 정보의 <헤더 이름, 값> 매핑을 저장한 Map 객체 |
| cookie | request.getCookies(). <쿠키 이름, Cookie> 매핑을 저장한 Map 객체 |
| initParam | application.getInitParameter(). 초기화 파라미터의 <이름, 값> 매핑을 저장한 Map 객체 |

## JSTL

- JavaServer Pages Standard Tag Library의 줄임알로 JSP 페이지 내에서 자바 코드를 바로 사용하지 않고 로직을 내장하는 효율적인 방법을 제공한다.
- 표준화된 태그셋을 사용하여 자바 코드가 들락거리는 것보다 더 코드의 유지보수를 용이하게 한다.

### JSTL 라이브러리

- 사용하기 위해서는 jstl.jar 와 standard.jar를 추가하고
- core에는 <%@ taglib prefix="c" uri="[http://java.sun.com/jsp/jstl/core](http://java.sun.com/jsp/jstl/core)" %> 를 추가해줘야 한다.

| 라이브러리 | 기능 | 내용 | 주소 |
| --- | --- | --- | --- |
| c | 코어 | 변수지원 흐름제어 URL 처리 | http://java.sun.com/jsp/jstl/core |
| xml | XML | XML코어 흐름 제어 XML변환 | http://java.sun.com/jsp/jstl/xml |
| fmt | 국제화 | 지역 메시지형식 숫자 및 날짜 형식 | http://java.sun.com/jsp/jstl/fmt |
| sql | 데이터베이스 | SQL | http://java.sun.com/jsp/jstl/sql |
| fnc | 함수 | 콜렉션처리 String 처리 | http://java.sun.com/jsp/jstl/functions |

### JSTL core 태그

| 태그명 | 설명 |
| --- | --- |
| <c:set> | 변수명에 값을 할당 |
| <c:out> | 값을 출력 |
| <c:if> | 조건식에 해당하는 블럭과 사용될 scope 설정 |
| <c:choose> | 다른 언어의 switch문과 비슷 |
| <c:when> | switch문의 case에 해당 |
| <c:otherwise> | switch문의 default에 해당 |
| <c:forEach> | 다른 언어의 loop문 items속성에 배열을 할당할 수 있음 |
| <c:remove> | 변수를 지운다 |



## 기존 스크립틀릿 방법과 JSTL 방법의 비교

### 스크립틀릿

- 이 방법을 사용하면 자바 코드를 jsp단에서 사용할수는 있지만, 가독성이 매우 좋지 못하다.

```jsx
<html>
 <body>
  <%
    for (int i = 1; i <= 10; i ++) {
  %>
      <%= i %><br/>
  <%
  }
  %>

  <%= request.getAttribute("person").getAddress().getCity() %>

 </body>
</html>
```

### JSTL

- 이 방법은 java코드 없이, 오직 태그로만 구성되어져있다.
- 가족성이 좋고 협업에 있어서도 군더더기가 없다.
- 또한 서버에서 넘어온 parameter를 꺼내는 방법에서도 훨씬 더 간결하게 사용이 가능하다.

```jsx
<% @taglib uri="http://java.sun.com/jstl/core" prefix="c" %>
<html>
 <body>
  <c:forEach var="i" begin="1" end="10" step="1">
   <c:out value="${i}"/>
   <br/>
  </c:forEach>

  ${person.address.city}

 </body>
</html>
```
