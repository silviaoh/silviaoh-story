---
title: '[ReactJS.3] React Props'
date: 2021-09-07 22:09:08
category: 'ReactJS'
draft: false
---

# 🏅 Today's Goal

- props의 개념을 한 문장으로 설명하기
- props의 개념으로 부모 요소의 state를 자식 요소에서 어떻게 반영시킬 수 있을까?
- props의 개념으로 자식에서 일어난 이벤트로 부모의 state 값을 어떻게 바꿀 수 있을까?

# props

- properties(속성)
- 나와 관련된 특징들이 있을 것이다. 예를 들어 `나는 여자이다.`, `나는 아빠의 얼굴을 닮았다.` 내가 가지고 있는 이런 속성들은 부모님에게서 태어나면서 가지고 있는 속성들이고 내가 스스로 바꿀 수 없다.
- props란 부모 컴포넌트로부터 전달 받은 데이터를 지니고 있는 **객체**이다.
- props를 통해서 부모 컴포넌트로부터 자식 컴포넌트에게 **state의 상태값**과 **event handler**를 넘겨줄 수 있다.
- 부모에게서 아무런 속성도 받지 않은 Child component에서 console.log로 출력해보면 아무 값도 나타나지 않는다. 자식 컴포넌트에서 props를 출력하고 싶다면 부모 컴포넌트에서 props를 전달해줘야 한다.

> #### Child 컴포넌트에 props를 전달하는 방법
>
> `<\Child message="나는 초콜릿을 매우 좋아합니다." />`

#### Child 컴포넌트에서 전달된 props를 보여줄 때

`console.log({this.props.message});`

- props는 javascript 자료형이 무엇이든지 다 넘겨줄 수 있다.(객체, 배열, 함수, Number 등등...)

# 🤔 부모의 state에 있는 데이터를 Child 컴포넌트에게 props로 넘기는 방법

```jsx
// Parent.js
import React from 'react';
import Child from '../pages/Child/Child';

class Parent extends React.Component {
  constructor() {
    super();
    this.state = {
      color: 'red';
    }
  }

  render() {
    return (
      <div>
        <h1>Parent Component</h1>
        <Child />
      </div>
    );
  }
}

export default Parent;
```

- 부모의 state에는 `color: 'red'` 가 저장되어 있다.
- 이것을 Child 컴포넌트에게 props를 통해 넘겨보자

```jsx
import React from 'react'
import Child from '../pages/Child/Child'

class Parent extends React.Component {
  constructor() {
    super()
    this.state = {
      color: 'red',
    }
  }

  render() {
    return (
      <div>
        <h1>Parent Component</h1>
        <Child titleColor={this.state.color} />
      </div>
    )
  }
}
```

- titleColor라는 속성에 값으로 this.state.color 값을 전달해주었다.
- 즉, 부모 컴포넌트의 state 객체 중에서 color의 값을 Child 컴포넌트에게 전달해준 것이다.

# 🤔 Child 컴포넌트 내부에서 전달 받은 props를 어떻게 사용할까?

```jsx
// Child.js

import React from 'react'

class Child extends React.Component {
  render() {
    retun(
      <div>
        <h1 style={{ color: this.props.titleColor }}>Child Component</h1>
      </div>
    )
  }
}

export default Child
```

- `h1` 태그의 글자색을 다른 색으로 바꾸고 싶다.
- 아까 부모 컴포넌트에서 부모 컴포넌트의 상태를 값으로 가지고 있는 `titleColor`라는 속성을 Child 컴포넌트에게 전달해줬다.
- 현재 Child 컴포넌트는 props 객체 중에서 titleColor 값을 가지고 있다.
- `h1` 태그의 색상을 바꿔주기 위해서 style에 인라인으로 css의 속성 중 color라는 속성을 부모 컴포넌트에서 받아온 `props.titleColor`로 설정해줬다.

# props를 통한 Event Handler 전달

```jsx
// Parent.js
import React from 'react'
import Child from '../pages/Child/Child'

class Parent extends React.Component {
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
    retun(
      <div>
        <h1>Parent Component</h1>
        <Child titleColor={this.state.color} changeColor={this.handleColor} />
      </div>
    )
  }
}
```

- 이벤트 핸들러`handleColor()`를 props 객체를 통해 Child 컴포넌트에게 전달할 수 잇다.

```jsx
// Child.js

import React from 'react'

class Child extends React.Component {
  render() {
    return (
      <div>
        <h1 style={{ color: this.props.titleColor }}>Child Component</h1>
        <button onClick={this.props.changeColor}>Click</button>
      </div>
    )
  }
}

export default Child
```

- `<button>` 요소에서 onClick 이벤트 발생
- 이벤트 발생 시 `this.props.changeColor` 실행
- props 객체의 `changeColor` = 부모 컴포넌트로부터 전달받은 `handleColor` 함수 실행
- `handleColor` 함수 실행 시 `setState` 함수 호출 - state의 color 값을 'blue'로 변경
- render 함수 호출
- Child 컴포넌트에 변경된 state 데이터(`this.state.color`) 전달
- `this.props.titleColor`를 글자 색상으로 지정하는 `h1` 타이틀 색상 변경
