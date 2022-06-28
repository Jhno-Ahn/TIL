# JQuery

- DOM과 관련된 처리 쉽게 구현
- 일관된 이벤트 연결 쉽게 구현
- 시각적 효과 쉽게 구현
- Ajax 애플리케이션 쉽게 개발

## JQuery 사용의 장점

- 웹 표준만으로도 플래시와 실버라이트로 구현한 웹 사이트와 비슷한 수준의 시각적 효과 구현
- 아이폰, 아이패드 같은 장치에서도 작동
- 브라우저마다 다른 이벤트 처리의 차이를 해결

## JQuery 사용 세팅

- 링크를 통해 제이쿼리 다운로드 [https://jquery.com/](https://jquery.com/)
    - 다운받은 파일을 프로젝트에 넣고
- 스크립트 소스를 추가해야만 사용 가능
    - ex ) <script src="/JQueryEx/jquery-3.6.0.js"></script>

## JQuery 실행

- jQuery(document).ready()
    - 문서 준비가 완료되면 매개변수로 전달된 함수를 실행하라는 의미
    - jQuery 이벤트 메서드 중 하나

```jsx
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<h2> JQuery </h2>

<script src="/JQueryEx/jquery-3.6.0.js"></script>
<script type="text/javascript">
	// <!--
	function show() {
		var result = document.getElementById( "result" );
		result.innerHTML = "onload<br>";		
	}

	window.onload = function() {
		var result = document.getElementById( "result" );
		result.innerHTML = "onload<br>";
	}
	
	//문서 준비가 완료되면 매개변수로 전달된 함수를 실행
	jQuery(document).ready(
		function() {
			var result = document.getElementById( "result" );
			result.innerHTML = "onload<br>";
		}		
	);
	
	//alert를 통해 알림창 띄움
	$(document).ready(
		function() {
			alert( "onload" );
		}		
	);

	//-->
</script>

<!-- 
<body onload="show()">
-->
<body>
	<div id="result"></div>
</body>
```
