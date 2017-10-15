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
3. [Can I Use..](#Can-I-Use)
    3-1. [함수형 프로그래밍에 필요한 기본 조건](#함수형-프로그래밍에-필요한-기본-조건)
    3-2. [Javascript in FP Style?](#Javascript-in-FP-Style)
4. [Real World Example](#Real-World-Example)
    4-1 [Problem: My Way Sandwich](#Problem-My-Way-Sandwich)

### 함수형 프로그래밍이란?

>함수형 프로그래밍은 자료 처리를 수학적 함수의 계산으로 취급하고 상태와 가변 데이터를 멀리하는 프로그래밍 패러다임의 하나이다.
>...
함수형 코드에서는 함수의 출력값은 그 함수에 입력된 인수에만 의존하므로 인수 x에 같은 값을 넣고 함수 f를 호출하면 항상 f(x)라는 결과가 나온다. 부작용을 제거하면 프로그램의 동작을 이해하고 예측하기가 훨씬 쉽게 된다. 이것이 함수형 프로그래밍으로 개발하려는 핵심 동기중 하나이다.
>...

출처: Wikipedia [함수형 프로그래밍](https://ko.wikipedia.org/wiki/%ED%95%A8%EC%88%98%ED%98%95_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D)

### 왜 함수형 프로그래밍인가?

함수형 프로그래밍은 불변하는 데이터 구조와 side-effect 없는 함수들의 조합을 이용하기 때문에 어플리케이션 디버깅의 복잡도를 줄여준다. 여기저기서 일어나는 데이터의 변조 시점을 파악하고, 수많은 상태의 변화에 따라 결과값이 달라지는 애플리케이션을 분석하는 것은 오랜 세월 개발자들에게 고통을 안겨주었다.
 

#### 선언형 vs 명령형
함수형 프로그래밍은 선언형 프로그래밍의 형태 중 하나다. 
선언형은 명령형과 비교하여 아래와 같은 차이가 있다.

|\| 선언형 | 명령형 |
|:---:|:---:|:---:|
|상태 (state)|없음|존재|
|데이터 변조(mutability)|불가능 (immutable)| 가능 (mutable) |
|문제해결 방식|문제를 먼저 정의하고 문제 해결을 위해 무엇(what)이 필요한지 정의|어떻게(how) 문제를 해결할지 step by step으로 명령|
|코드실행 순서|비교적 중요하지 않음 | 매우 중요 |

#### 함수형 프로그래밍의 이점
1. 모듈화 (Modularity): 함수는 매개변수 이외의 값에 의존하지 않으며 Side-effect를 일으키지 않기 때문에 모듈 단위별로 분리가 용이
2. 느슨한 의존성 (Loose Coupling): 모듈간 의존성이 줄어들기 때문에 리팩토링이 쉬워진다.
3. 수학적 정확성 (Mathematical Correctness): 함수는 인풋에 따라 언제나 동일한 값을 반환하기 때문에 수학적으로 정확하다. 수학적으로 정확한 함수끼리의 composition에서 에러가 있다면 인풋자체에 문제가있거나 컴포지션 자체가 잘못됐다는 결과가 나오기 때문에 디버깅에 유리하다.
4. 재사용성 (Reusability): 수학적으로 정확한, pure-function은 언제나 재사용할 수 있다.

### Can I Use..

함수형 프로그래밍을 위해서는 프로그래밍 기법도 중요하지만 언어적 차원에서 지원해야 하는 부분이 존재한다.

#### 함수형 프로그래밍에 필요한 기본 조건

|코드차원|언어차원|
|---|---|
|함수는 Side-effect가 없다|함수는 First-Class Object다|
|함수는 언제나 값을 반환한다|Closure가 존재한다|
|재할당을 사용하지 않는다|데이터는 불변한다|
||Lazy Evaluation(call by need)|
||Tail-call Optimization을 지원한다|
||익명함수를 지원한다|
||함수는 즉시실행할 수 있다|


### Javascript in FP Style?
자바스크립트를 함수형으로 작성하는 것은 자바스크립트로 객체지향프로그래밍을 하는 것이다; 비슷하게는 할 수 있다.

완전하진 않지만 자바스크립트는 함수형 프로그램에 필요한 상당부분의 기능을 언어 차원에서 제공한다.

|기능|지원|Workaround|
|---|:---:|:---:|
|함수는 First-Class Object| O |-|
|Closure|O|-|
|데이터는 불변한다|X| Object.freeze() (in ES5.1) 또는 Immutable.js 존재|
|Lazy Evaluation(call by need)|X|Lazy.js 또는 커링 기법 등을 통해 일정부분 구현 가능|
|Tail-call Optimization|X|ES6스펙, trampoline을 이용해 구현 가능|
|익명함수|O|-|
|즉시실행함수|O|-|

### Real World Example

다음과 같은 이유로 이론상의 완전한 함수형 프로그램을 작성하는 것은 불가능하다.
- 자바스크립트는 완전한 함수형 언어가 아니다. 
- 현실 세계의 프로그램에서 side-effect는 존재할 수 밖에 없다. (ajax call, DOM 조작, logging 등)

다음 포스팅에서는 함수형 프로그래밍을 실제 개발환경에 맞게 적용하려면 어떻게 해야할지 알아보도록 하겠다