---
layout: post
title: Model Field 
description: "Model field reference 정리하기 1"
modified: 2017-10-16
tags: [django]
categories: [django]
---

# Model field reference

Django가 제공하는 필드 옵션과 필드 유형을 포함하여 필드의 모든 API 참조를 포함 합니다 

# Field options

다음 인수들은 모든 필드 유형에서 사용할 수 있습니다

## null 

### field.null 

**True**이면 Django는 빈 값을 **NULL**로 데이터베이스에 저장합니다. 
기본값은 **False**입니다.

문자열 기반 필드가 `null = True`이면 'no data'의 두 가지 값이 가능하다  
`:NULL`, 그리고 빈 스트링 `''`

대부분의 경우 '데이터 없음'에 대해 가능한 두 가지 값을 갖는 것은 불필요합니다. 
Django 규칙은 **NULL**이 아닌 빈 문자열을 사용하는 것입니다.

한 가지 예외는 **CharField**에 `unique = True`와 `blank = True`가 설정된 경우입니다.
**null = 빈 값**으로 여러 객체를 저장할 때 고유 제한 조건 위반을 피하려면 **True**가 필요합니다.

이 경우 빈 값으로 여러 오브젝트를 저장할 때 고유 제한 조건 위반을 피하려면 `null = True`가 필요합니다.

문자열 기반 및 비 문자열 기반 필드의 경우 **null** 매개 변수가 데이터베이스 저장소에만 영향을 주기 때문에 양식에서 빈 값을 허용하려면 **blank = True**로 설정해야합니다.

## blank

### Field.blank

**True**이면 필드는 비워 둘 수 있습니다. 기본값은 **False**입니다. 

**blank**는  **null**과 다릅니다. **null**은 순전히 데이터베이스와 관련된 반면 blank는 유효성 검사와 관련이 있습니다. 
필드에 `blank = True`가 있으면 폼 유효성 검사에서 빈 값을 입력 할 수 있습니다. 
필드에 `blank = False`가 있으면 필드가 필요합니다.

## Choices

### Field.choices


순회가능한 (예: list 와 tuple)로 이루어진 정확히 두 항목 (예 : **[(A, B), (A, B) ...]**)의 반복 가능한 항목은 이 표준 텍스트 필드의 `choices` 항목으로 사용합니다. 

튜플의 첫 번째 요소는 모델에 설정 될 실제 값이며,
두 번째 요소는 사람이 읽을 수있는 이름입니다.

```python

YEAR_IN_SCHOOL_CHOICES = (
    ('FR', 'Freshman'),
    ('SO', 'Sophomore'),
    ('JR', 'Junior'),
    ('SR', 'Senior'),
)

```

일반적으로 모델 클래스 내에서 선택 사항을 정의하고 각 값에 대해 적절히 명명 된 상수를 정의하는 것이 가장 좋습니다.

```python

from django.db import models

class Student(models.Model):
    FRESHMAN = 'FR'
    SOPHOMORE = 'SO'
    JUNIOR = 'JR'
    SENIOR = 'SR'
    YEAR_IN_SCHOOL_CHOICES = (
        (FRESHMAN, 'Freshman'),
        (SOPHOMORE, 'Sophomore'),
        (JUNIOR, 'Junior'),
        (SENIOR, 'Senior'),
    )
    year_in_school = models.CharField(
        max_length=2,
        choices=YEAR_IN_SCHOOL_CHOICES,
        default=FRESHMAN,
    )

    def is_upperclass(self):
        return self.year_in_school in (self.JUNIOR, self.SENIOR)

```
모델 클래스 외부에서 선택 목록을 정의한 다음 참조 할 수는 있지만 모델 클래스 내의 각 선택 항목에 대한 선택 사항과 이름을 정의하면 해당 정보를 사용하는 클래스와 모든 정보가 유지되고 선택 사항을 쉽게 참조 할 수 있습니다.
조직 목적으로 사용할 수있는 명명 된 그룹으로 사용 가능한 선택 사항을 수집 할 수도 있습니다.
```python

MEDIA_CHOICES = (
    ('Audio', (
            ('vinyl', 'Vinyl'),
            ('cd', 'CD'),
        )
    ),
    ('Video', (
            ('vhs', 'VHS Tape'),
            ('dvd', 'DVD'),
        )
    ),
    ('unknown', 'Unknown'),
)

```
각 튜플의 첫 번째 요소는 그룹에 적용 할 이름입니다. 
두 번째 요소는 2- 튜플의 반복 가능이며 
각 2- 튜플에는 옵션에 대한 값과 사람이 읽을 수있는 이름이 들어 있습니다. 
그룹화 된 옵션은 단일 리스트 내의 그룹화되지 않은 옵션과 결합 될 수 있습니다.

Django는 **choices set**이 있는 각 모델 필드에 대해 필드의 현재 값에 대한 사람이 읽을 수 있는 이름을 검색하는 '**get_FOO_display()**'메소드를 추가합니다

선택 사항은 모든 반복 가능한 객체 일 수 있습니다. 반드시 목록 또는 튜플 일 필요는 없습니다.
그러나 스스로 동적인 **choices**를 해킹하는 경우, **ForeignKey**를 사용하여 적절한 데이터베이스 테이블을 사용하는 것이 더 나을 것입니다.

**blank=False** 기본값과 함께 field에 설정되어 있지 않으면 **"--------"**가 포함된 레이블이 select box와 함께 렌더링 됩니다. 이 동작을 무시하려면 **None을** 포함하는 **choice** 튜플에 추가 한다. 
그렇지 않으면, **None** 대신에 빈 문자열을 **Charfeild**와 같이 적절한 곳에서 사용할 수 있다.

## db_column

### Field.db_column

이 필드에 사용할 데이터베이스 column의 이름이 주어지지 않으면 장고는 필드의 이름을 사용합니다.

데이터베이스 column 이름이 SQL 예약어이거나 Python 변수 이름에서 허용되지 않는 문자를 포함하면 - 하이픈- 은 괜찮다. Django는 뒤에서 열과 테이블 이름을 인용합니다.

## db_index

### Field.db_index

**True**이면 이 필드에 대해 데이터베이스 인덱스가 생성됩니다.


## db_tablespace

### Field.db_tablespace

이 필드의 색인이 작성된 경우,이 필드의 색인에 사용할  database tablespace의 이름. 그 기본값은 프로젝트의 **DEFAULT_INDEX_TABLESPACE** 설정 (설정된 경우) 또는 모델의 **db_tablespace** (있는 경우)입니다. 백엔드가 인덱스의 테이블 공간을 지원하지 않으면 이 옵션은 무시됩니다.

## default

### Field.default

필드의 기본값입니다. 값 또는 호출 가능 객체 일 수 있습니다. 호출 가능하면 새로운 객체가 생성 될 때마다 호출됩니다.

기본값은 변경 가능한 객체 (model instance, **list**, **set** 등) 일 수 없습니다. 해당 객체의 동일한 인스턴스에 대한 참조가 모든 새 모델 인스턴스의 기본값으로 사용됩니다.

대신 원하는 기본값을 호출 가능 코드로 래핑하십시오. 예를 들어, **JSONField**의 기본 **dict**를 지정하려면 다음 함수를 사용하십시오.

```python 

def contact_default():
    return {"email": "to1@example.com"}

contact_info = JSONField("ContactInfo", default=contact_default)

```

**lambda**는 **migration**에 의해 직렬화 될 수 없기 때문에 **default**와 같은 field options에 사용할 수 없습니다. 

모델 인스턴스에 매핑되는 **ForeignKey**와 같은 필드의 경우, 기본값은 모델 인스턴스 대신 참조하는 필드 값 (**to_field**가 설정되지 않은 경우 **pk**)이여야합니다.

기본값은 새 모델 인스턴스가 만들어지고 값이 필드에 제공되지 않을 때 사용됩니다. 필드가 primary key인 경우, 그 기본값 또한 field는 **None**으로 설정 되었을 때 사용됩니다.

## editable

### Field.editable

**False** 인 경우 필드는 관리자 또는 다른 **ModelForm**에 표시되지 않습니다. 또한 모델 유효성 검사 도중 건너 뜁니다. 기본값은 **True**입니다.

## error_messages

### Field.error_messages

**error_messages** 인수를 사용하면 필드에서 발생시키는 기본 메시지를 대체 할 수 있습니다. 덮어 쓰려는 오류 메시지와 일치하는 키가 있는 dictionary을 전달하십시오.

오류 메시지 키에는 **null, blank, invalid, invalid_choice, unique** 및 **unique_for_date**가 포함됩니다. 추가 오류 메시지 키는 아래 필드 유형 섹션의 각 필드에 지정됩니다.

#### [model’s error_messages 에 대해 고려해야 할 것](https://docs.djangoproject.com/en/1.11/topics/forms/modelforms/#considerations-regarding-model-errormessages)

**form field** 레벨 또는 **form Meta** 레벨에서 정의 된 오류 메시지는 항상 model field 레벨에 정의 된 오류 메시지보다 우선합니다.

**NON_FIELD_ERRORS** 키를 **ModelForm** 내부 메타 클래스의 **error_messages** dictionary에 추가하여 모델 유효성 검사로 발생한 **NON_FIELD_ERRORS**에서 오류 메시지를 무시할 수 있습니다.

```python

from django.forms import ModelForm
from django.core.exceptions import NON_FIELD_ERRORS

class ArticleForm(ModelForm):
    class Meta:
        error_messages = {
            NON_FIELD_ERRORS: {
                'unique_together': "%(model_name)s's %(field_labels)s are not unique.",
            }
        }
        
```

## help_text

### Field.help_text

form 위젯과 함께 표시되는 추가 'help'텍스트는 field가 from을 사용하지 않아도 문서화 하는데 편리하다.

이 값은 자동 생성 양식에서 HTML 이스케이프 처리되지 않습니다. 원하는 경우 **help_text**에 HTML을 포함시킬 수 있습니다. 예 :

```python

help_text="Please use the following format: <em>YYYY-MM-DD</em>."

```

또한 일반 텍스트와 `django.utils.html.escape ()`를 사용하여 HTML 특수 문자를 이스케이프 처리 할 수 있습니다. 

cross-site 스크립팅 공격을 피하기 위해 신뢰할 수 없는 사용자로부터 온 도움말 텍스트를 이스케이프해야합니다.

## primary_key

### Field.primary_key

**Primary_key=True**이면 이 필드는 모델의 기본 키입니다. 

모델의 모든 필드에 대해 **primary_key = True**를 지정하지 않으면 Django는 기본 키를 보유 할 자동 필드를 자동으로 추가합니다. 기본 기본 키 동작을 덮어 쓰지 않으려면 모든 필드에서 **primary_key = True****를 설정할 필요가 없습니다.

**primary_key = True**는 **null = False** 및 **unique = True**를 의미합니다. 하나의 기본 키만 객체에 허용됩니다.

기본 키 필드는 읽기 전용입니다. 기존 개체의 기본 키 값을 변경 한 다음 저장하면 이전 개체와 함께 새 개체가 만들어집니다.

## unique

### Field.unique

**unique=True**, 이 필드는 테이블 전체에서 고유해야합니다.

이는 데이터베이스 레벨 및 모델 검증에 의해 시행됩니다. 고유 한 필드에 중복 값이 있는 모델을 저장하려고하면 모델의 **save ()** 메소드에 의해 **django.db.IntegrityError**가 발생합니다.

이 옵션은 **ManyToManyField** 및 **OneToOneField**를 제외한 모든 필드 유형에 유효합니다.

**unique=True** 일 때 **unique**은 인덱스 생성을 의미하기 때문에 **db_index**를 지정할 필요가 없습니다.


## unique_for_date

### Field.unique_for_date

이것을 **DateField** 또는 **DateTimeField**의 이름으로 설정하여이 필드가 날짜 필드의 값에 대해 고유해야합니다.

예를 들어, **unique_for_date = 'pub_date'**인 필드 제목이 있으면 Django는 같은 제목과 **pub_date**를 가진 두 개의 레코드를 입력 할 수 없습니다.

**DateTimeField**를 가리 키도록 설정하면 필드의 날짜 부분 만 고려됩니다. 게다가 **USE_TZ=True** 일 때, 객체가 저장 될 때 현재 시간대에서 검사가 수행됩니다.

## unique_for_month 

### Field.unique_for_month

**unique_for_date**와 비슷하지만 해당 달에 대해 필드가 고유해야합니다. 

## unique_for_year 

### Field.unique_for_year

**unique_for_date** 및 **unique_for_month**와 같습니다. 

## verbose_name

### Field.verbose_name 

사람이 읽을 수 있는 필드 이름, 자세한 이름이 주어지지 않으면 Django는 필드의 속성 이름을 사용하여 밑줄을 공백으로 변환하여 자동으로 생성합니다. 

[Verbose field names](https://docs.djangoproject.com/en/1.11/topics/db/models/#verbose-field-names)

이 예제에서 `verbose name`은 'person 's first name'입니다.

```python

first_name = models.CharField("person's first name", max_length=30)

```

이 예제에서, verbose name은 "first name"이다.:

```python

first_name = models.CharField(max_length=30)

```

ForeignKey, ManyToManyField 및 OneToOneField에는 첫 번째 인수가 모델 클래스가되어야하므로 verbose_name 키워드 인수를 사용하십시오.

```python

poll = models.ForeignKey(
    Poll,
    on_delete=models.CASCADE,
    verbose_name="the related poll",
)
sites = models.ManyToManyField(Site, verbose_name="list of sites")
place = models.OneToOneField(
    Place,
    on_delete=models.CASCADE,
    verbose_name="related place",
)

```
verbose_name의 첫 문자를 대문자로 사용하지 않습니다. Django는 필요한 첫 문자를 자동으로 대문자로 표시합니다.


## validators 

### Field.validators

이 필드에 실행할 검사기 목록입니다. 자세한 내용은  [validators 설명서](https://docs.djangoproject.com/en/1.11/ref/validators/)를 참조하십시오.

필드는  [lookup registration API](https://docs.djangoproject.com/en/1.11/ref/models/lookups/#lookup-registration-api) 를 구현합니다. API를 사용하여 필드 클래스에 사용할 수있는 조회와 필드에서 조회를 가져 오는 방법을 사용자 정의 할 수 있습니다.


validator(유효성 검사기)는 값을 가져 와서 일부 조건을 충족시키지 않으면 **ValidationError**를 발생시키는 호출 가능 함수입니다. 
유효성 검사기는 다른 유형의 필드간에 유효성 검사 논리를 다시 사용하는 데 유용 할 수 있습니다. 
예를 들어, 짝수 만 허용하는 유효성 검사기는 다음과 같습니다.

```python

from django.core.exceptions import ValidationError
from django.utils.translation import ugettext_lazy as _

def validate_even(value):
    if value % 2 != 0:
        raise ValidationError(
            _('%(value)s is not an even number'),
            params={'value': value},
        )
        
```

필드의 **validators** argument를 통해 모델 필드에 추가 할 수 있습니다.

```python 

from django.db import models

class MyModel(models.Model):
    even_field = models.IntegerField(validators=[validate_even])
    
```
validators가 실행되기 전에 값이 Python으로 변환되기 때문에 form과 동일한 validators를 사용할 수도 있습니다.

```
from django import forms

class MyForm(forms.Form):
    even_field = forms.IntegerField(validators=[validate_even])
```
더 복잡하거나 구성 가능한 유효성 검사기에 **__call __ ()** 메서드가있는 클래스를 사용할 수도 있습니다. 예를 들어, **RegexValidator**는 이 기술을 사용합니다. 클래스 기반 유효성 검사기가 유효성 검사기 모델 필드 옵션에서 사용되는 경우 **deconstruct()** 및 **__eq __ ()** 메서드를 추가하여 마이그레이션 프레임 워크에서 해당 클래스를 직렬화 할 수 있는지 확인해야합니다.

## Field types

### AutoField

class AutoField (** options)

사용 가능한 ID에 따라 자동으로 증가하는 IntegerField. [[source:link]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/#AutoField)
보통 이것을 직접 사용할 필요는 없습니다. 별도로 지정하지 않으면 기본 키 필드가 자동으로 모델에 추가됩니다. [(Automatic primary key fields)](https://docs.djangoproject.com/en/1.11/topics/db/models/#automatic-primary-key-fields)

```
id = models.AutoField(primary_key=True)
```
## BigAutoField

### class BigAutoField(**options)[[source:link]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/#BigIntegerField)

`New in Django 1.10`

1에서 9223372036854775807까지의 숫자에 맞도록 보장된다는 점을 제외하고는 AutoField와 매우 유사한 64 비트 정수입니다.

## BigIntegerField

### class BigIntegerField(**options)[[source:link]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/#BigIntegerField)

-9223372036854775808에서 9223372036854775807까지의 숫자를 맞출 수 있다는 것을 제외하고는 IntegerField와 매우 흡사 한 64 비트 정수입니다.이 필드의 기본 양식 위젯은 TextInput입니다.


## BinaryField

### class BinaryField(**options)[[source:link]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/#BinaryField)

원 이진 데이터를 저장하는 필드입니다. 바이트 할당 만 지원합니다. 
이 입력란에는 기능이 제한되어 있습니다. 예를 들어, BinaryField 값에 대한 쿼리 집합을 필터링 할 수 없습니다. 
또한 BinaryField를 ModelForm에 포함시키는 것도 불가능합니다.

> note: BinaryField의 악용 
>데이터베이스에 파일을 저장하는 것에 대해 생각할 수도 있지만, 99 %의 경우에는 잘못된 디자인이라고 생각하십시오. 이 필드는 적절한 정적 파일 처리를 대체하지 않습니다.
>

## BooleanField

### class BooleanField (** options) [[source:link]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/#BooleanField) 

true / false 필드. 

이 필드의 기본 양식 위젯은 **CheckboxInput**입니다. 

**null** 값을 받아 들일 필요가 있다면 대신 **NullBooleanField**를 사용하십시오. 

**Field.default**가 정의되어 있지 않으면 **BooleanField**의 기본값은 **None**입니다.

## CharField

### class CharField (max_length = None, ** options) [[source]]
작은 문자열에서 큰 문자열까지의 문자열 필드. 

대량의 텍스트의 경우 **TextField**를 사용하십시오. 

이 필드의 기본 양식 위젯은 **TextInput**입니다. 

**CharField**에는 하나의 추가 인수가 필요합니다 : 

**CharField.max_length**

	필드의 최대 길이 (문자 수)입니다. max_length는 데이터베이스 레벨과 Django의 유효성 검사에서 적용됩니다.
    
    
## CommaSeparatedIntegerField

### class CommaSeparatedIntegerField(max_length=None, **options)[source:link](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/#CommaSeparatedIntegerField)

	버전 1.9부터는 사용되지 않습니다 : 
	이 필드는 CharField와 함께 validators = [validate_comma_separated_integer_list]와 함께 사용되지 않습니다.
    
 정수 필드는 쉼표로 구분됩니다. **CharField**와 마찬가지로 **max_length** 인수가 필요하며 여기에 언급 된 데이터베이스 휴대성에 대한 참고 사항을 주의해야합니다.
 
 
## DateField

### class DateField(auto_now=False, auto_now_add=False, **options)[[source]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/#DateField)

Python에서 datetime.date 인스턴스로 표현되는 날짜입니다. 추가로 몇 가지 선택적 인수가 있습니다.

### DateField.auto_now

개체가 저장 될 때마다 now every time을 필드에 자동으로 설정합니다. 'last-modified'타임 스탬프에 유용합니다. Note that the current date는 항상 사용됩니다. 재정의 할 수있는 기본값이 아닙니다. 

이 필드는 **Model.save ()** 를 호출 할 때 자동으로 업데이트됩니다. 이 필드는 **QuerySet.update()** 와 같은 다른 방법으로 다른 필드를 업데이트 할 때 업데이트되지 않지만 이와 같은 업데이트에서 필드의 사용자 지정 값을 지정할 수는 있습니다.

### DateField.auto_now_add
 
객체가 처음 생성 될 때 자동으로 필드를 현재로 설정합니다. 타임 스탬프 생성에 유용합니다. 현재 날짜는 항상 사용됩니다. 재정의 할 수있는 기본값이 아닙니다. 따라서 객체를 만들 때이 필드의 값을 설정하더라도 무시됩니다. 이 필드를 수정하려면 **auto_now_add = True** 대신 다음을 설정하십시오.

 - For DateField: default=date.today - from datetime.date.today()
 - For DateTimeField: default=timezone.now - from django.utils.timezone.now()

이 필드의 기본 양식 위젯은 **TextInput** 입니다. 관리자는 JavaScript 캘린더와 'Today'에 대한 바로 가기를 추가합니다. **invalid_date** 오류 메시지 키가 추가로 포함됩니다. 

**auto_now_add**, **auto_now** 및 **default** 옵션은 상호 배타적입니다. 이러한 옵션을 함께 사용하면 오류가 발생합니다.

> Note: 현재 구현 된 것처럼 **auto_now** 또는 **auto_now_add**를 **True**로 설정하면 필드의 **editable=Fals** 및  **blank=True**로 설정됩니다.
>


> Note: **auto_now** 및 **auto_now_add** 옵션은 생성 또는 업데이트 할 때 항상 기본 시간대의 날짜를 사용합니다. 다른 것이 필요한 경우 **auto_now** 또는 **auto_now_add**를 사용하는 대신 자신의 호출 가능 기본값을 사용하거나 **save ()** 를 재정의하는 것이 좋습니다. 또는 **DateField** 대신 **DateTimeField**를 사용하고 표시 시간에 **datetime**에서 **date** 로 변환 처리하는 방법을 결정할 수 있습니다.
>

## DateTimeField

### class DateTimeField (auto_now = False, auto_now_add = False, ** options) [[source link:]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/#DecimalField)

날짜와 시간. 파이썬에서 **datetime.datetime** 인스턴스로 표현됩니다. **DateField** 와 동일한 추가 인수를 사용합니다. 

이 필드의 기본 양식 위젯은 단일 **TextInput** 입니다. 관리자는 JavaScript shortcuts에 있는 두 개의 별도 **TextInput** 위젯을 사용합니다.

## DecimalField 

### class DecimalField(max_digits = None, decimal_places = None, ** options) [[source link:]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/#DecimalField)

고정 소수점 이하의 십진수로 파이썬에서 **Decimal** 인스턴스로 표현됩니다. 두 개의 required arguments가 있습니다. 

### DecimalField.max_digits
숫자에 허용되는 최대 자릿수입니다. 이 수는 **decimal_places**보다 크거나 같아야합니다. 

### DecimalField.decimal_places
숫자와 함께 저장할 소수점 이하 자릿수. 

예를 들어 소수점 이하 두 자리의 해상도로 999까지의 숫자를 저장하려면 다음을 사용하십시오.


	models.DecimalField(..., max_digits=5, decimal_places=2)


소수점 이하 10 자리의 해상도로 약 10 억 개의 숫자 저장 :

	models.DecimalField(..., max_digits=19, decimal_places=10)
    

이 필드의 기본 양식 위젯은 **localize**가 **False** 일 때 **NumberInput** 이고 그렇지 않으면 **TextInput** 입니다.

> Note: FloatField 및 DecimalField 클래스 간의 차이점에 대한 자세한 내용은 [FloatField vs DecimalField](https://docs.djangoproject.com/en/1.11/ref/models/fields/#floatfield-vs-decimalfield)를 참조하십시오.
>

## DurationField

### class DurationField (** options) [[source]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/#DurationField)

시간 구간을 저장하는 필드. 파이썬에서 timedelta로 모델링됩니다. 
PostgreSQL에서 사용되는 데이터 유형 간격이며 Oracle에서는 데이터 유형이 **INTERVAL DAY (9) TO SECOND (6)** 입니다. 그렇지 않으면 microseconds의 **bigint**가 사용됩니다.

> Note : **DurationField**를 사용한 산술은 대부분의 경우에 작동합니다. 그러나 PostgreSQL 이외의 모든 데이터베이스에서 **DurationField**의 값을 **DateTimeField**의 산술 인스턴스와 비교하는 것은 예상대로 작동하지 않습니다.
> 

## EmailField

### class EmailField (max_length = 254, ** options) [[source link:]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/files/#FileField)

값이 유효한 전자 메일 주소인지 확인하는 **CharField** **EmailValidator**를 사용하여 입력의 유효성을 검사합니다.
