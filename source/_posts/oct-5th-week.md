---
title: 2017년 10월 5째주 ~ 11월 1째주 프론트엔드 이슈
date: 2017-11-05 23:29:41
categories:
- weekly
tags:
- node.js
- angular.js
- w3c
- webcomponents
---

## 1. [Node.js Best Practices](https://github.com/i0natan/nodebestpractices)
Node.js 애플리케이션을 작성할 때 참고해야 할 best practice가 모여있다. 코드스타일부터 프로젝트 구조 구성법, 에러 핸들링 등 모르면 그냥 넘어갈 수 있는 정보들을 총집합 해두었다.

## 2. [Angular 5.0.0 출시](https://blog.angular.io/version-5-0-0-of-angular-now-available-37e414935ced)
앵귤러가 벌써 5번째 버전을 출시했다. 주요 변경 내용은 다음과 같다.

1. 빌드 최적화 도구 - 번들 파일의 용량을 낮추고 데코레이터를 제거하여 런타임속도를 빠르게 해주는 빌드 최적화 도구가 이제 기본 내장.
2. Angular Universal State Transfer API와 DOM 지원
4. 컴파일러 개선 - incremental compilation 을 지원하여 속도 개선, 컴포넌트 공백 제거를 통한 빌드 용량 개선, 더욱 강력해진 데코레이터 
5. 숫자 날짜, 통화 pipe 국제화 - 브라우저의 i18n API에 의지하여 생겼던 여러 문제를(국가별, 브라우저별 동일하지 않은 결과값) 해결하기 위해 자체 툴 도입하여 개발자가 예상하는 결과값 제공 
6. ReflectiveInjector 를 StaticInjector 로 교체 - 기존의 폴리필을 제거하여 플러그인 사이즈를 줄임
7. Zone 속도 개선 - 기본적인 속도 개선과 함께, zone을 bypass 할 수 있는 방법 제공
8. exportAs 속성 지원 - component, directive를 여러 name으로 export 할 수 있도록 하는 기능
9. HttpClient - @angular/httplibrary를 deprecate 시키고 이제 HttpClient가 앵귤러의 공식 http 통신 모듈이 되었다
10. CLI v1.5 - 해당 버전부터 Angular 프로젝트는 5버전을 기반으로 생성된다.
11. Form 이벤트 Blur / Submit  지원 - 이제 매번 user input때마다 유효성검사를 실행하지 않고, 해당 이벤트때만 실행할 수 있도록 지원한다
12. Template Driven Form - 이제 컴포넌트 ts 파일 뿐 아니라 템플릿위주로 설정 양방향 바인딩을 할 수 있도록 지원한다. (코드는 본문 참조)
13. RxJS 5.5 도입
14. 새로 추가된 라우터 라이프사이클 이벤트 (GuardsCheckStart, ChildActivationStart, ActivationStart, GuardsCheckEnd, ResolveStart, ResolveEnd, ActivationEnd, ChildActivationEnd)

자세한 내용은 본문 참고

## 3. [Apple의 HTML Template Instantiation 제안서](https://github.com/w3c/webcomponents/blob/gh-pages/proposals/Template-Instantiation.md)

내용이 너무 길기 때문에 육하원칙에 의거 간단히 요약을 하였다.
2017년 11월 1일부로 애플이 W3C에 &lt;template&gt;를 javascript로 native 하게 instantiate 할 수 있도록 하는 내용을 안건으로 내었다.
mustache의 문법을 표준으로 하여 어떤식으로 native 템플릿 API를 제공할 지 본문에 상세히 기술하였다.
HTML5 스펙으로 &lt;template&gt; 엘리먼트는 정의되었으나, 브라우저 자체 템플릿 인스턴스에 대한 가이드가 없었다. 애플은 그동안 개발자들이 라이브러리에 따라 제각각인 템플릿을 사용하고 있었고, 이는 코드 재사용성을 떨어뜨린다는 점을 들어 제안의 배경을 밝혔다.

## 4. [MDN += MSDN](https://blogs.windows.com/msedgedev/2017/10/18/documenting-web-together-mdn-web-docs/)
마이크로 소프트와 모질라가 손을 잡았다.
Google, The W3C, Samsung과 함께 이제 마이크로 소프트도 웹 표준화 문서를 MDN에 작성하겠다는 오피셜이 나왔다.
이제 MDN이 명실상부 Web Documentation의 표준 공간이 되었다는 뜻.
이제 혹자가 제2의 IE라고 칭하는 애플만 남은 듯 하다.

## 5. [Node.js 9 버전이 릴리즈](https://medium.com/the-node-js-collection/news-node-js-8-moves-into-long-term-support-and-node-js-9-becomes-the-new-current-release-line-74cf754a10a0)

Node.js 8.9.0이 첫 정식 Node.js 8 릴리즈로 확정되었다. 해당 버전은 전작인 6에 비해 20%가량의 속도향상이 있었으며, promise의 문법설탕인 async / await를 공식 지원한다.


