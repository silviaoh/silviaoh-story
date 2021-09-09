---
title: '[Record.녹차록] List & Detail Page 구현 내용'
date: 2021-09-07 22:09:88
category: 'Record'
draft: false
---

# Intro

녹차록 페이지에서 내가 맡은 부분인 List, Detail의 기능에 대해 간단히 설명하고자 한다.

# List

### Video Carousel

![](https://images.velog.io/images/silviaoh/post/94fa7339-5491-4c53-bd6f-89c809dcb46c/image.png)

- 버튼을 클릭하면 이동하는 슬라이드
- 카테고리별로 동영상이 하나씩 존재하여 현재 재생되는 동영상의 카테고리 이름이 밑에 보이도록 동시에 슬라이드되는 기능이 추가됨
- 카테고리 이름에 해당하는 검은 띠 부분은 드래그가 되도록 구현!

### Sorting

![](https://images.velog.io/images/silviaoh/post/2c5e36be-522a-481f-b6f2-b5c1d8b1b920/image.png)

- 신상품순, 높은 가격순, 낮은 가격순 정렬이 가능하도록 구현
- 백에서 구현해주신 엔드포인트로 접근하여 결과 fetch함

### Category Button

![](https://images.velog.io/images/silviaoh/post/9b1b195a-4a75-4df7-9213-61efb3c5245d/image.png)

- 백에서 구현해주신 엔드포인트로 접근하여 결과 fetch함
- 쿼리를 조작하여 `category=(id)`라는 결과를 만든 뒤, 이것으로 엔드포인트에 접근함

### Filtering

![](https://images.velog.io/images/silviaoh/post/598aa7e2-dad0-48e8-a59d-cdb2bc4104bc/image.png)

- 여러 기준을 중복하여 필터링한 결과가 나오게 해야 해서 매우 어려웠음.
- 특히 쿼리 파라미터를 조작해서 내가 원하는 쿼리가 나오게 해야하는 부분에서 매번 화를 다스려야 했음
- 버튼을 다시 눌러서 취소해야할 때 `product_type`이란 이름을 가진 쿼리 중 내가 누른 버튼에 해당하는 id를 가진 `product_type`만 제거해야했는데 하나의 버튼을 누르면 동시에 삭제되어 매우 곤란했다.

### Pagination

![](https://images.velog.io/images/silviaoh/post/b2a22be1-2bcb-4430-a453-20a74a474c6c/image.png)

- 버튼을 누르면 서버의 데이터를 24개씩 fetch하여 보여줌
- 이것도 쿼리를 조작하여 `offset=&limit=` 으로 엔드포인트에 접근

# Detail

### 카카오톡 공유하기

![](https://images.velog.io/images/silviaoh/post/8a275504-d10d-496e-9467-42cfe853dcf7/image.png)

- cross-origin 에러 발생으로 고생함
- 카카오톡 개발자 페이지에서 플랫폼 등록과 환경 변수를 추가하여 해결

> 자세한 글을 보고 싶다면 [여기](https://silviastory.netlify.app/Record/[record.녹차록]-kakao-link/)로!

### 상품금액 합계 계산 & 쇼핑백 동봉 +100원

![](https://images.velog.io/images/silviaoh/post/fbd412c8-9708-40ff-b2a5-e6230b11067c/image.png)

- 서버의 price 데이터를 이용하여 합계가 계산되도록 기능 구현
- 쇼핑백 동봉 함을 클릭시 합계에 100원이 추가되도록 구현

### URL 붙여넣기

![](https://images.velog.io/images/silviaoh/post/b599ed2c-bd9a-4b84-b480-0f2641160efa/image.png)

- 현재 URL이 복사되도록 구현
