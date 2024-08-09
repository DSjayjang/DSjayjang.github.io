---
layout: single
title: "[Python] file I/O (파일 입출력)"
categories: Python
tag: [python, filein, fileout, .read(), .readline(), .readlines(), os, os.getcwd(), os.chdir(), os.listdir(), pickle]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ filein / fileout
- storage와 프로그램 사이의 I/O를 file I/O라고 함
- 스토리지로부터 파일을 불러오는 것은 input, 결과를 스토리지에 저장하는 것은 output
- with open() 함수를 통해서 텍스트 파일을 불러올 수 있음
- ‘r’, ‘w’, ‘a’ 등의 mode를 바꿔서 파일을 다른 옵션으로 열 수 있다. (read, write, append 순)
- 다른 타입의 파일을 열기 위해선 다른 라이브러리가 필요
  - e.g. csv, excel 파일을 열기 위해, pandas, csv, openpyxl 라이브러리 사용
  - e.g. png, jpg 파일을 열기 위해, PIL, opencv 라이브러리 사용
  - e.g. pk, pkl 파일을 열기 위해, pickle 라이브러리를 사용 (파일 타입이 binary라서, ‘rb’를 써야함)
- I/O가 데이터 처리를 할 때 가장 느린 파트이기 때문에 신경써줘야 함 (performance bottleneck)

```py
# 파일 불러오기 예시
> with open("a.txt", 'r') as f:
    data = f.realines()
```

<br>

### □ txt 파일을 불러오는 방법
- 텍스트 파일을 여는 방법은 read(), readline(), readlines(), for문 등을 이용

<br>

#### **◎ read**()를 이용한 방법
- 파일에 있는 모든 내용을 불러옴
- 파일은 반드시 'r'이나 'rb'로 불러와야 함

```py
> file_path = "~.txt"

> with open(file_path, 'r') as f:
    data = f.read()

> data
# 엔터값들이 \n함수로 이어짐
```

<br>

#### **◎ readline**()를 이용한 방법
- 파일에 있는 한 줄(\n 기준 및 포함)을 불러옴
- 파일은 반드시 'r'이나 'rb'로 불러와야 함

```py
> file_path = "~.txt"

> with open(file_path, 'r') as f:
    data = f.readline()
> data # 첫줄 한줄만 읽어들임
```

```py
# e.g.
> file_path = "~.txt"
> f = open(file_path, 'r')
> header = f.readline() # 첫 번째 row
> data = []

> line = f.readline() # 두 번째 row
> while line: # line이 빈 문자열이 될 때까지
    data.append(list(map(float, line.split(','))))
    line = f.readline()
> f.close()
```

<br>

#### **◎ readlines**()를 이용한 방법

```py
> file_path = "~.txt"

> with open(file_path, 'r') as f:
    data = f.readlines()

> data
# 모든 데이터를 엔터 기준으로 잘라서 리스트로 가져옴
```

<br>

#### **◎ for**()문을 이용한 방법

```py
> file_path = "~.txt"

> L = [] with open(file_path, 'r') as f:
    for line in f:
      L.append(line)

> L
# readlines와 같음
```

<br>

#### ◎ txt 불러오기 활용
- os library 사용하기

```py
# 라이브러리 호출
> import os

# os method
# 현재 워킹디렉토리 확인
> os.getcwd() # 경로가 출력됨

# 워킹디렉토리 변경
> os.chdir('변경할 경로')

# e.g. 경로 안에 있는 모든 파일명을 리스트로 반환
> os.listdir('경로')

# e.g. 워킹디렉토리 안에 있는 모든 파일명을 리스트로 반환
> os.listdir(os.getcwd())
```

<br>

- txt파일에서 한글자 짜리를 다 지우고 다시 저장하기

```py
> output = []
> with open(file_path, 'r') as f:
    data = f.readlines()
> print(data)

# 한글자 이상인 텍스트만 output list에 저장
> for word in data:
    word = word.strip() # 공백제거 (\n도 공백으로 취급)
    if len(word) > 1:
      output.append(word)

> print(output)
```

<br>

- pickle 라이브러리를 이용하여 파이썬 object 자체를 저장하기

```py
# 리스트 자체를 저장히기
> import pickle

> with open("result.pk", 'wb') as f: # write as binary
    pickle.dump(output, f)

> with open("result.pk", 'rb') as f: # read as binary
    output2 = pickle.load(f)

> output2
```
