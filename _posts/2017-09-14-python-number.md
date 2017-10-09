---
layout: post
title: Python - Number
description: "python study"
modified: 2017-09-14
tags: [python]
---

# python 숫자형 (Number)


## 정수형 

정수형(Integer)이란 말 그대로 정수를 뜻하는 자료형을 말한다. 다음 예는 양의 정수와 음의 정수, 숫자 0을 변수 a에 대입하는 예이다.

```
>>> a = 123
>>> a = -178
>>> a = 0
```
## 실수형

파이썬에서 실수형(Floating-point)은 소수점이 포함된 숫자를 말한다. 다음 예는 실수를 변수 a에 대입하는 예이다.
```
>>> a = 1.2
>>> a = -3.45
```
 우리가 일반적으로 볼 수 있는 실수형의 소수점 표현 방식이다.
```
>>> a = 4.24E10
>>> a = 4.24e-10
```
> 여기서 **4.24E10**은 4.24∗10104.24∗1010, **4.24e-10**은 4.24∗10−104.24∗10−10을 의미한다.


## 8진수와 16진수
8진수(Octal)를 만들기 위해서는 숫자가 0o 또는 0O(숫자 0 + 알파벳 소문자 o 또는 대문자 O)로 시작하면 된다.

```
>>> a = 0o177
```
16진수(Hexadecimal)를 만들기 위해서는 0x로 시작하면 된다.
```
>>> a = 0x8ff
>>> b = 0xABC
```
8진수나 16진수는 파이썬에서 잘 사용하지 않는 형태의 숫자 자료형이니 간단히 눈으로 익히고 넘어가자.

## 변수 

파이썬은 모든 (정수, 문자열, 함수)이 객체 (object)로 이루어져 있다.
객체는 데이터의 형태를 결정해주는 타입으로, 파이썬에서는 객체의 타입을 바꿀 수 없다. 

변수를 선언하면 -> 객체의 메모리 주소를 가리킨다. 

> 일반적으로, 프로그래밍 언어에서 같다(Equal)의 의미는 `=`이 아닌 `==`이 담당한다.

변수는 단지 이름일 뿐이며, 그 자체가 어떤 값을 갖는것이 아니다.

```
  var1 = 100
  var2 = var1
  var3 = var1
  var4 = var1
```
어떠한 변수가 참조하고 있는 객체가 메모리 상에서 가지고 있는 고유 주소를 출력하는 (id) 내장함수를 사용한다. 

```
  id(var1) 4520513888
  id(var2) 4520513888
  id(var3) 4520513888
  id(var4) 4520513888
```

모든 변수들이 같은 객체를 가리킨다.

```
var1 = 101
id(var1)
4520513920
```

## 변수의 타입 확인

내장함수**type**사용

``` 
 type('안녕하세요')
 <class 'str'>
```
문자열은 **str**(문자열)형임을 나타낸다.

위의 출력에서, 클래스(class)는 객체의 타임(정의)를 나타낸다.
`class`와 `type`은 거의 같은 의미로 사용된다.

## 변수의 이름 제한

**사용 가능한 문자**

- 소문자
- 대문자
- 숫자
- 언더스토어(_)

이름은 숫자로 시작할 수 없으며, 언더스코어로 시작하는 변수명은 특별한 처리방법을 따르므로 일반적으로 사용하지 않는다.

**예약어**

아래 예약어는 파이썬 구문을 정의하는데 사용되기 때문에 변수로 사용할 수 없다. 

False, class, finally, is, return,
None, continue, for, lambda, try,
True, def, from, nonlocal, while,
and, del, global, not, with,
as, elif, if, or, yield,
assert, else, import, pass,
break, except, in, raise

**변수의 입력과 출력**

입력은 내장함수 **input**사용

``` 
 var = input()
```	
입력받는 프롬프트를 띄우려고 할 경우, `input`에 문자열을 인자로 전달해 준다. 

```
 var = input ('숫자를 입력해주세요 : ')
```

출력은 내장함수 **print** 사용


# 내장 데이터 타입 (숫자)

## 수학 연산자

연산자|설명|예|결과
---|---|---|---|
\+	| 더하기		| 32 + 7	| 39 
\-	| 빼기		| 82 - 2	| 80
\*	| 곱하기		| 3 * 7	| 21
/	| 나누기		| 7 / 2	| 3.5
//	| 정수나누기	| 7 // 2	| 3
%	| 나머지		| 7 % 3	| 1
**	| 지수		| 2**10	| 1024

## 산술 연산자 결합 

a에 100을 할당하고, 3을 뺀 결과를 다시 a에 할당한다.

```
 a = 100
 result = a - 3
 a = result
 print(a)
 97
```

위 코드는 아래와 같이 줄여서 사용 가능

```
a = 100
a = a -3
print(a)
97

```
산술 연산자 결합으로 

```
a = 100
a -= -3
print(a)
97

```
x의 y제곱을 나타내는 ** 연산자

```
>>> a = 3
>>> b = 4
>>> a ** b
81
```
## 우선순위

```
 10 + 5 * 4
```
우선 순위 규칙이 적용 되지만, 가독석에 문제가 있을 경우 괄호호 묶어준다.

```
 20 + (300 + 25 * 4)
```

## 진수(base)

기본적으로 숫자형 데이터는 10진수로 간주되지만, 파이썬에서는 2진수, 8진수, 16진수 표현 가능

- 2진수(**b**inary): **0b**또는 **0B**로 시작
- 8진수(**o**ctal): **0o**또는 **0O**로 시작
- 16진수(**h**ex): **0x**또는 **0X**로 시작

![](///Users/janggunhee/Documents/md-file/images/base.png)

## 형변환 

내장함수 **int**, **float**를 사용

```
int("35")
35
```
