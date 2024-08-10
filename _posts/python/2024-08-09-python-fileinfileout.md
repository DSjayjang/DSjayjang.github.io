---
layout: single
title: "[Python] file I/O (파일 입출력)"
categories: Python
tag: [python, filein, fileout, open(), .readline(), .readlines(), .read(), pickle, .write()]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ filein / fileout
- storage와 프로그램 사이의 I/O를 file I/O라고 함
- 스토리지로부터 파일을 불러오는 것은 input, 결과를 스토리지에 저장하는 것은 output
- 다른 타입의 파일을 열기 위해선 다른 라이브러리가 필요
  - e.g. csv, excel 파일을 열기 위해, pandas, csv, openpyxl 라이브러리 사용
  - e.g. png, jpg 파일을 열기 위해, PIL, opencv 라이브러리 사용
  - e.g. pk, pkl 파일을 열기 위해, pickle 라이브러리를 사용 (파일 타입이 binary라서, ‘rb’를 써야함)
- I/O가 데이터 처리를 할 때 가장 느린 파트이기 때문에 신경써줘야 함 (performance bottleneck)

<br>

## ■ 파일 모드
- w (쓰기 모드): 파일에 내용을 쓸 때 사용
- r (읽기 모드): 파일을 읽기만 할 때 사용
- a (추가 모드): 파일의 마지막에 새로운 내용을 추가할 때 사용

<br>

### □ txt 파일 쓰기 (write)

```py
# 기본 구조
> f = open('저장경로/file_name.txt', 'w')
> f.close()

# with문을 사용하면 close()를 사용하지 않아도 된다.
> with open('저장경로/file_name.txt', 'w') as f
    f.write('something')
```

```py
# e.g. 파일 쓰기로 열고 내용 작성하기
> f = open('~.txt', 'w')
> for i in range(10):
    data = f'{i+1} 번째 줄이다.\n'
    f.write(data)
> f.close()

# with문을 사용하면 close()를 사용하지 않아도 된다.
> with open('~.txt', 'w') as f:
    for i in range(10):
        data = f'{i+1} 번째 줄이다.\n'
        f.write(data)
```

<br>
<br>

### □ txt 파일 읽기 (read)
1. readline()
2. readlines()
3. read()
4. for문 등을 이용
- 파일은 반드시 'r'이나 'rb'로 불러와야 함 'w'로 불러올 경우 파일의 내용이 사라질 수 있음



#### 1. readline()
- 파일에 있는 한 줄(\n 기준 및 포함)을 불러옴 (파일의 첫 번째 한줄만 읽어들임)

```py
# 기본 구조
> f = open('저장경로/file_name.txt', 'r')
> data = f.readline()
> f.close()
```

```py
# e.g. 파일 읽기로 열고 내용 출력하기
> f = open('~.txt', 'r')
> data = f.readline()
> print(data)
> f.close()
# 1 번째 줄이다.


# e.g. 모든 데이터 출력하기
> f = open('~.txt', 'r')
> while data:
    data = f.readline()
    print(data)
> f.close()
# 1 번째 줄이다.

# 2 번째 줄이다.

# ...
# 10 번째 줄이다.
```

```py
# e.g.1 모든 데이터 리스트 형태로 만들기
> f = open('~.txt', 'r')
> header = f.readline() # 첫 번째 row
> data = []

> line = f.readline() # 두 번째 row
> while line: # line이 빈 문자열이 될 때까지
    data.append(line.strip()) # '\n' 제거
    line = f.readline()
> f.close()

# e.g.2 모든 데이터 리스트 형태로 만들기
> with open('~.txt', 'r') as f:
    header = f.readline().strip() # '\n' 제거
    data = [line.strip() for line in f]
> print(data)
```

<br>

#### 2. readlines()
- 모든 데이터를 '\n' 기준으로 잘라서 ```리스트```로 저장함

```py
# 기본 구조
> f = open('저장경로/file_name.txt', 'r')
> data = f.readlines()
> f.close()
```

```py
# e.g.
> with open('~.txt', 'r') as f:
    data = f.readlines()
> type(data) # <class 'list'>
> data # ['1 번째 줄이다.\n', '2 번째 줄이다.\n', ... , '10 번째 줄이다.\n']
```

<br>

#### 3. read()
- 파일에 있는 모든 내용을 문자열로 불러옴

```py
# 기본 구조
> f = open('저장경로/file_name.txt', 'r')
> data = f.read()
> f.close()
```

```py
# e.g.
> with open('~txt', 'r') as f:
    data = f.read()
> type(data) # <class 'str'>
> data
# 1 번째 줄이다.
# 2 번째 줄이다.
# ...
# 10 번째 줄이다.
```

<br>

#### 4. for문 이용

```py
# e.g.
> L = []
> with open('~txt', 'r') as f:
    for line in f:
        L.append(line.strip())
> L # ['1 번째 줄이다.', '2 번째 줄이다.', ..., '10 번째 줄이다.']
```

<br>

#### ◎ txt 불러오기 활용
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

<br>
<br>

### □ txt 파일에 내용 추가하기 (append)
- 'a' 사용

```py
> with open('file_name.txt', 'a') as f:
   for line in range(10,20):
      data = f'{line+1} 번째 줄이다.\n'
      f.write(data)
> data
# 1 번째 줄이다.
# ...
# 10 번째 줄이다.
# 11 번째 줄이다.
# ...
# 20 번째 줄이다.
```