170728

# Javascript Syntax basics

## 1. Hello world
- 정적인 HTML을 동적으로 변경할 수 있는 유일한 방법은 js를 사용하는 것이다.

```
    function myFunction() {
      var myHeader = document.getElementById('demo');
      myHeader.innerHTML = 'Hello world!';
    }
```

## 2. 외부의 Javascript 실행하기
- HTML과 Javascript는 역할(관심사 Concern)이 다르므로 분리된 파일로 작성하는 것이 바람직하다.

```
<script src="extern.js"></script>
```
- 코드의 실행과정
  - 1.script 요소를 만나면 웹페이지의 파싱을 잠시 중단한다.
  - 2.src 어트리뷰트에 정의된 자바스크립트 파일을 로드한 후 실행한다.
  - 3.중단된 웹페이지의 파싱을 계속 진행한다.

  > body 요소의 가장 아래에 스크립트를 위치시키는 것은 좋은 아이디어이다. HTML 요소들이 스크립트 로딩 지연으로 인해 렌더링에 지장 받는 일이 발생하지 않아 페이지 로딩 시간이 단축된다.

- HTML은 script를 만나면 멈추게 된다.
  - 스크립트 로딩 지연으로 인한 병목 현상을 근복적으로 방지하기 위한 어트리뷰트가 추가되었다.
  ```
  <script async src="extern.js"></script>
  <script defer src="extern.js"></script>
  ```
  - async = 스크립트는 다운로드 완료 직후 실행된다.
  - defer = 스크립트는 웹페이지 파싱 완료 직후 실행된다.
    - async와 defer 어트리뷰트는 웹페이지 파싱과 외부 스크립트 파일의 다운로드가 동시에 진행된다는 면에서는 동일하다. 하지만 스크립트의 실행 시점이 다르다.

  > IE9이상을 쓸거면 defer가 좋다.

## 3. JavaScript Output
  - alert box	-> alert()
  - HTML output ->	document.write()
  - HTML element ->	innerHTML
  - Browser console ->	console.log()

## 4. Javascript Syntax Basics

### 4.1 구문(statement)
-  단계별로 수행될 명령들의 집합이다. 각각의 명령을 statement(구문)이라 하며 statement가 실행되면 무슨 일인가가 일어나게 된다.
- 구문은 값(Value), 연산자(Operator), 표현식(Expression), 키워드(Keyword), 주석(Comment)으로 구성되며 세미콜론( ; )으로 끝나야 한다.
- 구문은 block으로 그룹화 되며 이것을 함수라고 부른다.
- 조건문이나 반복문의 사용으로 제어될 수 있으며 이것을 Control Flow라고 한다.

### 4.2 표현식(Expression)
- 결과론 적으로 값 1개로 수렴되는 것이다.


### 4.2 변수(variable)
- 값을 저장하거나 참조하기 위해 사용된다.
- 메모리와 관련이 있다.
- 유지할 필요가 있는 값을 경우 `변수`를 사용한다.
  ```
  var x; // 변수의 선언과 초기화
  x = 6; // 정수값의 할당
  ```

### 4.4 값(Value)
```
String str = "Hello World";
<1>    <2>        <3>
```
- 자바스크립트는 7가지의 데이터 타입을 제공한다.
- 기본 자료형
  - Boolean
  - null
  - undefined
  - Number
  - String
  - Symbol(New In ECMAScript 6)

- object(객체)

```
// literal : Number
10.50
1001

// literal : String
'Hello'
"World"

// literal : Object
{ name: 'Lee', gender: 'male' }

// literal : Array
[ 'Black', 'Gray', 'White' ];

```

### 4.5 연산자(Operator)
- 산술 연산자, 대입 연산자, 문자열 연산자, 비교 연산자, 논리 연산자

```
// 대입 연산자
var color = 'red';

// 산술 연산자
var area = 5 * 4;

// 문자열 연산자
var str = 'Hi! ' + 'My name is Lee';

// 비교 연산자
var foo = 3 > 5; // false

// 논리 연산자
var bar = (5 > 3) && (2 < 4);  // true

```

### 4.6 키워드(keyword)
- 규정을 미리 정의해둔 것이다.

### 4.7 주석(Comment)
- // //(1줄 짜리) or /* */(여러줄 짜리) 방법이 있다. 