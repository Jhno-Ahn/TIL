### appendTo

- $(A).appendTo(B)
    - A를 B의 뒷 부분에 추가

/

### pependTo

- $(A).prependTo(B)
    - A를 B 앞부분에 추가

### insertAfter

- $(A).insertAfter(B)
    - A를 B의 뒤에 추가
    - appendTo보다 멀음

### insertBefore

- $(A).insertBefore(B)
    - A를 B의 앞에 추가
    - appendTo보다 멀음

### append

- $(A).append(B)
    - B를 A의 뒷부분에 추가

### prepend

- $(A).prepend(B)
    - B를 A의 앞부분에 추가

### after

- $(A).after(B)
    - B를 A의 뒤에 추가

### before

- $(A).before(B)
    - B를 A의 앞에 추가

```jsx
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<h2> append / appendTo </h2>
<script src="/JQueryEx/jquery-3.6.0.js"></script>
<script type="text/javascript">
	// <!--
	$(document).ready(
		function() {
			// DOM
			var dom = document.getElementById( "dom" );
			// var textnode = document.createTextNode( "After" );
			// var spannode = document.createElement( "span" );
			// spannode.appendChild( textnode );
			// dom.appendChild( spannode );
			var afternode = document.createElement( "span" );
			afternode.innerHTML = "<b> After </b>";
			dom.appendChild( afternode );
			
			var beforenode = document.createElement( "span" );
			beforenode.innerHTML = "<b> Before </b>";
			dom.parentNode.insertBefore( beforenode, dom );
						
			// JQuery
			// $(A).Append(B)			B -> A
			$("#append").append("<b> Append </b><br>"); // 대상을 기준으로 뒤에 붙여라
			$("#append").prepend("<b> Prepend </b><br>"); // 대상을 기준으로 앞에 붙여라
			$("#append").before("<b> Before </b><br>"); 
			$("#append").after("<b> After </b><br>");
			
			// $(A).AppendTo(B)			A -> B
			$("<b> AppendTo </b><br>").appendTo("#appendTo"); //대상을 기준으로 앞에 붙여라
			$("<b> PrependTo </b><br>").prependTo("#appendTo"); //대상을 기준으로 뒤에 붙여라
			$("<b> insertBefore <b/><br>").insertBefore("#appendTo"); //prepend보다 멀음 (앞)
			$("<b> insertAfter </b><br>").insertAfter("#appendTo"); //append보다 멀음(뒤)
			
			
			$("<img>").attr(
				{
					"src" : "/JQueryEx/images/a.jpg",
					"width" : "200px",
					"height" : "100px"
				}		
			).appendTo("#img");
			
			$("div:eq(1)").append(
				"<br>",
				$("<img>").attr(
					{
						"src" : "/JQueryEx/images/b.jpg",
						"width" : "200px",
						"height" : "100px"
					}	
				),
				"<br>"
			);
			
			//id값 img인 녀석의 앞에 속성값을 텍스트로 출력
			$("<b></b><br>").text( $("img").first().attr("src")).prependTo("#img");
			
			//prepend
			$("div").eq("1").prepend(
				"<br>",
				$("<b></b>").text(
				$("img").last().attr("src")),
			);
			
			// $(selector).append(function(index) {} )
			var m = [
				{"name" : "홍길동", "age" : 20},
				{"name" : "이순산", "age" : 30},
				{"name" : "김유산", "age" : 40} 
			];
			$("h4").append( //append뒤에는 출력할꺼가 와야함
				function(index){ 
					return m[index].name + " : " + m[index].age;
				}		
			);
			
		}	
	);	
	// -->
</script>
<br>

<h4></h4>
<h4></h4>
<h4></h4>

<br><br>
<div id="img"></div><br>
<div></div>

<div id="dom">
	DOM <hr size="3" color="red">
</div>
<br>

<div id="append">
	Append <hr size="3" color="blue">
</div>
<br>

<div id="appendTo">
	AppendTo <hr size="3" color="green">
</div>
```
