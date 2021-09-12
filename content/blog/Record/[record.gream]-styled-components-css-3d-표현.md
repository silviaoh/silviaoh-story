---
title: '[Record.GREAM] styled-components CSS 3D 표현'
date: 2021-09-07 23:09:27
category: 'Record'
thumbnail: { thumbnailSrc }
draft: false
---

Carousel을 구현하면서 뭔가 심심한 느낌이 들어서 상품을 더욱 강조하기 위해 디자인을 3D로 표현해봤다.

## 3D를 표현하기 위한 준비물은?!

3D를 표현하기 위해서 새로 등장한 속성이 있다. 바로 `perspective`이다.

### transform-style: preserve-3d & Perspective

Perspective는 투영점으로 어떤 개체에 원근감을 줄 수 있다. 관찰자 관점에서 가까이 볼 때와 멀리서 볼 때 사물의 모습이 다른 것을 볼 수 있는데, perspective 속성을 지정하게 되면 우리가 현실에서 직접 볼 때와 같이 웹 상에서 입체감을 부여할 수 있다.

!codepen[silviaoh/embed/NWjXKmJ?default-tab=html%2Cresult]

`transform: translateZ(200px)`을 두 개의 div에 동일하게 부여하였지만 우리의 눈에는 다르게 보여진다. 3번째 박스가 더 가까이 있는 것처럼 보인다. 세 번째 박스에서는 `transform-style: preserve-3d`로 이 박스는 3d로 보여지게 하겠다고 미리 선언하고 `perspective`로 원근감을 조절했기 때문에 이런 결과가 나타난 것이다.

!codepen[silviaoh/embed/WNjdeWW?default-tab=html%2Cresult]

perspective는 0이 평면이고 값이 작을수록 가까이 있는 것을 보는 것처럼 표현되며 값이 크면 클수록 멀리 있는 것을 보는 것처럼 표현된다. **perspective 속성은 3d를 적용할 대상에 직접적으로 부여하는 것이 아닌 한 단계 위의 부모에서 속성을 부여해야 올바르게 적용된다는 것도 알아두자!**

## 그럼 적용해보자!

이번 프로젝트에서는 Radio 버튼과 Label을 이용해서 슬라이더를 구현해보았다.

### Carousel Component

```jsx
...

return (
    <Wrapper>
      <LeftButton>
        <i class="fas fa-chevron-left" />
      </LeftButton>
      <InWrapper>
        <Slides>
          {RADIOS.map(id => {
            return <Image key={id} />;
          })}
        </Slides>
      </InWrapper>
      <RightButton>
        <i class="fas fa-chevron-right" />
      </RightButton>
      <Controls>
        {RADIOS.map(id => {
          return (
            <Label key="id">
              <Radio
                type="radio"
                name="radio"
                id={id}
                value={id}
              />
            </Label>
          );
        })}
      </Controls>
    </Wrapper>
```

### styled-components(3D 관련 컴포넌트)

```jsx
const InWrapper = styled.div`
  position: relative;
  height: 500px;
  width: 500px;
  max-width: 473px;
  padding: 50px;

  ${/*아래는 3d 효과 적용 부분*/}
  transform: perspective(2000px) rotateY(-30deg) translateZ(-40px);
  transform-style: preserve-3d;
`;

const Slides = styled.div`
  min-width: 540px;
  transition: 0.7s linear;
`;

const Image = styled.img.attrs(props => ({
  src: 'http://source.unsplash.com/1000x1000/?flower',
}))`
  position: absolute;
  height: 70%;
  width: 70%;
  transition: all 0.5s linear;
  box-shadow: 2px 2px 5px #000;
  border-radius: 1%;
`;
```

![](https://images.velog.io/images/silviaoh/post/01ad0fc6-611e-413d-b43a-5a1f6f182028/image.png)

> 디자인 참고 Youtube : https://www.youtube.com/watch?v=xuf4o7WoPU8
