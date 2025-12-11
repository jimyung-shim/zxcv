`pandas.Series() : Series 자료형`   type = <class 'pandas.core.series.Series'>
파라미터 옵션: `index=` 


`<Series 객체>.index` type = pandas.Index


`<Series 객체>.values` type = numpy.ndarray
Series 자료형 안에 있는 아이템들로 이루어진 시퀀스 자료형(Numpy 배열)


`pandas.DataFrame() : DataFrame 자료형`  type = <class 'pandas.core.frame.DataFrame'>
파라미터 옵션: `index=`, `columns=`


`<DataFrame 객체>.index` type = pandas.Index
행 인덱스들의 시퀀스 자료(Row index들의 Index 객체)


`<DataFrame 객체>.columns` type = pandas.Index
열 이름들의 시퀀스 자료(Column name들의 Index 객체)


`<DataFrame 객체>.rename() : DataFrame`
`<DataFrame 객체>.rename(..., inplace=True) : None`  
파라미터 옵션을 `columns=`로 하여 열 이름들을 바꾸거나, `index=`로 하여 행 인덱스 이름들을 변경할 수 있다. 


`<DataFrame 객체>.drop() : DataFrame` , `DataFrame.drop(inplace=True): None`
파라미터 옵션: (행 인덱스 또는 배열 , axis=0) >> 행 삭제, (열 이름 또는 배열 , axis=1) >> 열 삭제
기존 객체를 변경하지 않고 새로운 객체를 반환하기 때문에 원본 객체를 직접 변경하고 싶다면 파라미터 옵션으로 inplace=True 옵션을 추가해야한다.


`<DataFrame 객체>.copy() : DataFrame` 
`def copy(deep: bool = True) -> DataFrame`


`<DataFrame 객체>.loc['인덱스 이름']`  ex) loc['hello']
`<DataFrame 객체>.iloc[<정수형 위치 인덱스>]`    ex) iloc[2]


`<DataFrame 객체>.set_index("<열 이름>") : DataFrame`, 
`<DataFrame 객체>.set_index("<열 이름>", inplace=True) : None`


`<DataFrame 객체>.transpose() : DataFrame` 
DataFrame 행렬을 전치시켜서 리턴


`<DataFrame 객체>.reindex(<인덱스 배열>) : DataFrame`
파라미터로 받아온 인덱스 배열로 인덱스를 재지정하여 새로운 객체를 리턴.
값이 비어있는 곳은 기본적으로 Nan이 채워짐
`fill_value=` 옵션으로 값이 빈 곳에 대신 채울 값 지정 가능


`<DataFrame 객체>.reset_index() : DataFrame`
행 인덱스를 다시 정수형으로 초기화


`<DataFrame 객체>.sort_index() : DataFrame` 오름차순으로 행 정렬
`<DataFrame 객체>.sort_index(ascending=False) : DataFrame` 내림차순으로 행 정렬


`<DataFrame 객체>.sort_values(by='<열 이름>') : DataFrame` 파라미터로 들어온 열을 기준으로 전체 DataFrame 오름차순으로 행정렬
`<DataFrame 객체>.sort_values(by='<열 이름>', ascending=False) : DataFrame` 파라미터로 들어온 열을 기준으로 전체 DataFrame 내림차순으로 행정렬


`<Series 객체> / <숫자 'a'>  -> Series`  Series 각 원소들을 a로 나눈다

`<Series 객체> + or - or * or / <Series 객체>  -> Series`   
각 인덱스 라벨별로 대응되는 값끼리 연산한다.
어떤 인덱스 라벨에 대해 한쪽 Series에 값이 없으면 그 인덱스의 결과가 NaN이 된다. 

`<Series 객체>.add(<또 다른 Series 객체>, fill_value=<Nan을 대체할 값>) : Series` 
`<Series 객체>.sub(<또 다른 Series 객체>, fill_value=<Nan을 대체할 값>) : Series` 
`<Series 객체>.mul(<또 다른 Series 객체>, fill_value=<Nan을 대체할 값>) : Series` 
`<Series 객체>.div(<또 다른 Series 객체>, fill_value=<Nan을 대체할 값>) : Series` 
시리즈 객체끼리 사칙 연산을 수행한다.

`seaborn.load_dataset('<데이터 파일 이름>') : DataFrame`

`<DataFrame 객체>.head() : DataFrame` 기존 DataFrame 객체의 첫 5행 까지의 데이터만 담긴 DataFrame 객체를 리턴

`<DataFrame 객체>.tail() : DataFrame` 기존 DataFrame 객체의 마지믹 5행의 데이터만 담긴 DataFrame 객체를 리턴


`pandas.read_csv('<파일 이름>', header=None) : DataFrame`  파라미터로 받아온 파일 이름에 해당하는 파일로부터 데이터를 가져와 DataFrame에 채워넣어서 리턴한다. 
header=None은 csv 파일의 첫 행을 열 이름으로 삼지 말라는 소리다. 이 옵션을 빼먹을 경우 csv 파일의 첫 행이 열의 이름으로 자동 설정되어버린다. 

`pandas.read_excel('<파일 이름>', engine='openpyxl') : DataFrame`   엑셀 파일을 읽어서 그 데이터들을 DataFrame 객체에 담아서 리턴한다. 엑셀 파일을 다루기 위해서 엑셀 관련 파이썬 라이브러리를 사용하는 옵션인 engine='openpyxl' 을 파라미터 옵션으로 넣는다.

`<DataFrame 객체>.shape  -> tuple`  (행의 갯수, 열의 갯수)형태의 튜플 데이터다

`<DataFrame 객체>.info() : None` DataFrame 객체의 정보들을 출력한다.

`<DataFrame 객체>.describe() : DataFrame` DataFrame 의 각 열들에 대한 데이터들의 기술 통계 정보가 담긴 DataFrame 객체 리턴

`<DataFrame 객체>.dtypes : Series`  각 열(column)의 “전체적인 자료형(dtype)”을 나타내는 Series를 리턴한다.

`<DataFrame 객체>.count() : Series` DataFrame 객체의 각 열의 데이터 갯수 정보를 담고있는 Series 객체를 리턴한다.

`<DataFrame 객체>.value_counts() : Series`  전체 DataFrame 객체의 각 행이 몇번 나타났는지에 대한 정보가 담긴 Series를 리턴

`<DataFrame 객체>.max() : Series` 각 열의 데이터에 대한 최대값 정보들이 담긴 Series 리턴

`<DataFrame 객체>.min() : Series` 각 열의 데이터에 대한 최소값 정보들이 담긴 Series 리턴

`<DataFrame 객체>.mean() : Series` 각 열의 데이터에 대한 평균값 정보들이 담긴 Series 리턴

`<DataFrame 객체>.median() : Series` 각 열의 데이터에 대한 중앙값 정보들이 담긴 Series 리턴

`<DataFrame 객체>.std() : Series` 각 열의 데이터에 대한 표준편차 정보들이 담긴 Series 리턴

`<DataFrame 객체>.corr() : DataFrame` 열과 열 사이의 상관관계를 계산하여 DataFrame 전체의 상관계수 행렬이 담긴 DataFrame을 리턴.

`<DataFrame 객체>.plot() : matplotlib.axes.Axes`   선 그래프 그리기
파라미터 옵션 `kind='hist'` 을 넣어서 히스토그램 그리기
파라미터 옵션 `kind='box'` 를 넣어서 박스 플롯 그리기 

`<DataFrame 객체>.T   ->  DataFrame`   기존 데이터프레임 객체의 전치행렬

`<Seires 객체>.apply(function) : Series`    Series.apply(func) = Series의 모든 원소를 하나씩 func에 넣어서 나온 결과를 새로운 Series로 반환하는 메서드

`<DataFrame 객체>.applymap(function) : DataFrame` DataFrame 개별 원소에 특정 함수 매핑

`<DataFrame 객체>.isnull() : DataFrame` 각 원소가 null 인지 아닌지에 대한 bool 값이 담겨있는 DataFrame 객체 리턴

`<Series 객체>.isnull() : Series` 각 원소가 null 인지 아닌지에 대한 bool 값이 담겨있는 Series 객체 리턴

`<DataFrame 객체>.pipe(function)  :  Dataframe | Series | 임의의 값` function(<DataFrame 객체>) 와 의미가 같으며 apply() 와는 달리 데이터프레임 객체 통째로 function()의 파라미터로 넘긴다.

`<DataFrame 객체>.groupby(['<기준이 되는 열 이름>'])  :  DataFrameGroupBy`  해당 열의 값이 같은 행들을 그룹으로 정의해 두고, 실제 그룹 데이터는 계산하지 않은 채 그룹 연산을 위한 DataFrameGroupBy 객체를 리턴한다.


`<DataFrameGroupBy 객체>.get_group('<특정 값>')  :  DataFrame `  해당 값으로 묶인 그룹을 데이터프레임으로 리턴한다.


`<DataFrame 객체>.fillna(value) :  None`  NaN을 value로 채우기

`<DataFrame 열 객체>.isin(추출 값의 리스트)  :  Series`  각 인덱스마다 “그 행의 값이 리스트 안에 존재하는지(True/False)”를 판단하여 Series로 반환한다.

`<DataFrameGroupBy 객체>.agg(function)  :  DataFrame`  그룹별로 어떤 함수를 적용해서 요약표(DataFrame)를 만드는 메서드





