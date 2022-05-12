## 13장 Numpy 데이터분석

- Numpy : ‘Numerical Python’
    - 파이썬을 이용한 데이터 분석과 산술 연산의 가장 기본적인 패키지
- 배열의 구조, 다차원 배열, 배열 간 연산, 배열의 정렬 등의 많은 편리한 기능 제공
- Ndarray : 배열 객체, 리스트와 유사, 배열을 다루는 편리한 기능 제공
- ndarray 생성 메소드
    
    
    | 메소드 | 설명 |
    | --- | --- |
    | array() | 매개 변수로 사용되는 리스트, 튜플, 배열 형의 데이터를 이용하여 ndarray 객체를 생성한다. |
    | random.randn() | 가우시안 정규 분포를 갖는 랜덤 수를 생성한다. |
    | zeros() | ndarray 객체를 생성하고 0으로 초기화한다. |
    | ones() | ndarray 객체를 생성하고 1로 초기화한다. |
    | arange() | 내장 함수 range()와 동일, ndarray 객체를 반환, |
    | reshape() | ndarray 객체의 차원을 재구성한다. 예를 들어 reshape(3,5)은 배열의 구조를 3행 5열의 2차원으로 변환한다. |
- ndarray 속성
    
    
    | 속성 | 설명 |
    | --- | --- |
    | dtype | ndarray 객체의 데이터 형을 나타낸다. int32는 32비트 정수형, float64는 64비트 실수형을 의미한다. |
    | shape | ndarray객체의 행과 열을 튜플로 나타낸다. |
- ndarray 객체의 메소드
    
    
    | 메소드 | 설명 |
    | --- | --- |
    | sum() | 배열의 모든 요소들의 합계를 반환한다. |
    | mean() | 배열의 모든 요소들의 평균 값을 반환한다. |
    | max() | 배열의 요소들중에서 최댓값을 반환한다. 옵션 axis=0 은 각 열의 최댓값, axis = 1은 각 행의 최댓값을 구하는데 사용 |
    | min() | 배열의 요소들중에서 최솟값을 반환한다. |
    | argmax() | 열 또는 행의 요소들 중 최댓값을 가지는 요소의 인덱스를 반환한다. |
    | argmin() | 열 또는 행의 요소들 중 최솟값을 가지는 요소의 인덱스를 반환한다. |
    | where() | 조건식에 따라 배열의 요소 값을 특정 값으로 변경한다. |
    | sort() | 배열을 오름차순으로 정렬한다. 2차원 배열인 경우 sort(0)는 열을 중심으로, sort(1)은 행을 중심으로 요소들을 정렬 |
    | insert() | 배열에 행 또는 열을 삽입한다. |

- nadarray 산술 연산

```python
import numpy as np

a = np.array([[10,7,-8,2],[-2,2,8,3],[6,-8,-5,3]])
b = a * 2 #각각의 요소 다 *2
print(b)
c = a * a 
print(c)
print(a>b)

#실행결과
[[ 20  14 -16   4]
 [ -4   4  16   6]
 [ 12 -16 -10   6]]
[[100  49  64   4]
 [  4   4  64   9]
 [ 36  64  25   9]]
[[False False  True False]
 [ True False False False]
 [False  True  True False]]
```

- 배열의 합계, 평균, 최대최솟값

```python
import numpy as np

data = np.array([[80,78,90,93],
                 [65,87,88,75],
                 [98,100,68,80]])
print(data.sum()) #총 합
print(data.mean()) #평균값
print(data.max())  #최대값
print(data.min())  #최솟값
print()

print(data.max(axis=0)) #asix=0은 열별(세로)
print(data.max(axis=1)) #aisx=1은 행별(가로)
print()

index1 = np.argmax(data, axis=0) #열별의 최댓값 index위치
index2 = np.argmin(data, axis=1) #행별의 최솟값 index위치
print(index1, index2)

#실행결과
1002
83.5
100
65

[ 98 100  90  93]
[ 93  88 100]

[2 2 0 0] [1 0 2]
```

- 배열에 조건식 사용

```python
import numpy as np

data = np.random.randn(3,4) #3행 , 4열 랜덤값
print(data)

print(data > 0) #0보다 큼? 결과값 true,false로 출력

total = (data<0).sum() #0보다 작은거 몇개? (조건에 맞는 것들의 개수 합)
print(total)

data2 = np.where(data > 0, 1, -1) #data가 0보다 크면 1, 0보다 작으면 -1
print(data2)

data3= np.where(data > 0,5,data) #data가 0보다 그면 5, 0보다 작으면 data
print(data3)

#실행결과
[[ 0.23448271  0.14093993  0.09236937  1.81197998]
 [-0.76434055 -0.1158366  -1.8505512  -2.61521919]
 [ 0.3015737   0.5638495   1.30858522  0.19978179]]
[[ True  True  True  True]
 [False False False False]
 [ True  True  True  True]]
4
[[ 1  1  1  1]
 [-1 -1 -1 -1]
 [ 1  1  1  1]]
[[ 5.          5.          5.          5.        ]
 [-0.76434055 -0.1158366  -1.8505512  -2.61521919]
 [ 5.          5.          5.          5.        ]]
```

- 배열의 요소 정렬

```python
import numpy as np

data = np.array([[13,22,17,2],
                 [-2,20,8,3],
                 [-16,10,-5,33]])
data.sort(0) #열(세로)로 정렬
print(data)

data.sort(1) #행(가로)로 정렬
print(data)

#실행결과
[[-16  10  -5   2]
 [ -2  20   8   3]
 [ 13  22  17  33]]
[[-16  -5   2  10]
 [ -2   3   8  20]
 [ 13  17  22  33]]
```

- 배열의 열과 행 삽입

```python
import numpy as np

a = np.arange(10) #길이 10개짜리 배열 a에 초기화
print(a)

b = np.insert(a,3,10) #a배열에 3번인덱스에 10을 삽입해 b에 초기화
print(b)

x=np.array([[1,1,1],[2,2,2],[3,3,3]])
print(x)

y=np.insert(x, 1, 10, axis=0) #x배열 1번 인덱스 열(세로)별로 10을 삽입
print(y)

y=np.insert(x, 1, 10, axis=1) #x배열 1번 인덱스 행(가로)별로 10을 삽입
print(y)

#실행결과
[0 1 2 3 4 5 6 7 8 9]
[ 0  1  2 10  3  4  5  6  7  8  9]
[[1 1 1]
 [2 2 2]
 [3 3 3]]
[[ 1  1  1]
 [10 10 10]
 [ 2  2  2]
 [ 3  3  3]]
[[ 1 10  1  1]
 [ 2 10  2  2]
 [ 3 10  3  3]]
```

- CSV → 2차원 리스트

```python
import csv
import numpy as np

f = open('school_2019.csv','r',encoding='utf-8')
lines = csv.reader(f)
header = next(lines)
print(header)

list_data = []
for line in lines : 
     list_data.append(line[:])#한 행의 데이터를 끝에 추가

print(list_data)
f.close

#실행결과
['지역', '학교명', '학급수', '학생수', '교사수']
[['서울특별시 서초구', '서울교육대학교부설초등학교',
 '28', '616', '32'],............................
```

- 2차원 리스트 → ndarray

```python
import csv
import numpy as np

f = open('school_2019.csv','r',encoding='utf-8')
lines = csv.reader(f)
header = next(lines)

list_data = []

for line in lines :
    list_data.append(line[:]) #한 행의 데이터를 끝에 추가

lenth = len(list_data) #리스트데이터의 길이를 초기화
print(lenth)
data = np.zeros((lenth, 3), dtype='int32') #배열객체 data생성 후 요소값을 0을 초기화, #3열의 배열 객체 생성

for i in range(lenth) : #3개의 열에대해 6264개의 행으로 구성
    for j in range(3) :
        data[i][j] = list_data[i][j+2]
print(data)
f.close()

#실행결과
6264
[[ 28 616  32]
 [ 31 632  35]
 [ 31 837  38]
 ...
 [ 36 985  42]
 [ 34 862  41]
 [ 26 603  31]]
```

- 최대 학생 수 학교

```python
import csv
import numpy as np

f = open('school_2019.csv','r',encoding='utf-8')
lines = csv.reader(f)
header = next(lines)

list_data = []
for line in lines:
    list_data.append(line[:]) 

length = len(list_data)

data = np.zeros((length, 3), dtype='int32')

for i in range(length) :
    for j in range(3) :
        data[i][j] = list_data[i][j+2]

max_index = np.argmax(data, axis=0) #열별의 최댓값 index위치
print(max_index)
    
max_class = list_data[max_index[0]][1] #최대 학급수 초등학교
num_class = list_data[max_index[0]][2] #학급수 개수

max_student = list_data[max_index[1]][1] #최대 학생수 초등학교
num_student = list_data[max_index[1]][3] #학생수 개수

max_teacher = list_data[max_index[2]][1] #최대 교사 초등학교
num_teacher = list_data[max_index[2]][4] #교사수 개수

print('최대 학급수의 초등학교 :%s, 학급 수 :%s개'%(max_class,num_class))
print('최대 학생수의 초등학교 :%s, 학생 수 :%s개'%(max_student,num_student))
print('최대 교사수의 초등학교 :%s, 교사 수 :%s개'%(max_teacher,num_teacher))

f.close

#실행결과
[ 138 1999  138]
최대 학급수의 초등학교 :서울신정초등학교, 학급 수 :75개
최대 학생수의 초등학교 :탄벌초등학교, 학생 수 :2178개
최대 교사수의 초등학교 :서울신정초등학교, 교사 수 :91개
```

- 학생수와 교사수 비교

```python
import csv
import numpy as np
import matplotlib.pyplot as plt
from matplotlib import rc
rc('font', family='Malgun Gothic')
f = open('school_2019.csv','r',encoding='utf-8')
lines = csv.reader(f)
header = next(lines)

schools = {}

for line in lines:
    if('광주' in line[0]) and ('마재' in line[1]):
        schools.update({'마재':[line[2],line[3],line[4]]})
    if('울산' in line[0]) and ('약사' in line[1]):
        schools.update({'약사':[line[2],line[3],line[4]]})
    if('용인' in line[0]) and ('정평' in line[1]):
        schools.update({'정평':[line[2],line[3],line[4]]})
    if('제주' in line[0]) and ('도평' in line[1]):
        schools.update({'도평':[line[2],line[3],line[4]]})
        
print(schools)

data = np.zeros((4,3), dtype='int32') #4열 3행 데이터 int32 데이터배열 생성

school = list(schools.values())

for i in range(len(schools)) : #schools의 열 길이 만큼
    for j in range(3) : #3행 만큼
        data[i][j] = school[i][j]
print(data) #학급수 학생수 교사수 출력

data = np.insert(data, 2, 0, axis=1) #2번째 열에 0삽입
data = np.insert(data, 4, 0, axis=1) #4번째 열에 0삽입
print(data) #학급수 학생수 학급당학생수 교사수 교사일인당 학생수 맞게 배열 조정

row = data.shape[0] #튜플의 첫 번째 요소의 값, 배열의 전체 행의 개수 의미
for i in range(row):
    data[i][2] = round(data[i][1]/data[i][0]) #학급당 학생수 초기화
    data[i][4] = round(data[i][1]/data[i][3]) #교사 1인당 학생수 초기화
print(data) #학급수 학생수 학급당학생수 교사수 교사일인당학생수 출력

xdata = ['마재','약사','정평','도평']
plt.plot(xdata, data[:,1], label='학생 수', color='red', linestyle='--', marker='x')
plt.plot(xdata, data[:,3], label='교사 수', color='blue', linestyle=':', marker='d')
plt.title('마재/약사/정평/도평 초등학교 학생수와 교사 수')
plt.legend(loc='best')
plt.show() 

plt.plot(xdata, data[:,2], label='학급당 학생수', color='magenta', linestyle='-.', marker='o')
plt.plot(xdata, data[:,4], label='교사 1인당 학생수', color='green', linestyle='--', marker='x')
plt.title('마재/약사/정평/도평 초등학교 학급당 학생수 및 교사 1인당 학생수')
plt.legend(loc='best')
plt.show()

f.close()

#실행결롸
{'마재': ['24', '481', '28'], '약사': ['29', '685', '33'], '정평': ['36', '945', '43'], '도평': ['14', '300', '17']}
[[ 24 481  28]
 [ 29 685  33]
 [ 36 945  43]
 [ 14 300  17]]
[[ 24 481   0  28   0]
 [ 29 685   0  33   0]
 [ 36 945   0  43   0]
 [ 14 300   0  17   0]]
[[ 24 481  20  28  17]
 [ 29 685  24  33  21]
 [ 36 945  26  43  22]
 [ 14 300  21  17  18]]
```
