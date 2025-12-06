`pandas.Series() : Series 자료형`   type = <class 'pandas.core.series.Series'>
파라미터 옵션: `index=` 


`<Series 객체>.index` type = RangeIndex(start=0, stop=5, step=1)


`<Series 객체>.values` type = Series 자료형 안에 있는 아이템들로 이루어진 시퀀스 자료형


`pandas.DataFrame() : DataFrame 자료형`  type = <class 'pandas.core.frame.DataFrame'>
파라미터 옵션: `index=`, `columns=`


`<DataFrame 객체>.index` type = 행 인덱스들의 시퀀스 자료


`<DataFrame 객체>.columns` type = 열 이름들의 시퀀스 자료


`<DataFrame 객체>.rename() : None`  
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





