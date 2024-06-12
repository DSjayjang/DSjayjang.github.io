---
layout: single
title: "Web Crawling in Python"
categories: Python
tag: [python, crawling, pandas, beautifulsoup]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# **※ 웹 크롤링**

## ■ Pandas 활용 / 표 형태 데이터 크롤링

```py
# 사용 예시
> url = 'https://…'
> table_df_list = pd.read_html(url, encoding = 'euc-kr')
> table_df = table_df_list[3]

> import FinanceDataReader

> kospi = FinanceDataReader.StockListing('KOSPI')

> kospi_info_list = []
> for code in kospi['Code'][:10]:
    url = f'https://…code={code}'
    table_df_list = pd.read_html(url, encoding = 'euc-kr')
    table_df = table_df_list[3]

    kospi_info_dic = {}
    kospi_info_dic['code'] = code
    kospi_info_dic['table'] = table_df

    kospi_info_list.append(kospi_info_dic)

> print(kospi[0]['code'])
> print(kospi[0]['table'])
```

<br>

## ■ BeautifulSoup 활용
- 파이썬으로 웹 서버 정보 요청 후 HTML 가져오기
- 데이터 파싱
- 정보 저장

```py
# 사용 예시
> import requests from bs4
> import BeautifulSoup as bs

> keyword = '제주도'
> url = f'https://…query={keyword}'
> res = requests.get(url)
> res # <Response [200]>

> soup = bs(res.text, 'html.parser')
> soup # html 코드를 가져옴

> soup.find_all('a', class_ = 'title_link') # 해당 요소를 가진 모든 정보를 찾음
> soup.find_all('a', class_ = 'title_link')[0] # 첫 번째 블로그의 html 정보
> soup.find_all('a', class_ = 'title_link')[0].text # 첫 번째 블로그의 html 정보 중 텍스트 출력
> soup.find_all('a', class_ = 'title_link')[0]['href'] # 첫 번째 블로그의 블로그 주소

"""
> a = []
> for idx in range(len(soup.find_all('a', class_ = 'title_link'))):
    a.append(soup.find_all('a', class_ = 'title_link')[idx].text)
"""

> title = [idx.text for idx in soup.find_all('a', class_ = 'title_link')]
> date = [idx.text for idx in soup.find_all('span', class_ = 'sub')]
> content = [idx.text for idx in soup.find_all('a', class_ = 'dsc_link')]
> df.DataFrame({'title' : title, 'date' : date, 'content' : content})
```