---
title: '[GREAM] Review'
date: 2021-09-07 23:09:08
category: 'Review'
thumbnail: { thumbnailSrc }
draft: false
---

### 한 번 더 시작되는 도전

바람보다도 빠르게 휙~ 지나갔던 1차 프로젝트를 마감하고 2021.7.19일부터 7.30일까지 새로운 팀원들과 매칭되어 2차 프로젝트에 돌입했다. 이미 1차 프로젝트에서 많은 체력을 소모하였기 때문에 2차 프로젝트를 진행할 때는 내 기분이 필요 이상으로 많이 다운되지 않도록 하는 데 많은 주의를 기울였다.

필요 이상으로 기분이 다운된다면 내 텐션이 팀원들에게까지 영향을 미칠까 염려되었기 때문이다. 나만 힘든 것도 아니고 모두 이미 체력이 첫 프로젝트 시작할 때보다 많이 떨어지셨을텐데 굳이 내 감정대로 행동하는 것은 현명하지 못한 태도라는 판단이 들었다.

이번에는 [KREAM](https://kream.co.kr/)이라는 웹 사이트를 모티브로하여 프로젝트를 진행하였다. 이 사이트는 신발을 판매하는 사이트인데 일반 커머스 사이트처럼 단순히 구매 가격이 딱 정해져 있는 것이 아니라 입찰해서 구매하고 판매할 수도 있는 사이트라는 점이 핵심이었다.

![](https://images.velog.io/images/silviaoh/post/1a476218-f465-45b3-ba22-0660ebdd81b3/image.png)

신발을 판매하는 것이기 때문에 저작권 문제가 존재하였다. 그래서 팀원들과 상의한 끝에 신발을 판매하는 것이 아닌 판매 대상을 **그림**으로 바꾸어 그림 경매 사이트로 만들어보기로 결정하였다.

### 우리의 프로젝트에 도움을 준 Trello와 Notion

#### Trello

저번 프로젝트에서는 Trello를 주로 사용하였지만 이번에는 Trello와 Notion을 병행하여 사용하였다.

![](https://images.velog.io/images/silviaoh/post/e11a0336-24bc-4283-b2ca-3ed6416a8d85/image.png)

Trello에서는 Backlog에 처음에 우리가 해야 할 일을 카드로 다 작성하여 놓고 각 스프린트 때마다 진행해야 할 카드들을 각 보드에 옮기면서 서로의 진행사항과 현재 전체적으로 어디까지 완료가 되었는지 등을 알 수 있었다. 또한 추가적으로 Staging, Notification, 추가 구현 사항 부분을 생성하여 구현 중 막힌 부분이 무엇인지 우리가 기본적으로 알아야 할 사항들에는 어떤 것들이 있는지, 추가 구현할 기능들은 어떤 것이 있는지 한 눈에 알 수가 있었다.

이번에 Trello를 사용하면서 개인적으로 좋았던 점은 태그들을 세분화하여 표시했다는 점이다. 1차 때는 단순히 Front / Back 태그, 1차 스프린트 / 2차 스프린트 태그만 만들어서 표시해서 어떤 페이지에 포함된 기능인지는 한 눈에 알 수 없었다. 하지만 이번에는 서로 맡은 공통된 부분들을 태그로 생성하여 각각 카드에 입력해놓았는데 가독성이 훨씬 좋아져서 회의할 때 이 카드는 어떤 페이지에 속해 있는 기능인지 명확하게 알 수가 있었다.

#### Notion

![](https://images.velog.io/images/silviaoh/post/2fd2e8c2-ac77-45ff-8bbc-659c127ea02d/image.png)

2차에서는 Notion도 같이 사용하였다. Notion에는 FRONT의 진행상황이 현재 어디까지 완료되었는지 시각적으로 보여주기 위하여 각각 맡은 페이지들을 gif파일로 업로드해놓았다. 매일 아침 11시에 Stand up Meeting을 진행하였는데 빠른 진행을 위하여 어제 한 일, 오늘 할 일, 논의해야 할 일, 블로커에 대한 아젠다를 Meeting Notes에 따로 미리 작성하여 회의 시간을 단축할 수 있었다.

Notion에서 백엔드 분들이 따로 Postman에 엔드포인트 정보를 적어주셔서 백과의 소통이 좀 더 원활해졌고, Front 팀원들끼리도 개발할 때 찾은 정보들을 Notion에 따로 공유하였기 때문에 개발 시간을 많이 손실하지 않고 프로젝트를 진행할 수 있었다는 점도 이번 프로젝트에서 만족했던 부분이다.

### 쉽다고 생각했지만 여전히 존재하는 어려움

난 저번에 리스트와 상세페이지를 맡았었기 때문에 로그인과 회원가입 기능을 구현해보고 싶었다. 첫 Planning Meeting에서 각자 어떤 부분을 맡을지 논의를 해 본 결과 팀원들 간에 원하는 기능이 겹치게 되었고 서로 양보를 하여 난 상세페이지 부분을 구현하게 되었다. 사실 상세페이지는 데이터를 가져와서 보여주는 것이 대부분이었기 때문에 비교적 빨리 마무리 할 수 있을 줄 알았다. 하지만 이것은 나의 오판이었다..😅

백에서 보내주는 데이터의 양이 상당했고 구조도 1차 때보다 비교적 복잡했다. 프로젝트 초반에 내 부분을 빨리 구현하고 다른 분들 것을 도와드려야겠다고 생각한 내 자신을 반성하게 되었다.. **'빨리'**에 집중을 하는 것이 아니라 **'정확히'**로 목표를 바꿔 내 페이지가 결과적으로 잘 보여지도록 하는 것이 좋겠다는 생각이 들었다.

1차 때보다 더 많은 소통이 오고 갔다. 그도 그럴 것이 중간에 데이터 구조가 변경되는 일도 있었고 필요한 데이터가 들어 있지 않은 경우, 특정한 상품에 대한 데이터가 표시되는 엔드포인트가 존재하지 않는 경우.. 여러 상황에서 예상치 못하게 프론트와 백이 서로 맞지 않는 부분이 존재하였고 상세 페이지를 맡으신 재경님과 대화를 하지 않으면 해결이 되지 않는 상황이었기 때문이다. 결과적으로 서로 맞춰가면서 해결해나갈 수 있었다!

난 이때 백에서 온 데이터를 프론트에서 알맞게 표시해주기 위해서 새로운 알고리즘을 작성하는 법을 연습할 수 있어서 좋았다. 그래프에 들어가는 데이터에는 배열 형식으로 값은 값대로, 날짜는 날짜대로 들어가야하는데 백에서 온 데이터는 price와 날짜를 값으로 가진 객체를 가지는 배열 형식이었다. 보내준 게 다르다면 내 입맛대로 바꿔서 먹어야한다는 것을 이 때 알게 되었다. 처음부터 백에서 알맞은 형식으로 보내줬다면 더 좋았겠지만 그게 어려울 경우 프론트에서 데이터 구조를 맞게 변경하여 내가 원하는 형식으로 쓸 수 있어야 한다!

한편으로 내가 직접 로직을 작성해본 것은 너무 좋지만 다른 한 편으로 아쉬웠던 점은 처음에 데이터 구조를 처음에 어떤 형식으로 보내야할지 미리 생각을 해뒀어야겠다는 생각이 들었다. 처음부터 이것을 알고 미리 재경님께 이런 형식으로 보내주실 수 있으신지 여쭤봤다면 충분히 쉽게 해결가능했을텐데.. 나도 구현하다가 알게 된 부분이어서 다음 번에는 이것에 대해 미리 생각을 해보고 백과 소통을 한다면 더 수월한 개발이 가능할 것으로 예상된다!

### 어려움에 봉착했을 때 빛을 발하는 팀워크!

마지막에 마지막 날까지 예상치 못한 문제가 발생했다. 갑자기 AWS 서버가 켜져 있는데도 데이터가 나오지 않는 문제가 발생하였다. 최종 결과물에 대한 영상을 찍어야했는데 갑자기 이런 문제가 터지니 당황스러웠지만 백엔드 분들이 마지막까지 해결하려고 계속 노력하였고 우리 프론트 팀원들도 옆에서 같이 격려해가면서 프론트 쪽 문제가 아닐까 다시 생각도 해보고 멘토님께도 여쭤보면서 결국 문제를 해결하였다.

이번 프로젝트에서 이렇게 많이 소통해보고 같이 오손도손 모여서 문제를 해결해볼 수 있는 기회가 생겨서 너무 좋았고 체력적으로 힘들었지만 정말로 가족같은 분위기 안에서 팀 프로젝트를 마무리할 수 있어서 만족스러웠다.

> 상세페이지의 그 무수한 데이터로 고통받으신 우리 재경님, 서버 문지기 정민님, 분위기 메이커 한준님, 프론트 팀 마스터 정훈님, 폭풍 질문해주시는 경민님! 우리 팀원들 너무 고생 많으셨고 수고하셨어요! 기업 협업 가서도 우리 힘내고 또 프로젝트 같이 하면 너무 좋을 것 같습니다. 😆 모두 화이팅!!

> [GREAM Youtube](https://youtu.be/Mvr7map6Y2M)
