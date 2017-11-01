---
layout: post
title: Model Field 3
description: "Model field reference 정리하기 3"
modified: 2017-10-16
tags: [Django]
categories: [Django]
---

## FilePathField

#### class FilePathField(path=None, match=None, recursive=False, max_length=100, **options)[[source]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/#FilePathField)


**CharField**는 파일 시스템의 특정 디렉토리에있는 파일 이름으로 제한됩니다. 세 가지 특수한 arguments가 있으며 그 중 첫 번째 arguments이 필요하다.


### FilePathField.path

필수 사항. 이 **FilePathField**가 선택 사항을 가져올 디렉토리에 대한 절대 파일 시스템 경로

예 : `/home/images`

### FilePathField.match

선택 사항. **FilePathField**가 파일 이름을 필터링하는 데 사용할 정규 표현식입니다. 정규 표현식은 전체 경로가 아닌 기본 파일 이름에 적용됩니다. 

예 : `foo.*\.txt$`

foo23.txt이지만 bar.txt 또는 foo23.png 파일은 일치하지 않습니다. 


### FilePathField.recursive

선택 사항. **True or False**. 기본값은 **False**입니다. **path**의 모든 하위 디렉토리를 포함해야하는지 여부를 지정합니다. 

### FilePathField.allow_files

선택적. **True or False**. 기본값은 **True**입니다. 지정된 위치의 파일을 포함할지 여부를 지정합니다. 또는 **allow_folders**는 **True** 여야합니다. 


### FilePathField.allow_folders

선택 사항. True or False. 기본값은 False입니다. 지정된 위치의 폴더를 포함할지 여부를 지정합니다. 또는 **allow_files**는 **True** 여야합니다.

물론 이러한 인수를 함께 사용할 수 있습니다. 

하나의 잠재적 인 문제는 전체 경로가 아닌 기본 파일 이름에 일치가 적용된다는 것입니다.

#### so, this example:

```python

FilePathField(path="/home/images", match="foo.*", recursive=True)

```

`/home/images/foo.png`는 일치하지만 `/home/images/foo/bar.png`는 일치하지 않습니다.
기본 파일 이름 (foo.png 및 bar.png)에 적용되기 때문입니다.

**FilePathField** 인스턴스는 기본 최대 길이가 100자인 **varchar** 열로 데이터베이스에 만들어집니다. 다른 필드와 마찬가지로 **max_length** 인수를 사용하여 최대 길이를 변경할 수 있습니다.


## FloatField 

#### class FloatField (** options) [[source]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/#FloatField)

Python에서 **float** 인스턴스로 표현 된 부동 소수점 숫자. 이 필드의 기본 양식 위젯은 localize가 **False**이거나 **TextInput**이면 **NumberInput**입니다.


> Note: FloatField 대 DecimalField 
> 
>FloatField 클래스는 때때로 DecimalField 클래스와 혼합됩니다. 둘 다 실수를 나타내지 만 그 수를 다르게 나타냅니다. FloatField는 내부적으로 Python의 float 유형을 사용하고 DecimalField는 Python의 Decimal 유형을 사용합니다. 두 함수의 차이점에 대한 정보는 십진수 모듈에 대한 파이썬 문서를 참조하십시오.
>


## ImageField

#### class ImageField(upload_to=None, height_field=None, width_field=None, max_length=100, **options)[[source]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/files/#ImageField)


**FileField**의 모든 속성과 메서드를 상속하지만 업로드 된 객체가 유효한 이미지인지 확인합니다. **FileField**에 사용할 수있는 특수 특성 외에 **ImageField**에도 **height** 및 **width** 특성이 있습니다. 이러한 속성에 대한 쿼리를 용이하게하기 위해 **ImageField**에는 두 개의 추가 옵션 인수가 있습니다. 

### ImageField.height_field

모델 인스턴스가 저장 될 때마다 이미지 높이로 자동 채워지는 모델 필드의 이름입니다. 

### ImageField.width_field

모델 인스턴스의 이름이 저장 될 때마다 이미지 너비가 자동으로 채워지는 모델 필드의 이름. 

#### [pillow](https://pillow.readthedocs.io/en/latest/) 라이브러리가 필요합니다. 

**ImageField** 인스턴스는 기본 최대 길이가 100자인 **varchar** 열로 데이터베이스에 만들어집니다. 다른 필드와 마찬가지로 **max_length** 인수를 사용하여 최대 길이를 변경할 수 있습니다. 

이 필드의 기본 양식 위젯은 **ClearableFileInput**입니다.

## IntegerField

#### class IntegerField (** options) [[source]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/#IntegerField) 

정수입니다. -2147483648에서 2147483647까지의 값은 장고가 지원하는 모든 데이터베이스에서 안전합니다. 
이 필드의 기본 양식 위젯은 **localize**가 **False**일 때 **NumberInput**이고 그렇지 않으면 **TextInput**입니다.

## GenericIPAddressField

#### class GenericIPAddressField (protocol = 'both', unpack_ipv4 = False, ** options) [[source]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/#GenericIPAddressField)

IPv4 또는 IPv6 주소 (문자열 형식, 192.0.2.30 또는 2a02 : 42fe :: 4). 이 필드의 기본 양식 위젯은 TextInput입니다. 

IPv6 주소 정규화는 RFC 4291 섹션 2.2 섹션 2.2를 따르며, 그 섹션의 3 단락에서 제안 된 IPv4 포맷 (예 : ffff : 192.0.2.0)을 사용합니다. 예를 들어 2001 : 0 :: 0 : 01은 2001 :: 1로 표준화되고 :: ffff : 0a0a : 0a0a는 :: ffff : 10.10.10.10으로 정규화됩니다. 모든 문자는 소문자로 변환됩니다. 

### GenericIPAddressField.protocol

지정된 프로토콜에 대한 유효한 입력을 제한합니다. 허용되는 값은 'both'(기본값), 'IPv4'또는 'IPv6'입니다. 일치는 대소 문자를 구분하지 않습니다. 

### GenericIPAddressField.unpack_ipv4 

:: ffff : 192.0.2.1과 같은 IPv4 매핑 주소의 압축을 풉니 다. 이 옵션을 사용하면 주소가 192.0.2.1로 압축 해제됩니다. 기본값은 사용 불가능합니다. 프로토콜이 'both'로 설정된 경우에만 사용할 수 있습니다. 

공백 값을 허용하는 경우 공백 값은 null로 저장되므로 null 값을 허용해야합니다.


## NullBooleanField 

#### class NullBooleanField (** options) [[source link:]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/#NullBooleanField)

**BooleanField**와 비슷하지만 **NULL** 중 하나를 옵션으로 허용합니다. **BooleanField** 대신 **null = True**를 사용하십시오. 이 필드의 기본 양식 위젯은 **NullBooleanSelect**입니다.


## PositiveIntegerField

#### class PositiveIntegerField (** options) [[source]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/#PositiveIntegerField)

**IntegerField**와 비슷하지만 양수 또는 영 (0)이어야합니다. 0에서 2147483647 사이의 값은 장고가 지원하는 모든 데이터베이스에서 안전합니다. 이전 버전과의 호환성을 위해 0 값이 허용됩니다. 

## PositiveSmallIntegerField

#### class PositiveSmallIntegerField (** options) [[source]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/#PositiveIntegerField)

**PositiveIntegerField**와 비슷하지만 특정 (데이터베이스 종속적 인) 점에서만 값을 허용합니다. 0에서 32767 사이의 값은 장고가 지원하는 모든 데이터베이스에서 안전합니다. 

## SlugField

#### SlugField (max_length = 50, ** options) [[source]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/#SlugField)

슬러그는 신문 용어입니다. 슬러그는 글자, 숫자, 밑줄 또는 하이픈 만 포함하는 짧은 레이블입니다. 일반적으로 URL에 사용됩니다. 

**CharField**와 마찬가지로 **max_length**를 지정할 수 있습니다 (이 절에서 데이터베이스 이식성 및 **max_length**에 대한 참고 사항도 참조하십시오). **max_length**가 지정되지 않으면 Django는 기본 길이 인 50을 사용합니다. 

**Field.db_index**를 **True**로 설정합니다. 

다른 값의 값을 기반으로 SlugField를 자동으로 미리 채울 때 유용합니다. **prepopulated_fields**를 사용하여 관리자에서 자동으로이 작업을 수행 할 수 있습니다. 

#### SlugField.allow_unicod

**True**면 이 필드는 ASCII 문자 외에도 유니 코드 문자를 허용합니다. 기본값은 **False**입니다.


## SmallIntegerField

#### class SmallIntegerField (** options) [[source]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/#SmallIntegerField)

**IntegerField**처럼 특정 (데이터베이스 종속적 인) 점에서만 값을 허용합니다. -32768에서 32767 사이의 값은 장고가 지원하는 모든 데이터베이스에서 안전합니다. 

## TextField 

#### class TextField (** options) [[source]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/#TextField)

큰 텍스트 필드. 이 필드의 기본 양식 위젯은 Textarea입니다. 

**max_length** 속성을 지정하면 자동 생성 양식 필드의 **Textarea** 위젯에 반영됩니다. 그러나 모델 또는 데이터베이스 수준에서는 적용되지 않습니다. **CharField**를 사용하십시오. 

## TimeField 

#### class TimeField (auto_now = False, auto_now_add = False, ** options) [[source]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/#TimeField)

Python에서 **datetime.time** 인스턴스로 표현되는 시간. **DateField**와 동일한 자동 채우기 옵션을 적용합니다. 

이 필드의 기본 양식 위젯은 **TextInput**입니다. 관리자가 몇 가지 JavaScript 바로 가기를 추가합니다.

## URLField

#### class URLField (max_length = 200, ** options) [[source link:]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/#TimeField) 

URL의 **CharField**입니다. 

이 필드의 기본 양식 위젯은 **TextInput**입니다. 모든 **CharField** 서브 클래스와 같이 **URLField**는 선택적 **max_length** 인수를 취합니다. **max_length**를 지정하지 않으면 기본값 200이 사용됩니다. 

## UUIDField

#### class UUIDField (** options) [[source link:]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/#UUIDField)

범용 적으로 고유 한 식별자를 저장하기위한 필드. 파이썬의 UUID 클래스를 사용합니다. **PostgreSQL**에서 사용될 때 이것은 **uuid** 데이터 유형에 저장되고, 그렇지 않으면 **char(32)**에 저장됩니다. 

범용 적으로 고유 한 식별자는 **primary_key**에 대한 **AutoField** 대신 사용할 수있는 좋은 방법입니다. 데이터베이스는 **UUID**를 생성하지 않으므로 기본값을 사용하는 것이 좋습니다.


```python

import uuid
from django.db import models

class MyUUIDModel(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    # other fields
    
```

> UUID의 인스턴스가 아니라 호출 가능 객체 (괄호 생략)가 기본값으로 전달된다는 점에 유의하십시오.
> 

