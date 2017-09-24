170728

# Javascript Introduction

## 1. Introduction

- 웹브라우저에서 동작하는 유일한 언어이다.
- jQuery의 등장으로 DOM(Document Object Model)를 보다 쉽게 제어할 수 있게 되었다.
- javascript는 interpreter language 컴파일러가 필요없다 동시에 번역한다.
- 명령형, 함수형, `프로토타입 기반 객체지향형 언어`이다.
  -  자유도(3가지가 다된다)가 높다보니 어렵다.
- Node.js의 등장으로 Full stack 개발 언어가 되었다.

## 2. 브라우저 동작 원리
![브라우저 동작 원리](../images/client-server.png)
- javascript는 위치가 의미가 있다 dom을 만들기 때문이다.
> HTML 파서는 script 태그를 만나면 DOM 생성 프로세스를 중지하고 자바스크립트 엔진에 제어 권한을 넘긴다. 자바스크립트 엔진의 실행이 완료된 후 브라우저가 중지했던 시점부터 DOM 생성을 재개한다. 이것은 script 태그의 위치에 의해 DOM의 생성이 지연될 수 있음을 의미한다.

## 3. History 
- ECMAScript 3 : 가장 범용적으로 지원되는 버전이다 (1999.12)
- ECMAScript 5 : HTML5와 함께 출현한 표준안이다. JSON(JavaScript Object Notation)과 Strict Mode가 추가되었다. 인터넷 익스플로러 9이상이나 그 외 브라우저에서만 작동한다.(2009.12)
- ECMAScript 6 : let, const 키워드, Arrow Function, class, Symbol 타입 등이 추가되었다.

## 4. Browsers Support
- 대부분의 브라우저는 ES6를 지원하고 있지만 100%는 아니다. 그리고 Node.js의 경우 v4부터 지원을 시작하였다.