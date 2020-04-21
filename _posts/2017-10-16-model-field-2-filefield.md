---
layout: post
title: Model Field 2
description: "Model field reference 정리하기 2"
modified: 2017-10-16
permalink: /:title/
tags: [Django]
categories: [Django]
---


## FileField

### class FileField(upload_to=None, max_length=100, **options)[[source link:]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/files/#FileField)

파일 업로드 필드이다. 

> Note : primary_key 인수는 지원되지 않으며 사용되는 경우 오류가 발생합니다.
>

두 개의 optional 인수가 있습니다.

```
 - FileField.upload_to
 - FileField.storage
```

## FileField.upload_to

이 속성은 업로드 디렉토리와 파일 이름을 설정하는 방법을 제공하며 두 가지 방법으로 설정할 수 있습니다. 
두 경우 모두 값은 **Storage.save()** 메서드에 전달됩니다. 

문자열 값을 지정하면 **strftime()** formtting이 포함될 수 있습니다. 이 형식은 업로드 된 파일이 주어진 디렉토리를 채우지 않도록 파일 업로드 date/time 으로 대체됩니다. 

예 :

```python

class MyModel(models.Model):
    # file will be uploaded to MEDIA_ROOT/uploads
    upload = models.FileField(upload_to='uploads/')
    # or...
    # file will be saved to MEDIA_ROOT/uploads/2015/01/30
    upload = models.FileField(upload_to='uploads/%Y/%m/%d/')
    
```

기본 **FileSystemStorage**를 사용하는 경우 문자열 값이 **MEDIA_ROOT** 경로에 추가되어 업로드 된 파일이 저장 될 로컬 파일 시스템의 위치가 형성됩니다. 다른 저장 용량을 사용하는 경우 저장 용량 설명서에서 **upload_to** 처리 방법을 확인하십시오.

### upload_to 

함수와 같은 호출 가능 함수 일 수도 있습니다. 이것은 파일 이름을 포함하여 업로드 경로를 얻기 위해 호출됩니다. 이 호출 가능 객체는 두 개의 인수를 받아 들여 스토리지 시스템에 전달되는 유닉스 스타일 경로 (슬래시 포함)를 반환해야합니다. 

#### The two arguments are:



| Argument   | 	Description   |
|:-----------|:---------------|
|instance	 | FileField가 정의 된 모델의 인스턴스입니다. 보다 구체적으로, 이것은 현재 파일이 첨부되는 특별한 경우입니다. 대부분의 경우이 객체는 아직 데이터베이스에 저장되지 않았으므로 기본 자동 필드를 사용하는 경우 기본 키 필드의 값이 아직 없을 수 있습니다.    |
|filename    | 원래 파일에 주어진 파일 이름. 최종 목적지 경로를 결정할 때 고려 될 수도 있고 고려되지 않을 수도 있습니다.               |

#### For example:

```python

def user_directory_path(instance, filename):
    # file will be uploaded to MEDIA_ROOT/user_<id>/<filename>
    return 'user_{0}/{1}'.format(instance.user.id, filename)

class MyModel(models.Model):
    upload = models.FileField(upload_to=user_directory_path)
    
```

## FileField.storage

파일의 저장 및 검색을 처리하는 저장 개체입니다. 
이 객체를 제공하는 방법에 대한 자세한 내용은 [Managing files](https://docs.djangoproject.com/en/1.11/topics/files/) 를 참조하십시오.

이 필드의 기본 양식 위젯은 **ClearableFileInput** 입니다.

model에서 **FileField** 또는 **ImageField** (아래 참조)를 사용하면 몇 단계만 거치면됩니다.


 1. 설정 파일에서 Django가 업로드 된 파일을 저장할 디렉토리의 전체 경로로 **MEDIA_ROOT**을 정의해야합니다. 성능을 위해 이러한 파일은 데이터베이스에 저장되지 않습니다. **MEDIA_URL**을 해당 디렉토리의 기본 공개 URL로 정의하십시오. 이 디렉터리에 웹 서버의 사용자 계정이 쓸 수 있는지 확인하십시오. 
 
 2. 업로드 된 파일에 사용할 **MEDIA_ROOT**의 하위 디렉토리를 지정하기 위해 **upload_to** 옵션을 정의하여 **FileField** 또는 **ImageField**를 모델에 추가합니다. 
 
 3. 데이터베이스에 저장 될 모든 것은 (**MEDIA_ROOT**에 상대적인) 파일에 대한 경로입니다. Django가 제공하는 편의 url 속성을 사용하기를 원할 것입니다. 예를 들어 **ImageField**의 이름이 **mug_shot** 인 경우 **{{object.mug_shot.url}}** 템플릿을 사용하여 이미지의 절대 경로를 가져올 수 있습니다.

예를 들어 **MEDIA_ROOT**이 **'/home/media'** 로 설정되고 **upload_to**가 **'photos/%Y/%m/%d'** 로 설정되어 있다고 가정해 보겠습니다.

**upload_to**의 **'%Y/%m/%d'** 부분은 **strftime()** 형식입니다. **'%Y'** 는 네 자리 숫자 연도이고 **'% m'** 은 두 자리 숫자 월이고 **'%d'** 은 두 자리 날짜입니다. 2007 년 1 월 15 일에 파일을 업로드하면 **/home/media/photos/2007/01/15** 디렉토리에 저장됩니다.

> Note: 파일은 모델을 데이터베이스에 저장하는 과정의 일부로 저장되므로 디스크에 사용 된 실제 파일 이름은 모델을 저장해야만 신뢰할 수 있습니다.
>

업로드 된 파일의 상대 URL은 url 속성을 사용하여 얻을 수 있습니다. 내부적으로 이것은 기본 **Storage** 클래스의 **url()** 메서드를 호출합니다.

업로드 된 파일을 다룰 때마다 업로드 할 파일과 파일의 유형에 세심한주의를 기울여 보안 허점을 피하십시오. 업로드 된 모든 파일의 유효성을 검사하여 파일이 자신이 생각하는 것임을 확신해야합니다. 

예를 들어, 누군가 맹목적으로 검증없이 파일을 웹 서버의 문서 루트에 있는 디렉토리에 업로드하도록 허락한다면 누군가가 CGI 또는 PHP 스크립트를 업로드하고 사이트의 URL을 방문하여 해당 스크립트를 실행할 수 있습니다. 그것을 허용하지 마십시오.

또한 업로드 된 HTML 파일은 브라우저가 (서버가 아닌) 실행할 수 있기 때문에 XSS 또는 CSRF 공격과 동일한 보안 위협이 될 수 있습니다.

**FileField** 인스턴스는 기본 최대 길이가 100자인 **varchar** 열로 데이터베이스에 만들어집니다. 다른 필드와 마찬가지로 **max_length** 인수를 사용하여 최대 길이를 변경할 수 있습니다.



## FileField and FieldFile

### class FieldFile[[source link:]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/files/#FieldFile)

모델에서 FileField에 액세스하면 FieldFile 인스턴스가 기본 파일에 액세스하기위한 프록시로 제공됩니다.

**FieldFile**의 API는 **File**의 API를 미러링합니다. 하나의 주요한 차이점이 있습니다. 클래스에 의해 래핑 된 객체는 반드시 파이썬의 내장 파일 객체를 감싸는 래퍼 일 필요는 없습니다. 

대신 **Storage.open()** 메서드의 결과를 둘러싼 래퍼입니다.이 메서드는 **File** 객체 일 수도 있고 **File** API의 custom storaged의 구현 일 수도 있습니다.

**read()** 및 **write()** 와 같이 **File**에서 상속 된 API 외에도 **FieldFile**에는 기본 파일과 상호 작용하는 데 사용할 수있는 몇 가지 메서드가 포함되어 있습니다.

> Warning!! 
> 이 클래스의 두 가지 메소드 **save()** 및 **delete()** 는 기본적으로 연관된 **FieldFile** 의 모델 객체를 데이터베이스에 저장합니다.
>


### FieldFile.name

연결된 **FileField**의 **Storage** 루트로 부터의 상대 경로를 포함하는 파일의 이름입니다. 

### FieldFile.size

기본 **Storage.size()** 메서드의 결과입니다. 

### FieldFile.url 

기본 **Storage** 클래스의 **url()** 메서드를 호출하여 파일의 상대 URL에 액세스하는 읽기 전용 속성입니다. 

### FieldFile.open (mode = 'rb') [[source link:]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/files/#FieldFile.open)

이 모드와 관련된 파일을 열거나 다시 엽니다. 표준 파이썬 **open()** 메소드와는 달리, 파일 디스크립터를 리턴하지 않는다. 

기본 파일은 액세스 할 때 암시 적으로 열리므로 기본 파일에 대한 포인터를 재설정하거나 모드를 변경하는 경우를 제외하고는이 메소드를 호출 할 필요가 없습니다. 

### FieldFile.close() [[source link:]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/files/#FieldFile.close)

표준 Python **file.close()** 메서드와 비슷하게 동작하고이 인스턴스와 관련된 파일을 닫습니다. 

### FieldFile.save (name, content, save = True) [[source link:]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/files/#FieldFile.save) 

이 메서드는 파일 이름과 파일 내용을 가져 와서 필드의 저장소 클래스에 전달한 다음 저장된 파일을 모델 필드와 연결합니다. 

모델의 **FileField** 인스턴스에 파일 데이터를 수동으로 연결하려면 **save()** 메서드를 사용하여 해당 파일 데이터를 유지합니다.

두 개의 필수 인수를 취합니다 : **name**은 파일의 이름이고 **content**는 파일 내용을 포함하는 객체입니다. 선택적 save 인수는이 필드와 연관된 파일이 변경된 후에 모델 인스턴스가 저장되는지 여부를 제어합니다. **True**로 기본값. 

**content** 인수는 파이썬의 내장 파일 객체가 아닌 **django.core.files.File**의 인스턴스 여야합니다. 다음과 같이 기존의 Python 파일 객체에서 **File**을 생성 할 수 있습니다 :

```python

from django.core.files import File
# Open an existing file using Python's built-in open()
f = open('/path/to/hello.world')
myfile = File(f)

```
아니면 다음과 같이 파이썬 문자열로 만들 수 있습니다 :

```python 

from django.core.files.base import ContentFile
myfile = ContentFile("hello world")

```

자세한 내용은 [Managing files](https://docs.djangoproject.com/en/1.11/topics/files/)를 참조하십시오.


### FieldFile.delete(save=True)[[source link:]](https://docs.djangoproject.com/en/1.11/_modules/django/db/models/fields/files/#FieldFile.delete)

이 인스턴스와 관련된 파일을 삭제하고 필드의 모든 특성을 지 웁니다. 
> Note: 이 메소드는 **delete()** 가 호출 될 때 열려있을 경우 파일을 닫습니다. 

선택적 **save** 인수는이 필드와 연관된 파일이 삭제 된 후에 모델 인스턴스가 저장되는지 여부를 제어합니다. 
**True**로 기본값. 

모델이 삭제되면 관련 파일이 삭제되지 않습니다. 분리 된 파일을 정리해야하는 경우 직접 처리해야합니다. 
(예 : 수동으로 실행하거나 cron 등을 통해 주기적으로 실행할 수있는 맞춤 관리 명령 사용)






