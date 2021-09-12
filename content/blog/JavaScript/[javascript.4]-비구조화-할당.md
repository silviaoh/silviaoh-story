---
title: '[JavaScript.4] 비구조화 할당'
date: 2021-09-07 23:09:74
category: 'JavaScript'
thumbnail: { thumbnailSrc }
draft: false
---

# Intro

- 프로젝트를 진행하면서 비구조화 할당 문법에 대해서 접하게 되었는데 잘 이해가 되지 않아 글로 정리해보면서 다시 복습해보고자 한다.

# 비구조화 할당

## 객체

#### 객체 안에 있는 값을 추출해서 변수 또는 상수로 바로 선언해 줄 수 있다.

```javascript
const object = { a: 5, b: 6 }
const { a, b } = object

conosole.log(a) // 5
console.log(b) // 6
```

#### 함수의 파라미터에서도 할 수 있는 비구조화 할당

```javascript
const object = { a: 4, b: 5, c: 6 }

print = ({ a, b, c }) => {
  console.log(a) // 4
  console.log(b) // 5
  console.log(c) // 6
}

print(object)
```

#### 비구조화 할당 시 기본값 설정

```javascript
const object = { a: 4 }

print = ({ a, b = 3 }) => {
  console.log(a) // 4
  console.log(b) // 3
}

print(object)
```

```javascript
const object = { a: 4 }
const { a, b = 3 } = object

console.log(a) // 4
console.log(b) // 3
```

#### 비구조화 할당 시 이름 바꾸기

```javascript
const flowers = {
  name: 'rose',
  color: 'red',
}

const { name: flower } = flowers
console.log(flower) // 'rose'
```

## 배열

```javascript
const array = [1, 3]
const [one, three] = array

console.log(one) // 1
console.log(three) // 3
```

#### 배열 안에 있는 원소를 다른 이름으로 새로 선언하기

```javascript
const array = [3]
const [three, two = 2] = array

console.log(three) // 3
console.log(two) // 2
```
