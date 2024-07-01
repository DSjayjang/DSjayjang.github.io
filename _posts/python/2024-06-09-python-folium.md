---
layout: single
title: "[Python] Folium Library"
categories: Python
tag: [python, folium]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# **※ folium**
- 지도 시각화 라이브러리

<br>

## ■ 라이브러리 호출

```py
> import folium
```

<br>

## ■ folium method

### □ 기초 method

1. 지도 크기 지정
2. 지도 만들기
3. 지도 출력
4. 파일로 저장

```py
> f = folium.Figure(width = 가로, height = 세로) # 지도 크기 지정
> m = folium.Map(location = [위도, 경도], zoom_start = 얼마나 확대할건지).add_to(f) # 지도 만들기

> m # 출력
> m.save('file_name.html') # 파일로 저장
```

<br>

### □ 마커 추가

- tooltip : 마우스 오버 시 나타남
- popup : 클릭 시 나타남
- icon : 아이콘 커스텀
- color : 아이콘 색 지정
- icon : 아이콘 모양 지정 e.g. star
- radius : 원형 크기 지정

```py
# 장소 표시 마커
> folium.Marker([위도, 경도], tooltip = "", popup = "", icon = folium.Icon(color = 색, icon = 모양)).add_to(m)

# 원형 마커
> folium.CircleMarker([위도, 경도], radius = 크기, color = 색).add_to(m)
```

<br>

### □ Heat Map

```py
> from folium import plugins

> m = folium.Map(location, zoom_start)
> plugins.HeatMap(위도, 경도, 가중치).add_to(m)
```

<br>

## ■ folium 사용 예시

```py
> f = folium.Figure(width = 700, height = 500)
> m = folium.Map(location = [37.51, 127.09], zoom_start = 16).add_to(f)

# 장소표시 마커 추가
> folium.Marker([37.51, 127.09], 
    tooltip = '롯데', # 툴팁 추가
    icon = folium.Icon(color = 'red', icon = 'star'),
    popup=’<iframe src="https://~~~.jpg"></iframe>’).add_to(m)

# 원형 마커 추가
> folium.CircleMarker([37.49, 127.12], color=’red’,
    radius=50,
    tooltip = '경복궁',
    icon = folium.Icon(color = 'green', icon = 'star')).add_to(m)

> m # 출력
> m.save('test.html') # 저장
```

<br>

### □ json 파일을 활용한 folium 사용 예시
- geo_data : 지리데이터
- data : 시각화할 data frame
- columns : data frame에서 사용할 컬럼 이름
- key on : geo_data에서 데이터를 매핑할 key 컬럼
- fill_color : 지도의 색상 팔레트
- fill_opacity : 채우기 투명도
- line_opacity : 경계산 투명도
- legend_name : 범례

```py
> folium.Choropleth(geo_data, data, columns, key_on, fill_color, fill_opacity, line_opacity, legend_name, …)
```

```py
# json 파일 load
> geo_json = json.load(open("경로", encoding = 'utf-8'))

> f = folium.Figure(width = 700, height = 500)
> m = folium.Map(location = [15, 120], zoom_start = 11).add_to(f)

# json 지역 경계데이터를 지도에 표시 후 data 추가
> folium.Choropleth(geo_data = geo_json,
    data = df,
    columns = ['지역명', '개수'],
    key on = 'properties.name',
    fill_color = 'YlGn',
    fill_opacity = 0.7,
    line_opacity = 0.7,
    legend_name = '서울시 지역별 매장수').add_to(m)

> m
> m.save('test.html')
```

```py
# df : data frame
> f = folium.Figure(width=700, height=500)
> m = folium.Map(location=[37.5, 126.9], zoom_start=11).add_to(f)

> for idx in df.index:
    lat = df.loc[idx, '위도'],
    long = df.loc[idx, '경도'],
    title = df.loc[idx, '상호명']

    if df.loc[idx, 'kind'] == 'A':
        color = 'black'
    else:
        color = 'red'
    folium.CircleMarker([lat, long],
        radius = 3,
        color = color,
        tooltip = title).add_to(m)

> m.save('tt1.html')
```

<br>

# ※ haversine
- 위도 / 경도의 거리를 잴 수 있는 라이브러리

<br>

## ■ 라이브러리 호출

```py
> from haversine import haversine
```

<br>

## ■ haversine method

```py
# 기본 구조
# unit = 'm' : 거리단위 m
> haversine(위도, 경도, unit = 'm')
```

<br>

```py
# e.g. 위도,경도를 이용하여 지하철역까지의 거리계산 함수 만들기
> def distance(station_name, lat, long):
    station_lat = df.query(f'지하철역 == "{station_name}"')['위도'].values[0]
    station_long = df.query(f'지하철역 == "{station_name}"')['경도'].values[0]

    distance = haversine((station_lat, station_long), (lat, long), unit = 'm')

    return distance

> distance('강남역', 37, 126) # 9999m

> for s in station_list:
    data[s] = data.apply(lambda x: distance(s, x['위도'], x['경도']), axis = 1)
```