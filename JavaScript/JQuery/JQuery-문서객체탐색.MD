# 체이닝

- 한 줄로 서로 다른 문서 객체에 스타일 적용 가능
- 체이닝은 문서 객체를 점점 좁게 선택해야 한다.
- 체이닝 시 추가한 filter() 메서드를 제거한다.

```jsx
$(document).ready(function(){
		$('h3').css('background','orange').filter(':even').css('color','red');
});
```

### end()

- 문서 객체 선택을 한 단계 뒤로 돌린다.

```jsx
$(document).ready(
		function(){
					$("h5").filter(":even").filter(":odd").css("color","red")
					.end().css("color","blue"); 
				//한단계 전으로 돌려감 (4개중에 짝수녀석들 고르고 그 중에 홀수를 고른 
				//상태에서 이전 상태로 돌아가고 그 녀석을 블루로 바꿈)
			});
```

# 특정 위치의 문서 객체 선택

## 필터 선택자 이용

- 특정 위치에 존재하는 문서 객체 선택
- 필터 선택자는 자주 사용하므로 메서드로 제공
- eq() → 특정 위치에 존재하는 문서 객체를 선택
- first() → 첫 번째에 위치하는 문서 객체를 선택
- last() → 마지막에 위치하는 문서 객체를 선택

### eq() 메서드

- 매개 변수에 숫자 입력
- 음수를 입력하면 뒤쪽 기준으로 선택
- 맨 뒤의 문서 객체가 -1번쨰

```jsx
$(document).ready(
		function(){
			$("h5").filter(":odd").css("color","green")
			.add("h5").filter(":even").css("color","red");
});
```

# 문서 객체 추가 선택

### add() 메서드

- 문서 객체를 추가로 선택

```jsx
$(document).ready(
		function(){
			//add
			$("h5").filter(":odd").css("color","green")
			.add("h5").filter(":even").css("color","red");

});
```

# 문서 객체의 특징 판별

### is()

- 문서 객체가 특징을 가지고 있는지 판단
- 선택한 객체가 선택자와 일치하는지 판별해 불리언 리턴

```jsx
$(document).ready(
		function(){
		//is
			$("h5").each(
				function(index, item){
					if($(item).is(".point")){
						$(this).css("color","gold");
					}
				}		
			);

});
```
