---
layout: single
title: "Web Crawling in Python"
categories: Python
tag: [python, pandas, beautifulsoup]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# 웹크롤링

# 판다스 / 표 형태 데이터 가져오기
url = 'https://finance.naver.com/item/main.nhn?code=035720'
table_df_list = pd.read_html(url, encoding = 'euc-kr')
table_df_list[3]
table_df = table_df_list[3]
table_df

# pip install finance-datareader
import FinanceDataReader
kospi = FinanceDataReader.StockListing("KOSPI")
kospi

kospi_info_list = []
for code in kospi['Code'][:10]:
    url = f'https://finance.naver.com/item/main.nhn?code={code}'
    table_df_list = pd.read_html(url, encoding = 'euc-kr')
    table_df = table_df_list[3]
    kospi_info_dic = {}
    kospi_info_dic['code'] = code
    kospi_info_dic['table'] = table_df
    kospi_info_list.append(kospi_info_dic)
print(kospi_info_list[0]['code'])
print(kospi_info_list[0]['table'])

# beautifulsoup
크롤링의 과정
파이썬으로 웹서버에 정보 요청하고 HTML 데이터 가져오기
데이터 파싱
원하는 정보 저장

import requests
from bs4 import BeautifulSoup as bs

keyword = '제주도'
url = f'https://search.naver.com/search.naver?ssc=tab.blog.all&sm=tab_jum&query={keyword}'
res = requests.get(url)
res # <Response [200]>

soup = bs(res.text, 'html.parser')
soup # html코드를 가져옴

soup.find_all('a', class_='title_link') # 해당 요소를 가진 모든 정보를 찾아라
soup.find_all('a', class_='title_link')[0] # 첫 번째 블로그 html 정보
soup.find_all('a', class_='title_link')[0].text # 텍스트
soup.find_all('a', class_='title_link')[0]['href'] # 블로그 주소

soup.find_all('span', class_='sub')[2].text

a=[]
for idx in range(len(soup.find_all('a', class_='title_link'))):
    a.append(soup.find_all('a', class_='title_link')[idx].text)

[idx.text for idx in soup.find_all('a', class_='title_link')]
[idx['href'] for idx in soup.find_all('a', class_='title_link')]


title = [idx.text for idx in soup.find_all('a', class_='title_link')]
date = [idx.text for idx in soup.find_all('span', class_='sub')]
date = date[:-2]
content = [idx.text for idx in soup.find_all('a', class_='dsc_link')]

df = pd.DataFrame({'title' : title, 'date' : date, 'content' : content})
df