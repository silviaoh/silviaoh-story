---
title: '[ReactJS.1] React'
date: 2021-09-07 20:09:89
category: 'ReactJS'
draft: false
---

# React란?

- 웹의 발전으로 웹 애플리케이션도 규모가 커지고 복잡해짐에 따라 더 쉽고 효율적으로 개발하여 생산성을 향상시키기 위한 Web Framework(Library)가 등장하게 됨.
- 가장 많이 쓰이는 3가지로는 Anglar, Vue, React가 존재함
- 이 중에 React는 2013년에 Facebook에 개발한 Library
- 사용자 인터페이스(UI)를 만들기 위한 JavaScript Library
- 오로지 View만 담당함

# JSX

- 자바스크립트의 확장 문법
- 자바스크립트 구문 안에 HTML 문법을 같이 작성한 형태
- JSX로 작성한 코드는 브라우저에서 동작하는 과정에서 바벨을 통해 일반 자바스크립트 형태의 코드로 변환된다.

## 특징

- JSX 안에서 자바스크립트 문법을 표현할 때 : `{...javascript...}`
- HTML의 `class` -> `className`으로..
- Inline Styling: `<div style={{color: "red"}}>Hello React</div>`
- Self Closing tag : `<div></div>`를 `<div />`로 표현 가능
- 모든 요소를 감싸는 최상위 태그가 존재해야 한다.
  - React Fragments`<>...</>`
    - DOM에 별도의 노드를 추가하지 않고도 하나의 컴포넌트에 여러 개의 자식 요소들을 간단하게 그룹화 할 수 있다.(`<div>`태그의 불필요한 생성을 막을 수 있어 유용하게 사용됨)

# Component

- 재활용 가능한 UI 구성 단위
- 화면을 보았을 때 똑같은 구성 요소들을 Component로 나눌 수 있다.

## 특징

- UI 요소를 재활용할 수 있기 때문에 유지 보수 하기가 좋다.
- 해당 페이지가 어떻게 구성되어 있는지 한 눈에 파악할 수 있다.
- Component 안에는 또 다른 Component를 넣을 수 있다.

## Class Component

```javascript
import React from 'react';

class Component extends React.Component {
  render() { // 필수로 작성해야 하는 메서드
  	return (
      // JSX 문법
    );
  }

export default Component;
```

## Function Component

```javascript
import React from 'react';

const Component = () => {
 return (
 	// JSX 문법
 );
}
```

# CRA(Create-React-App)

- 리액트 프로젝트를 시작하는데 필요한 개발 환경을 세팅해주는 도구(toolchain)
- React는 UI 기능만 제공
- 웹 애플리케이션 개발을 하기 위해서는 CRA를 만들어 적절한 환경을 만들어주는 것이 필요하다.

>

- 바벨, 웹팩과 같이 React 애플리케이션 실행에 필요한 다양한 패키지가 포함되어 있고, 테스트 시스템, ES6+문법, CSS 후처리 등 거의 필수라고 할 수 있는 개발 환경도 구축해준다.

## CRA 설치

```
// 1. 내 프로젝트 폴더에 진입
cd (내 프로젝트 폴더 위치)

// 2. React 프로젝트 설치
npx create-react-app (프로젝트 폴더에 적용할 이름)

// 3. React 프로젝트 진입
cd (React 프로젝트)

// 4. 로컬 서버 띄우기
npm start
```

## CRA 기본 폴더 및 파일 구성

![](https://images.velog.io/images/silviaoh/post/70f91a22-fb89-4f0a-a8de-3a9f1e303246/image.png)

### 1. node_modules

- CRA를 구성하는 모든 패키지 소스 코드가 들어있음

### 2. public

- index.html, images, data...
- src : component를 모아놓은 디렉토리와 index.js가 들어있다.

### 3. .gitignore

- git에 push할 때 push 하지 않아도 될 디렉토리나 파일들을 이 안에 작성해놓으면 push가 이루어지지 않는다.
