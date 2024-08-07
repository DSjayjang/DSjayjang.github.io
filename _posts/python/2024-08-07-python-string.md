---
layout: single
title: "[Python] String Data (문자열 데이터)"
categories: Python
tag: [python, string, formatting, format-code, .format(), f-string, len(), .upper(), .lower(), .strip(), .lstrip(), rstrip(), .count(), .find(), .index(), .join(), .split(), .replace(), .startswith(), .endswith()]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ String Data (문자열 데이터)

## ■ 기초 연산
- 문자열 덧셈: 문자열을 이어붙여서 출력
- 문자열 곱셈: 문자열 반복

```py
# e.g. 문자열 덧셈
> s1 = 'Hello'
> s2 = 'World'
> print(s1 + s2)
# HelloWorld

# e.g. 문자열 곱셈
> s = 'Hello'
> s * 10
# HelloHelloHelloHelloHelloHelloHelloHelloHelloHello
```

<br>
<br>

## ■ 문자열 관련 함수
- **`변수를 변경하는 것이 아니라 출력하는 역할만 함`**
- len(): 문자열의 길이 출력
- .upper() : 대문자로 출력
- .lower() : 소문자로 출력
- .strip() : 문자열 좌우 공백제거
- .lstrip() / .rstrip() : 문자열 왼/오 공백 제거

```py
# e.g. 문자열 길이 출력
> s = 'abcde'
> len(a) # 5

# 대/소문자 출력
> s1 = 'abcde'
> s1.upper() # 'ABCDE'

> s2 = 'ABCDE'
> s2.lower() # 'abcde'

# 공백 제거
> s3 = '  abcd  '
> s3.strip() # 'abcd'
> s3.lstrip() # 'abcd  '
> s3.rstrip() # '  abcd'
```

<br>

- .count() : 특정 문자가 변수 안에서 몇번 나왔는지
- .find() : 특정문자가 처음으로 나온 index 번호
  - 찾는 문자가 없는 경우 -1 출력
- .index() : 특정문자가 처음으로 나온 index
  - 찾는 문자가 없는 경우 에러
- '삽입할문자'.join('문자열')
- s.split('구분자') : 괄호안에 아무것도 안쓰면 공백을 기준으로 잘라줌
- s.replace('변경전 문자', '변경후 문자')
- .startswith() / .endswith() : '문자'로 시작/끝나는지를 T/F 출력

```py
> s = 'apple'

> s.count('p') # 2

> s.find('p') # 1
> s.find('z') # -1 # 찾는 문자가 없는 경우

> s.index('p') # 1
> s.index('z') # 에러 발생

> '-'.join(s) # 'a-p-p-l-e'

> s.split('l') # ['app', 'e']

> s.replace('p','z') # 'azzle'

> s.startswith('a') # True
> s.endswith('a') # False
```

<br>
<br>

## ■ 문자열 포맷팅
- 문자열 안에 값을 삽입하는 방법

<br>

### □ 포맷 코드를 사용한 포맷팅
- %d: 정수
- %s: 문자열
- %f: float
- %c: 문자 1개
- %o: 8진수
- %x: 16진수
- %%: %문자 자체

```py
# e.g. 포맷 코드를 사용한 formatting
> var1 = "사과"
> var2 = 5

> print('%s는 %d개' %(var1, var2))
# 사과는 5개
```

<br>

#### 포맷 코드로 문자열 길이 지정하기
- %s 또는 %d 사이에 숫자를 넣음으로써 출력하고자 하는 값의 길이를 지정할 수 있음
    - e.g. %10s : 총 길이 10으로 지정 후 오른쪽 정렬
    - e.g. %-10s : 총 길이 10으로 지정 후 왼쪽 정렬

```py
# e.g.
> s = 'abc'
> print('Hi-%10s' %s) # Hi-       abc
> print('%-10s-Hi' %s) # abc       -Hi
```

<br>

#### 포맷 코드로 소수점 표현하기
- %와 f 사이에 숫자를 넣음으로써 출력하고자 하는 자릿수 지정 가능
    - e.g. %.4f
      - 소수점 네번째 자리까지 나타냄 (다섯번째 자리에서 반올림)
    - e.g. %10.2f
      - 소수점 둘째자리까지 나타내며 전체 길이를 10으로 지정 후 오른쪽 정렬

```py
# e.g.
> f1 = 3.123456789
> print('%.4f' %f1) # 3.1235

> f2 = 3.123456789
> print('%.4f' %f2) # 3.1234

> f3 = 3
> print('%.4f' %f3) # 3.0000

> f4 = 7.1234
> print('%10.2f' %f4) #       7.12

> f5 = 7.1234
> print('%-10.2f' %f4) # 7.12
```

<br>
<br>

### □ .format 함수를 사용한 포맷팅
- .format

```py
# e.g. .format을 사용한 formatting
> var1 = "사과"
> var2 = 5

> print('{}는 {}개' .format(var1, var2))
# 사과는 5개

> print('{}는 {}개' .format(var1='배', var2=10))
# 배는 10개
```

<br>

#### .format 함수로 정렬하기
- :< : 왼쪽 정렬
- :> : 오른쪽 정렬
- :^ : 가운데 정렬

```py
# 왼쪽 정렬 후 문자열 길이 10으로 지정
> print('Hi {:<10}' .format('Bye')) # Hi Bye

# 오른쪽 정렬 후 문자열 길이 10으로 지정
> print('Hi {:>10}' .format('Bye')) # Hi        Bye

# 가운데 정렬 후 문자열 길이 10으로 지정
> print('Hi {:^10}' .format('Bye')) # Hi    Bye
```

```py
# 공백 채우기
> print('Hi {:=<10}' .format('Bye')) # Hi Bye=======
> print('Hi {:>10}' .format('Bye')) # Hi =======Bye
> print('Hi {:^10}' .format('Bye')) # Hi ===Bye====
```

<br>

#### .format 함수로 소수점 표현하기

```py
# e.g.
> f1 = 3.123456789
> print('{:.4f}' .format(f1)) # 3.1235

> f2 = 3.123456789
> print('{:.4f}' .format(f2)) # 3.1234

> f3 = 3
> print('{:.4f}' .format(f3)) # 3.0000

f4 = 7.1234
print('{:10.2f}' .format(f4)) #       7.12

> f5 = 7.1234
> print('{:.2f}' .format(f4)) # 7.12
```

<br>
<br>

### □ f-string을 사용한 포맷팅
- f-string

```py
# e.g. f-string을 사용한 formatting
> var1 = "사과"
> var2 = 5

> print(f'{var1}는 {var2}개')
# 사과는 5개


# e.g. 계산도 가능
> age = 10
> print(f'내년에는 {age+1}살 이다.')
# 내년에는 11살 이다.
```

<br>

#### f-string을 사용한 정렬

```py
# 오른쪽 정렬 후 문자열 길이 10으로 지정
> print(f'Hi {"Bye":>10}') # Hi        Bye

# 왼쪽 정렬 후 문자열 길이 10으로 지정
> print(f'Hi {"Bye":<10}') # Hi Bye

# 가운데 정렬 후 문자열 길이 10으로 지정
> print(f'Hi {"Bye":^10}') # Hi    Bye
```

```py
# 공백 채우기
> print(f'Hi {"Bye":=>10}') # Hi =======Bye
> print(f'Hi {"Bye":=<10}') # Hi Bye=======
> print(f'Hi {"Bye":=^10}') # Hi ===Bye====
```