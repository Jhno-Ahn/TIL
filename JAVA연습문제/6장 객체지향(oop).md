![스크린샷 2021-11-15 오후 5.34.48.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/af550557-1a68-4a61-b417-51aa2ac7ae70/스크린샷_2021-11-15_오후_5.34.48.png)

- 내가 적은 답
    
    ```java
    class SutdaCard {
    		int num;
    		boolean isKwang;
    }
    ```
    
- 정답
- 오답노트

---

![스크린샷 2021-11-15 오후 5.39.40.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f059da55-6ab2-4d49-a4e4-22a700e821b4/스크린샷_2021-11-15_오후_5.39.40.png)

- 내가 적은 답
    
    ```java
    class SutdaCard {
    		int num;
    		boolean isKwang;
    
    	SutdaCard(){
    			this(1, true);
    	}
    	
    	SutdaCard(int num, boolean isKwang){
    			this.num = num;
    			this.isKwang = isKwang;
    	}
    	
    	String info() {
    			return num + ( isKwang? "K" : "");
    	}	
    }
    ```
    
- 정답
    
    ```java
    class SutdaCard {
    		int num;
    		boolean isKwang;
    
    	SutdaCard(){
    			this(1, true);
    	}
    	
    	SutdaCard(int num, boolean isKwang){
    			this.num = num;
    			this.isKwang = isKwang;
    	}
    	
    	String info() {
    			return num + ( isKwang? "K" : "");
    	}	
    }
    ```
    
- 오답노트
    - 객체를 생성할 때 두 개의 생성자를 사용했으므로 두 개의 생성자를 정의해야한다.
    - 

---

![스크린샷 2021-11-15 오후 5.57.23.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/735e6b73-366a-4442-9bd1-aebf22b6c1f1/스크린샷_2021-11-15_오후_5.57.23.png)

- 내가 적은 답
    
    ```java
    class Student {
    	String name;
    	int ban;
    	int no;
    	int kor;
    	int eng;
    	int math;
    }
    ```
    
- 정답
- 오답노트

---

![스크린샷 2021-11-15 오후 5.59.23.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c905028b-3ba1-4657-8545-cd0b00f1a9d4/스크린샷_2021-11-15_오후_5.59.23.png)

- 내가 적은 답
    
    ```java
    class Student {
    	String name;
    	int ban;
    	int no;
    	int kor;
    	int eng;
    	int math;
    
    	int getTotal() {
    		return kor + eng + math;
    	}
    
    	float getAverage(){
    		return (int)(getTotal() / 3f * 10 + 0.5f)/10f;
    	}
    }
    ```
    
- 정답
- 오답노트
    - 반환타입 int , float
    - 소수점 둘째자리로 구해야하기 때문에 getTotal() 앞에 (int)로 형변환
    - float로 값을 얻어야 하기 때문에 3f로 나눔
    - 소수점 2째까지 얻기 위해 10을 곱한뒤에, 반올림을 위한 0.5f를 더해줌.
    - 마지막으로 10f로 나누어주면 됨.
    
    ---
    

---

![스크린샷 2021-11-15 오후 7.41.38.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e2955a27-ea3d-4c4b-adfa-069dde4c9069/스크린샷_2021-11-15_오후_7.41.38.png)

- 내가 적은 답
    
    ```java
    package practice_6;
    
    public class Practice_6_4 {
    
    	public static void main(String[] args) {
    		Student s = new Student("홍길동", 1, 1, 100, 60, 76);
    
    		System.out.println(s.info());
    	}
    }
    
    class Student {
    
    	String name;
    	int ban;
    	int no;
    	int kor;
    	int eng;
    	int math;
    
    	public Student(String name, int ban, int no, int kor, int eng, int math) {
    		this.name = name;
    		this.ban = ban;
    		this.no = no;
    		this.kor = kor;
    		this.eng = eng;
    		this.math = math;
    	}
    	
    	int getTotal() {
    		return kor+eng+math;
    	}
    	
    	float getAverage() {
    		return (int)(getTotal()/3f*10+0.5f)/10f;
    	}
    
    	public String info() {
    		return name + "," + ban + "," + no + "," + kor + "," + eng + "," + math + "," + getTotal() + "," + getAverage();
    	}
    
    }
    ```
    
- 정답
- 오답노트
    
    

---

![스크린샷 2021-11-15 오후 7.55.33.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0a6adfb5-c20a-4ba7-80cc-107eff300f55/스크린샷_2021-11-15_오후_7.55.33.png)

- 내가 적은 답
    
    ```java
    package practice_6;
    
    public class Practice_6_6 {
    
    	static double getDistance(int x, int y, int x1, int y1) {
    		double xx = (x-x1)*(x-x1);
    		double yy = (y-y1)*(y-y1);
    		double xy = xx+yy;
    		double d = Math.sqrt(xy);
    		
    		return d;
    		
    	}
    	
    	public static void main(String[] args) {
    		System.out.println(getDistance(1, 1, 2, 2));
    	}
    }
    ```
    
- 정답
- 오답노트

---

![스크린샷 2021-11-16 오후 7.52.52.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2022bd19-fd96-4d05-8dde-d6a948b1ca44/스크린샷_2021-11-16_오후_7.52.52.png)

- 내가 적은 답
    
    
- 정답
    
    ```java
    package practice_6;
    
    class MyPoint{
    	int x;
    	int y;
    	
    	MyPoint(int x, int y){
    		this.x = x;
    		this.y = y;
    	}
    	
    	double getDistance(int x1, int y1) {
    		return Math.sqrt((x-x1)*(x-x1) + (y-y1)*(y-y1));
    		
    	}
    	
    }
    public class Practice_6_7 {
    
    	
    	
    //	static double getDistance(int x, int y, int x1, int y1) {
    //		double xx = (x-x1)*(x-x1);
    //		double yy = (y-y1)*(y-y1);
    //		double xy = xx+yy;
    //		double d = Math.sqrt(xy);
    //		
    //		return d;
    //		
    //	}
    	
    	public static void main(String[] args) {
    		MyPoint p = new MyPoint(1,1);
    		
    		//p와 (2,2)의 거리를 구한다.
    		System.out.println(p.getDistance(2, 2));
    	}
    }
    ```
    
- 오답노트

---

![스크린샷 2021-11-16 오후 9.43.13.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d2bed994-9b1f-4a17-9555-a22fc46818dc/스크린샷_2021-11-16_오후_9.43.13.png)

- 내가 적은 답
    - 클래스변수(static변수) : static int width; , static int height
    - 인스턴스 변수 : int kind; , int num;
    - 지역 변수 : int k, int n
- 정답
    
    지역변수 : k,n,card,args
    
- 오답노트
    - args 또한 매개변수...이다..
    - card는 참조변수이니깐 지역변수...

---

![스크린샷 2021-11-16 오후 9.45.33.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/77e2d319-497c-4785-ba88-0e57e30f6783/스크린샷_2021-11-16_오후_9.45.33.png)

- 내가 적은 답
    - int weapon, int armor
    - static을 붙이는 멤버들은 클래스멤버이다.
    - 클래스멤버들은 클래스가 생성될 때 같이 생성이 되고, 인스턴스가 없이도 사용이 가능하다.
    - 인스턴스멤버가 일회용인 반면에 클래스멤버는 항상 값이 상수이기 때문에, 모든 병사의 공격력과 방여력이 일정해야 하는 weapon과 armor는 static을 붙여서 클래스멤버로 만들어주어야 한다.
- 정답
    - weapon, armor, weaponUp,armorUp
- 오답노트
    - weapon, armor → 모든 Marine인스턴스에 대해 동일한 값이어야 하므로.
    - weaponUp(), armorUp → static 변수에 대한 작업을 해야하는 메서드이므로 얘네도 static 메서드가 되어야 함.

---
