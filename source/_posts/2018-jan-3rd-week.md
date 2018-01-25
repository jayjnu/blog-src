---
title: 1월 2~3째주 프론트엔드 이슈
date: 2018-01-24 19:44:53
categories:
- Weekly
tags:
- Chrome
- CSS
- TC39
- jQuey
- ASI
- ECMAScript
- Webpack
- Javascript
---

2주동안 밀린 것들이 많아 한번에 포스팅하도록 하겠습니다.

## [1. 크롬 65에 default로 탑재될 CSS Paint API](https://developers.google.com/web/updates/2018/01/paintapi)

CSS Paint API (CSS Custom Paint 등으로도 알려진)가 크롬에 기본으로 탑재될 예정이다.
CSS Paint API를 한마디로 정의하면, CSS에서 사용할 이미지를 JS로 미리 그려놓고 스타일시트에서 `paint()`함수로 해당 JS를 불러오면 이미지처럼 동작하게 해주는 API다.

CSS Paint API를 이용하여 CSS 이미지를 `url()`, `linear-gradient()` 등의 기본 CSS 메소드가 아니라 직접 Javascript로 paint worklet을 작성하여 `paint(myCustomImage)` 와 같이 작성할 수 있다.
본문에 실제 사용 법이 코드로 잘 설명되어 있으니 참고하면 좋을 듯 하다.

## [2. Webpack 4.0이 default로 설정없이(configless) 동작할 예정](https://github.com/webpack/webpack/issues/6244)

Webpack 4부터 귀찮은 Boilerplate 가 사라지고 기본적인 설정은 default로 동작할 예정이다.

> [Convention over Configuration](https://en.wikipedia.org/wiki/Convention_over_configuration)

즉 설정의 상당수가 사람들이 관습처럼 사용하고 있는 boilerplate 이기 때문에 설정 대신 컨벤션을 우선해서 따랐다는 평가다. 
[Parcel](https://parceljs.org/)이 설정없는 간단한 번들링 툴로써 웹팩의 대체재로 주목받기 시작한지도 얼마 되지 않았는데, 웹팩이 다시 선두자리를 굳건히 지킬듯 보인다.

## [3. jQuery 3.3.0 출시](http://blog.jquery.com/2018/01/19/jquery-3-3-0-a-fragrant-bouquet-of-deprecations-and-is-that-a-new-feature/)

React, Vue, Angular로 난무하는 프론트엔드 월드에 갑작스레 jQuery얘기가 나와서 김이 새는 느낌이 있지만, jQuery 3.3.0이 출시되었다. 새로 추가된 기능과 deprecation 목록이 나와있으니 참고하면 좋을 듯 하다.

## [4. semi-colon 사용을 의무화 하는 것을 고려중인 TC39](https://github.com/tc39/ecma262/pull/1062) 

ESLint 등 코딩 컨벤션에 대한 룰을 정할때 가장 고민 되는 요소중 하나가 세미콜론을 강제하느냐 마느냐의 문제다. (참고: [semi](https://eslint.org/docs/rules/semi))

기존 브라우저 환경의 경우 세미콜론이 없을때 자바스크립트 인터프리터가 에러를 뱉어내는 경우가 있기 때문에 세미콜론 사용이 자연스레 권장되었다. 그러나 babel과 lint를 사용한 자바스크립트 개발환경이 사실상 표준이 되면서 규칙이 또 한번 흔들리기 시작했다.

자바스크립트는 Automatic Semicolon Insertion(이하 ASI)을 이용한다. 흔한 예로 아래의 코드를 흔히 보았을 것이다.

```javascript
function foo() {
  return
  'foo';
}

console.log(foo()) // undefine
```

특정한 자바스크립트의 룰로 인해 return 다음에 새로운 라인에 자동적으로 세미콜론이 들어가기 때문에, 의도했던 것과 다른 코드가 나오는 것을 볼 수 있다. 자바스크립트의 ASI 룰을 잘 이해하고, 코딩 컨벤션을 잘 지키는 개발자들의 경우 이러한 문제를 실제로 겪을 일은 드물다.

그렇다면 TC39가 세미콜론을 명시적으로 사용하는 것을 표준으로 채택하는데 고심하게 된 배경은 무엇일까? (TC39가 궁금하다면?: [자바스크립트 표준은 어떻게 만들어지는가?](https://gamecodingschool.org/tag/tc39/))

proposal에 적힌 원문은 아래와 같다.

> as new syntactic features are added to ECMAScript, additional cases requiring explicit semicolons emerge over time. As such, consistently explicit semicolon use is recommended.

해석하자면 "새로운 문법이 ECMA스크립트로 추가되는 과정에서 명시적으로 세미콜론을 사용해야 하는 경우가 나타나고 있다. 그러므로 일관성있게 세미콜론을 명시적으로 사용하는 것을 권고한다."는 것이다.

물론 이에 대해 많은이들이 반박을 하고 나섰다. 그걸 다 번역하고 있기는 어려우므로 본문의 PR을 참고하도록 하자.

TC39의 입장에 대해 정리한 [ljharb](https://github.com/ljharb)의 [댓글](https://github.com/tc39/ecma262/pull/1062#issuecomment-357037779)을 인용하자면 아래와 같다.

> **ASI에대한 신뢰도를 떨어뜨리는 것**이 위원회의 컨센서스이며 의도다. 세미콜론을 사용하고 있지 않은 이들을 "나쁘다"거나 "오용한다"고 낙인을 하려는 의도는 아니지만, 본문은 말그대로 중립적인 스탠스라고는 할 수 없다.
> 세미콜론을 쓰느냐 마느냐의 문제로 논쟁하는 것은 이 PR 에서 하는 것이 생산적이라고 보진않는다. 부디 그방향으로 가지 말기를.. 

개인적으로는 세미콜론을 쓰는 것을 좋아한다. 그렇게 해왔던 것이 익숙하기도 하고, 애초에 에러를 일으킬 가능성이 있다면 사용하지 않는것이 낫다고 생각하기 때문이다.

## [5. 사소하지만 유용한 ES7 + ES8 기능 6가지](https://davidwalsh.name/es7-es8-features)

"ES6도 모르는데 ES8이라고?" 라는 생각을 한다면 정신차리고 노오오오오오오오력을 해서라도 알아야할 유용한 기능이다. 자바스크립트 개발자가 되기로 마음먹었다면 어쩔 수 없다. 같은 저자가 [ES6버전](https://davidwalsh.name/es6-features)도 올려두었으니 먼저 보고 오도록 하자

## [6. Javascript를 이용해 간단한 실시간 온라인 자동차게임 제작해보기](https://codeburst.io/how-to-make-a-simple-multiplayer-online-car-game-with-javascript-89d47908f995)

저번에 크롤러였다면 이번에는 실시간 자동차 게임이다. 자바스크립트로 실시간 온라인 게임을 만들어보고 싶은데 어떻게 해야할지 모르겠다면 많은 도움이 될 문서다.

## [7. 2017년 가장 인기있던 자바스크립트 관련 글들](https://medium.com/dailyjs/the-most-popular-javascript-links-of-2017-e4616e8b48c7)

가장 인기있는 Framework은 이제 식상하니 가장 사람들이 많이 본 자바스크립트 관련 글에 대해서 알아보면 어떨까?

## [8. github 파일의 아이콘을 해당 포맷에 맞게 변경해주는 크롬 확장프로그램](https://github.com/lvarayut/github-file-icons)

github repository를 보면 다소 단조로운 파일 아이콘이 심심하게 느껴질 수 있다. 저장소에 올라와있는 파일을 해당 파일의 포맷에 맞는 아이콘으로 변경해주는 크롬 익스텐션이 있으니 한번 사용해보면 재미있을 것 같다.

## [9. 새로운 NPM package 네이밍 규칙](http://blog.npmjs.org/post/168978377570/new-package-moniker-rules)

오타를 이용한 악성 패키지 설치(typosquatting)등의 문제를 해결하기 위해 NPM이 새로운 패키지 룰에 대해 발표했다. package명에는 구두점(예: _, ., - 등과 같은)을 포함할 수 있으나, 악성 패키지 배포자들이 이를 이용하여 실수로 악성 패키지를 받도록 하는 이슈가 있었다. 이를 방지하기 위한 새로운 룰은 다음과 같다

- 이전에 npm에 올라온적이 없는 새로운 이름의 패키지를 배포할 경우, npm은 모든 구두점을 제거한 뒤 기존의 패키지 (구두점을 제거한)와 비교한다.
- 만약 구두점을 제외한 패키지명이 동일할 경우, 해당 패키지명으로 npm에 등록할 수 없다.
- 대신, 패키지 배포자의 scope를 이용하여 배포하도록 제안한다.

예) react-native가 기존 패키지에 존재할 때 아래의 패키지명으로는 레지스트리에 등록이 불가능하다.

- reactnative
- react_native
- react.native

스코프를 사용할 경우 다음과 같이 해결할 수 있다.

변경전 (배포불가상태)

```json
{
  "name": "react_native"
}
```

변경 후 (스코프적용)

```json
{
  "name": "@jayjnu/react-native"
}
```

## [10. JSConf US가 돌아왔다](https://twitter.com/jsconfus/status/953310891595898880)

그동안 아시아, 유럽에서만 열렸던 JSConf가 다시 미국땅에서 열린다고 한다. Reddit 댓글을 살펴보니 초창기에 미국에서 열렸을때는 행사진행 경험 부족으로 다소 냉소적인 반응이었다고 한다. 개인적으로는 JSConf영상에서 자바스크립트 코어나 함수형 프로그래밍 관련하여 많은 도움을 얻었던 터라 상당히 기대가 된다. 미국은 가지 못해도 영상은 올라올 것이니..