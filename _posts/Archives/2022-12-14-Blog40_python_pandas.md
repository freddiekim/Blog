---

layout: post
title: "pandas"
categories: Archives
tags: [documentation,pandas]
image:
 feature:
 teaser:
 credit:
 creditlink:
published: True
---

#### Time : 2022-12-14
#### Title : pandas

#### reference

1. [](https://123okk2.tistory.com/293) 
2. [](https://moondol-ai.tistory.com/180)

***
#### pandas

python을 사용하다보면 pandas를 사용하게 되는데 정리의 필요성이 생겨서 적음.

이렇게 2D는 DataFrame()을 이용해서 만들 수 있음.
이 클래스를 이용하면 검색 및 합치는것 같은 잡일이 쉬워짐.
파일에서 정보를 읽어오고 합치고 추출하고 이정도만 알아도 쉽게 2D 데이터를 사용할 수 있음.
그리고 Series를 사용하면 1D데이터를 사용할 수 있음.
~~~
import pandas as pd

def generate_df(num_col,num_row):
    df = pd.DataFrame()
    for x in range(num_col):
        df[x] = np.random.normal(size=num_row)
    return df

s = pd.Series([1,2,3])
print(s)

data = pd.read_csv('.ignore')
d1 = generate_df(1,2)
print(d1)
temp_df = generate_df(1,1)
print(temp_df)
res_df = d1.append(temp_df, ignore_index=True)
print(res_df)
data2 = pd.DataFrame(data.values,columns=['aa'])
print(data2)
df = pd.DataFrame()
df['aa'] = ['aa/aa/aa']
d3 = data2.append(df, ignore_index=True)
print(d3)

// 이렇게 추가하고 검색 할 수 있음. colums를 사용하면 이름을 줄 수 있음. HEADER같은 것임.
data3 = pd.DataFrame(data.values,columns=['aa'])
data2.append(data3,ignore_index=True)
print(data2['aa'][1])
~~~

#### 트랜스포머 
https://wikidocs.net/31379
https://moondol-ai.tistory.com/460


#### 문자열에서 날짜 추출 하기
strptime 은 문자열을 날짜 객체로 변환하는 것이고
strftime 은 날짜 객체를 문자열로 변환하는 것임.
~~~
str_com = 'monkey 2010-07-10 love banana'
import re
from datetime import datetime

match = re.search(r'\d{4}-\d{2}-\d{2}', str_com)
print(match)
date = datetime.strptime(match.group(), '%Y-%m-%d').date()
print(date)

date_v = '2020-12-31'

date_test = datetime.datetime.strptime(date_v, '%Y-%m-%d')
print(date_test)
print(type(date_test))

date_test2 = date_test.strftime('%Y-%m-%d')
print(date_test2)
print(type(date_test2))
~~~




