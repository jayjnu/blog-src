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

함수형 프로그래밍을 실제 개발환경에 맞게 적용하려면 어떻게 해야할까?

#### Problem: My Way Sandwich
주어진 재료와 주문에 따라 샌드위치를 만들어주는 MyWaySandwich() 프로그램을 작성해보자

- 메뉴판에 샌드위치는 총 두 가지: 이탈리안 BLT, 필리치즈 스테이크.
- 메뉴판에 없는 주문은 받지 않으며, 거래를 종료한다.
- 필수재료가 떨어지면 샌드위치는 즉시 매진 상태가 된다.
- 돈이 부족한 경우 거래를 거절한다.
- 재료는 g 단위로 제공한다, 레시피에 적힌대로 잘랐을 때 양이 부족하면 재료 부족상태가 된다.
- 빵은 무제한이며, 무조건 하나를 반으로 잘라서 가장 바깥쪽에서 재료를 감싸야한다. 

- 제약조건
    - 비동기성은 일단 무시하자
    - 한번에 주문은 한개만 받는다.
    - 거스름돈은 무시한다
    - 소스는 없다

메뉴별 레시피는 아래와 같다.

- 이탈리안BLT
    - 재료: 베이컨10g, 상추2g, 토마토 2g
    - 가격: 5500
    - 레시피:
        1. 베이컨을 150도에서 3초동안 굽고나서 2등분 한다.
        2. 상추를 2조각으로 찢는다.
        3. 토마토를 3조각으로 슬라이스한다. 
        4. 토마토, 상추, 베이컨을 빵에 차례로 넣는다.
- 필리치즈스테이크
    - 재료: 스테이크 30g, 양파 10g, 치즈 10g
    - 가격: 8000
    - 레시피:
        1. 스테이크를 30등분으로 다지고 나서 140도에서 5초동안 볶는다.
        2. 양파를 10조각 슬라이스해서 자른 후 3초동안 볶는다.
        3. 치즈를 2초간 60도에서 가열한다.
        4. 스테이크, 양파, 치즈를 빵에 차례로 넣는다.


INPUT 예시
```JSON
{ "menu": "필리치즈스테이크", "money": 8900 }
```

OUTPUT 예시
```JSON
{
  "type": "필리치즈스테이크 샌드위치",
  "sandwich": [
    {
      "name": "빵",
      "cut": {
        "type": "sliced",
        "pieces": 0.5
      }
    },
    {
      "name": "스테이크",
      "cut": {
        "type": "chopped",
        "pieces": 30
      },
      "grilled": {
        "duration": 5000,
        "temperature": 140
      }
    },
    {
      "name": "양파",
      "cut": {
        "type": "sliced",
        "pieces": 10
      }
    },
    {
      "name": "치즈",
      "grilled": {
        "duration": 2000,
        "temperature": 60
      }
    },
    {
      "name": "빵",
        "cut": {
          "type": "sliced",
          "pieces": 0.5
        }
    }
  ]
}
```

제공되는 API
```javascript
// 공통상수
const BLT = '이탈리안BLT'
const PHILLY = '필리치즈스테이크'

const STOCKS = {
  '베이컨': 200,
  '상추': 100,
  '스테이크': 250,
  '양파': 40,
  '치즈': 100
}


/**
* @param menu string 메뉴이름
* @param money number 지불액
* @returns { order } 
*/
function order(menu, money) {
  return {
    menu,
    money
  }
}

/**
* @param order { order } order()를 통해 주문한 주문서
* @returns {*} 조리된 샌드위치의 배열  
*/
function MyWaySandwich(order) {
  // 여기에 코드 작성
}

function Main() {
  const orders = [
    order(PHILLY, 5500), 
    order(BLT, 6000), 
    order(PHILLY, 10000), 
    order(PHILLY, 8900)
  ]
  
  orders.forEach(function(order) {
    console.log(MyWaySandwich(order))
  })
}

Main();
```

[문제풀러 가기](https://jsfiddle.net/doublejnu/pmey550o/)

해답은 추후에..