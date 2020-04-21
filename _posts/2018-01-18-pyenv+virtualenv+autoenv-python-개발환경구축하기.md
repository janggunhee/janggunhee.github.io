---
layout: post
title: Python - pyenv+virtualenv+autoenv
description: "python study"
modified: 2018-01-18
permalink: /:title/
tags: [python]
categories: [python]
---

# Python - 개발 환경 구축하기 

> #### pyenv, virtualenv, pyenv-virtualenv, autoenv, pip
>
> `Mac os Sierra`  기준



#### :: 참고 ::  [kimtaewan blog](http://taewan.kim/post/python_virtual_env/#pyenv-%EC%84%A4%EC%B9%98) , [ansuchan blog](https://ansuchan.com/how-to-set-python-dev-env/), [lhy blog](https://lhy.kr/configuring-the-python-development-environment-with-pyenv-and-virtualenv)



파이썬에는 **Python 2**와 **Python 3**이 공존하고, 파이썬 별로 다수의 서브 버전이 존재한다. 그리고 또한, 파이썬 커뮤니티는 엄청난 수의 패키지를 만들고 공유하고 있다.

이러한 패키지들은 개별적으로 여러 버전을 갖고 있는데, 컴퓨터 한 대에 여러 파이썬 프로그램을 돌릴 경우, 파이썬 애플리케이션의 파이썬 런타임 버전과 파이썬 라이브러리 충돌 문제가 빈번하게 발생한다.

이러한 문제는 개발 언어와 런타임 및 라이브러리가 전역적으로 설치되고 운영되기 때문에 발생하는데, 사실 이러한 문제는 개발 컴퓨터에서 더 심각하게 발생한다.

---


### pyenv

 **"Simple Python Version Management"**, 로컬에서 다양한 파이썬 버전을 설치하고 사용할 수 있도록 한다. `pyenv`를 사용함으로써 파이썬 버전에 대한 의존성을 해결할 수 있다. 

파이썬 버전을 각각 분리해서 사용할 수 있는, **파이썬 버전관리 시스템**인 것이다. 

##### [pyenv github](https://github.com/pyenv/pyenv)



### virtualenv  

**“Virtual Python Environment builder”**, 로컬에 다양한 파이썬 환경을 구축하고 사용할 수 있도록 한다. 일반적으로 `Python Packages`라고 부르는 ( `pip install`을 통해서 설치하는 ) 패키지들에 대한 의존성을 해결할 수 있다.



### pyenv-virtualenv

**[pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv)**은 **virtualenv**의 **pyenv** 확장 플러그인. 파이썬 버전과 라이브러리의 완전히 격리된 환경을 제공한다.



### autoenv

 만약 `pyenv`와 `virtualenv`를 통해서 의존성을 해결한다고 하더라도 작업할때마다 설정해주는 것은 귀찮은 작업이다. 특정 프로젝트 폴더로 들어가면 자동으로 개발 환경을 설정해주는`.env`파일을 실행하여 가상환경을 활성화 해준다. `autoenv`라는 스크립트를 활용하자.



### pip 

**pip**는 파이썬으로 작성된 **패키지**(라이브러리)를 관리하는 프로그램이다. 

만약 사용해야할 라이브러리나 모듈이 있을 경우 , `pip install <설치모듈>` 을 실행하면 된다. 

**[pip Docs >> ](https://pip.pypa.io/en/stable/)**



---

### pyenv 를 통한 파이썬 버전 관리 

##### Simple Python Version Management: pyenv

- 파이썬 버전을 사용자 단위로 변경할 수 있습니다. 
- 프로젝트마다 파이썬 버전을 지원한다. 
- Python 버전을 환경 변수로 대체 할 수 있습니다. 
- 한 번에 여러 버전의 파이썬에서 명령을 검색합니다. Python 버전을 테스트하는 데 도움이 될 수 있습니다.

####  

#### 1. pyenv, pyenv-virtualenv 설치하기 

##### macOS

```
$ brew install pyenv
$ brew install pyenv-virtualenv
```

**[Ubuntu pyenv-installer >>](https://github.com/yyuu/pyenv-installer) **

pyenv 업그레이드는 다음 명령을 사용합니다.

```
$ brew upgrade pyenv
```



#### 2. 설치 후 pyenv 환경변수 적용 및 업데이트

다음 명령을 터미널에서 수행하여 환경변수를 등록합니다. 

>  zsh를 사용하실 때는 “**~/.bash_profile**“을 “**~/.zshrc**“로 변경해서 실행해야 합니다.

```
$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
$ echo 'eval "$(pyenv init -)"' >> ~/.bash_profile
$ source ~/.bash_profile
```



##### 혹은, 직접 `~/.bash_profile`, `~/.zshrc` 에 추가하기 

```
➜ vi ~/.bash_profile

# 가장 아래쪽에 아래 문장 추가
export PYENV_ROOT=/usr/local/var/pyenv
if which pyenv > /dev/null; then eval "$(pyenv init -)"; fi
if which pyenv-virtualenv-init > /dev/null; then eval "$(pyenv virtualenv-init -)"; fi
```



##### shell설정을 변경했으면, 해당 설정을 현재 shell에 적용

터미널을 재시작하거나, `source ~/.bashrc`또는 `source ~/.bash_profile`를 입력.
`zsh`을 사용할 경우 `source ~/.zshrc` 실행



##### pyenv 설치 점검

이제 pyenv 설치가 완료되었습니다. pyenv 정상 설치 여부는 다음 명령으로 확인할 수 있습니다.

```
$ pyenv install --list
Available versions:
  2.1.3
  2.2.3
  2.3.7
########
# 로그 생략
########
  stackless-3.4.1
  stackless-3.4.2
$ pyenv install --list | wc -l
323
$ pyenv --version
pyenv 1.1.3

```

위 예시와 같이 출력된다면 정상 설치로 간주할 수 있습니다.



##### 혹은, pyenv를 최신 버전으로 업데이트해야 할 경우 다음 명령을 수행합니다.

```
$ pyenv update
Updating /home/opc/.pyenv...
From https://github.com/yyuu/pyenv
 * branch            master     -> FETCH_HEAD
########
# 로그 생략
########
Updating /home/opc/.pyenv/plugins/pyenv-which-ext...
From https://github.com/yyuu/pyenv-which-ext
 * branch            master     -> FETCH_HEAD
Already up-to-date.
```



##### 혹은, 원하는 버전을 설치한다. 

pyenv를 이용해 설치 가능한 파이썬 버전을 확인한다. 

일반적인 신규 프로젝트에서는 파이썬3의 가장 마지막버전을 사용한다. (2018-01-18시점에서 3.6.2)

(dev 버전은 나와 같은 잔챙이들은 피하는게 좋을 것)

```
$ pyenv install --list 
# 설치가능한 파이썬 버전을 확인 
# 이후 원하는 버전을 설치한다.
$ pyenv install 3.6.2
```



##### 현재, 내 pyenv 버전 확인 

```
$ pyenv versions
  system
  3.5.3
* 3.6.2 (set by /usr/local/var/pyenv/version)
```



##### pyenv를 이용해 파이썬을 설치 하기 전, 필요 패키지 설치

필수 패키지를 설치하지 않을 경우 파이썬이 설치되지 않거나, 오작동을 일으킨다.
[Common build problems](https://github.com/yyuu/pyenv/wiki/Common-build-problems)를 참조



##### pyenv가 제공하는 서브 명령은 다음과 같습니다.

| 서브 명령     | 설명                                   |
|: --------- :|: ------------------------------------ :|
| local     | 현재 디렉터리에 python 버전 확인 및 python 버전 지정 |
| global    | 전역으로 설정된 python 버전                   |
| shell     | shell에 파이썬 버전을 지정                    |
| install   | python-build를 이용하여 파이썬 버전을 설치        |
| uninstall | 지정한 버전의 파이썬을 삭제                      |
| version   | 현재 활성화된 파이썬 버전 출력                    |
| versions  | pyenv로 설치되어 이용 가능한 버전을 출력            |
| which     | 활성화된 파이썬 명령의 위치 출력                   |
| whence    | 지정한 명령을 포함하는 모든 파이썬 버전 출력            |



