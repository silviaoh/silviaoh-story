---
title: '[Record.GREAM] Chart.js 라이브러리를 이용한 그래프 구현'
date: 2021-09-07 23:09:71
category: 'Record'
thumbnail: { thumbnailSrc }
draft: false
---

## 라이브러리 설치

```
npm install --save react-chartjs-2 chart.js
```

## Line Component import

```jsx
import { Line } from 'react-chartjs-2'

const Graph = ({ graphData }) => {
  return (
    <Wrapper>
      <Position>
        <Line />
      </Position>
    </Wrapper>
  )
}

//...styled component 부분 생략
```

## Line Component의 width, height 지정

```jsx
import { Line } from 'react-chartjs-2'

const Graph = ({ graphData }) => {
  return (
    <Wrapper>
      <Position>
        <Line width="10vw" height="3.5vh" />
      </Position>
    </Wrapper>
  )
}

//...styled component 부분 생략
```

## data 객체 생성

```jsx
const data = () => {
  labels: [1, 2, 3, 4, 5]
  datasets: [
    {
      data: [100, 200, 300, 400, 500]
      fill: true,
      backgroundColor: ''rgba(225,116,103,0.2)',
      borderColor: 'rgba(225,116,103)',
      borderWidth: 1,
      color: '#000'
    }
  ]
}
```

- label : x축
- data : y축 데이터
- fill : 그래프 안을 채울 것인지 정하는 속성
- backgroudColor: 그래프 안의 배경색
- borderWidth: 그래프 선 굵기
- color: 폰트 색깔

## Line Component에 width, height와 data props 부여

```jsx
import { Line } from 'react-chartjs-2';

const Graph = ({ graphData }) => {
  const data = () => {
  labels: [1, 2, 3, 4, 5, 6],
  datasets: [
    {
      data: [330000, 460000, 500000, 600000, 500000, 600000],
      fill: true,
      backgroundColor: ''rgba(225,116,103,0.2)',
      borderColor: 'rgba(225,116,103)',
      borderWidth: 1,
      color: '#000'
    }
  ]
}

  return (
    <Wrapper>
      <Position>
        <Line width="10vw" height="3.5vh" data={data} />
      </Position>
    </Wrapper>
  );
}
```

- data가 세팅되어 그래프가 나타남
- width와 height에 vw, vh 단위를 붙이면 반응형이 된다.

## 그래프 배경색에 그라데이션 효과 부여하기

```jsx
import { Line } from 'react-chartjs-2';

const Graph = ({ graphData }) => {

  const data = (canvas) => {
    const ctx = canvas.getContext('2d');
    const gradientFill = ctx.createLinearGradient(0,0,0,200);
    gradientFill.addColorStop(0, 'rgba(225,116,116,0.5)');
    gradientFill.addColorStop(1, 'rgba(225,116,116,0.1)');

    labels: [1, 2, 3, 4, 5]
    datasets: [
      {
        data: [100, 200, 300, 400, 500]
        fill: true,
        backgroundColor: ''rgba(225,116,103,0.2)',
        borderColor: 'rgba(225,116,103)',
        borderWidth: 1,
        color: '#000'
      }
    ]
}

  return (
    <Wrapper>
      <Position>
        <Line width="10vw" height="3.5vh" data={canvas => data(canvas)} />
      </Position>
    </Wrapper>
  );
}
```

## Graph option 속성 추가

```jsx
const options = {
  plugins: {
    legend: { display: false }, // 라벨 숨기기
    tooltip: {
      // 툴팁 속성 설정
      backgroundColor: 'rgba(255, 255, 255)',
      titleColor: 'rgba(225,116,103)',
      bodyColor: 'rgba(0,0,0)',
      caretSize: 0,
      displayColors: false,
      boxWidth: '100px',
      borderColor: 'rgba(225,116,103)',
      borderWidth: 1,
    },
  },
  elements: {
    point: {
      // 그래프 꼭짓점 모양
      pointStyle: 'star',
      radius: 2,
    },
  },
  scales: {
    x: { display: false }, // x축 보이지 않음
    y: {
      grid: { display: false, drawBorder: false }, //y축 선 없애기
      position: 'right', // y축 오른쪽에 위치시키기
      ticks: { color: `#a0a0a0` }, // y축 글자색 변경
    },
  },
  animation: {
    duration: 0, // 애니메이션 삭제
  },
}
```

## 결과

![](https://images.velog.io/images/silviaoh/post/022ab05f-dd8a-4c4d-823f-6ce42d139c1a/image.png)
