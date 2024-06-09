---
layout: single
title: "Folium in Python"
categories: Python
tag: [python, folium]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# **※ folium**
특정 장소의 지도 시각화하기
네이버 지도에서 원하는 위치를 검색하고 공유 버튼을 통해 URL을 복사하세요.
[링크](https://xn--yq5bk9r.com/blog/map-coordinates)에 복사한 url을 붙여넣고 위도와 경도를 확인하세요.

<br>

## ■ 라이브러리 호출

```py
> import folium
```
지도 크기
f = folium.Figure(width=가로길이, height=세로길이)
지도 만들기
m = folium.Map(location=[위도, 경도], zoom_start=줌할정도얼마나확대할건지).add_to(f)
m.save('test.html') #지도 저장


# 장소 표시 마커
folium.Marker([위도, 경도]
                , tooltip=마우스 오버시 나타남
                , popup=클릭시 나타남
                , icon=folium.Icon(color=색, icon=모양)).add_to(지도)

# 원 형태 마커
folium.CircleMarker([위도, 경도]
                , radius=범위
                , color=색).add_to(지도)

f = folium.Figure(width=700, height = 500)
m = folium.Map(location=[37.510781008592716, 127.09607026177875], zoom_start=16).add_to(f)
m
m.save('test.html') #지도 저장

# 마커 추가
folium.Marker([37.510781008592716, 127.09607026177875], tooltip='롯데').add_to(m) # 마커 추가
m.save('test.html') #지도 저장

folium.Marker([37.510781008592716, 127.09607026177875], tooltip='롯데', icon=folium.Icon(color='red', icon='star')).add_to(m) # 마커 추가
m.save('test.html') #지도 저장

folium.Marker([37.510781008592716, 127.09607026177875], tooltip='롯데', icon=folium.Icon(color='red', icon='star'), popup='<iframe src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c2/Lotte_World_Theme_Park.jpg/440px-Lotte_World_Theme_Park.jpg"></iframe>').add_to(m) # 사진추가
m.save('test.html') #지도 저장

folium.CircleMarker([37.510781008592716, 127.09607026177875], color='red', radius=50).add_to(m) # 원형 마커 추가
m.save('test.html') #지도 저장


================================

geo_json = json.load(open(file_path+'seoul_municipalities_geo_simple.json', encoding='utf-8'))
geo_json

df = pd.read_csv(file_path + '소상공인시장진흥공단_상가(상권)정보_서울_202306.csv')
df.head()
df.info()
df.describe()

cafe = df[df['상권업종소분류명'] == '카페'].reset_index()
cafe.head()
cafe.info()

ediya = cafe.loc[cafe['상호명'].str.contains('이디야'), ]
twosome = cafe.loc[cafe['상호명'].str.contains('투썸플레이스'), ]

ediya_count = ediya.groupby('시군구명').size().to_frame().reset_index().rename({0:'count'}, axis=1).sort_values('count', ascending=False)
ediya_count

twosome_count = twosome.groupby('시군구명').size().to_frame().reset_index().rename({0:'count'}, axis=1).sort_values('count', ascending=False)
twosome_count

fig = px.bar(data_frame=ediya_count, x='시군구명', y = 'count', text_auto='.2d', color_discrete_sequence = px.colors.qualitative.Set2)
fig.show()

fig = px.bar(data_frame=twosome_count, x='시군구명', y = 'count', text_auto='.2d', color_discrete_sequence = px.colors.qualitative.Set2)
fig.show()

f = folium.Figure(width=700, height = 500)
m = folium.Map(location=[37.566535, 126.9779692], zoom_start=11).add_to(f)
m.save('test1.html')

folium.Choropleth(geo_data = geo_json, fill_color = 'gray').add_to(m) # 경계데이터를 회색으로 칠함
m.save('test1.html')

folium.Choropleth(geo_data = geo_json, data=ediya_count, columns=['시군구명','count'], key_on='properties.name', fill_color='YlGn',fill_opacity=0.7, line_opacity=0.7,lengend_name='서울시 구별 이디야 매장수').add_to(m) # 경계데이터를 회색으로 칠함
m.save('test3.html')

f = folium.Figure(width=700, height = 500)
m = folium.Map(location=[37.566535, 126.9779692], zoom_start=11).add_to(f)
folium.Choropleth(geo_data = geo_json, data=twosome_count, columns=['시군구명','count'], key_on='properties.name', fill_color='YlGn',fill_opacity=0.7, line_opacity=0.7,lengend_name='서울시 구별 이디야 매장수').add_to(m) # 경계데이터를 회색으로 칠함
m.save('test4.html')

ediya_twosome = ediya_count.merge(twosome_count, on='시군구명', suffixes=('_이디야', '_투썸'))

ediya_twosome = pd.merge(ediya_count, twosome_count, on = '시군구명',suffixes=('_이디야', '_투썸'))

ediya_twosome['이디야_ratio'] = ediya_twosome['count_이디야'] / ediya_twosome['count_이디야'].sum()
ediya_twosome['투썸_ratio'] = ediya_twosome['count_투썸'] / ediya_twosome['count_투썸'].sum()
ediya_twosome['투썸 상대적 비율'] = ediya_twosome['투썸_ratio'] / ediya_twosome['이디야_ratio']
ediya_twosome

f = folium.Figure(width=700, height = 500)
m = folium.Map(location=[37.566535, 126.9779692], zoom_start=11).add_to(f)
folium.Choropleth(geo_data = geo_json, data=ediya_twosome, columns=['시군구명','투썸 상대적 비율'], key_on='properties.name', fill_color='YlGn',fill_opacity=0.7, line_opacity=0.7,lengend_name='서울시 구별 이디야 매장수').add_to(m) # 경계데이터를 회색으로 칠함
m.save('test5.html')

ediya_df = ediya[['상호명','경도', '위도']].copy()
ediya_df['kind'] = '이디야'
ediya_df

twosome_df = twosome[['상호명','경도', '위도']].copy()
twosome_df['kind'] = '투썸'
twosome_df

dff = pd.concat([ediya_df, twosome_df])
dff
dff.loc[7,:]
dff.iloc[0,:]

from _plotly_utils.basevalidators import TitleValidator
f = folium.Figure(width=700, height=500)
m = folium.Map(location=[37.566535, 126.9779692], zoom_start=11).add_to(f)

for idx in dff.index:
    lat = dff.loc[idx, '위도']
    long = dff.loc[idx, '경도']
    title = dff.loc[idx, '상호명']

    if dff.loc[idx, 'kind'] == "이디야":
        color = '#1d326c'
    else:
        color = '#D70035'
    folium.CircleMarker([lat, long]
                        , radius=3
                        , color = color
                        , tooltip = title).add_to(m)
m.save('tt1.html')