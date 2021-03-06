---
title: 9월 5째주 프론트엔드 이슈
date: 2017-10-02 13:06:24
categories:
- Weekly
tags:
- React.js
- javascript
---


## [React.js, 다시 MIT 라이센스로](https://code.facebook.com/posts/300798627056246)

Facebook이 9월 23일자 포스팅에서 논란 [(참고: facebook vs ASF 라이센스 이슈 요약)](http://writing.jan.io/2017/08/19/understanding-the-facebook-vs-asf-license-kerfuffle.html) 끝에 결국 React.js를 MIT 라이센스로 변경하기로 결정했다고 발표했다.
변경된 라이센스는 React v16의 배포에 업데이트 될 예정이다.


## [React v16](https://reactjs.org/blog/2017/09/26/react-v16.0.html)

React 16 버전이 공식 발표 됐다. 주요 내용은 아래와 같다.

- render 함수의 새로운 return 타입: string, fragments
    - JSX를 이용해 생성된 React.Component 인스턴스를 반환해야했던 기존의 방식을 개선
- 에러 핸들링 개선: Error boundary설정으로 페이지 리프레시를 할 필요 없이 특정 에러에 대해 fallback을 제공할 수 있게 됨
- Portal의 등장
    - DOM 구조와 상관 없이 원하는 container Node에 child React component를 렌더링 할 수 있게 해주는 헬퍼
- 서버사이드 렌더링 개선
- 커스텀 DOM attribute 지원
- 32%의 파일 사이즈 개선
    - react: 20.7kb(6.8kb gzipped) -> 5.3kb(2.2kb gzipped)
    - react-dom: 141kb(42.9kb gzipped) -> 103.7kb(32.6kb gzipped)
    - react + react-dom: 161.7kb(49.8k gzipped) -> 109kb(34.8kb gzipped)
    
- MIT 라이센스로 변경
- 새로운 코어 아키텍쳐 'Fiber'([참고](https://code.facebook.com/posts/1716776591680069/react-16-a-look-inside-an-api-compatible-rewrite-of-our-frontend-ui-library/)) 도