## [5-4] 배열에 담긴 모든 값을 더하는 프로그램.

```java
package practice_5;

public class Practice_5_4 {

	public static void main(String[] args) {
		int[][] arr = {{5, 5, 5, 5, 5},
					{10, 10, 10, 10, 10},
					{20, 20, 20, 20, 20},
					{30, 30, 30, 30, 30}};
		int total = 0;
		float average = 0;

		(?)
		
		System.out.println("total="+total);
		System.out.println("average="+average);
	}

```

- 내가 적은 답
    
    ```java
    package practice_5;
    
    public class Practice_5_4 {
    
    	public static void main(String[] args) {
    		int[][] arr = {{5, 5, 5, 5, 5},
    					{10, 10, 10, 10, 10},
    					{20, 20, 20, 20, 20},
    					{30, 30, 30, 30, 30}};
    		int total = 0;
    		float average = 0;
    		
    		for(int i=0; i<arr.length; i++) {
    			for(int j=0; j<=arr.length; j++) {
    				total += arr[i][j];
    				average++;
    				//[0,0],[0,1],
    				
    				
    			}
    		}
    		average = total / average;
    		
    		System.out.println("total="+total);
    		System.out.println("average="+average);
    	}
    
    }
    ```
    
- 정답
- 오답노트

---

## [5-5] 1과 9사이의 중복되지 않은 숫자로 이루어진 3자리 숫자를 만들어라.

```java
package practice_5;

public class Practice_5_5 {

	public static void main(String[] args) {
		int[] ballArr = {1,2,3,4,5,6,7,8,9};
		int[] ball3 = new int[3];
		
		// 배열 ballArr의 임의의 요소를 골라서 위치를 바꾼다.
		for(int i=0; i<ballArr.length; i++) {
			int j = (int)(Math.random() * ballArr.length);
			int tmp = 0;
			/*(?)*/
		
		}
		//배열 ballArr의 앞에서 3개의 수를 배열 ball3로 복사한다.
		/*(?)*/
		for(int i=0; i<ball3.length;i++){
				System.out.print(ball3[i]);
		}
		
	}

}
```

- 내가 적은 답
    
    ```java
    package practice_5;
    
    public class Practice_5_5 {
    
    	public static void main(String[] args) {
    		int[] ballArr = {1,2,3,4,5,6,7,8,9};
    		int[] ball3 = new int[3];
    		
    		// 배열 ballArr의 임의의 요소를 골라서 위치를 바꾼다.
    		for(int i=0; i<ballArr.length; i++) {
    			int j = (int)(Math.random() * ballArr.length);
    			int tmp = 0;
    			
    			tmp = ballArr[j];
    			ballArr[i] = tmp;
    		}
    		//배열 ballArr의 앞에서 3개의 수를 배열 ball3로 복사한다.
    		for(int i=0; i<3; i++) {
    			ball3[i] = (int)(Math.random() * ballArr.length +1);
    		}
    		
    		for(int i=0; i<ball3.length; i++) {
    			System.out.print(ball3[i]);
    		}
    		
    		
    	}
    
    }
    ```
    
- 정답
- 오답노트

---

## [5-6] 몇 개의 동전이 필요한지 출력.

```java
package practice_5;

public class Practice_5_6 {

	public static void main(String[] args) {
		//큰 금액의 동전을 우선적으로 거슬러 줘야한다.
		int[] coinUnit = {500, 100, 50, 10};
		
		int money = 2680;
		System.out.println("money = " + money);
		
		for(int i=0; i<coinUnit.length; i++) {
			/*?*/
		}
		
	}

}
```

- 내가 적은 답
- 정답
    
    ```java
    package practice_5;
    
    public class Practice_5_6 {
    
    	public static void main(String[] args) {
    		//큰 금액의 동전을 우선적으로 거슬러 줘야한다.
    		int[] coinUnit = {500, 100, 50, 10};
    		
    		int money = 2680;
    		System.out.println("money = " + money);
    		for(int i=0; i<conUnit.length; i++) {
    			
    			System.out.println(coinUnit[i]+"원:"+money/coinUnit[i]);
    			money = money % coinUnit[i];
    			
    		}
    		
    	}
    
    ```
    
- 오답노트
    
    

---

## [5-8] answer에 담긴 데이터를 읽고 각 숫자의 개수를 세어서 개수만큼 '*'을 찍어서 그래프를 그리는 프로그램

```java
package practice_5;

public class Practice_5_8 {

	public static void main(String[] args) {
		int[] answer = { 1,4,4,3,1,4,4,2,1,3,2};
		int[] counter = new int[4];
		
		for(int i=0; i<answer.length; i++) {
			//(1)
		}
		
		for(int i=0; i<counter.length; i++) {
			//(2)
			
			System.out.println();
		}
	}
}
```

- 내가 적은 답
- 정답
    
    ```java
    
    package practice_5;
    
    public class Practice_5_8 {
    
    	public static void main(String[] args) {
    		int[] answer = { 1,4,4,3,1,4,4,2,1,3,2};
    		int[] counter = new int[4];
    		
    		for(int i=0; i<answer.length; i++) {
    			counter[answer[i]-1]++;
    		}
    		
    		for(int i=0; i<counter.length; i++) {
    			System.out.print(counter[i]);
    
    			for(int j=0; j<counter[i]; j++) {
    					System.out.print("*"); // counter[i]의 값 만큼 '*'을 찍는다.
    			}			
    			System.out.println();
    		}
    	}
    }
    
    ```
    
- 오답노트
    - 배열을 이용해 데이터의 개수를 세는 문제
    - 크기가 4이지만 배열의 index는 0~3이기 때문에 answer[i]에서 1을 빼주어야 한다.
    - 예제 5-11 참고
    

---

## [5-9] 주어진 배열을 시계방향으로 90도 회전시켜서 출력

```java
package practice_5;

public class Practice_5_9 {

	public static void main(String[] args) {
		char[][] star = {
				{'*','*',' ',' ',' '}, 
				{'*','*',' ',' ',' '}, 
				{'*','*','*','*','*'}, 
				{'*','*','*','*','*'}
		};
		
		char[][] result = new char[star[0].length][star.length];
		
		for(int i=0; i<star.length; i++) {
			for(int j=0; j<star[i].length; j++) {
				System.out.print(star[i][j]);
			}
			System.out.println();
		}
		
		System.out.println();
		
		for(int i=0; i<star.length; i++) {
			for(int j=0; j<star[i].length; j++) {
			
				(?)
				
			}
		}
		
		for(int i=0; i<result.length; i++) {
			for(int j=0; j<result[i].length; j++) {
				System.out.print(result[i][j]);
				
			}
			System.out.println();
		}
		
	}
}
```

- 내가 적은 답
- 정답
    
    ```java
    package practice_5;
    
    public class Practice_5_9 {
    
    	public static void main(String[] args) {
    		char[][] star = {
    				{'*','*',' ',' ',' '}, 
    				{'*','*',' ',' ',' '}, 
    				{'*','*','*','*','*'}, 
    				{'*','*','*','*','*'}
    		};
    		
    		char[][] result = new char[star[0].length][star.length];
    		
    		for(int i=0; i<star.length; i++) {
    			for(int j=0; j<star[i].length; j++) {
    				System.out.print(star[i][j]);
    			}
    			System.out.println();
    		}
    		
    		System.out.println();
    		
    		for(int i=0; i<star.length; i++) {
    			for(int j=0; j<star[i].length; j++) {
    				int x=j;
    				int y=star.length-1-i;
    				
    				result[x][y]=star[i][j];
    			}
    		}
    		
    		for(int i=0; i<result.length; i++) {
    			for(int j=0; j<result[i].length; j++) {
    				System.out.print(result[i][j]);
    				
    			}
    			System.out.println();
    		}
    		
    	}
    }
    ```
    
- 오답노트
    - 원래의 위치를 (i,j), 옮길 위치를 (x,y)라고 할 때 i 와 j의 값을 이용해서 x와 y의 값을 어떻게 계산해 낼 것인지를 고민해보자.
    
    ![스크린샷 2021-11-14 오전 9.17.21.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/602045b5-41ce-4240-9866-ed4b5bf1165c/스크린샷_2021-11-14_오전_9.17.21.png)
    
    - star[0][0]은 result[0][3]으로, star[0][1]은 result[1][3]으로 이동해야 한다.
    - 표로 정리하면
        
        ![스크린샷 2021-11-14 오전 9.17.41.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3847b5e7-062b-4a8c-b7b5-4c9a505d9c2e/스크린샷_2021-11-14_오전_9.17.41.png)
        
    - x의 값은 j의 값과 정확히 일치한다.
    - y의 값을 보면 i와 y의 합이 일정함을 알 수 있다. i와 y의 합은 항상 3이다. 3은 star.length-1과 동일한 값이다.
    - 'i+y = star.length-1'이니까, 'y = star.length-1-i'가 된다.
    - 그림을 그리고 표를 그리면 도움이 된다.

---

![스크린샷 2021-11-14 오전 9.30.19.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c91c960c-a547-4e4c-85b3-efaf98f92074/스크린샷_2021-11-14_오전_9.30.19.png)

- 내가 적은 답
- 정답
    
    ```java
    package practice_5;
    
    public class Practice_5_10 {
    
    	public static void main(String[] args) {
    		char[] abcCode =
    			{ '`','~','!','@','#','$','%','^','&','*',
    			'(',')','-','_','+','=','|','[',']',
    			'{', '}',';',':',',','.','/'};
    		
    						// 0   1   2   3   4   5   6   7   8   9
    		char[] numCode = {'q','w','e','r','t','y','u','i','o','p'};
    		
    		String src = "abc123";
    		String result = "";
    		
    		//문자열 src의 문자를 charAt()으로 하나씩 읽어서 변환 후 result에 저장
    		for(int i=0; i<src.length(); i++) {
    			char ch = src.charAt(i);
    			
    				if('a' <= ch && ch <= 'z'){
    						result += abcCode[ch-'a'];
    				} else if('0' <= ch && ch<='9'){
    						result += numCode[ch-'0'];
    				}
    		}
    		
    		System.out.println("src:"+src);
    		System.out.println("result"+result);
    	}
    }
    ```
    
- 오답노트
    - 조건문을 통해 문자가 영어소문자인 경우와 숫자인 경우를 나누어서 처리했다.
    
    ![스크린샷 2021-11-14 오후 6.29.01.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5bacb4eb-34d8-42db-ac55-d5914b7d3d46/스크린샷_2021-11-14_오후_6.29.01.png)
    

---

![스크린샷 2021-11-14 오후 6.29.42.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/098fd63a-563a-41fc-a02a-66b50237938f/스크린샷_2021-11-14_오후_6.29.42.png)

- 내가 적은 답
- 정답
    
    ```java
    package practice_5;
    
    public class Practice_5_11 {
    
    	public static void main(String[] args) {
    		int[][] score = { { 100, 100, 100 }, 
    							{ 20, 20, 20 }, 
    							{ 30, 30, 30 }, 
    							{ 40, 40, 40 },
    							{ 50, 50, 50 } };
    
    		int[][] result = new int[score.length + 1][score[0].length + 1];
    
    		for (int i = 0; i < score.length; i++) {
    			for (int j = 0; j < score[i].length; j++) {
    				result[i][j] = score[i][j];
    				result[i][score[0].length] += result[i][j];
    				result[score.length][j] += result[i][j];
    				result[score.length][score[0].length] += result[i][j];
    			}
    		}
    		
    		for(int i=0; i < result.length;i++) {
    			for(int j=0; j < result[i].length;j++) {
    				System.out.printf("%4d",result[i][j]);
    			}
    			System.out.println();
    
    		}
    	}
    }
    ```
    
- 오답노트
    - 먼저 score[i][j]를 result[i][j]에 저장하고, result[i][j]는 아래 그림에 표시한 세 곳에 누적해서 더해주면 된다.
    
    ![스크린샷 2021-11-14 오후 8.47.57.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1f81cf5c-114b-41a2-b9c1-a0488c0c8bec/스크린샷_2021-11-14_오후_8.47.57.png)
    
    ![스크린샷 2021-11-14 오후 8.49.18.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d1a08eba-0d3a-4918-9661-370655de036d/스크린샷_2021-11-14_오후_8.49.18.png)
    

---

![스크린샷 2021-11-14 오후 8.50.43.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/07e2021f-01d2-4f31-b7dd-2fe3f2a530b6/스크린샷_2021-11-14_오후_8.50.43.png)

![스크린샷 2021-11-14 오후 8.50.52.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d985ccb1-4214-4b53-849c-0e3618902513/스크린샷_2021-11-14_오후_8.50.52.png)

- 내가 적은 답
- 정답
    
    ```java
    package practice_5;
    
    import java.util.Scanner;
    
    public class Practice_5_13 {
    
    	public static void main(String[] args) {
    
    		String[] words = { "television", "computer", "mouse", "phone" };
    		
    		Scanner scanner = new Scanner(System.in);
    		
    		for (int i = 0; i < words.length; i++) {
    			char[] question = words[i].toCharArray();
    			
    			for(int j=0; j<question.length; j++) {
    				int idx = (int)(Math.random() * question.length);
    				
    				char tmp = question[i];
    				question[i] = question[idx];
    				question[idx] = tmp;
    			}
    			
    			System.out.printf("Q%d. %s의 정답을 입력하세요.>",
    										i+1, new String(question));
    			String answer = scanner.nextLine();
    			
    			// trim()으로 answer의 좌우 공백을 제거한 후, equals로 word[i]와 비교 
    			if(words[i].equals(answer.trim()))
    				System.out.printf("맞았습니다. %n%n");
    			else
    				System.out.printf("틀렸습니다. %n%n");
    		}
    	}
    }
    ```
    
- 오답노트
    - idx를 만들어 그 안에 Math.random 메서드를 통해 각 단어의 길이만큼 숫자를 랜덤생성.
    - char tmp 생성해 단어의 i번째 저장
    - 랜덤으로 만들어진 idx번째를 i에 저장
    - 다시 i번째 저장했던 tmp를 idx번째에 저장.
    - question.length만큼 반복
    - 이렇게 하면 무작위로 섞인다.
