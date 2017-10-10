---
title: answer-fp
tags:
---

```ecmascript 6
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
  // 문제 정의
  /*
  - 재고
    - 재고 현황를 반환하는 state
    - 재고 현황을 업데이트하는 update
  - 주문 리셉션
    - 재고를 체크하는 stock checker
    - 받은 금액을 체크하는 validator
  - 조리
    - 재료를 자르거나 다질 때 쓰는 cutter
    - 지정된 온도와 시간동안 재료를 가열할 gril
    - 완성된 재료로 샌드위치를 조합하는 공정
  */
  const Stock = (state = {}) => ({
    state: () => state,
    update: (newState) => { state = {...state, ...newState} }
  })

  const cutter = (type) => (pieces) => (ingredient) => ({...ingredient, cut: {
    type,
    pieces 
  }})

  const grill = (temperature) => (duration) => (ingredient) => ({...ingredient, grilled: {
    duration,
    temperature
  }})

  const assembly = (order) => (ingredients) => ingredients.reduce(() => {}, {
    type: order.menu,
  })
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