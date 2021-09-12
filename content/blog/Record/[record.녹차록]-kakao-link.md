---
title: '[Record.녹차록] Kakao Link'
date: 2021-09-07 22:09:33
category: 'Record'
thumbnail: { thumbnailSrc }
draft: false
---

```jsx
kakaoSharePreference = () => {
  const { description, main_image_url, name } = this.state.product
  const URL = `http://localhost:3000/detail/${this.props.match.params.id}`
  dotenv.config()

  window.Kakao.init('키')

  window.Kakao.Link.createDefaultButton({
    container: '#kakao-link-btn',
    objectType: 'feed',
    content: {
      title: `${name}`,
      description: `${description}`,
      imageUrl: `${main_image_url}`,
      link: {
        webUrl: `${URL}`,
      },
    },
    buttons: [
      {
        title: '녹차록에서 확인하기',
        link: {
          mobileWebUrl: `${URL}`,
          webUrl: `${URL}`,
        },
      },
    ],
  })
}
```

```jsx
window.Kakao.init('키')
```

- 첫 단계에서 이런 식으로 적었더니 제대로 동작은 되었지만 키가 그대로 노출되는 문제점이 발생
- 연욱님이 리뷰를 주셔서 .env 파일을 만들어서 이 안에서 키를 관리하도록 하고 .gitignore 파일에 추가하여 gitHub에 업로드되지 않도록 수정

### 1. .env파일

![](https://images.velog.io/images/silviaoh/post/02142f2d-a591-4b6a-965f-207294967570/image.png)

### 2. .gitignore에 .env 추가

### 3. .env에 키 추가

```jsx
REACT_APP_KAKAO_LINK_KEY=28...
```

### 4. detail.jsx에 적용

```jsx
window.Kakao.init('키'); -> window.Kakao.init(process.env.REACT_APP_KAKAO_LINK_KEY);
```

But!! 여기서 CROS 에러 발생!!

![](https://images.velog.io/images/silviaoh/post/a8e188da-9777-417c-b4f3-820bd41c64cc/image.png)

- Cross-origin 이란 어떤 리소스를 사용할 때 그 리소스가 자신의 출처(도메인, 포트 등)와 다를 때 발생합니다.
- fetch와 XMLHttpRequest와 fetch는 동일 출처 정책을 따릅니다.
- 즉, 이 API를 사용하는 웹 애플리케이션은 자신의 출처와 동일한 리소스만 불러올 수 있고, 다른 출처의 리소스에 접근을 하려면 그 출처에서 올바른 응답을 반환해야 접근할 수 있다는 것!

  ### 해결 시도 1

  ### 카카오 개발자 플랫폼에 내 도메인 입력

  ![](https://images.velog.io/images/silviaoh/post/aad0a5b6-83f6-4ef3-8eac-5e5a0c5f8b15/image.png)

  - **여전히 에러가 발생한다.** 한참 고민하다가 멘토님의 도움을 받아 힌트를 얻게 되었다.
  - init의 인자로 들어간 `process.env.REACT_APP_KAKAO_LINK_KEY`를 확인해봤더니 `undefined`가 출력됨!

  ### 해결 시도 2

  ### 환경변수 등록

  1. **내 터미널에서 export(이 방법은 vscode를 켤 때마다 실행해야 함)**

  ```jsx
  export REACT_APP_KAKAO_LINK_KEY='키'
  ```

  2.  **해당 jsx 파일에 dotenv 라이브러리 import**

  - dotenv는 환경 변수를 파일에 저장할 수 있게 해준다.

  ```jsx
  import dotenv from 'dotenv';

  ...

  dotenv.config();
  window.Kakao.init(process.env.REACT_APP_KAKAO_LINK_KEY);
  ```

  - 이제 undefined가 뜨지 않고 제대로 키 값이 들어가 동작한다!
