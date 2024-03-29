---
title: "Data Science"
weight: 50
# bookFlatSection: false
bookToc: true
# bookHidden: false
# bookCollapseSection: false
bookComments: false
# bookSearchExclude: false
---

## Prerequisites  

### 

1. 데이터 획득 (Importing a working dataset)
2. 데이터 파악 
    - 일변량 (단수변수에 대한 변화) / 다변량 (복수변수의 변화)
    - Summary statistics (기초 통계량, non-graphic) / graphic (시각화)
3. 데이터 변환
4. 모델 적용 (ML)
5. 모델 평가 


</bar>

### VSCode with Jupyter extensions
https://code.visualstudio.com/docs/datascience/overview  
VSCode 에 Jupyter extensions 설치하고,  
해당 프로젝트를 github repo 에 저장  

```$ python3 -m venv .venv``` 을 이용해서 virtual 환경 설치   
```$ source .venv/bin/activate``` 으로 virtual 환경 실행   
```(.venv)$ pip install ipykerne``` 으로  Jupyter kernel 설치  
```(.venv)$ pip install pandas```으로 관련 python 모듈 설치  

### Jupyter lab (notebook)
https://github.com/jupyterlab/jupyterlab
```bash
$ pip install ipython
# or $ pip install jupyter (or notebook)
$ pip install jupyterlab
$ jupyter lab  
# or $ jupyter notebook 
```
git extension : ```pip install --upgrade jupyterlab jupyterlab-git```

### Other Jupyter 
> 1. [Anaconda](https://www.anaconda.com/) 을 설치해서 Jupyter Notebook 사용  (Local)  
> 2. [google colab](https://colab.research.google.com), [Kaggle](https://www.kaggle.com), [dacon](https://dacon.io/) 에서 제공하는 cloud 커널 을 사용  (Cloud)  



### Jupyter shortcuts



### VSCode shortcuts

</br>

### Kaggel 

kaggle 은 Data Science 을 배우기 위한 사이트 

- https://www.kaggle.com/ - google account
- https://dacon.io/ - 국내 사이트

</br>

### Importing a working dataset
kaggle API [^kaggleAPI]

```$ pip install kaggle``` 으로 kaggel API 설치  
Kaggle API TOKEN을 ~/.kaggle/kaggle.json 에 다운로드,  
kaggle API 을 이용하여 data 다운로드 가능   
```bash
# titanic competitions 에서 아래 명령어를 copy 해서 실행
$ kaggle competitions download -c titanic -p /path/to/dest
Downloading titanic.zip to /Users/myoungjunesung/pyproject/data
0%|                                                    | 0.00/34.1k [00:00<?, ?B/s]
100%|██████████████████████████████████████████████████| 34.1k/34.1k [00:00<00:00, 841kB/s]
```
적당한 곳에 압축을 풀어서 jupyter nb cell 에서 load  

```python
import pandas as pd

df = pd.read_csv('./content/titanic/test.csv')
```

> pd 말고 다른 모듈로 로딩하는 경우도 있다. 

## Understanding the big picture

### EDA

- raw data 의 description, dictionary 를 통해 데이터의 각 column들과 row의 의미를 이해
- 결측치 처리 및 데이터필터링
    - 분석 시 필요한 데이터가 수치형 데이터(numerical data)인데 범주형(categorical data)으로 되어 있다면 (데이터 타입이 ‘object’로 뜸) 수치형으로 변환(ex. astype 활용)해줘야 한다.
- 이해하기 쉬운 시각화

https://www.youtube.com/watch?v=xi0vhXFPegw  
https://datascienceschool.net/intro.html 

```python
import pandas as pd

df = pd.read_csv('./content/titanic/test.csv')

df.shape
df.head()
df.tail()
df.discribe()   # 전체적인 통계치
df.info()
df.columns      # 각 columns 을 보기 
```

indexing
```python
df[row index : row index -1]  row 출력
df['row label' : 'row label']   lable row 출력

df['column label']  column label 으로 생각함 (row label 은 오류)
df[['column label','column label_2']]
df.column_label

# selction by lable 
df.loc['row label']
df.loc[['row lable','column label_2']]        # df
df.loc[ : , 'column label']  # row label 생략 불가
...
df.loc['row label' : 'row label' , 'column label' : 'column label']  # 연속
df.loc[['row lable','row lable'],['colum lable','column lable']]     # 불연속

# selection by position 
df.iloc[row index]
df.iloc[[row index, row index_2]]         # df
df.iloc[ : , column index]   # row index 생략불가
...
df.iloc[row index : row index-1 , column index : column index -1 ]
df.iloc[[row index, rowindex],[row index, row index]]

```

```df[[ 'column lable','column lable', ... ]]``` 을 이용한 column selecting 예  
![edit column by column](edit_column.png)

1. 일변 (단수변수) : 데이터를 distrubution 

- Summary statistics : 

    - Numeric data
                    Center (Mean, Median, Mod),  
                    Spread (Variance, SD, IQR, Range),   
                    Modality (Peak)  
                    Shape (Tail, Skewness, Kurtosis)  
                    Outliers  

    - Categorical data
                    occurence, frequency, tabulation (도수분포)

- 시각화 (graphic)

    - Histogram 혹은 Pie chart, Stem-leaf plot, Boxplot, QQplot

Useful properties and functions in Pandas

```python
#수치화모듈
import numpy as np
import pandas as pd
#pd.set_option('max_columns'=200)

#시각화 모듈
import matplotlib.pylab as plt
import seaborn as sns
plt.style.use('ggplot')

.mean() # 평균
.median() # 중앙값
.mode() # 최빈값

plt.hist(titanic.Fare, bin = 5, edgecolor = 'gray') # 히스토그램
plt.xlable('Fare')
plt.ylable('Frequency')
plt.show()

sns.kdeplot(titanic['Fare'])
plt.show()

plt.boxplot(age)
plt.show()

```

</br>

2. 다변 (복수 변수) : 변수간의 관계 correlation

- Summary statistics 

    - Numerical data :  Cros Statistics
    - Categorical data :  Cross-Tabulation

- 시작화 (graphic)

    - Category data & Numeric data : Boxplots, Stacked bar, Parallel Coordinate, Heatmap 
    - Numeric data & Numeric data : Scatter Plot 

    </br>

</br>

https://www.youtube.com/watch?v=xi0vhXFPegw 

https://blog.naver.com/dtddtd4861/222985892251  




</br>

[^kaggleAPI]: https://github.com/Kaggle/kaggle-api