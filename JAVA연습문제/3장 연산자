## 3-1 다음 연산의 결과를 적으시오.

```java
class Exercise3_1 {
public static void main(String[] args) {
		int x = 2;
		int y = 5;
		char c = 'A'; // 'A'의 문자코드는 65

		System.out.println(1 + x << 33); 
		System.out.println(y >= 5 || x < 0 && x > 2); 
		System.out.println(y += 10 - x++); System.out.println(x+=2);
		System.out.println( !('A' <= c && c <='Z') ); 
		System.out.println('C'-c); 
		System.out.println('5'-'0'); 
		System.out.println(c+1); 
		System.out.println(++c); 
		System.out.println(c++); 
		System.out.println(c);
		}
}
```

- **내가 적은 답**
    - true
    - true
    - 12
    - 4
    - false
    - 2
    - 5
    - 66
    - B
    - 65
    - A
- **정답**
    - 6
    - true
    - 13
    - 5
    - false
    - 2
    - 5
    - 66
    - B
    - B
    - C
- **오답노트**
    - '1 + 2 << 33' 가 되고 int는 32bit이므로 1번만 쉬프트 한다. '3 << 1'은 3에 '2의 1제곱'인 2를 곱하는 것과 같은 결과를 얻으므로 '3 * 2'가 되여 6을 얻는다

---

## 3-2 필요한 바구니 수를 구하는 코드이다. (1)에 알맞은 코드를 넣으시오

```java
int numOfApples = 129; // 사과의 개수
		int sizeOfBucket = 10;
		int numOfBucket =  (1)
		System.out.println("필요한 바구니의 수 :"+numOfBucket);
```

- **내가 적은 답**
    
    sizeOfBucket / numOfApples;
    
- **정답**
    
    numOfApples / sizeOfBucket + (numOfApples % sizeOfBucket > 0 ? + 1 : 0);
    
- **오답노트**
    - 우선 나누는 순서부터 잘못 적었다. 기본기가 너무 부실했다는걸 느낌 ㅜㅜ
    - 두번째로 나머지가 남으면 그것도 담을 바구니의 개수가 추가되어야 하는데 그걸 놓침
    - 그래서 % 연산자를 사용해 나머지가 0을 초과한다면 +1을 해주고 나머지가 없다면 0을 더해준다.

---

## 3-3 변수 num에 따라 '양수', '음수','0'을 출력하는 코드이다. 삼항연산자를 두번 사용해서 코드를 넣으시오

```java
int num = 10; 
System.out.println(?);
```

- **내가 적은 답**
    
    num = 0 ? 0 :
    num < 0 ? "음수" : "양수"
    
- **정답**
    
    num > 0 ? "양수" : (num == 0 ? "0" : "음수")
    
- **오답노트**
    - 힌트로 삼항연산자를 두 번 이용하라고 했는데, 나는 두번 따로 사용하려고만 생각했다.
    - 0보다 큰 수를 "양수"로 먼저 설정하는 삼항연산자를 만들고 "양수"가 아닐시 0인지, 혹은 그 수보다 작은 수일 경우에는 "음수"로 출력되는 삼항연산자를 괄호안에 한번 더 넣는 삼항연산자를 설정.

---

## 3-7 변환공식이 'C = 5/9 * (F-32)'라고 할때 소수점 셋째자리에서 반올림해서 구하시오(Math.round() 사용x)

```java
int fahrenheit = 100;
float celcius = ?

System.out.println("Fahrenheit:"+fahrenheit); 
System.out.println("Celcius:"+celcius);

//실행 결과 
Fahrengeit : 100
Celcius : 37.78
```

- **내가 적은 답**
- **정답**
    
    ```java
    (int)((5/9f * (fahrenheit - 32)) * 100 + 0.5 / 100f
    ```
    
- **오답노트**
    - float나 double로 해야만 실수 형태의 결과 얻을 수 있다. 따라서 9대신 9f를 사용.
    - 소수점 셋째자리에서 반올림을 하려면 다음 과정.
    1. 값에 100을 곱한다.
    - 37.77778 * 100
    1. 1의 결과에 0.5를 더한다.
    - 3777.778 + 0.5 → 3778.278
    1. 2의 결과를 int타입으로 변환한다.
    - (int)3778.278 → 3778
    1. 3의 결과를 100f로 나눈다.
    - 3778 / 100f → 37.78
