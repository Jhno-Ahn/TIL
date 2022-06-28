## 배열 관리

- 매개 변수로 입력한 함수 사용
- for in 반복문처럼 객체나 배열의 요소 검사하는 메서드
- each() 메서드 사용
    - 첫 번째 매개 변수 → 배열
    - 두 번째 매개 변수 → index와 item 갖는 콜백 함수
    - Index → 배열의 인덱스 또는 객체의 키 의미
    - item → 해당 인덱스나 키가 가진 값 의미
- each() 메서드의 형태
    1. $.each(object, function(index, item){})
    2. $(selector).each(function(index, item){})

```jsx
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<h2> 반복문 </h2>
<script src="/JQueryEx/jquery-3.6.0.js"></script>
<script type="text/javascript">
	//<!--
	$(document).ready(
		function() {
			var msg = "";
			
			// 배열
			var m = [10, 20, 30, 40, 50];
			for( var i=0; i<m.length; i++ ) {
				msg += m[i] + "&nbsp;";
			}
			msg += "<br>";
			for( var i in m ) {
				msg += m[i] + "&nbsp;";
			}
			msg += "<br>";
			var w = new Array( 10, 20, 30, 40, 50 );
			for( var i in w ) {
				msg += w[i] + "&nbsp;";
			}
			msg += "<br>";
			
			
			//JSON
			var z = [
				{"name" : "홍길동", "age":20},
				{"name" : "김유신", "age":30},
				{"name" : "이순신", "age":40}
			];
			for(var i=0; i<z.length; i++){
				msg += "이름: " + z[i].name +"<br>"
					+ "나이: " + z[i].age +"<br>";
			}
			
			
			
			
			
			// $.each( object, function( index, item ) {} )
			// 배열이 있을때 매개변수로 
			$.each(
				m, //object
				function(index, item){
				//	msg += index + " : " + item +"<br>";
				//	mgs += item + "<br>";
				//	msg += m[index] + "<br>";
					msg += this + "<br>"; //this == item 중요!
					
				}
			);
			msg + "<br>";
			
			$.each(
				z,
				function(index, item) {
					//msg += z[index].name + " : " + z[index].age	 + "<br>";
					//msg += item.name + " : " + item.age + "<br>";
					msg += this.name + " : " + this.age + "<br>";
				}
			);
			
			msg + "<br>";
			
			// $(selector).each( function( index, item ) {} )
			var colors = ["red", "blue", "green", "yellow"];
			$("h4").each(
				function(index, item){
					//msg += index + " : " + $(item).text() + "<br>";
					//msg += index + " : " + $(this).text() + "<br>";
					//if( index % 2 == 0 ) $(item).css("color", "red");
					$(this).css("color",colors[index]);
				}		
			);
			
			
			$("#result").html( msg );
		}		
	);
	//-->
</script>
<h4> 축구 </h4>
<h4> 야구 </h4>
<h4> 농구 </h4>
<h4> 배구 </h4>
<br>
<div id="result"></div>
```
