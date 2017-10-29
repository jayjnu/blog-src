---
title: 2017년 10월 4째주 프론트엔드이슈
date: 2017-10-29 21:30:32
categories:
- Weekly
tags:
- node.js
- chrome
- test
- Functional Programming
- webpack
---


## 1. body-parser 가 Express.js의 코어 미들웨어로

express 4.16.0 릴리즈에 기존 body-parser 라이브러리의 역할을 하는 express.json이 패키지로 추가됐다.
이제 매번 express로 리퀘스트 바디를 파싱하기위해 따로 라이브러리를 추가해야 하는 불편함이 사라졌다.


관련 링크: https://github.com/expressjs/express/releases/tag/4.16.0


## 2. 크롬 62 릴리즈

크롬 62 버전이 나오며 다음의 기능들이 추가되었다

### network information API  
기존에 제공하던 navigator.connection.type이라는 api는 이론적인 네트워크 상태 결과값만을 제공한다. 예를 들어 연결은 wifi지만 실제로는 3g 핫스팟에 연결된 핸드폰일 경우 wifi가 리턴된다.
반면에 새로 추가된 navigator.connection.effectiveType 속성은 이론적인 추정치가 아닌 실제 반환되는 값을 측정한다.
    
```javascript
// 기존 API
console.log(navigator.connection.type);
// returns wifi

//신규 API
console.log(navigator.getConnectionUrl.effectiveType);
//returns 4G
```
    
속도가 느린 디바이스일경우 더 축소된 버전의 웹페이지를 제공하는 등의 기법을 사용하면. 느린 네트워크에서도 사용자 경험을 향상시킬 수 있다.

### 오픈타입 가변 폰트 (OpenType Variable Fonts)  
기존에는 폰트파일 하나당 하나의 스타일만 적용 가능 했다. 예를 들어 폰트 하나에 Bold, Italic, Light 등의 스타일을 클라이언트에서 로드하려면 각각의 스타일에 해당하는 총 3개의 폰트 파일이 필요했다.
이번에 제공되는 오픈타입 가변 폰트를 사용하면 하나의 파일만으로도 수많은 폰트 스타일을 적용할 수 있다.
    
```css
.heading {
  font-family: "Avenir Next Variable";
  font-size: 48px;
  font-variation-settings: 'wght' 700, 'wdth' 75;
}
.content {
  font-family: "Avenir Next Variable";
  font-size: 24px;
  font-variation-settings: 'wght' 400;
}
```
    
오픈타입 가변 폰트를 이용하면 반응형 타이포그래피를 적용하기 더 쉬워질 뿐 아니라 페이지 로드 속도도 개선할 수 있다.

관련 링크: [Introducing OpenType Variable Fonts](https://medium.com/@tiro/https-medium-com-tiro-introducing-opentype-variable-fonts-12ba6cd2369)
    
### DOM Element에서 미디어 캡쳐
video나 audio같은 HTMLMediaElements에서 바로 MediaStream으로 컨텐트를 실시간 캡쳐할 수 있다.
HTMLMediaElement에 captureStream()을 호출하여 스트리밍된 컨텐츠를 변형하거나 조작할 수 있으며 기록하거나 원격으로 전송할 수 있다.

### HTTP 페이지에 '안전하지 않음' 라벨
크롬 62 버전부터 유저가 http페이지를 방문할 시 해당 페이지에 '안전하지 않음'을 상단 주소바에 표기한다.

### 기타 추가 및 변경 사항
- Payment Request API가 iOS 용 크롬에 탑재
- WebVR origin trial을 통해 본인의 사이트에 실험적으로 VR 경험을 제공할 수 있는 기회 제공.
    
## 3. [부분적용 (또는 커링) 함수를 사용시 자바스크립트 스택 트레이스가 모호해질 수 있다.](https://hackernoon.com/partially-applied-curried-functions-could-obfuscate-the-javascript-stack-trace-84d66bd8032e)

함수형 프로그래밍에서는 함수를 정의할 때 전달받는 매개변수의 이름을 명시적으로 선언하지 않고, 함수의 composition에 의해 정의되는 Point-free style을 사용한다.

```javascript
// non-point-free style
const initials = (name) => name
  .split(' ')
  .map(compose(toUpperCase, head))
  .join(' ')
  
// point-free style
const initials = compose(
  join('. '), 
  map(compose(toUpperCase, head)), 
  split(' ')
) 
```

예시 출처: by [Brunno](https://stackoverflow.com/a/43620110)


point-free style 코딩 스타일의 경우 일일이 이름을 지어야 하는 개발자들의 고충을 덜어주고, 코드를 더욱 간결하게 해줄 수 있지만,
에러가 터졌을 때 스택 트레이스가 어느 부분에서 에러가 터졌는지 제대로 알려주지 않는다는 문제가 있다.

이 문제는 point-free 함수를 호출하는 non-point-free 함수를 중간에 삽입하여 직접 스택 프레임을 만듦으로써 해결 할 수 있다.

해결방법은 본문 참고 (부제: Create a function yourself to establish a stack frame)

## 4. [적당한 양의, 대부분은 모듈간 결합에 관한, 테스트코드를 작성하라](https://blog.kentcdodds.com/write-tests-not-too-many-mostly-integration-5e8c7fff591c)
socket.io의 참시자인 Guillermo Rauch는 한줄의 트윗을 남겼다

>Write tests. Not too many. Mostly integration

TC39의 멤버이자 페이팔 엔지니어인 Kent C. Dodds는 이를 보고 각각이 의미하는 것이 무엇인지 본인의 해석을 장문의 글로 남겼는데, 이를 짧게 요약해보았다.

1. Write tests (테스트 코드를 작성하라)
    - 테스트코드를 작성하는 것은 개발 당시에는 시간을 조금 늦출 지는 몰라도 추후 유지보수에 들어가는 시간을 대폭 줄여준다. 
    - 타입체크와 린팅 만으로는 비즈니스 로직에 잠재해있는 버그를 검사하진 못한다.

2. Not too many (적당한 양으로)
    - 테스트 할 필요없는 모든 코드에 대해 테스트 케이스를 작성하는 것은 시간 낭비일 뿐더러 개발 효율을 오히려 다운시킨다. 
    - 스태틱 타입체커나 린트 툴이 담당할 수 없는 비즈니스 로직에 관한 코드에만 적용하는 것이 적절하다.

3. Mostly integration (대부분은 결합의 단계에 대해서만)
    - 테스팅은 피라미드 상위 순서대로 E22, Integration, Unit Testing으로 나눌 수 있으며 피라미드 위에 있을 수록 테스트 환경 조성에 시간이 많이 든다.
    - 시간대비 효율 때문에 대부분의 경우 unit testing을 강조한다.
    - 그러나 유닛테스팅만 집중할 경우 다음의 상황이 발생한다: [이미지](https://cdn-images-1.medium.com/max/800/0*eCs8GoVZVksoQtQx.gif)
    - E2E테스트의 경우 신뢰도가 매우 높지만 리소스가 너무 많이 들어간다.
    - 결합 테스트는 위에 언급한 두가지 테스트 사이에서 적절히 균형을 맞춰준다.
    

## 5. [webpack-dashboard 1.0 출시](https://github.com/FormidableLabs/webpack-dashboard/blob/master/README.md)

웹팩의 빌드 스테이터스를 한눈에 볼 수 있는 대쉬보드플러그인이 출시되었다.
본인들 소개로는 dev-server를 띄울 때 나오는 콘솔 메세지가 NASA에서 일하는 느낌을 주도록 바뀌었다니 활용하면 좋을 듯 하다.