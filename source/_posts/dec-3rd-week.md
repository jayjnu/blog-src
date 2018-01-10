---
title: 12월 3째 주 프론트엔드 이슈
date: 2017-12-22 10:44:45
categories:
- Weekly
tags:
- ServiceWorker
- Javascript
- React.js
- V8
---

## [1. 여자친구의 인스타그램 업로드에 자동으로 좋아요를 눌러주고 푸쉬알림을 올려주는 봇](https://github.com/gulzar1996/auto-like-my-gf-insta-pic)
[Reddit/r/javascript](https://github.com/gulzar1996/auto-like-my-gf-insta-pic)에 한 유저가 제목과 같은 Node js 앱을 올려서 화제다.
말그대로 여자친구가 새로운 인스타그램 사진을 올리면 자동으로 좋아요를 누르고 slack과 연동하여 푸쉬알림을 넣어준다.


## [2. 서비스워커, 개발자용 사파리 46 버전에 디폴드로 탑재](https://webkit.org/blog/8042/release-notes-for-safari-technology-preview-46/)
고성능의 Progressive Web App을 제작함에 있어 필수적이라고 할 수 있는 서비스 워커가 개발자용 사파리 버전에 디폴트로 탑재되어 선공개되었다.

## [3. 2,300명의 개발자가 생각하는 자바스크립트는?](https://medium.freecodecamp.org/i-just-asked-23-000-developers-what-they-think-of-javascript-heres-what-i-learned-9a06b61998fa)

얼마전 이슈가 됐던 [State of Javascript](https://stateofjs.com/2017/introduction/)라는 통계 발표 이후, 관련 조사를 했던 [@sachagreif](https://medium.freecodecamp.org/@sachagreif) 가 이번에는 2,300명의 개발자에게 자바스크립트에 대한 의견을 모아 하나의 글로 정리하였다.

1. React는 지금의 인기를 유지할것이다.
2. Angular는 기존과는 다른 포지션을 가져갈 것이다.
3. Vue.js는 더이상 무시할 수 없는 지위로 성장했다.
4. 라이브러리에 대한 지식이 연봉 상승에 큰 도움이 된다. (당신이 생각할만한 이유때문은 아니다 - 역주: 통계의 함정)
5. 2018년은 GraphQL의 해가 될 것이다
6. Javascript != Front-end 
7. VSCode, 마이크로소프트의 역습
8. 각 나라별로 다른 Javascript 생태계
9. 정적타입을 지원하는 Javascript의 부상
10. 자바스크립트의 (거의)무한한 가능성


## [4. 리액트로 새단장한 Outlook.com](https://react-etc.net/entry/new-outlook-com-built-with-react)

구글의 Gmail과 함께 세계에서 가장 큰 메일 서비스 중 하나인 Outlook에서 마이크로소프트가 리액트를 사용했다는 것은 시사하는 점이 크다. 본문 아티클에서 마이크로소프트가 핵심 웹 UI기술의 왕좌를 React.js로 넘겼으며, React.js의 개발자들이 현재 웹 개발의 패러다임을 얼마나 크게 바꾸었는지를 확인 할 수 있다고 평가했다.

## [5. V8엔진 - Javascript Code Coverage](https://v8project.blogspot.kr/2017/12/javascript-code-coverage.html)

Code Coverage는 App이 구동되는 동안 특정 코드 영역이 얼마나 실행되는지에 대한 정보를 제공한다.
이 기능은 디버깅을 하거나 테스트를 할 때 상당히 유용해 보인다.
본문에 어떻게 사용하는지에 대한 자세한 정보가 사진을 통해 나와있으니 참고하자