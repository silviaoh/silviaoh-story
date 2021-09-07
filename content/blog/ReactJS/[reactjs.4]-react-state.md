---
title: '[ReactJS.4] React State'
date: 2021-09-07 22:09:41
category: 'ReactJS'
draft: false
---

# 🏅 Today's Goal

- state의 개념에 대해 한 문장으로 설명할 수 있다.
- state를 이용해서 UI를 구성할 수 있다.
- 이벤트를 통해 state를 변경할 수 있다.

# State(상태)

- 컴포넌트 내부에서 가지고 있는 컴포넌트의 상태값
- **화면에 보여줄 컴포넌트의 UI 정보(상태)를 지니고 있는 객체**
- 내 지금의 상태는 부모님에게서 물려받을 수 없다.
- 상태는 바꿀 수 있다. ex) 배고픔 -> 배부름

> JavaScript에서는 DOM으로 HTML에 접근해서 동적인 기능을 추가했지만 **React에서는 state 중심으로 사고를 바꿔야 한다.**

```jsx
import React from 'react'

class State extends React.Component {
  constructor() {
    super()
    this.state = {
      color: 'red',
    }
  }

  render() {
    return (
      <div>
        <h1>Class Component | State</h1>
      </div>
    )
  }
}

export default State
```

- `constructor()` state를 설정할 때 작성한다.

  - 이 안에는 super()와 this.state 값에 **컴포넌트의 초기 상태값**을 설정해 주어야 한다.

> #### 왜? 상태값을 설정할까?
>
> 컴포넌트 안의 요소에서 그 상태값을 반영해서 데이터가 바뀔 때마다 효율적으로 화면(UI)에 나타내기 위해서이다.

```jsx
import React, { Component } from 'react'

class State extends Component {
  constructor() {
    super()
    this.state = {
      color: 'red',
    }
  }

  handleColor = () => {
    this.setState({
      color: 'blue',
    })
  }

  render() {
    return (
      <div>
        <h1 style={{ color: this.state.color }}>Class Component | State</h1>
        <button onClick={this.handleColor}>Click</button>
      </div>
    )
  }
}

export default State
```

- `button`에서 `onClick` 이벤트 발생
- 현재 state의 handleColor 함수 실행
- handleColor 함수 안의 setState 함수 실행 : state의 color 값을 'blue'로 변경
- render 함수 호출
- 바뀐 state 값을 반영하여 `h1` 태그 글자 색상 변경

> React에서는 state를 통해서 자신의 UI를 구성한다.
> 절차적이지 않고 태그 안에 선언하여 자동적으로 업데이트 된 state가 반영되는 방식으로 흘러간다는 것을 명심하자!

> #### ❗️ 인라인 태그를 지양하자!
>
> 유지보수가 어려워지기 때문이다.

> #### React에서는 설계 자체가 단방향이다.

- 항상 위->아래, 부모->자식으로 흐른다.
- 이렇게 가는 이유도 유지 보수를 쉽게 하기 위해서이다.
- 만약에 자식 -> 부모, 형제 -> 형제 간에도 흐를 수 있다면 props가 어디서 왔는지 알 수가 없어서 추적이 어려워지기 때문이다.
