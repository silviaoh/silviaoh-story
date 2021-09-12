---
title: '[Record.GREAM] Click 시 활성화되고 비활성화되는 Dropdown'
date: 2021-09-07 23:09:23
category: 'Record'
thumbnail: { thumbnailSrc }
draft: false
---

## original Dropdown

![](https://images.velog.io/images/silviaoh/post/3b28ec0d-4914-4cc3-86fa-4f700210dd8a/dropdown%20original.gif)

KREAM 웹에 나와있는 확인사항이 드롭다운되는 기능이다. 이것을 바탕으로 기능을 구현해보고자 한다.

## 어떻게 시작해야할까?

```jsx
return (
  <Wrapper>
    <Title>구매 전 꼭 확인해주세요!</Title>
    {CONFIRMINFO.map(info => {
      return (
        <div key={info.id}>
          <Header>
            <InfoTitle>{info.title}</InfoTitle>
            <i className="fas fa-chevron-down" />
          </Header>
          <Body>
            <strong>{info.notice}</strong>
          </Body>
        </div>
      )
    })}
  </Wrapper>
)
```

- 내 코드는 map으로 여러 개의 확인사항이 출력되고 있는 상황이다.
- Click한 상태인지 아닌지 구별하기 위한 State가 필요하다.
- 해당 드롭다운 버튼이 클릭되었는지 판별하기 위한 State가 필요하다.
- 드롭다운 버튼 하나를 클릭할 때마다 Click 상태가 변해야한다.
- 버튼을 클릭했을 때 버튼을 구별할 수 있는 어떤 수가 State에 저장되어야 한다.

### 1. State 작성

```jsx
const [isClick, setIsClick] = useState(true)
const [dropdownId, setDropdownId] = useState(0)
```

### 2. 버튼을 클릭할 때 내용이 보여져야 함

```jsx
const [isClick, setIsClick] = useState(true)
const [dropdownId, setDropdownId] = useState(0)

const showDropdownBody = id => {
  if (id === dropdownId) {
    setIsClick(!isClick)
  }
  setDropdownId(id)
}

return (
  <Wrapper>
    <Title>구매 전 꼭 확인해주세요!</Title>
    {CONFIRMINFO.map(info => {
      const showCondition = info.id === dropdownId && isClick

      return (
        <div key={info.id}>
          <Header
            onClick={() => showDropdownBody(info.id)}
            show={showCondition}
          >
            <InfoTitle show={showCondition}>{info.title}</InfoTitle>
            <i className="fas fa-chevron-down" />
          </Header>
          <Body show={showCondition}>
            <strong>{info.notice}</strong>
          </Body>
        </div>
      )
    })}
  </Wrapper>
)
```

상수 데이터에 저장된 id값이 state에 저장된 id와 일치한다면 Click의 상태가 클릭할 때마다 바뀌도록 코드를 작성하였다.

그리고 body 부분에 show라는 속성을 부여하였다. 이 속성에는 상수 데이터 id의 값과 dropdownId의 값이 일치하고 isClick이 true일 때 true가 되도록 하는 조건을 주었다.

이제 이 조건이 일치하면 body부분의 스타일이 display: none에서 display: block으로 되어 보여지는 것이다.

이제 되겠지?! 두근두근...

![](https://images.velog.io/images/silviaoh/post/c39a8d8f-a92c-41e8-b89a-5fb8b6040191/error%20dropdown.gif)

?

처음에 엄청 좋아했다가 드롭다운 버튼 클릭해서 접고 다시 다른 확인사항 열려고 클릭하면 바로 열리지 않고 한 번 더 눌러야 열리는 현상을 목격해버렸다..

이거 생각하느라 한참을 머리 싸매고 콘솔에 로그 찍어보기도 하고 이리저리 코드 순서를 바꿔보기도하고 계속 고민하다가 드디어 원인을 발견하였다.

내가 선택한 3번 드롭다운 버튼을 처음 클릭하면 초기값이 true이기 때문에 열리고 dropdownId에 3이 설정된다. 한 번 더 클릭하면 id와 dropdownId가 일치하기 때문에 setIsClick이 다시 실행되어 false로 바뀐다.

이 상태에서 2번이나 1번 버튼을 클릭하면 id와 dropdownId가 값이 달라 조건을 만족하지 못하기 때문에 상태가 false 그대로이게 된다. 그래서 한 번만에 열리지 않는 것이다.

원인을 찾았으니 코드를 수정해볼까!

```jsx
const showDropdownBody = id => {
  id === dropdownId ? setIsClick(!isClick) : setIsClick(true)
  setDropdownId(id)
}
```

일치하지 않을 때 true로 바꾸면 되니까 id===dropdownId가 false일 경우에 isClick 상태를 항상 true로 업데이트하도록 해주면 되는 것이다!

## 성공!!

![](https://images.velog.io/images/silviaoh/post/83818eae-00b0-4c3e-a1e4-6de51a3c3dcf/dropdown%20success.gif)
