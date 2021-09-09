---
title: '[ReactJS.2] React Router'
date: 2021-09-07 22:09:21
category: 'ReactJS'
draft: false
---

# 프론트엔드에서 라우팅이란?

- 다른 경로에 따라서 특정 View(화면)을 보여주는 것이다.
- React 자체에는 이러한 기능이 내장되어 있지 않다.
- `React-Router` : 리액트의 라우팅 기능을 위해 가장 많이 사용되는 라이브러리
  > 여기에서 '경로'는 **URL**을 말함

# SPA(Single Page Application)

- 페이지가 한 개인 애플리케이션
- html 문서를 한 개만 가지고 있다.

> #### 반대되는 개념
>
> **MPA(Multiple Page Application)**

- 여러 개의 웹 페이지를 가지고 있는 애플리케이션
- html 문서 여러 개를 가지고 있다.

# Routing

## 1. react-router 설치

```
npm install react-router-dom --save
```

> #### --save
>
> 내 프로그램을 누군가 클론해서 사용하려고 했을 때 --save로 package.json에 버전 정보를 저장해놓지 않으면 그 사람은 내 소스에 적용된 라이브러리 파일들을 설치 받을 수 없다.

## 2. Routes Component 구현

`Routes.js`

```jsx
import React from 'react'
import { BrowserRouter as Router, Switch, Route } from 'react-router-dom'

import Login from '(내 Login.js 경로)'
import Main from '(내 Main.js 경로)'

class Routes extends React.Component {
  render() {
    return (
      <Router>
        <Nav />
        <Switch>
          <Route exact path="/" component={Login} />
          <Route exact path="/main" component={Main} />
        </Switch>
      </Router>
    )
  }
}

export default Routes
```

> #### `<>` 안에 작성한 것 = Component

- Component 이름은 시작을 무조건 대문자로 작성할 것!

  >

- <Switch> 밖에다가 작성하면 어느 경로에서든지 공통으로 나타난다.

  - ex) `<Nav />`

#### `exact`(정확한)

- /를 구분할 수 없어서 '/main'을 url로 입력하여도 login 페이지로 간다.

## index.js

```jsx
ReactDOM.render(<Routes />, document.getElementById('root');
```

named export vs default export
export {Routes};
import 할 때도 똑같이 중괄호 쳐야 함
여러 가지의 파일을 내보내야 할 때

# Route 이동하기

## 1. Link Component

```jsx
import React from 'react'
import {Link} from 'react-router-dom';

class Login extends React.Component {
  render() {
    return (
      <div>
        <Link to="/main">메인 페이지로</Link>
      </div>
    )
  }
}

exports default Login;
```

- Link 컴포넌트는 react-router-dom에서 제공하는 것이다.
- Link 컴포넌트는 DOM에서 a 태그로 변환된다.

> <a\> vs <Link\>
>
> - <a\> : 외부 프로젝트 파일로 이동하는 경우
> - <Link\> : 프로젝트 내에서 페이지 전환하는 경우
>
> #### Q. 왜 링크를 쓸까?
>
> - 효율이 다르기 때문이다.
> - `a 태그` : 서버에다 파일을 요청해서 다시 html파일을 받아온다(전체 다시 다운)
> - `Link` : 새롭게 파일을 받아오는 요청을 하지 않는다.
> - 효율적으로 진짜 바뀌는 부분만 가져온다.

## 2. withRouterHOC

```jsx
import React from 'react';
import {withRouter} from 'react-router-dom';

  // 실제 활용 예시
  // goToMain = () => {
  //   if(response.message === "valid user"){
  //     this.props.history.push('/main');
  //   } else {
  //     alert("너 우리 회원 아님. 가입 먼저 해주세요")
  //     this.props.history.push('/signup');
  //   }
  // }
render() {
  return (
    <div>
      <button
        className="loginBtn"
        onClick={this.goToMain}
      >
        로그인
      </button>
    </div>
  );
}

export default withRouter(Login);

```

- `HOC`는 컴포넌트를 감싸는 컴포넌트
- `withRouter(Login)` : withRouter와 같이 해당 컴포넌트를 감싸주는 것이 Higher Order Component라고 한다.
- 감싸주는 이유? = props에서 route 정보들을 받기 위해서 감싸준다.
