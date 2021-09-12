---
title: '[Record] Gatsby + Netlify를 이용한 나만의 Blog 배포 '
date: 2021-09-08 22:09:50
category: 'Record'
thumbnail: { thumbnailSrc }
draft: false
---

## Blog 이사해야겠네

개발자로서 꾸준함을 무기로 장착하기 위한 가장 좋은 방법은 바로 블로그를 작성하는 것이다. 난 Velog라는 블로그 사이트에서 틈틈이 글을 작성하고 있다. 하지만 좀 더 개발자스럽게 블로그를 커스터마이징해보고 싶다는 소망이 생기게 되었다.

직접 구현하면 더욱 좋겠지만 시간의 소비를 좀 더 단축할 수 있다는 장점 때문에 템플릿을 사용하기로 마음먹었다.

찾아보니 대표적으로 Jekyll, Gatsby라는 페이지 생성 프레임워크들이 많이 서치되었다. Jekyll는 Ruby로 작성되어있어서 custom하는데 시간과 노력이 비교적 더 걸리겠다는 생각이 들었기 때문에 나는 배운 기술을 좀 더 활용할 겸 React를 기반으로 만들어진 **Gatsby**를 선택하기로 결정했다!

## Process

**📍 To-Do**

- Gatsby 설치
- Template 설치
- Netlify 배포

> ❗️ 내 노트북에만 일어난 문제인지는 모르겠지만 난 기본적으로 npm으로 설치할 때 ERR문구가 설치할 때마다 나와서 무진장 애를 먹었다. node랑 npm 버전이 맞지 않아서 그런 건가 생각이 되어서 여러 버전 설치해서 node랑 npm 버전 바꿔봤는데 실패.. 구글링 계속 해도 나같은 사례가 없는 것 같아서 결국 그냥 싹 지우고 동작되는 버전을 계속 확인하면서 제대로 동작할 때까지 다시 깔았다.
> 최종적으로 세팅된 node랑 npm version은 다음과 같다.
>
> - node: v14.7.6
> - npm: 7.22.0 [npm은 node 설치될 때 같이 설치되는데 6.14.15로 깔려서 최신으로 업데이트해주는 것이 필요하다.]

### 1. Gatsby & Template 설치

```
npm install gatsby-cli
```

설치가 완료되면 `gatsby` 명령어를 사용할 수 있게 된다.

### 2. GitHub에 Repository 생성

![](https://images.velog.io/images/silviaoh/post/00fea24a-0607-4835-99d9-477564765e9f/image.png)

나는 Netlify로 배포를 진행할 것이기 때문에 Repository name은 내가 원하는 이름으로 지었다.

### 3. Gatsby Blog Custom하기

![](https://images.velog.io/images/silviaoh/post/c34ba44e-c622-4e50-9fcf-cda170a026cb/image.png)

`gatsby-starter-bee`라는 템플릿을 사용하였는데 기본 원판이 워낙 깔끔하다보니 그렇게 많이 손대진 않았다.

블로그를 사용하다가 커스텀하고 싶은 부분이 생기면 추후에 계속 변경해나갈 예정이다.

Custom 할 때 참고해서 변경해야 할 파일들은 `gatsby-starter-bee` [README 파일](https://github.com/JaeYeopHan/gatsby-starter-bee)에 잘 작성되어있다.

### 4. Netflify에 배포하기

[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start)

![](https://images.velog.io/images/silviaoh/post/b495db07-6c4d-4ebb-a876-a414f86b8dc4/image.png)
위의 링크를 클릭하면 내 GitHub 계정과 연결할 수 있는 화면이 보여진다.

![](https://images.velog.io/images/silviaoh/post/7b8b8280-3cf6-48e8-9761-634e7fb43cf7/image.png)

내 깃허브 계정이 인증이 된다면 나의 Repository 목록들을 좌르륵 보여주는데 여기서 배포할 Repository를 선택한다.

![](https://images.velog.io/images/silviaoh/post/d9cb5ae0-11c2-48c9-8941-ed5cabd83676/image.png)

거의 기본으로 설정된대로 놔두고 `npm run build`를 `gatsby build`로 변경하였다.

![](https://images.velog.io/images/silviaoh/post/e23dadbb-aea5-40e5-942e-a1e36153a8e4/image.png)

난 `NODE_VERSION`을 14로 하고 `NPM_VERSION`을 7로 설치하도록 하는 변수 항목을 추가로 설정하였다.

![](https://images.velog.io/images/silviaoh/post/05a76354-58d0-4629-9f5a-0c6255c0ca76/image.png)

왜냐하면 다른 blog 글을 보면 바로 배포를 눌러도 잘만 배포되던데 나는 Error가 나서 Failed가 계속 났기 때문이다.

![](https://images.velog.io/images/silviaoh/post/dcf6079d-c551-429c-b1d2-404375295ea2/image.png)

Failed된 이유를 찾기 위해 코드를 봤는데 아니나 다를까..npm이 설치되는 도중에 한참을 Installing에 머물러있다가 에러가 나는 현상을 목격하게되었다.

결국 또 배포하기 전에 템플릿을 설치할 때 발생했던 node, npm 버전 문제가 또 터진 것이다.

그래서 이것을 해결하기 위해 위에서와 같이 node를 14버전으로, npm을 7버전으로 설치하라고 미리 변수 설정을 해주었더니...

![](https://images.velog.io/images/silviaoh/post/93e3a193-dbe8-409d-b518-d7c18fbdadb0/image.png)

정상적으로 배포가 되었다!

## 완성!

![](https://images.velog.io/images/silviaoh/post/6953e0a5-e1a6-4814-a789-c07a15088fc4/image.png)
