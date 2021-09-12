---
title: '[JavaScript.3] spread & rest'
date: 2021-09-07 23:09:82
category: 'JavaScript'
thumbnail: { thumbnailSrc }
draft: false
---

# Intro

- Spread와 rest 문법은 ES6에서 도입된 문법들이다.

# spread

- '펼치다', '퍼뜨리다'
- 이 문법을 사용하면 객체 또는 배열을 펼칠 수 있다.
- spread 문법의 핵심은 기존의 것을 건드리지 않고 새로운 객체를 만들 수 있다는 것이다.

### 객체

```javascript
const flower = {
  name: '장미',
}

const redFlower = {
  ...flower,
  color: 'red',
}

const leafFlower = {
  ...redFlower,
  leaf: true,
}

console.log(flower) // { name: '장미' }
console.log(redFlower) // { name: '장미', color: 'red' }
console.log(leafFlower) // { name: '장미', color: 'red', leaf: true }
```

### 배열

```javascript
const flowers = ['장미', '해바라기', '코스모스']
const anotherFlowers = [...flowers, '백합']
// ['장미', '해바라기', '코스모스', '백합']
```

# rest

- 객체, 배열, 함수의 파라미터에서 사용 가능

### 객체

```javascript
const leafFlower = {
  name: '장미',
  color: 'red',
  leaf: true,
}

const { color, ...rest } = leafFlower
// color -> 'red'
// rest -> { name: '장미', leaf: true }
```

rest를 사용하면 color를 제외한 name과 leaf 값을 제외한 값이 들어있다. 이 때, 추출한 값의 이름이 꼭 rest일 필요는 없다.

### 배열

```javascript
const numbers = [6, 7, 8, 9, 10]

const [six, ...rest] = numbers

console.log(one) // 6
console.log(rest) // [7,8,9,10]
```

배열 비구조화 할당으로 원하는 값을 밖으로 꺼낼 수 있다.
하지만

```javascript
const numbers = [6,7,8,9,10];

const [...rest, last] = numbers;

console.log(one); // 6
console.log(rest); // [7,8,9,10]
```

이렇게는 작성하면 동작하지 않는다.

또 함수의 파라미터가 몇 개가 될 지 모르는 상황에서 rest 파라미터를 사용하면 매우 유용하다.

```javascript
sum = (...rest) => {
  return rest.reduce((acc, current) => acc + current, 0)
}

const result = sum(2, 4, 6, 8, 10)
console.log(result) // 30
```
