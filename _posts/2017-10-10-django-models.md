---
layout: post
title: Django Documentation - Models
description: "Django Documentation Study"
modified: 2017-19-10
tags: [Django]
categories: [Django]
---

## Django Models

> 모델은 데이터에 대한 단일 정보 소스입니다. 여기에는 저장중인 데이터의 필수 필드와 동작이 포함되어 있습니다. 
> 일반적으로 각 모델은 단일 데이터베이스 테이블에 매핑됩니다.모델은 데이터에 대한 단일 정보 소스입니다. 여기에는 저장중인 데이터의 필수 필드와 동작이 포함되어 있습니다. 일반적으로 각 모델은 단일 데이터베이스 테이블에 매핑됩니다.
>

- 각 모델은 [django.db.models.Model](https://docs.djangoproject.com/ko/1.11/ref/models/instances/#django.db.models.Model)을 하위 클래스로 묶는 Python 클래스입니다. 

- 모델의 각 속성은 데이터베이스 필드를 나타냅니다. 

- 이 모든 것을 통해 Django는 자동으로 생성 된 데이터베이스 액세스 API를 제공합니다. [쿼리 만들기](https://docs.djangoproject.com/ko/1.11/topics/db/queries/)를 참조하십시오.

### :: example model

이 예시는 **Person**의 **first_name** 과 **last_name**을 정의한다.

```python
from django.db import models

class Person(models.Model):
    first_name = models.CharField(max_length=30)
    last_name = models.CharField(max_length=30)
```
**first_name**과 **last_name**은 model의 [필드(field)](https://docs.djangoproject.com/ko/1.11/topics/db/models/#fields)입니다. 각 field는  속성으로 지정되며 각 속성은 데이터베이스 열에 매핑됩니다.

`make migrations` 를 하면 

위의 **Person** 모델은 아래와 같은 **database table**을 만들어 냅니다.

 - **class** (Person) 는 **database table**이 되고 
 - **first_name** 과 **lsat_name**은 coloum(database field)이 된다. 

```python
CREATE TABLE myapp_person (
    "id" serial NOT NULL PRIMARY KEY,
    "first_name" varchar(30) NOT NULL,
    "last_name" varchar(30) NOT NULL
);
```

`python manage.py makemigrations`를 하면 sql 실행문이 담긴 migrations 파일이 생성된다. 

## Using models

> 모델을 정의한 후에는 Django에게 해당 모델을 사용할 것이라고 알려야합니다. `settings.py`을 편집하고 `INSTALLED_APPS` 설정을 변경하여 `models.py`가 포함 된 모듈의 이름을 추가하십시오.
> 

- 예를 들어 너의 applicarion이 myapp.models 의 모듈에 있는 경우, [INSTALLED_APPS](https://docs.djangoproject.com/ko/1.11/ref/settings/#std:setting-INSTALLED_APPS)에 applicarion명을 다음과 같이 작성해 주어야 읽는다. 
- 이 pakage 구조는 [`manage.py startapp` ](https://docs.djangoproject.com/ko/1.11/ref/django-admin/#django-admin-startapp) 으로 만들어진 application이다.

`settings.py`
```python
INSTALLED_APPS = [
    #...
    'myapp',
    #...
]
```

- **INSTALLED_APPS**에 새 applicarion을 추가 할 때는 꼭 `manage.py migrate`를 실행해야 한다. 
 
- 선택적으로 `manage.py makemigrations`를 사용하여 마이그레이션을 수행하도록 한다. 
 
- 보통 `model class`를 새로 정의했을때 수행한다. 

## Feilds

> - **Django**에서 모델을 생성하는 필수 요소이고, model의 가장 중요한 파트이다. 이것은 데이터베이스 필드 list의 정의이다.
> - 필드이름을  `clean`, `save`, `delete` 등과 같이 [모델 API](https://docs.djangoproject.com/ko/1.11/ref/models/instances/) 와 동일한 이름으로 생성하지 않도록 주의해야 한다.
> 

```python
from django.db import models

# class 모델이름(models.Model):
#	필드이름1 = models.필드타입(필드옵션)
#	필드이름2 = models.필드타입(필드옵션)

class Musician(models.Model):
    first_name = models.CharField(max_length=50)
    last_name = models.CharField(max_length=50)
    instrument = models.CharField(max_length=100)

class Album(models.Model):
    artist = models.ForeignKey(Musician, on_delete=models.CASCADE)
    name = models.CharField(max_length=100)
    release_date = models.DateField()
    num_stars = models.IntegerField()
```

## [Field types](https://docs.djangoproject.com/ko/1.11/topics/db/models/#field-types)

> 모델의 각 필드는 해당 Field 클래스의 인스턴스 여야합니다. Django는 필드 클래스 유형을 사용하여 몇 가지를 결정합니다.
> 

- 데이터베이스에 저장할 데이터 종류 (예 : INTEGER, VARCHAR, TEXT)를 나타내는 열 유형입니다.

- form field를 렌더링 할 때 사용할 기본 HTML 위젯입니다 (예 : `<input type = "text">, <select>`).

- django 관리자 및 자동생성 양식에서 사용되는 최소 유효성 확인 요구 사항.


> 1.  `Django`에는 수십 가지 내장 필드 유형이 있습니다. [**model field** reference](https://docs.djangoproject.com/ko/1.11/ref/models/fields/#model-field-types)에서 전체 목록을 찾을 수 있습니다.
> 2.  기본 제공하는 모델로 부족할때, custom하게 모델필드를 정의할 수 있다. [Writing custom model fields](https://docs.djangoproject.com/ko/1.11/howto/custom-model-fields/)
(예를 들어: 전화번호 입력해 주는 field, 한국식으로 주소를 입력하는 field)

| 필드타입 |  HTML 위젯	| 필수 옵션 |	설명 |
|--------|:--------:|:-------:|-----|
|[BooleanField](https://docs.djangoproject.com/ko/1.11/_modules/django/db/models/fields/#BooleanField)|	CheckboxInput|	-	|`True/False` 값을 가지는 필드.|
|[CharField](https://docs.djangoproject.com/ko/1.11/_modules/django/db/models/fields/#CharField)| TextInput |	max_length	|문자열 데이터를 저장하는 필드. 최대 글자 수를 반드시 지정해주어야 한다.|
|[DateField](https://docs.djangoproject.com/ko/1.11/_modules/django/db/models/fields/#DateField)	| TextInput |	-	|datetime.date 인스턴스인 날짜 데이터를 저장하는 필드. 달력 위젯과 오늘 날짜 입력 기능을 기본제공한다.|
|[DateTimeField](https://docs.djangoproject.com/ko/1.11/_modules/django/db/models/fields/#DateTimeField)| TextInput |	-   |datetime.datetime 인스턴스인 날짜와 시간 데이터를 저장하는 필드. 두 개의 TextInput, 달력 위젯, 오늘 날짜 입력 기능을 기본제공한다.|
|[FloatField](https://docs.djangoproject.com/ko/1.11/_modules/django/db/models/fields/#FloatField)|	NumberInput |	-|	Python의 float과 같은 실수 데이터를 저장하는 필드.|
|[IntegerField](https://docs.djangoproject.com/ko/1.11/_modules/django/db/models/fields/#IntegerField)|	NumberInput|	-	|Python의 integer과 같은 정수 데이터를 저장하는 필드. -2147483648과 2147483647 사이의 값을 저장할 수 있다.|
|TextField	|Textarea	|-	|글자 수 제한이 없는 문자열 데이터를 저장하는 필드. max_length 값을 지정하면 폼에서는 제한이 되지만, 데이터베이스에는 영향을 주지 않음.|

### [Relationship fields](https://docs.djangoproject.com/ko/1.11/ref/models/fields/#module-django.db.models.fields.related) - 관계 정의 필드

|필드타입 |	HTML 위젯	| 필수 옵션 |	설명 |
|-------|:---------:|:-------:|-----|
|Forignkey|	-	| to, on_delete |	필드를 외래키로 설정한다. 다른 테이블의 레코드와 일대다 관계를 형성한다. 관계 설정 대상이 되는 모델과 레코드 삭제 시 처리 방식을 필수로 설정해주어야 한다.|
|ManytoManyField|	-	| to |	필드가 대상 테이블과 다대다 관계를 형성하도록 설정한다.관계 설정 대상이 되는 모델을 필수로 설정해주어야 한다.|
|OneToOneField|	-	| to, on_delete	|   필드가 대상 테이블과 일대일 관계를 형성하도록 설정한다. 관계 설정 대상이 되는 모델과 레코드 삭제 시 처리 방식을 필수로 설정해주어야 한다.|



## Field options

> 모든 필드에는 여러가지 설정을 변경할 수 있는 필드 옵션을 지정해 줄 수 있습니다. 
> [모델 필드 참조](https://docs.djangoproject.com/ko/1.11/ref/models/fields/#model-field-types)
> 또한, 모든 필드 유형에 사용할 수 있는 일련의 common arguments가 있습니다. 모두 선택 옵션입니다.
> 

###  가장 자주 사용되는 Field options

### :: [null](https://docs.djangoproject.com/ko/1.11/ref/models/fields/#django.db.models.Field.null) 

- `True`이면 Django는 빈 값을 `NULL`로 데이터베이스에 저장합니다. 기본값은 `False`입니다.
- 빈 값으로 여러 오브젝트를 저장할 때 고유 제한 조건 위반을 피하려면 `null = True`가 필요합니다. 


### :: [blank](https://docs.djangoproject.com/ko/1.11/ref/models/fields/#django.db.models.Field.blank)

- `True`이면 필드는 비워 둘 수 있습니다. 기본값은 `False`입니다. 

- blank는 값이 있는 것이다. " " 빈 string으로 database에 저장된다. 

- 이것은 `null`과 다릅니다. `null`은 순전히 데이터베이스와 관련된 반면 `blank`는 유효성 검사와 관련이 있습니다. 

- 필드에 `blank = True`가 있으면 django admin form 유효성 검사에서 빈 값 `" "`을 입력 할 수 있습니다. 필드에 `blank = False`가 있으면 필드가 필수 요소이다.
 
```python
models.DateTimeField(blank=True) # 비어있는 경우 IntegrityError를 발생시킵니다.

models.DateTimeField(null=True) # NULL은 허용되지만 form을 채워야합니다.
```
```
models.CharField(blank=True) # 문제 없습니다. 공백은 ' '로 저장됩니다.

models.CharField(null=True) # NULL은 허용되지만 NULL로 설정되지 않습니다.
```
>  **CHAR**와 **TEXT** 타입은 **Django**에 의해 결코 `NULL`로 저장되지 않으므로, `null = True`는 불필요하다. 
>  그러나 이러한 필드 중 하나를 수동으로 `none`으로 설정하면 강제로 `NULL`로 설정할 수 있습니다. 필요할 수도 있는 시나리오가 있는 경우에도 `null = True` 를 포함 해야합니다. 
>

### :: [choice](https://docs.djangoproject.com/ko/1.11/ref/models/fields/#choices)

 - iterable 한 2개의 (예 : [(A, B), (A, B) ...])의 반복 가능 항목으로 구성된다. (예 : list 또는 tuple)입니다.

- 이것이 주어지면, 기본 양식 위젯은 표준 텍스트 필드 대신이 선택 사항을 가진 select box가됩니다. 

```python
YEAR_IN_SCHOOL_CHOICES = (
    ('FR', 'Freshman'),
    ('SO', 'Sophomore'),
    ('JR', 'Junior'),
    ('SR', 'Senior'),
)
```

- 각 튜플의 **첫 번째 요소**는 데이터베이스에 저장 될 value-값입니다.

- **두 번째 요소**는 기본 양식 위젯 또는 [ModelChoiceField](https://docs.djangoproject.com/ko/1.11/ref/forms/fields/#django.forms.ModelChoiceField), 선택박스에 'Freshman', 'Shphomore' 문자로 사용자에게 표시됩니다.

`models.py`
```
from django.db import models

class Person(models.Model):
    SHIRT_SIZES = (
        ('S', 'Small'),
        ('M', 'Medium'),
        ('L', 'Large'),
    )
    name = models.CharField(max_length=60)
    shirt_size = models.CharField(max_length=1, choices=SHIRT_SIZES)
```
- 모델 인스턴스가 주어지면 선택 필드의 표시 값은 `get_FOO_display ()` 메소드를 사용하여 액세스 할 수 있습니다.

```
>>> p = Person(name="Fred Flintstone", shirt_size="L")
>>> p.save()
>>> p.shirt_size
'L'
>>> p.get_shirt_size_display()
'Large'
```

#### 참고 :: [django Coding style](https://docs.djangoproject.com/en/dev/internals/contributing/writing-code/coding-style/)


### :: [default](https://docs.djangoproject.com/ko/1.11/ref/models/fields/#django.db.models.Field.default)

- 필드의 기본값입니다. 
- 값 또는 호출 가능 객체 일 수 있습니다. 호출 가능하면 새로운 객체가 생성 될 때마다 호출됩니다.
- 필드에 아무것도 입력하지 않을 경우 기본값이 들어간다.


### :: [help_text](https://docs.djangoproject.com/ko/1.11/ref/models/fields/#django.db.models.Field.help_text)

- 필드에 대한 설명을 추가할 수 있다. 관리자 페이지에서 확인 가능.

### :: [primary_key](https://docs.djangoproject.com/ko/1.11/ref/models/fields/#django.db.models.Field.primary_key)

- 모델의 모든 필드에 대해 `primary_key = True`를 지정하지 않으면 Django가 기본 키를 보유 한다. 

- IntegerField를 자동으로 추가하므로 해당 필드를 재정의하지 않는 한 모든 필드에서 `primary_key = True`를 설정할 필요가 없습니다. 

- 기본 기본 키 동작. 자세한 내용은 [Automatic primary key fields](https://docs.djangoproject.com/ko/1.11/topics/db/models/#automatic-primary-key-fields)를 참조하십시오.

- **primary key field**는 read-only입니다. 기존 개체의 primary key의 value를 변경 한 다음 저장하면 새 개체가 이전 개체와 함께 만들어집니다.

`models.py`
```python 
from django.db import models

class Fruit(models.Model):
    name = models.CharField(max_length=100, primary_key=True)
```
`python manage.py shell_plus`

```
>>> fruit = Fruit.objects.create(name='Apple')
>>> fruit.name = 'Pear'
>>> fruit.save()
>>> Fruit.objects.values_list('name', flat=True)
<QuerySet ['Apple', 'Pear']>
```

### :: [unique](https://docs.djangoproject.com/ko/1.11/ref/models/fields/#django.db.models.Field.unique)

 - `unique=True` 면 필드는 항상 테이블 전체에 고유한 값만 가지도록 한다.
 
 - 이것은 데이터베이스 수준 및 모델 검증에 의해 시행됩니다. 고유 한 필드에 중복 값이있는 모델을 저장하려고하면 모델의 `save ()` 메소드에 의해 django.db.IntegrityError가 발생합니다. 
 
 - 이 옵션은 `ManyToManyField` 및 `OneToOneField`를 제외한 모든 필드 유형에 유효합니다. 
 
 - `unique=True이면` db_index를 지정할 필요가 없습니다. unique은 인덱스 생성을 의미하기 때문입니다.


 