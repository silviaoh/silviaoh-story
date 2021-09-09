---
title: '[Git.2] 맥 M1에서 Git install & setup'
date: 2021-09-07 23:09:13
category: 'git'
draft: false
---

## 0. git 버전 확인

```
git -version
```

나의 컴퓨터에 git이 설치되어 있는지 먼저 확인한다.

Git이 설치되어 있지 않다면 [여기](https://git-scm.com/)에서 git을 설치한다.

난 애플 M1칩을 탑재하고 있는 맥북 프로를 사용하고 있기 때문에 git 페이지에 있는 가이드라인에 따라 터미널에서 설치를 진행하였다.

## 1. homebrew 설치

터미널을 열고 아래의 명령문을 입력하여 설치한다.

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## 2. git 설치

터미널에서 아래에 나온 명령문을 입력해준다.

`brew install git`
<br>

만약 애플 M1칩을 탑재하고 있는 새로운 맥북이라면 아마 여기서

```
zsh: command not found: brew
```

brew 명령을 찾을 수 없다는 오류가 출력될 것이다.
<br>

그럴 때 해결법은

```
eval $(/opt/homebrew/bin/brew shellenv)
```

이렇게 입력해주면 정상적으로 brew가 작동된다.
![](https://images.velog.io/images/silviaoh/post/5faf3f55-6dbf-4408-8e9c-1dfe47b240d8/image.png)

다시 `brew install git`으로 git을 설치해주자.

## 3. 사용자이름과 이메일 추가

이제 사용자 설정 파일에 들어가서 사용자의 이름과 이메일을 추가해줘야한다. 이 정보는 commit할 때 적용되는 정보들이다.

- git config --global user.name "사용자이름"
- git config --global user.email 사용자이메일

> **--global로 적용하는 것은 딱 한번만 하면 된다!**
> 프로젝트마다 다른 이름과 이메일을 사용하고 싶다면 --global 옵션을 빼고 실행하자

## 4. git에서 CRLF 개행 문자열로 인한 문제를 해결하기 위한 설정

- git config --global core.autocrlf input
  (윈도우 사용자는 input 대신 true로 설정)

운영체제마다 줄바꿈을 할 때 들어가는 문자열이 다르다.

- Windows : \r\n
- Mac : \n

나중에 git repository를 다양한 운영체제에서 사용하는 경우 이 차이 때문에 코드를 보고 이해하는 것에 문제가 생길 수 있기 때문에 설정한다.

## 5. git repository 만들기

> **여기서 잠깐❗️ Git Repository란?**

- Git으로 관리하는 프로젝트 저장소(즉, 디렉토리)
- **Git repository**에는 크게 두 가지 종류가 있다.
  - **Local repository** : 본인의 컴퓨터에 저장된 로컬 버전의 프로젝트 저장소
  - **Remote repository** : 내 컴퓨터가 아닌 원격 서버의 프로젝트 저장소. 팀에서 작업할 때 유용하다.
    > Git으로는 버전 관리를 할 수는 있지만 다른 사람의 코드를 확인하고 공유하는 것은 하지 못한다. Local repository에 존재하는 파일을 Remote repository에 push(업데이트)할 때 비로소 다른 사람과의 협업이 가능하다.

### 1. local directory를 만들고 이것을 git repository로 변환

`git init`
현재 있는 디렉토리에 .git파일이 생성된다. 하지만 이 명령만 가지고는 프로젝트의 어떤 파일도 관리하지 않기 때문에 repository에 파일을 추가하고 commit해야 한다.

> **.git**
> 저장소에 필요한 뼈대 파일이 들어있다.

### 2. repository 복제하기

`git clone <repository URL> <directory path>`

URL에 있는 저장소를 그대로 복제하여 다운로드 받으며 초기화도 자동으로 이루어진다

만약 repository를 현재 있는 폴더가 아닌 다른 위치에 저장하고 복제한 원래 저장소 이름을 다른 이름으로 변경하여 복제하고 싶다면 URL 뒤에 디렉토리 경로를 입력한다.
