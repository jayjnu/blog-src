---
title: Brief Introduction to Functional Javascript
date: 2017-10-10 19:37:49
categories:
- Javascript
tags:
- javascript
- Functional Programming
---

## Contents

1. [함수형 프로그래밍이란?](#함수형-프로그래밍이란)
2. [왜 함수형 프로그래밍인가?](#왜-함수형-프로그래밍인가)
    2-1. [선언형 vs 함수형](#선언형-vs-함수형) 
4. [Can I Use..?](#Can-I-Use)
5. [Real World Example](#Real-World-Example)



### 함수형 프로그래밍이란?

>함수형 프로그래밍은 자료 처리를 수학적 함수의 계산으로 취급하고 상태와 가변 데이터를 멀리하는 프로그래밍 패러다임의 하나이다.
>...
함수형 코드에서는 함수의 출력값은 그 함수에 입력된 인수에만 의존하므로 인수 x에 같은 값을 넣고 함수 f를 호출하면 항상 f(x)라는 결과가 나온다. 부작용을 제거하면 프로그램의 동작을 이해하고 예측하기가 훨씬 쉽게 된다. 이것이 함수형 프로그래밍으로 개발하려는 핵심 동기중 하나이다.
>...

출처: Wikipedia [함수형 프로그래밍](https://ko.wikipedia.org/wiki/%ED%95%A8%EC%88%98%ED%98%95_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D)

### 왜 함수형 프로그래밍인가?

#### 선언형 vs 명령형

함수형 프로그래밍은 선언형 프로그래밍의 형태 중 하나다. 

선언형은 명령형과 비교하여 아래와 같은 차이가 있다.

|항목| 선언형 | 명령형 |
|:---:|:---:|:---:|
|상태 (state)|없음|존재|
|데이터 변조(mutability)|불가능 (immutable)| 가능 (mutable) |
|문제해결 방식|무엇(what)이 필요한지 정의|어떻게(how) 해결할지 직접 명령|
|코드실행 순서|(때에따라) 중요하지 않음 | 매우 중요 |
|1|4|5|

### Can I Use..?
자바스크립트를 함수형으로 사용할 수 있을까? 어느정도는 가능하다.


### Real World Example