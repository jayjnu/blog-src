---
title: 1월 1째주 이슈
date: 2018-01-08 18:55:41
categories:
- Weekly
tags:
- webpack
- Intel
- javascript
- node.js
- npm
---

## 1. [Webpack 4.0에서 JSON Tree Shaking을 지원할 예정](https://react-etc.net/entry/json-tree-shaking-lands-in-webpack-4-0)

곧 출시될 Webpack 4에 JSON tree shaking 이 탑재된다고 한다 (참고: [Tree Shaking이란?](https://github.com/FEDevelopers/tech.description/wiki/Webpack-2-Tree-Shaking-Configuration)). 실제로 코드레벨에서 사용하지 않는 JSON 속성은 컴파일 타임에 삭제된다.


## 2. [Intel의 CPU 게이트가 프론트엔드에 미칠 영향](https://twitter.com/dan_abramov/status/948742752103223297)

인텔의 CPU 설계상 치명적 결함이 발견되면서 세계가 들썩이고 있다. ReactJS 의 maintainer인 Dan Abramov 는 그의 트윗에 이 사건이 프론트엔드에 미칠 이슈에 대해 "Bye bye performance.now() resolution?" 이라는 우려의 글을 남겼는데, 한 reddit 유저가 해당 트윗과 관련되어 나눈 글을 아래와 같이 정리했다.

 
- SharedArrayBuffer 를 사용할 수 없게 된다.
- 장기적으로는 performance.now() and SharedArrayBuffer 를 사용할 수 있을지 모르겠지만, 현재로서는 불가능 할듯
- 위에 언급된 사항은 시작점에 불가하며 CPU에 의존적인 여타 API 또한 취약점에 노출된다고 하면 사용할 수 없게 될지도 모른다.


## 3. [존재하는지도 몰랐던(사실 몰라도 상관없는) 각종 JS 기능들](https://air.ghost.io/js-things-i-never-knew-existed/)

알고보면 쓸모는 없지만 신기한 자바스크립트의 각종 기능들을 몇가지 나열해두었다. 실제로 사용할만한 것은 그다지 없어보이고, 코드리뷰 역풍을 맞게 될 것이니 재미로만 보도록 하자


## 4. [마트에서 특정 물품이 세일하면 와이프에게 SMS를 보내는 봇을 만든 후기](https://chatbotsmagazine.com/building-a-foodkick-sms-sale-notifier-bot-64106c9de945)

원제는 "Building a FoodKick SMS Sale Notifier Bot with PhatomJs + Node.js + SElenium + Heroku + Twilio SMS" 으로 대충 해석하면 "노드 등등 으로 마트 세일 알림 봇 만들기" 쯤 된다. 
이 블로그 포스팅은 노드JS를 이용한 실제 웹사이트 크롤러에 대해 관심이 있는 사람이라면 읽어볼만 하다.

## 5. [NPM 운영 사고 - 약 130개의 repository가 사용 불가 상태가 되다](http://blog.npmjs.org/post/169432444640/npm-operational-incident-6-jan-2018)
지난 5일 NPM 라이브러리가 몇시간동안 다운로드가 되지않는 초유의 사태가 있었다. 본문에 따르면 외부 공격에 의한 것은 아니며, 기존 NPM 사용자의 계정과 관련된 패키지에는 아무 영향이 없다고 한다.
보안상의 이유로 자세한 원인에 대해 설명은 못한다고 했지만, 악성 패키지를 검증하여 삭제하는 봇이 정상적인 패키지를 악성으로 인식하여 일어난 것이 원인이라고 밝혔다. 