## find() - xml

- 문서 객체에서 특정 태그를 선택하는 방법
- XML 문서에서 데이터를 추출 많이 사용

## parseXML()

- parseXML() 메서드를 사용해 문자열을 XML 문서 객체로 변경
- XML을 바로 사용하는 것도 가능하지만 익스플로러에서는 문제가 발생할 수도 있다.

```jsx
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<h2> find - XML </h2>
<script src="/JQueryEx/jquery-3.6.0.js"></script>
<script type="text/javascript">
	//<!--
	var xml = "<books>"
			+ 	"<book>"
			+		"<title>Java 프로그래밍</title>"
			+		"<author>홍길동</author>"
			+		"<price>20,000</price>"
			+ 	"</book>"
			+ 	"<book>"
			+		"<title>JSP 웹프로그래밍</title>"
			+		"<author>이순신</author>"
			+		"<price>30,000</price>"
			+ 	"</book>"
			+ 	"<book>"
			+		"<title>Spring 프레임워크</title>"
			+		"<author>김유신</author>"
			+		"<price>40,000</price>"
			+ 	"</book>"
			+ "</books>";
			
	
	$(document).ready( // == window.onload (현재 문서 준비됐으면 시작해라)
		function(){
			var xmldoc = $.parseXML(xml);
			var msg = "";
			
			// DOM
			var booklist = xmldoc.getElementsByTagName("book");
			var titlelist = xmldoc.getElementsByTagName("title");
			var authorlist = xmldoc.getElementsByTagName("author");
			var pricelist = xmldoc.getElementsByTagName("price");
			for(var i=0; i<booklist.length; i++){
				msg += "제목 : " + titlelist.item(i).firstChild.nodeValue + "<br>" //배열이 아니기 때문에 item 함수 사용
					+ "저자 : " + authorlist.item(i).firstChild.nodeValue + "<br>"
					+ "가격 : " + pricelist.item(i).firstChild.nodeValue + "<br><br>";
			}
			
			//JQuery
			$(xmldoc).find("book").each(	//book 태그 찾아서  each로 반복문 실행
				function(index, item){		//index는 book태그(0,1,2) , item은 title,author,price
					msg += "제목 : " + $(item).find("title").text() + "<br>" //text함수 사용해서 변환해줘야 정상출력
						+ "저자 : " + $(item).find("author").text() + "<br>"
						+ "가격 : " + $(item).find("price").text() + "<br><br>";
				}		
			);
			
			
			$("#result").html(msg);
		}		
	);
	
	
	//-->
</script>
<br>
<div id="result"></div>
```

## find() - JSON

```jsx
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<h2> find - JSON </h2>
<script src = "/JQueryEx/jquery-3.6.0.js"></script>
<script type="text/javascript">
	//<!--
	var xml = "<books>"
			+	"<![CDATA["
			+ 		"{"
       		+			"book : ["
       		+				"{"
       		+					"title : 'Java Programming',"
       		+					"author : '홍길동',"
       		+					"price : '25,000'"
       		+				"},"
       		+				"{"
       		+					"title : 'JSP Web Programming',"
       		+					"author : '이순신',"
       		+					"price : '35,000'"
       		+				"},"
       		+				"{"
       		+					"title : 'Spring FrameWork',"
       		+					"author : '김유신',"
       		+					"price : '45,000'"
       		+				"},"
       		+			"]"
			+		"}"
			+	"]]>" //안에가 데이터다
			+ "</books>";
	
	$(document).ready(
		function(){
			var msg ="";
			var xmldoc = $.parseXML(xml);
			
			//DOM
			var books = eval( "(" + xmldoc.getElementsByTagName("books").item(0).firstChild.nodeValue + ")");
			for(var i=0; i<books.book.length; i++){
				msg += "제목 : " + books.book[i].title + "<br>"
					+ "저자 : " + books.book[i].author + "<br>"
					+ "가격 : " + books.book[i].price + "<br><br>";
			}
			
			//JQuery
			var data = eval("(" + $(xmldoc).find("books").text() +")");
			for(var i=0; i<data.book.length; i++){
				msg +="제목 :"  + books.book[i].title + "<br>"
					+ "저자 : " + books.book[i].author + "<br>"
					+ "가격 : " + books.book[i].price + "<br><br>";
			}
			
			//each함수 (반복문)
			$.each(
				data.book,
				function(index, item) {
					msg += "제목 : " + item.title + "<br>"
						+ "저자 : " + this.author + "<br> "
						+ "가격 : " + this.price + "<br><br>";
				} 
			);
			
			
			$("#result").html(msg);
		}
	);
	//-->
</script>
<div id="result"></div>
```
