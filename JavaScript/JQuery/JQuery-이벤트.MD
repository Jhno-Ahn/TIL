# 이벤트 연결

### bind()

- $(selector).bind(eventName, function(event) { })
    - 첫 번째 매개 변수에 이벤트 이름 입력
    - 두 번쨰 매개 변수에 이벤트 핸들러 입력
    - 이벤트 핸들러 안에서 this 키워드는 이벤 발생한 객체 의미
    - 앞으로 거의 사용 안함, 대신 on메서드 사용
    

### toggle()

- click 이벤트를 여러 이벤트 핸드러를 번갈아 가며 실행할 수 있게 연결
- 매개 변수에 여러 개의 함수 입력 가능

# 이벤트 연결 제거

### unbind()

- 이벤트 제거 시 unbind() 메서드 사용

### one()

- 같은 기능 하는 one() 메서드
- 한번만 실행할 때 사용

```jsx
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<h2> bind </h2>
<style type="text/css">      
   .reverse {          
      color : white;
      background : black;
   }
</style>
<script src="/JQueryEx/jquery-3.6.0.js"></script>
<script type="text/javascript">
   //<!--
   $(document).ready(
      function() {
         // $(selector).bind( eventName, function(event){} )
         $("h4").bind(
            "click",
            function( event) {
               $(this).text( $(this).text() + "凸" );   // 해당하는 것만 들어가는 코딩
            }
         );
                  
         // $(selector).bind( object ) 이건 JSON 방법 오브젝트는 JSON 방법이라구 했어요~ 간단히하기위해 저 위에 css 스타일 잡아줌 근데 왜잡는걸까?
         var size = 16;      
         $("h4").bind(
            {
               "mouseover" : function( event ) {
                  $(this).addClass( "reverse" );   
               },
               "mouseout" : function( event ) {
                  $(this).removeClass( "reverse" );
               },
               "dblclick" : function( event ) {            // "ondblclick"은 더블클릭임
                  $(this).css( "font-size", ++size );
               }
            }   
         );
         
         // unbind       / 바인드로 단것만 빼는거임  아래 설정해놓은 onclick은 못빼는거지
         setTimeout(      // 한번만 호출함 사용방법은 펑션에 이름을 주거나 만들어라
            function() {
               $("h4").unbind("mouseover").unbind("mouseout").unbind("click");
            },
            3000
         );
         
         // toggle
         $("button").bind(
            "click",
            function( event ) {
               $("h3").toggle();
            }
         );
         
         // one , 실행했을때 한번은 뜨지만 그다음부터는 안뜸. 한번만 실행할때 쓰는거래
         $("h5").one(
            "click",
            function( event ) {
               alert( "event" );
            }
         );
         
         
      }      
   );
   function additem() {
      $("h4").text(
         function( index, text ) {
            if( index % 2 == 0 ) {         // if 이거 의미없음 걍해보는거
               return text + "★";
            } else {
               return text + "☆";
            }     
         }      
      );
   }
   //-->
</script>

<h5> one </h5>
<br><br>
<button> 토글 </button> <br>
<h3> 토글 </h3> <br>

<br><br>
<h4 onclick="additem()"> 독서 </h4> <!-- 눌렀을때 동작하는 함수하나 호출해줌 -->
<h4> 등산 </h4>
<h4> 운동 </h4>
<h4> 게임 </h4>
```

# 이벤트 강제 발생

### trigger()

- 강제로 이벤트 발생시킴

```jsx
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<h2> trigger </h2>
<script src="/JQueryEx/jquery-3.6.0.js"></script>
<script type="text/javascript">
	//<!--
	 $(document).ready(
		function(){
		
			//$(selector).trigger(eventname)
			$("h4").bind(
				"click",
				function(event){
					$(this).text($(this).text() +"◆");
				}
			);
			
			
			var cnt=0;
			setInterval(
				function(){
					$("h4:eq("+ cnt++ %4 +")").trigger("click");
				},
				1000
			);
			
			//$(selector).trigger(eventname, [data1, data2, ...])
			$("h3").bind(
				"click",
				function(event, data1, data2){
					$(this).text($(this).text() + data1 + data2);
				}
			);
			
			setInterval(
				function(){
					$("h3").trigger("click",["◁","▷"]);
				},
				1000
			);
			
			
			setTimeout(
				function(){
					$("h4, h3").unbind("click");
				},		
				10000
			);
			
			
			$("a").bind(
				"click",
				function(){
					$(this).css("color","red");
					//event.preventDefault(); //이벤트  전달은 되지만, 실행은 안함
					event.stopPropagation(); //이벤트 전달을 안함, 실행도 안댐
					return false;
				}
			);
			
			$("h5").bind(
				"click",
				function(){
					$(this).css("background","gray");
				}
			);
		}
	 );
	//-->
</script>

<h5><a href="http://www.naver.com">내버</a></h5> <br>
<h5><a href="http://www.daum.net">데엄</a></h5> <br>

<br><br>
<h4>애플</h4>
<h4>버네나</h4>
<h4>슻류배리</h4>
<h4>박수</h4>

<h3>축구</h3>
<h3>야구</h3>
<h3>배구</h3>
<h3>농구</h3>
```
