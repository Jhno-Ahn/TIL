![1](https://user-images.githubusercontent.com/81155572/168066518-bde41200-542b-40e0-b46c-88f77ec8470b.PNG)

```python
import csv
import numpy as np

f = open('high_school_2019.csv','r',encoding='utf-8')
lines = csv.reader(f)
header = next(lines)

list_data = [] #데이터 받을 2차원 리스트 초기화
for line in lines : #전체데이터만큼 반복하여
    list_data.append(line[:]) #한행씩 추가 
print(list_data)
f.close

#실행결과
[['서울특별시 강남구', '국립국악고등학교', '5', '150',
'5', '149', '5', '143'], 
['서울특별시 성북구', '서울대학교사범대학부설고등학..]
.........................
```

![2](https://user-images.githubusercontent.com/81155572/168066532-1662540c-4044-4f73-9f7c-ee362e5e6d12.PNG)

```python
import csv
import numpy as np

f = open('high_school_2019.csv','r',encoding='utf-8')
lines = csv.reader(f)
header = next(lines)
print('-----------------------------------------------------------------------------------')
print(header[2],header[3],header[4],header[5],header[6],header[7])
print('-----------------------------------------------------------------------------------')

list_data = []

for line in lines : #한 행의 데이터를 끝에 추가
    list_data.append(line[:])

lenth = len(list_data) #리스트데이터의 길이를 초기화
#print(lenth)
data = np.zeros((lenth, 6), dtype='int32') #배열객체 data생성 후 요소값은 0으로 초기화 6개의 열에 int32타입으로 만듬

for i in range(lenth) : #리스트데이터의 길이만큼 반복(행의 개수)
    for j in range(6) : #출력해야하는 개수 6개니깐 6번 반복
        data[i][j] = list_data[i][j+2] #데이터배열 저장
print(data)
f.close()

#실행결과
-----------------------------------------------------------------------------------
 1학년 학급수  1학년 학생수  2학년 학급수  2학년 학생수  3학년 학급수  3학년 학생수
-----------------------------------------------------------------------------------
[[  5 150   5 149   5 143]
 [  8 239   8 228   8 270]
 [  6 182   6 174   6 169]
 ...
 [  4  76   5  91   5 103]
 [  4  99   4  95   4  92]
 [  5 116   5  98   5 126]]
```

![3](https://user-images.githubusercontent.com/81155572/168066557-c1a65f26-fdf0-4c58-bf9a-02a72e7f5637.PNG)

```python
import csv
import numpy as np

f = open('high_school_2019.csv','r',encoding='utf-8')
lines = csv.reader(f)
header = next(lines)
print('-----------------------------------------------------------------------------------')
print(header[2],header[3],header[4],header[5],header[6],header[7],'총학생수')
print('-----------------------------------------------------------------------------------')

list_data = []

for line in lines : #한 행의 데이터를 끝에 추가
    list_data.append(line[:])

lenth = len(list_data) #리스트데이터의 길이를 초기화
#print(lenth)
data = np.zeros((lenth, 6), dtype='int32') #배열객체 data생성 후 요소값은 0으로 초기화 6개의 열에 int32타입으로 만듬

for i in range(lenth) : #리스트데이터의 길이만큼 반복(행의 개수)
    for j in range(6) : #출력해야하는 개수 6개니깐 6
        data[i][j] = list_data[i][j+2]
        
data = np.insert(data, 6, 0, axis=1) #insert함수를 통해 6번째열 인덱스에 0을 추가

for i in range(lenth) : #lenth길이만큼
    data[i][6] = data[i][1] + data[i][3] + data[i][5] #학년별 학생수를 더해 총 학생수에 초기화
    
print(data)
f.close()

#실행결과
-----------------------------------------------------------------------------------
 1학년 학급수  1학년 학생수  2학년 학급수  2학년 학생수  3학년 학급수  3학년 학생수 총학생수
-----------------------------------------------------------------------------------
[[  5 150   5 ...   5 143 442]
 [  8 239   8 ...   8 270 737]
 [  6 182   6 ...   6 169 525]
 ...
 [  4  76   5 ...   5 103 270]
 [  4  99   4 ...   4  92 286]
 [  5 116   5 ...   5 126 340]]
```

![4](https://user-images.githubusercontent.com/81155572/168066580-27aa1b4d-4c50-4d67-8db3-4b6a1c7ec9c1.PNG)

```python
import csv
import numpy as np

f = open('high_school_2019.csv','r',encoding='utf-8')
lines = csv.reader(f)
header = next(lines)
print('1학년 총 학생 수 :%s'%number[0])
print('2학년 총 학생 수 :%s'%number[1])
print('3학년 총 학생 수 :%s'%number[2])

list_data = []

for line in lines : #한 행의 데이터를 끝에 추가
    list_data.append(line[:])

lenth = len(list_data) #리스트데이터의 길이를 초기화
#print(lenth)
data = np.zeros((lenth, 6), dtype='int32') #배열객체 data생성 후 요소값은 0으로 초기화 6개의 열에 int32타입으로 만듬

for i in range(lenth) : #리스트데이터의 길이만큼 반복(행의 개수)
    for j in range(6) : #출력해야하는 개수 6개니깐 6
        data[i][j] = list_data[i][j+2]
        

number = [0,0,0] #학년별 총 학생수 0으로 초기화하는 리스트 만듬
grade = ['1학년','2학년','3학년'] #학년 초기화하는 grade 리스트

for i in range(lenth) : #총 길이만큼
    number[0] += data[i][1] #1학년의 총 학생수를 반복해서 더해줌
    number[1] += data[i][3] #2학년의 총 학생수를 반복해서 더해줌
    number[2] += data[i][5] #3학년의 총 학생수를 반복해서 더해줌

plt.bar(grade,number) #바를통해 x축데이터에는 학년을, y축데이터에는 학생수를 표시
plt.title('전국 고등학교 학년별 총 학생수')
plt.show()
    

f.close()
```
