---
title: '[Record.GREAM] 경로와 쿼리 변경될 시 최상단으로 이동'
date: 2021-09-07 23:09:80
category: 'Record'
draft: false
---

## ScrollToTop.jsx

```jsx
import { useEffect } from 'react'
import { useLocation } from 'react-router-dom'

const ScrollToTop = () => {
  const { pathname, search } = useLocation()

  useEffect(() => {
    window.scrollTo(0, 0)
  }, [pathname, search])

  return null
}

export default ScrollToTop
```

## 컴포넌트 위치

![](https://images.velog.io/images/silviaoh/post/c98eef30-0b7a-48c2-849a-99d39f507da3/image.png)

## Router 컴포넌트 안에 작성

![](https://images.velog.io/images/silviaoh/post/d4dc5273-30ba-4846-8f01-c7a62948d53e/image.png)

> ❗️ 공용 컴포넌트 디렉토리에 위치시켜두고 Routes.js 폴더에 선언하여 pathname과 search를 인식하도록 함
