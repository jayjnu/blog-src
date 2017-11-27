---
title: nov-4th-week
date: 2017-11-26 12:28:06
categories:
- Weekly
tags:
- Web Assembly
- Chrome
- javascript
---

## [1. Chrome 63에 탑재되는 동적 import](https://developers.google.com/web/updates/2017/11/dynamic-import)

지난번 크롬 61에 정적 import가 탑재된 이후 다음의 요구사항이 생겼다

- 모듈이 필요할떄 (또는 조건에 부합할때)만 import
- module specifier를 런타임에 연산
- 일반적인 스크립트문 내부에서 모듈을 import

이런 점을 보완하는 동적 import()가 크롬 63에 탑재되었다.
import(moduleSpecifier)를 사용하면 Promise를 리턴하고 then(resolve)의 매개변수로는 해당 모듈의 네임스페이스가 전달된다

```javascript
<script typer="module">
  const moduleSpecifier = './utils.mjs';
  import(moduleSpecifier).then((module) => {
    module.default();
    module.doStuff();
  });
</script>
```

## [2. Modern Javascript Tutorial](https://javascript.info)

자바스크립의 기본부터 심화까지 모든 개념을 익힐 수 있는 오픈소스 공간


## [3. Flappy Bird 게임을 자바스크립트로 만드는 법](https://www.youtube.com/watch?v=L07i4g-zhDA&feature=youtu.be)

한때 최고의 멘탈 파괴 게임이었던 Flappy Bird를 HTML5 Canvas와 자바스크립트로 만드는 법을 소개한다.
코드를 라인 하나하나마다 그림으로 설명해주기때문에 영어로 돼있어도 이해하기 쉬우므로 따라해보자.

## [4. 웹어셈블리, 언제 자바스크립트 대신 써야할까](https://blog.sessionstack.com/how-javascript-works-a-comparison-with-webassembly-why-in-certain-cases-its-better-to-use-it-d80945172d79)

[Alexander Zlatkov](https://blog.sessionstack.com/how-javascript-works-a-comparison-with-webassembly-why-in-certain-cases-its-better-to-use-it-d80945172d79)가 Medium에 시리즈로 연재하고 있는 [How Javascript Works](https://blog.sessionstack.com/tagged/tutorial)시리즈의 6번째 포스팅으로 웹 어셈블리에 대해 소개한다.

### 웹어셈블리(wasm)란?

> 웹어셈블리는 웹에서 사용할 수 있는 로우레벨 언어로 W3C의 차세대 표준이다. C, C++같은 언어로 작성한 코드를 브라우저에서도 돌아가게 해준다.

### 로드시간
> .js 파일을 로드하고 해석해야되는 기존의 자바스크립트와는 달리 웹 어셈블리는 이미 컴파일이 된 상태로 서브하기 때문에 훨씬 빠르다.

### 실행시간
> wasm은 글이 작성된 시점에서 네이티브코드보다 20%정도 느리게 동작한다. 이는 놀라운 수치이며 미래에는 더 빨라질 것이다. 모든 메이져 브라우저 벤더가 웹 어셈블리 환경을 지원하기 때문에 크로스 브라우징 이슈도 해소된다.

어떻게 웹 어셈블리가 이렇게 빠르게 동작할 수 있는지는 본문에 그림으로 친절하게 설명하고 있다.

### 메모리 모델
> Wasm으로 컴파일 되는 C++은 실행스택과 프로그램의 공간이 분리되어있어 잠재적인 멀웨어 감염을 막는다. 실행스택이 wasm 프로그램과 분리되어있고 함수의 경우 포인터가아니라 integer offset으로 참조한다. wasm 모듈을 동시에 로드해도 메모리공간의 offset을 이용하기 때문에 모두 제대로 동작한다.

### 가비지콜렉션
> 자바스크립트는 가비지 콜렉터를 이용하여 메모리 관리를 하지만, wasm의 경우 수동으로 메모리를 관리한다 (애초에 로우레벨에 가까운 언어단을 지원하기 때문에)
> Wasm이 지원하는 언어는 DOM 조작과 같이 내부 복잡도가 높은 테스크를 수해하기는 적절치 않기에 모든 HTML App을 C++로 작성하는 것은 바람직하지 않다.
> 추후 Wasm가 GC를 지원하지 않는 언어에 대한 지원을 할 예정이다.

### 플랫폼 API 접근

> Wasm으로는 DOM, CSSOM, WebGL 등 플랫폼에 특정한 API에 접근할 수 없다. 해당 API를 이용하기 위해서는 Javascript를 이용해야 한다. (예: console.log)
> 스펙에 따르면 wasm를 위한 지원이 예정되어 있다.

### 소스맵
> 현재 wasm은 소스맵을 지원하지 않고 있으며, 관련한 스펙도 없는 상태지만, 지원이 될거라 생각한다.


### 멀티 쓰레딩
> Wasm은 현재 멀티 쓰레딩을 지원하지 않으나, 빠르게 지원이 될 것이라고 예상된다.

### 크로스 플랫폼(Portability)
> 어느 브라우저에서나 동작하는 Javascript처럼, Wasm도 모든 환경에서 동작하는 것을 목표로 설계 되었다.

### 어떤 상황에서 웹 어셈블리를 사용하는 것이 적절할까?

|상황|Wasm|Javascript|
|---|---|---|
|게임|O|X|
|이미지연산, 조작|O|X|
|DOM, BOM조작|X|O|

> 무거운 CPU 연산이 플요하고 플랫폼 API에 의존성이 없는 태스크에서 Wasm은 빛을 발한다.


## [5. 알면 유용한 리액트 컴포넌트 라이브러리 8선](https://blog.bitsrc.io/11-react-component-libraries-you-should-know-178eb1dd6aa4)

마크업이나 디자인은 신경쓰지 않고 리액트 애플리캐이션 개발을 신속히 끝내고 싶다면 위에서 열거한 컴포넌트 라이브러리를 사용하는 것이 어떨까?

google의 material, twitter의 bootstrap등의 테마를 바탕으로 리액트 컴포넌트의 접목시킨 여러 라이브러리를 만나볼 수 있다.