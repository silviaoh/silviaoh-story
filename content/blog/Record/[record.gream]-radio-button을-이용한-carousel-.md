---
title: '[Record.GREAM] Radio Button์ ์ด์ฉํ Carousel'
date: 2021-09-07 23:09:96
category: 'Record'
thumbnail: { thumbnailSrc }
draft: false
---

## ๐ Carousel์์ ์ด๋ค์ผ ํ  ๋ชฉํ

- label์ ํด๋ฆญ ์ ํด๋น ์ด๋ฏธ์ง๋ก ์ด๋
- ๋ค์ ๋ฒํผ์ ํด๋ฆญ ์ ๋ค์ ์ด๋ฏธ์ง๋ก ์ด๋
- ์ด์  ๋ฒํผ์ ํด๋ฆญ ์ ์ด์  ์ด๋ฏธ์ง๋ก ์ด๋
- ์ด๋ ์ fade ํจ๊ณผ ๋ถ์ฌ

## label ํด๋ฆญ ์ ํด๋น ์ด๋ฏธ์ง๋ก ์ด๋ & ์ด๋ ์ fade ํจ๊ณผ ๋ถ์ฌ

#### Q. label๊ณผ Radio๋ฅผ ์ด๋ป๊ฒ ์ฐ๊ฒฐ์ํค์ง?

label์ ์์ฑ์ธ for=<id๊ฐ>์ ์ด์ฉํ๋ฉด ๋๋ค. React์์๋ for๊ฐ ์๋ htmlfor์ด๋ผ๋ ๋ช์นญ์ ์ฌ์ฉํ๋ค๋ ๊ฒ์ ๊ธฐ์ตํ์!

```
<Controls>
        {RADIOS.map(id => {
          return (
            <Label key="id" htmlFor={id}>
              <Radio
                type="radio"
                name="radio"
                id={id}
              />
            </Label>
          );
        })}
      </Controls>
```

#### Q. ์ฌ๋ฌ ๊ฐ์ label ์ค ํด๋ฆญํ label์ ํด๋นํ๋ ์ด๋ฏธ์ง๋ง ์ด๋ป๊ฒ ๋์ค๋๋ก ํ์ง?

- buttonId๋ผ๋ state๋ฅผ ์์ฑ
- ๋ผ๋ฒจ์ ํด๋ฆญํ๋ฉด ๋ผ๋ฒจ์ ํด๋นํ๋ ์์ ๋ฐ์ดํฐ ์์ ์๋ id๋ฅผ state์ ์ ์ฅ(์ด๋ฏธ์ง๋ ๋ผ๋ฒจ๊ณผ ๋๊ฐ์ id๋ฅผ ๊ฐ์ง๊ณ  ์์)
- map์ ๋งค๊ฐ๋ณ์์ธ id์ state์ ์ ์ฅ๋์ด ์๋ id๊ฐ ์ผ์นํ๋ ์ด๋ฏธ์ง๋ง opacity: 1์ด ๋๋๋ก ์ฝ๋ ์์ฑ

```jsx
const Carousel = () => {
  const [buttonId, setButtontId] = useState('r1');

  ...

  const handleRadioChange = e => {
    setButtontId(e.target.value);
  };

  ...

return (
    ...

<Controls>
  {RADIOS.map(id => {
     return (
      <Label key="id" htmlFor={id} checked={id == buttonId}>
        <Radio
          type="radio"
          name="radio"
          id={id}
          value={id}
          onChange={handleRadioChange}
         />
       </Label>
      );
   })}
</Controls>
    ...

)};
...

const Image = styled.img.attrs(props => ({
  src: 'http://source.unsplash.com/1000x1000/?flower',
}))`
  position: absolute;
  height: 70%;
  width: 70%;
  transition: all 0.5s linear;
  box-shadow: 2px 2px 5px #000;
  border-radius: 1%;
  opacity: ${({ checked }) => (checked ? 1 : 0)};
`;
```

## ๋ค์ ๋ฒํผ์ ํด๋ฆญ ์ ๋ค์ ์ด๋ฏธ์ง๋ก ์ด๋

#### Q. state buttonId๋ฅผ ์ด์ฉํ๋ฉด ๋  ๊ฒ ๊ฐ์๋ฐ ์ด๋ป๊ฒ ์ด์ฉํด์ผํ์ง?

์์์ ๋งค๊ฐ๋ณ์ id === buttonId์ ๋น๊ตํ๋ checked ์์ฑ์ด ์ฐธ์ด๋ฉด ์ด๋ฏธ์ง๊ฐ ๋ํ๋๋๋ก ์ฝ๋๋ฅผ ์์ฑํ์๊ธฐ ๋๋ฌธ์ buttonId๋ง ๋ค์ id๋ก ๊ฐ๋๋ก ์ค์ ํด์ฃผ๋ฉด ๋๋ค.

buttonId์ ์ ์ฅ๋์ด ์๋ id๊ฐ `r1`์ด๋ฐ ํ์์ผ๋ก ๋์ด์๊ธฐ ๋๋ฌธ์ ์ซ์๋ง ์ด์ฉํ๊ธฐ ์ํด์ ๋ณ์๋ฅผ ๋ฐ๋ก ์ ์ธํ์ฌ slice๋ก ์ธ๋ฑ์ค 1์ ํด๋นํ๋ ๋ถ๋ถ๋ง ์ ์ฅํ์๋ค.

๋ค์ ๋ฒํผ์ ๋๋ ์ ๋ id์ ์ซ์ ๋ถ๋ถ๋ง ์ ์ฅ๋ ๋ณ์์๋ค 1์ ๋ํ๋๋ก ๋ก์ง์ ๊ตฌ์ฑํ์๊ณ  ๋ง์ฝ ์ ์ผ ๋ ๋ถ๋ถ์์ ๋ฒํผ์ ๋๋ฅธ๋ค๋ฉด ์ฒ์ id๋ฅผ ์ค์ ํ๋๋ก ํ์๋ค.

```jsx
const moveRight = () => {
 const changedNum = Number(buttonId.slice(1));
 setButtontId(`r${changedNum + 1}`);
 changedNum === RADIOS.length && setButtontId(`r1`);
};

return (
  ...

  <LeftButton onClick={moveLeft}>
    <i class="fas fa-chevron-left" />
  </LeftButton>

  ...

);
```

## ์ด์  ๋ฒํผ์ ํด๋ฆญ ์ ์ด์  ์ด๋ฏธ์ง๋ก ์ด๋

์ด์  ๋ฒํผ๋ ๋ค์ ๋ฒํผ๊ณผ ๋ก์ง์ ๋น์ทํ๋ค. ๋ค์ ๋ฒํผ์ ๋๋ ์ ๋๋ 1์ ๋ํด์คฌ๋ค๋ฉด ์ด์  ๋ฒํผ์ 1์ ๋นผ๋ฉด ๋๊ณ  ๋งจ ์ฒ์ ์ด๋ฏธ์ง๋ผ๋ฉด ๋ค์ ๋์ ์ด๋ฏธ์ง์ id๋ก buttonId๋ฅผ ์ค์ ํด์ฃผ๋ฉด ๋๋ค.

```jsx
const moveLeft = () => {
  const changedNum = Number(buttonId.slice(1))
  setButtontId(`r${changedNum - 1}`)
  changedNum === 1 && setButtontId(`r${RADIOS.length}`)
}
```

## ์์ฑ!!

![](https://images.velog.io/images/silviaoh/post/83efc9ff-07c3-4d1e-b27a-5c34c9fe39ca/GREAM%20carousel.gif)
