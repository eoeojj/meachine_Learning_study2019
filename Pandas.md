# Python Pandas

## Python Pandas

>   파이썬 판다스는 파이썬 언어로 데이터를 분석하기 쉽게하기 위한 자료구조 및 기능들을 제공하는 패키지이다. 판다스가 제공하는 여러기능들을 통해서 데이터분석 과정 중 가장 까다로은 작업 중 하나인 데이터 전처리를 보다 쉽게 처리할 수 있다. 
>

판다스에서는 다음과 같은 기능을 위해서 만들어졌다

- 축의 이름을 따라 데이터를 정렬할 수 있는 자료구조, 다양한 소스에서 가져온 다양한 방식으로 색인된 데이터를 핸들링 가능한 기능

- 산술연산 및 한 열의 모든 값을 더하는 등의 축약 연한이 가능

- 누락된 데이터의 유연한 처리 가능

- SQL과 같은 관계연산 수행 가능

판다스는 크게 3가지의 자료구조를 지원하고 있는데, 1차원 자료구조인 Series, 2차원 자료구조인 DataFrame, 그리고 3차원 자료구조인  Panel을 지원한다.

#### Series

   그 중 가장 간단한 1차원 자료구조인 Series는 배열/리스트와 같은 일련의 시퀀스 데이터를 받아들이는데 별도의 인덱스레이블을 지정하지 않으면 자동적으로 0부터 시작되는 디폴트 인덱스를 사용한다. 

```python
import pandas as pd
data = [ 1, 2, 3, 4]
sr = pd.Series(data)
```

#### DataFrame

   2차원 자료구조인 DataFrame는 행과 열이 있는 테이블 데이타(Tabular Data)를 받아들이는데, 아래 예제는 그 한가지 방법으로서 열(column)을 dict의 Key로, 행(row)을 dict의 Value로 한 Dictionary 데이타를 pd.DataFrame()을 사용하여 pandas의 Data Frame 자료구조로 변환한 예이다. 

![](C:\Users\lejle\Desktop\머신러닝_스터디\dataframe.png)

```python
data = {
    'year' : [2017,2018,2019],
    'rate' : [50, 60, 70]
}
df = pd.DataFrame(data)
```

#### Panel

   3차원 자료구조인 Panel은 Axis 0 (items), Axis 1 (major_axis), Axis 2 (minor_axis) 등 3개의 축을 가지고 있는데, Axis 0은 그 한 요소가 2차원의 DataFrame 에 해당되며, Axis 1은 DataFrame의 행(row)에 해당되고, Axis 2는 DataFrame의 열(column)에 해당된다. 

### df.head() & df.tail()

df.head() : 처음 5개 출력

df.tail() : 마지막 5개 출력

### pd.read_csv()

외부 csv파일을 불러와서 DataFrame으로 저장하는 방법이다.  

```python
csv_test = pd.read_csv('C:/Users/.../csv_file_name.csv')
csv_test.shape  #csv 파일을 불러와서 행과 열의 개수를 확인해 본다 (m, n)으로 출력 결과가 나온다
csv_test #전체데이터를 호출해 본다

#특정 줄을 제외하고 csv파일을 불러오는 경우 ex) 1,2 번째 행을 제외
csv_test_sub = pd.read_csv('C:/Users/.../csv_file_name.csv', skiprows[1,2]) 

#위에서 n번째 행만 불러오는 경우 ex)3번째
csv_test_sub = pd.read_csv('C:/Users/.../csv_file_name.csv', nrows = 3) 

#0번 째 행부터일 때 n번 째 행을 header로 설정해 준다, header가 없을 땐 None을 하면 자동으로 header 생성
csv_test_sub = pd.read_csv('C:/Users/.../csv_file_name.csv', header = 0) 
```

다음과 같이 파일 경로와 파일의 이름을 적어주면 된다. 

### df.to_csv()

```python
#dataframe 을 csv파일로 내보낸다, 데이터셋을 저장하기 위하여 쓰인다
df.to_csv('csv_file.csv', index = False, encoding = 'utf-8')
```

### df.append()

```python
#새로운 내용을 추가한다 행이 늘어난다  
df = df.append([a,b],ignore_index=True)
```

### df.reindex(    ,   method= '   ')

데이터를 새로운 색인에 맞게 재배열, 없는 색인 값이 있다면 비어있는 값을 새로 추가, method 옵션을 사용하면 시계열 데이터를 재색인할 때 값을 채워넣을 수 있음

reindex method 옵션

 \- ffill 또는 pad : 앞의 값으로 채워 넣음

 \- bfill 또는 backfill : 뒤의 값으로 채워 넣음

```python
#인덱스 이름을 새로 설정한다 
df = df.reindex(index=random_np, columns=[a,b,c..])
```

### df[ ].unique()

```python
#지정한 행 또는 열에서 중복 값을 제외한 값들을 얻기
df['a'].unique()
```

### y = df.iloc[ a : b , c ].values

```python
#a부터 b 미만의 행들, c부터 d미만의 열들의 값을 y 에 저장한다
y = df.iloc[ a : b , c : d ].values

#a와 b 행, c 열들의 값을 y 에 저장한다
y = df.iloc[ [a , b] , c ].values

## ! df.loc 인경우 인덱싱의 라벨값을 받는다는 것만 차이가 있다. iloc 은 정수형으로 인거
```

### df.isnull().sum()

```python
#누락된 데이터에 True 누락이 안된 데이터엔 False로  
df.isnull()

#열마다의 누락된 값의 개수 
df.isnull().sum()
```

### df.columns = [a,b,c,d ..]

데이터프레임에 있는 모든 열을 인덱스 배열로 반환한다. 열의 인덱스를 설정한다고 볼 수 있다.

### df.dropna

```python
#누락된 값이 있는 행을 삭제한다
df.dropna(axis=0)

#누락된 값이 있는 열을 삭제한다
df.dropna(axis=1)

#모든 열이 누락된 값일 때에 행을 삭제한다
df.dropna(how='all')

#행에 있는 열의 값이 누락된값이 있어서 개수가 n보다 작은 행을 삭제한다
df.dropna(thresh=n)

#특정 n열에 누락된 값이 있는 행을 삭제한다
df.dropna(subset=['c'])
```

   위의 함수들로 누락된 값을 확인 또는 삭제할 수 있다. 하지만 만약 누락된 값이있는 행이나 열에 중요한 데이터를 포함할 수 있으므로 위의 삭제기법보다는 보간기법을 쓰는 것이 대부분이다. 보간기법은 사이킷런의 Imputer클래스를 사용하여 누락된 값을 특성 열의 전체평균으로 채우는 것이다.

### df.T

  이 함수에서  T란 Transpose를 가리킨다. 열과 행의 위치를 변환시키는 데에 이용한다. 아달린 구현 시 쓰인 것을 볼 수 있다.  

### 순서가 없는 범주형 데이터 다루기

   범주형 데이터는 순서가 없는 데이터 순서가 있는 데이터로 나눌 수 있다. 순서가 없는 특성은 색깔, 지역 또는 붓꽃의 종류로  볼 수 있다. 순서가 있는 특성은 옷의 사이즈로 볼 수 있다.

```python
df = pd.DataFrame([
    ['green', 'M', 10.1, 'class1'],
    ['blue', 'S', 8.3, 'class2'],
    ['red', 'L', 13.5, 'class1'],])
# 각 열의 frame을 지정한다 
df.colums = ['color', 'size', 'price', 'classlabel' ]
```

위의 df에서 순서가 있는 특성인 옷의 사이즈는 문자 값을 숫자 값으로 변환시켜야 특성의 순서를 알 수 있다. 이를 위하여 size_mapping 이라는 매핑 함수를 선언하다.

```python
# L = M + 1 = S + 2
size_mapping = {
    'L':3
    'M':2
    'S':1
}
# 문자 size 에서 size_mapping 숫자와 매핑한다
df['size'] = df['size'].map(size_mapping)
# 딕셔너리 성질을 변환시키기
inv_size_mapping = {v: k for k, v in size_mapping.items()}
# 숫자 size 에서 inv_size_mapping 문자와 매핑한다
df['size'].map(inv_size_mapping)
```

### 2중 리스트를 1차원 리스트로 만들기

#### df.flatten()

다차원의 배열을 1차원으로 만드는 함수 



#### 참고 사이트

https://doorbw.tistory.com/172

https://sacko.tistory.com/18

https://pandas.pydata.org/pandas-docs/stable/getting_started/10min.html