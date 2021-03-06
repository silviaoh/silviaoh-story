---
title: '[ReactJS.3] React Props'
date: 2021-09-07 22:09:08
category: 'ReactJS'
draft: false
---

# ๐ Today's Goal

- props์ ๊ฐ๋์ ํ ๋ฌธ์ฅ์ผ๋ก ์ค๋ชํ๊ธฐ
- props์ ๊ฐ๋์ผ๋ก ๋ถ๋ชจ ์์์ state๋ฅผ ์์ ์์์์ ์ด๋ป๊ฒ ๋ฐ์์ํฌ ์ ์์๊น?
- props์ ๊ฐ๋์ผ๋ก ์์์์ ์ผ์ด๋ ์ด๋ฒคํธ๋ก ๋ถ๋ชจ์ state ๊ฐ์ ์ด๋ป๊ฒ ๋ฐ๊ฟ ์ ์์๊น?

# props

- properties(์์ฑ)
- ๋์ ๊ด๋ จ๋ ํน์ง๋ค์ด ์์ ๊ฒ์ด๋ค. ์๋ฅผ ๋ค์ด `๋๋ ์ฌ์์ด๋ค.`, `๋๋ ์๋น ์ ์ผ๊ตด์ ๋ฎ์๋ค.` ๋ด๊ฐ ๊ฐ์ง๊ณ  ์๋ ์ด๋ฐ ์์ฑ๋ค์ ๋ถ๋ชจ๋์๊ฒ์ ํ์ด๋๋ฉด์ ๊ฐ์ง๊ณ  ์๋ ์์ฑ๋ค์ด๊ณ  ๋ด๊ฐ ์ค์ค๋ก ๋ฐ๊ฟ ์ ์๋ค.
- props๋ ๋ถ๋ชจ ์ปดํฌ๋ํธ๋ก๋ถํฐ ์ ๋ฌ ๋ฐ์ ๋ฐ์ดํฐ๋ฅผ ์ง๋๊ณ  ์๋ **๊ฐ์ฒด**์ด๋ค.
- props๋ฅผ ํตํด์ ๋ถ๋ชจ ์ปดํฌ๋ํธ๋ก๋ถํฐ ์์ ์ปดํฌ๋ํธ์๊ฒ **state์ ์ํ๊ฐ**๊ณผ **event handler**๋ฅผ ๋๊ฒจ์ค ์ ์๋ค.
- ๋ถ๋ชจ์๊ฒ์ ์๋ฌด๋ฐ ์์ฑ๋ ๋ฐ์ง ์์ Child component์์ console.log๋ก ์ถ๋ ฅํด๋ณด๋ฉด ์๋ฌด ๊ฐ๋ ๋ํ๋์ง ์๋๋ค. ์์ ์ปดํฌ๋ํธ์์ props๋ฅผ ์ถ๋ ฅํ๊ณ  ์ถ๋ค๋ฉด ๋ถ๋ชจ ์ปดํฌ๋ํธ์์ props๋ฅผ ์ ๋ฌํด์ค์ผ ํ๋ค.

> #### Child ์ปดํฌ๋ํธ์ props๋ฅผ ์ ๋ฌํ๋ ๋ฐฉ๋ฒ
>
> `<\Child message="๋๋ ์ด์ฝ๋ฆฟ์ ๋งค์ฐ ์ข์ํฉ๋๋ค." />`

#### Child ์ปดํฌ๋ํธ์์ ์ ๋ฌ๋ props๋ฅผ ๋ณด์ฌ์ค ๋

`console.log({this.props.message});`

- props๋ javascript ์๋ฃํ์ด ๋ฌด์์ด๋ ์ง ๋ค ๋๊ฒจ์ค ์ ์๋ค.(๊ฐ์ฒด, ๋ฐฐ์ด, ํจ์, Number ๋ฑ๋ฑ...)

# ๐ค ๋ถ๋ชจ์ state์ ์๋ ๋ฐ์ดํฐ๋ฅผ Child ์ปดํฌ๋ํธ์๊ฒ props๋ก ๋๊ธฐ๋ ๋ฐฉ๋ฒ

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

- ๋ถ๋ชจ์ state์๋ `color: 'red'` ๊ฐ ์ ์ฅ๋์ด ์๋ค.
- ์ด๊ฒ์ Child ์ปดํฌ๋ํธ์๊ฒ props๋ฅผ ํตํด ๋๊ฒจ๋ณด์

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

- titleColor๋ผ๋ ์์ฑ์ ๊ฐ์ผ๋ก this.state.color ๊ฐ์ ์ ๋ฌํด์ฃผ์๋ค.
- ์ฆ, ๋ถ๋ชจ ์ปดํฌ๋ํธ์ state ๊ฐ์ฒด ์ค์์ color์ ๊ฐ์ Child ์ปดํฌ๋ํธ์๊ฒ ์ ๋ฌํด์ค ๊ฒ์ด๋ค.

# ๐ค Child ์ปดํฌ๋ํธ ๋ด๋ถ์์ ์ ๋ฌ ๋ฐ์ props๋ฅผ ์ด๋ป๊ฒ ์ฌ์ฉํ ๊น?

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

- `h1` ํ๊ทธ์ ๊ธ์์์ ๋ค๋ฅธ ์์ผ๋ก ๋ฐ๊พธ๊ณ  ์ถ๋ค.
- ์๊น ๋ถ๋ชจ ์ปดํฌ๋ํธ์์ ๋ถ๋ชจ ์ปดํฌ๋ํธ์ ์ํ๋ฅผ ๊ฐ์ผ๋ก ๊ฐ์ง๊ณ  ์๋ `titleColor`๋ผ๋ ์์ฑ์ Child ์ปดํฌ๋ํธ์๊ฒ ์ ๋ฌํด์คฌ๋ค.
- ํ์ฌ Child ์ปดํฌ๋ํธ๋ props ๊ฐ์ฒด ์ค์์ titleColor ๊ฐ์ ๊ฐ์ง๊ณ  ์๋ค.
- `h1` ํ๊ทธ์ ์์์ ๋ฐ๊ฟ์ฃผ๊ธฐ ์ํด์ style์ ์ธ๋ผ์ธ์ผ๋ก css์ ์์ฑ ์ค color๋ผ๋ ์์ฑ์ ๋ถ๋ชจ ์ปดํฌ๋ํธ์์ ๋ฐ์์จ `props.titleColor`๋ก ์ค์ ํด์คฌ๋ค.

# props๋ฅผ ํตํ Event Handler ์ ๋ฌ

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

- ์ด๋ฒคํธ ํธ๋ค๋ฌ`handleColor()`๋ฅผ props ๊ฐ์ฒด๋ฅผ ํตํด Child ์ปดํฌ๋ํธ์๊ฒ ์ ๋ฌํ  ์ ์๋ค.

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

- `<button>` ์์์์ onClick ์ด๋ฒคํธ ๋ฐ์
- ์ด๋ฒคํธ ๋ฐ์ ์ `this.props.changeColor` ์คํ
- props ๊ฐ์ฒด์ `changeColor` = ๋ถ๋ชจ ์ปดํฌ๋ํธ๋ก๋ถํฐ ์ ๋ฌ๋ฐ์ `handleColor` ํจ์ ์คํ
- `handleColor` ํจ์ ์คํ ์ `setState` ํจ์ ํธ์ถ - state์ color ๊ฐ์ 'blue'๋ก ๋ณ๊ฒฝ
- render ํจ์ ํธ์ถ
- Child ์ปดํฌ๋ํธ์ ๋ณ๊ฒฝ๋ state ๋ฐ์ดํฐ(`this.state.color`) ์ ๋ฌ
- `this.props.titleColor`๋ฅผ ๊ธ์ ์์์ผ๋ก ์ง์ ํ๋ `h1` ํ์ดํ ์์ ๋ณ๊ฒฝ
