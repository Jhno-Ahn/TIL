# JSON의 정의

- JavaScript Object Notation (제이슨)
- 자바 스크립트를 위한 객체 형식의 자료 표현 방식
- 간단한 데이터를 xml보다 좀 더 간단하게 표현하기 위한 방법
- 단순한 데이터를 받아서 객체나 변수로 할당해서 사용하기 위한것

# JSON 표기법

## Object

- 키/값으로 이루어진 데이터 쌍들의 집합
- 이 객체는 {} 표현
- 키/값의 데이터쌍 사이는 콜론( : ) 으로 구분

```jsx
{이름1: 값1, 이름2: 값2, 이름3:값3}

-----------------------------------------

var contries = {ko:'대한민국', uk:'영국'};
var koName = contries.ko;
var ukName = contries.['uk'];
```

## Value

- a number(integer or float)
    - integer형이나 float형을 넣을 수 있습니다.
    - “clickNumber” : 1
- a String
    - String형을 표현하고 싶을 때는 큰 따옴표로 묶어줍니다.
    - “nme” : “홍길동”
- a boolean
    - true 나 false를 넣을 수 있습니다.
    - “bResult” : true
- an object
    - 여러개의 key/value를 입력하여 중괄호로 둘러싸여집니다.
    - {”firstName” : “길동”, “lastName”:”홍”}
- an array
    - 순서가 있는 값들의 목록, 일반적으로 배열로 구성되어 이싿.
    - JSON 배열은 [] 값들의 순서가 있는 집합.
    - 배열의 값들은 콤마로 구분
    
    ```jsx
    var ee = [
        	  {"name":"홍길동", "age":20},
        	  {"name":"이순신", "age":30},
        	  {"name":"김유신", "age":40}
          ];
          
          for(var i=0; i<ee.length; i++){
          msg += "이름:" + ee[i].name + "<br>"
          		+ "나이:" + ee[i].age + "<br>";
          }
    ```
    

 

## JSON 표기법 클래스 정의

- 함수 이름이 “이름” 부분에 들어가고 함수 정의가 “값” 부분에 들어가게 된다.
- JSON표기법을 사용하면 함수를 개별적으로 정의하지 않고 하나의 데이터로 표시할 수 있기 때문에 많이 사용한다.

```jsx
클래스이름 = function(파라미터){
	...
}

클래스이름.prototype = {
		함수명1 : function(파라미터1) {
		...
		},
		함수명2 : function(파라미터2){
		...
		},
}
```
