---
title: '[JavaScript.2] async vs defer'
date: 2021-09-07 20:09:26
category: 'JavaScript'
thumbnail: { thumbnailSrc }
draft: false
---

## 1. head 태그 안에 위치

```
<!DOCTYPE html>
<html>
  <head>
    <title>동작 원리</title>
    <script src="main.js"></script>
  </head>
  <body>
    <h1>자바스크립트는 어떻게 동작할까요?</h1>
    <p>궁금하죠?</p>
  </body>
</html>
```

웹 브라우저가 서버에서 HTML 문서를 받아서 코드를 위에서부터 한줄씩 읽어서 분석하여 트리 형태의 DOM 모델로 만드는 파싱 작업을 진행한다.

그러다가 script 태그를 만나면 작업을 중단하게 된다.
웹 브라우저는 자바스크립트 엔진을 통하여 js파일을 다운로드하고 실행한 후 다시 HTML 파싱 작업으로 돌아와서 페이지 로딩 준비를 완료한다.

![](https://images.velog.io/images/silviaoh/post/06653887-4728-4d21-a4b3-83fb6d2c53b0/image.png)

`<head>` 태그 안에 `<script>` 태그를 넣으면 파싱 중간에 작업을 멈추고 js 파일을 불러오고 실행하기 때문에 전체 페이지를 띄우는 시간이 오래 걸린다.

> [웹 페이지의 동작원리](https://velog.io/@silviaoh/TIL8-웹-브라우저의-동작원리)

## 2. body 태그 안에 위치

```
<!DOCTYPE html>
<html>
  <head>
    <title>동작 원리</title>
  </head>
  <body>
    <h1>자바스크립트는 어떻게 동작할까요?</h1>
    <p>궁금하죠?</p>
    <script src="main.js"></script>
  </body>
</html>
```

![](https://images.velog.io/images/silviaoh/post/81133795-9c94-43d7-a0da-941261b9a875/image.png)

코드를 전부 읽어내리고 맨 마지막에 자바스크립트 파일을 호출하고 실행하기 때문에 head 태그 안에 있는 것보다 웹 페이지 로딩 속도가 빠르다.

하지만 만약 javascript에 의존적인 페이지라면 기능이 보여지기까지 fetch와 실행을 기다려야한다는 단점이 있다.

## 3. head + async

```
<!DOCTYPE html>
<html>
  <head>
    <title>동작 원리</title>
    <script async src="main.js"></script>
  </head>
  <body>
    <h1>자바스크립트는 어떻게 동작할까요?</h1>
    <p>궁금하죠?</p>
  </body>
</html>
```

![](https://images.velog.io/images/silviaoh/post/b0160e63-760d-4422-a6a1-d9bdbfb9e5ec/image.png)

코드를 읽어가다가 script 태그의 async를 만나면 '병렬로 처리하는거구나.' 라고 브라우저가 인식을 한다.

브라우저가 HTML 파일을 파싱하는 도중에 js파일이 다운로드되고 완료되면 파싱 작업을 멈추고 js를 실행하며 그 후에 파싱 작업을 마무리한다.

이 방법은 JavaScript를 다운로드 받는 시간을 절약할 수 있다.
하지만 아직 정의되지 않은 HTML 요소가 있다면 JavaScript가 실행되지 못할 수 있다.

또 크기가 다른 js 파일이 여러 개가 있을 때는 서로 다운로드 속도가 다르기 때문에 완료되는 시점이 다를 수 있다. async는 언제든지 자바스크립트를 실행하기 위해 파싱 작업을 멈출 수 있어서 페이지 로딩 시간이 오래 걸린다.

## 4. head + defer

```
<!DOCTYPE html>
<html>
  <head>
    <title>동작 원리</title>
    <script defer src="main.js"></script>
  </head>
  <body>
    <h1>자바스크립트는 어떻게 동작할까요?</h1>
    <p>궁금하죠?</p>
  </body>
</html>
```

자바스크립트 파일을 적용할 때 효율적이고 안전하기 때문에 제일 선호하는 방법이다.

![](https://images.velog.io/images/silviaoh/post/0b2eff67-44dc-49f7-b54b-efa33cc650b4/image.png)

defer은 필요한 스크립트 파일을 전부 다운로드한 뒤, 페이지를 전부 로딩하고 자바스크립트 파일을 실행한다.

자바스크립트 파일이 여러 개가 있더라도 먼저 전부 다운로드 한 뒤, 순서대로 실행하기 때문에 async에서 발생한 문제도 일어나지 않는다.

> 참고 : https://www.youtube.com/watch?v=tJieVCgGzhs
