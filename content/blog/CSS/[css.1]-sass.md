---
title: '[CSS.1] SASS'
date: 2021-09-07 22:09:64
category: 'CSS'
draft: false
---

# Intro

CSS를 공부하는 사람이라면 누구나 한 번쯤은 들어봤을 그 이름! 바로 SASS이다.
SASS는 무엇이고 어떻게 이용하는지 한 번 배워보자!

# SASS란?

SASS는 CSS 전처리기라고 많이 부른다. 전처리기란 CSS가 동작하기 전에 실행되는 기능이다. SASS를 사용하면 SASS만의 문법을 사용하여 CSS만의 불편함을 쉽게 해소해주는 역할을 하고 있다.

- CSS에서는 속성을 적용할 선택자를 일일히 다 적어야 하는 불편함이 있었지만 전처리기는 중첩, 모듈 등 CSS보다 훨씬 더 많은 기능을 가지고 있기 때문에 더 편리하게 작성할 수 있다는 장점을 가지고 있다.

# 동작 과정

> 1. 전처리기로 작성한다.
> 2. CSS로 컴파일한다.
> 3. 동작시킨다.

# 설치

> **먼저, 터미널에서 npm을 다운로드해야함**

```
npm install node-sass@4.14.1 --save
```

- 설치 시 node-modules 폴더에 node-sass 디렉토리가 생성됨
- `--save` : package.json에 설치된 패키지의 이름과 버전 정보를 업데이트

```JSON
// package.json
{
  "name": "westagram-react",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "@testing-library/jest-dom": "^4.2.4",
    "@testing-library/react": "^9.3.2",
    "@testing-library/user-event": "^7.1.2",
    "node-sass": "^4.14.1",
    "react": "^16.13.1",
    "react-dom": "^16.13.1",
    "react-scripts": "3.4.3"
  }
}
```

이런 식으로 package.json에 정보가 업데이트 됩니다.

# 확장자를 .scss로 바꾸기

> Sass 파일의 확장자는 **.scss**입니다

# 문법

## CSS

```css
nav .item1 {
  display: flex;
  align-items: center;
}

nav .item2 {
  margin: 45px;
  border: 1px solid #000000;
}

nav .item3 {
  padding: 5px 0;
  background-color: yellow;
}
```

## SASS

```css
nav {
  .item1 {
    display: flex;
    align-items: center;
  }

  .item2 {
    margin: 45px;
    border: 1px solid #000000;
  }

  .item3 {
    padding: 5px 0;
    background-color: yellow;
  }
}
```

> 이것말고도 더 많은 문법이 존재합니다.
> [공식홈페이지](https://sass-lang.com/)를 참고하여 학습하시면 더 도움이 됩니다!
