---
title: '[ReactJS.4] React State'
date: 2021-09-07 22:09:41
category: 'ReactJS'
draft: false
---

# ๐ Today's Goal

- state์ ๊ฐ๋์ ๋ํด ํ ๋ฌธ์ฅ์ผ๋ก ์ค๋ชํ  ์ ์๋ค.
- state๋ฅผ ์ด์ฉํด์ UI๋ฅผ ๊ตฌ์ฑํ  ์ ์๋ค.
- ์ด๋ฒคํธ๋ฅผ ํตํด state๋ฅผ ๋ณ๊ฒฝํ  ์ ์๋ค.

# State(์ํ)

- ์ปดํฌ๋ํธ ๋ด๋ถ์์ ๊ฐ์ง๊ณ  ์๋ ์ปดํฌ๋ํธ์ ์ํ๊ฐ
- **ํ๋ฉด์ ๋ณด์ฌ์ค ์ปดํฌ๋ํธ์ UI ์ ๋ณด(์ํ)๋ฅผ ์ง๋๊ณ  ์๋ ๊ฐ์ฒด**
- ๋ด ์ง๊ธ์ ์ํ๋ ๋ถ๋ชจ๋์๊ฒ์ ๋ฌผ๋ ค๋ฐ์ ์ ์๋ค.
- ์ํ๋ ๋ฐ๊ฟ ์ ์๋ค. ex) ๋ฐฐ๊ณ ํ -> ๋ฐฐ๋ถ๋ฆ

> JavaScript์์๋ DOM์ผ๋ก HTML์ ์ ๊ทผํด์ ๋์ ์ธ ๊ธฐ๋ฅ์ ์ถ๊ฐํ์ง๋ง **React์์๋ state ์ค์ฌ์ผ๋ก ์ฌ๊ณ ๋ฅผ ๋ฐ๊ฟ์ผ ํ๋ค.**

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

- `constructor()` state๋ฅผ ์ค์ ํ  ๋ ์์ฑํ๋ค.

  - ์ด ์์๋ super()์ this.state ๊ฐ์ **์ปดํฌ๋ํธ์ ์ด๊ธฐ ์ํ๊ฐ**์ ์ค์ ํด ์ฃผ์ด์ผ ํ๋ค.

> #### ์? ์ํ๊ฐ์ ์ค์ ํ ๊น?
>
> ์ปดํฌ๋ํธ ์์ ์์์์ ๊ทธ ์ํ๊ฐ์ ๋ฐ์ํด์ ๋ฐ์ดํฐ๊ฐ ๋ฐ๋ ๋๋ง๋ค ํจ์จ์ ์ผ๋ก ํ๋ฉด(UI)์ ๋ํ๋ด๊ธฐ ์ํด์์ด๋ค.

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

- `button`์์ `onClick` ์ด๋ฒคํธ ๋ฐ์
- ํ์ฌ state์ handleColor ํจ์ ์คํ
- handleColor ํจ์ ์์ setState ํจ์ ์คํ : state์ color ๊ฐ์ 'blue'๋ก ๋ณ๊ฒฝ
- render ํจ์ ํธ์ถ
- ๋ฐ๋ state ๊ฐ์ ๋ฐ์ํ์ฌ `h1` ํ๊ทธ ๊ธ์ ์์ ๋ณ๊ฒฝ

> React์์๋ state๋ฅผ ํตํด์ ์์ ์ UI๋ฅผ ๊ตฌ์ฑํ๋ค.
> ์ ์ฐจ์ ์ด์ง ์๊ณ  ํ๊ทธ ์์ ์ ์ธํ์ฌ ์๋์ ์ผ๋ก ์๋ฐ์ดํธ ๋ state๊ฐ ๋ฐ์๋๋ ๋ฐฉ์์ผ๋ก ํ๋ฌ๊ฐ๋ค๋ ๊ฒ์ ๋ช์ฌํ์!

> #### โ๏ธ ์ธ๋ผ์ธ ํ๊ทธ๋ฅผ ์ง์ํ์!
>
> ์ ์ง๋ณด์๊ฐ ์ด๋ ค์์ง๊ธฐ ๋๋ฌธ์ด๋ค.

> #### React์์๋ ์ค๊ณ ์์ฒด๊ฐ ๋จ๋ฐฉํฅ์ด๋ค.

- ํญ์ ์->์๋, ๋ถ๋ชจ->์์์ผ๋ก ํ๋ฅธ๋ค.
- ์ด๋ ๊ฒ ๊ฐ๋ ์ด์ ๋ ์ ์ง ๋ณด์๋ฅผ ์ฝ๊ฒ ํ๊ธฐ ์ํด์์ด๋ค.
- ๋ง์ฝ์ ์์ -> ๋ถ๋ชจ, ํ์  -> ํ์  ๊ฐ์๋ ํ๋ฅผ ์ ์๋ค๋ฉด props๊ฐ ์ด๋์ ์๋์ง ์ ์๊ฐ ์์ด์ ์ถ์ ์ด ์ด๋ ค์์ง๊ธฐ ๋๋ฌธ์ด๋ค.
