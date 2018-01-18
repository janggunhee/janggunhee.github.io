---
layout: post
title: Python - String
description: "python study"
modified: 2017-09-14
tags: [python]
categories: [python]
---

# 문자열 (String)

> 문자열(String)이란 문자, 단어 등으로 구성된 문자들의 집합을 의미한다. 예를 들어 다음과 같은 것들이 문자열이다.
> 파이썬3에서는 문자열에서 기본적으로 유니코드(Unicode)를 사용하며, 불변(immutable)하다.

## 문자열 표현

- 작은 따옴표 또는 큰 따옴표 

- 작은 따옴표 또는 큰 따옴표를 사용했을 때, 사용하지 않은 인용 부호는 문자열 내부에서 사용 가능하다.

- 세 개의 작은 따옴표 또는 큰 따옴표 
  여러줄에 걸친 문자열을 나타낼 때 사용
  

<image height=30%>![](///Users/janggunhee/Documents/md-file/images/lines.png)</image>


## 문자열 더하기 

<image height = 30% >![](///Users/janggunhee/Documents/md-file/images/textlines.png)</image>

## 형변환

내장함수 **str**을 사용

```
 str(147)
 '147'
``` 
문자열을 제외한 객체를 `print`함수로 호출하면, 내부적으로 `str`함수를 사용한 결과를 나타낸다.

## 인덱스 연산 

- 문자열에서 문자를 추출하기 위해 대괄호와 오프셋을 지정할 수 있다. 
가장 왼쪽은 0이며, 가장 오른쪽은 -1

- 문자열은 불변이므로 인덱싱한 부분에 새 값을 대입할 수 없다. 

```
  lux = '빛으로 강타해요!'
  lux[0]
  '빛'
  lux[-1]
  '!'
  lux[0] = '손'
  Error
```

## 슬라이스 연산

**[sta:end:step]** 형식을 사용한다.

- [\:] 
	- 처음부터 끝까지
- [start\:]
	- start오프셋부터 마지막까지
- [:end]
	- 처음부터 end오프셋까지
- [start:end]
	- start오프셋부터 end오프셋까지
- [start\:end\:step]
	- start오프셋부터 end오프셋까지, step만큼씩 뛰어넘은 부분

슬라이싱의 예를 조금 더 보도록 하자.
```
>>> a = "Life is too short, You need Python"
>>> a[0:4]
>>> 'Life'
```
```
>>> a[0:2]
'Li'
>>> a[5:7]
'is'
>>> a[12:17]
'short'
```
a[시작 번호:끝 번호]에서 끝 번호 부분을 생략하면 시작 번호부터 그 문자열의 끝까지 뽑아낸다.
```
 >>> a[19:]
'You need Python'
```
a[시작 번호:끝 번호]에서 시작 번호를 생략하면 문자열의 처음부터 끝 번호까지 뽑아낸다.
```
>>> a[:17]
'Life is too short'
```
a[시작 번호:끝 번호]에서 시작 번호와 끝 번호를 생략하면 문자열의 처음부터 끝까지를 뽑아낸다.
```
>>> a[:]
'Life is too short, You need Python'
```
슬라이싱에서도 인덱싱과 마찬가지로 마이너스(-) 기호를 사용할 수 있다.
```
>>> a[19:-7]
'You need'
```
### 슬라이싱으로 문자열 나누기

```
>>> a = "20010331Rainy"
>>> date = a[:8]
>>> weather = a[8:]
>>> date
'20010331'
>>> weather
'Rainy'
```

"Pithon"이라는 문자열을 "Python"으로 바꾸려면 어떻게 해야 할까?

```
>>> a = "Pithon"
>>> a[:1]
'P'
>>> a[2:]
'thon'
>>> a[:1] + 'y' + a[2:]
'Python'
```

### 문자열 포매팅 따라 하기

#### 1) 숫자 바로 대입
```
 "I eat %d apple." % 3
```
 위의 예제는 문자열 내에 3이라는 정수를 삽입하는 방법을 보여 준다. 문자열 안에서 숫자를 넣고 싶은 자리에 	`%d`라는 문자를 넣어 주고, 삽입할 숫자인 3은 가장 뒤에 있는 `% 문자` 다음에 써넣었다. 여기서 `%d`는 **문자열 포맷 코드**라고 부른다.

#### 2) 문자열 바로 대입

숫자 대신 문자열을 넣어 보자.

```
>>> "I eat %s apples." % "five"
'I eat five apples.'
```
숫자를 넣기 위해서는 %d를 써야 하고, 문자열을 넣기 위해서는 %s를 써야 한다.

#### 3) 숫자 값을 나타내는 변수로 대입

```
>>> number = 3
>>> "I eat %d apples." % number
'I eat 3 apples.'

>>> num = "3"
>>> "I eat %s apples." % num
 'I eat 3 apples.'
```
#### 3) 숫자 값을 나타내는 변수로 대입

```
>>> number = 10
>>> day = "three"
>>> "I ate %d apples. so I was sick for %s days." % (number, day)
'I ate 10 apples. so I was sick for three days.'
```

#### 4) 2개 이상의 값 넣기

```
>>> number = 10
>>> day = "three"
>>> "I ate %d apples. so I was sick for %s days." % (number, day)
'I ate 10 apples. so I was sick for three days.'
```


## 길이 

내장함수**len**

```
  In [1]: a = 'holla hi hello ni hao 안녕'

  In [2]: len(a)
  Out[2]: 24

```


### 문자열 나누기(split)

문자열의 내장함수 **split**을 사용  
**split**함수에 인자로 주어진 **구분자**를 기준으로 하나의 문자열을 리스트 형태로 반환해준다.

```
In [78]: girlsday = "민아,유라,소진,혜리"

In [79]: girlsday.split(',')
Out[79]: ['민아', '유라', '소진', '혜리']

In [80]: girlsday.split(' ')
Out[80]: ['민아,유라,소진,혜리']
```

**split**함수에 인자를 주지 않을 경우, 공백문자를 구분자로 사용한다.


## 문자열 결합(join)

**split** 함수와 반대의 역할을 한다.  
문자열 리스트를 하나의 문자열로 결합해주며, 각 문자열을 결합해줄 구분자 문자열을 지정한 후 **join**함수를 사용해준다.

```
 girlsday_list = girlsday.split(',')

 girlsday_str = ', '.join(girlsday_list)

 print(girlsday_str)
 민아, 유라, 소진, 혜리
```


## 대소문자 다루기 

```
 lux = 'lux, the Lady of Luminosity'

 lux.capitalize()
 'Lux, the lady of luminosity'

 lux.title()
 'Lux, The Lady Of Luminosity'

 lux.upper()
 'LUX, THE LADY OF LUMINOSITY'

 lux.lower()
 'lux, the lady of luminosity'

 lux.swapcase()
 'LUX, THE lADY OF lUMINOSITY'
```

## 공식문서

https://docs.python.org/3/library/stdtypes.html#string-method


## 문자열 포맷

#### 옛 스타일 (%)

```
string % data
```

변환타입|설명
---|---
%s	|	문자열 (string)
%d	|	10진수 , 정수 (Integer)
%x	|	16진수 
%o	|	8진수
%f	|	10진 부동소수점수 (floatinf-point)
%e	|	지수로 나타낸 부동소수점수
%g	|	10진 부동소수점수 혹은 지수로 나타낸 부동소수점수
%%	|	리터럴 %


> **%s** 포맷 코드, 이 코드는 어떤 형태의 값이든 변환해 넣을 수 있다.

```
>>> "I have %s apples" % 3
'I have 3 apples'
>>> "rate is %s" % 3.234
'rate is 3.234'
```

3을 문자열 안에 삽입하려면 %d를 사용하고, 3.234를 삽입하려면 %f를 사용해야 한다. 하지만 %s를 사용하면 이런 것을 생각하지 않아도 된다. 왜냐하면 %s는 자동으로 % 뒤에 있는 값을 문자열로 바꾸기 때문이다.

> 문자열 포맷 코드인 %d와 %가 같은 문자열 내에 존재하는 경우, %를 나타내려면 반드시 %%로 써야 하는 법칙이 있다.
> 

```
>>> "Error is %d%%." % 98
'Error is 98%.'
```

## 포맷 코드와 숫자 함께 사용하기

> %d, %s 등의 포맷 코드는 문자열 내에 어떤 값을 삽입하기 위해서 사용된다. 하지만 포맷 코드를 숫자와 함께 사용하면 더 유용하게 사용할 수 있다. 다음의 예를 보고 따라 해보자.
 
1) 정렬과 공백

```
>>> "%10s" % "hi"
'        hi'
```
**"%10s"** 의 의미는 전체 길이가 10개인 문자열 공간에서 hi를 오른쪽으로 정렬하고 그 앞의 나머지는 공백으로 남겨 두라는 의미이다.

```
 >>> "%-10sjane." % 'hi'
'hi        jane.'
```

2) 소수점 표현하기 
 
```
>>> "%0.4f" % 3.42134234
'3.4213'
```
'.'의 의미는 소수점 포인트를 말하고 그 뒤의 숫자 4는 소수점 뒤에 나올 숫자의 개수를 말한다. 

```
>>> "%10.4f" % 3.42134234
'    3.4213'
```
3.42134234라는 숫자를 소수점 네 번째 자리까지만 표시하고 전체 길이가 10개인 문자열 공간에서 오른쪽으로 정렬하는 예를 보여준다.