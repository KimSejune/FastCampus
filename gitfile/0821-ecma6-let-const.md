170821

# ECMAScript6 - let, const

- ES5에서의 변수선언의 유일한 방법은 `var키워드`를 사용하는 것이다.
- var 키워드의 단점
  - 1.`Function-level-scope`
    - 전역 변수의 남발(전역 변수는 어디서 변경될지 알기 힘들어지기 때문에 사용하지 않는 것이 좋다.)
    - for loop 초기화식에서 사용한 변수를 for loop 외부 또는 전역에서 참조할 수 있다.

  - 2.var 키워드 생략 허용
    - 의도하지 않은 변수의 전역화
  
  - 3.중복 선언 허용 
    - 의도하지 않은 변수값 변경

  - 4.`변수 호이스팅`
    - 변수를 선언하기 전에 참조가 가능하다.

 - 전연 변수는 유효범위가 넓어서 어디에서 사용될 것인지 파악하기 힘들다 따라서 변수의 유효범위는 좁을수록 좋다.

## 1. let

### 1.1 Block-level scope

- 대부분의 C-family 언어는 Block-level-scope를 지원하지만 JS는 Function-level-scope를 갖는다.

  - `Function-level scope` : 함수내에서 선언된 변수는 함수 내에서만 유효하며 함수 외부에서는 참조할 수 없다. 즉, 함수 내부에서 선언한 변수는 지역 변수이며 함수 외부에서 선언한 변수는 모두 전역 변수이다.
  - `Block-level scope` : 코드 블럭 내에서 선언된 변수는 코드 블럭 내에서만 유효하며 코드 블럭 외부에서는 참조할 수 없다.

```javascript
console.log(foo); // undefined
var foo = 123;
console.log(foo); // 123
{
  var foo = 456;
}
console.log(foo); // 456
```

- ES6는 `Block-level scope`를 갖는 변수를 선언하기 위해 `let 키워드`를 제공한다.

```javascript
let foo = 123;
{
  let foo = 456;
  let bar = 456;
}
console.log(foo); // 123
console.log(bar); // ReferenceError: bar is not defined

```
- let 키워드로 선언된 변수는 Block-level scope를 갖는다. 


### 1.2 중복 선언 금지
- var는 중복 선언이 가능하였으나 let은 `중복 선언시 SyntaxError`가 발생한다.

```javascript
var foo = 123;
var foo = 456;  // OK

let bar = 123;
let bar = 456;  // Uncaught SyntaxError: Identifier 'bar' has already been declared

```

### 1.3 호이스팅(Hoisting)
- 자바스크립트는 ES6에서 도입된 let, const를 포함하여 모든 선언(var, let, const, function, function*, class)을 호이스팅한다.
  > 호이스팅이란? var 선언문이나 function 선언문 등을 해당 스코프의 선두로 옮기는 것을 말한다.

- let 키워드로 선언된 변수를 선언문 이전에 참조하면 ReferenceError가 발생한다.
- let 키워드로 선언된 변수는 스코프의 시작에서 변수의 선언까지 일시적 사각지대`(Temporal Dead Zone; TDZ)`에 빠지기 때문이다.

```javascript
console.log(foo); // undefined
var foo;

console.log(bar); // Error: Uncaught ReferenceError: bar is not defined
let bar;

```

- 변수는 3단계에 걸쳐 생성된다.
  - `선언 단계(Decllaration phase)`
    - 변수 객체(Variable Obejct)에 변수를 등록한다. 이 변수 객체는 스코프가 참조하는 대상이 된다.
  - `초기화 단계(Initialization phase)`
    - 변수 객체(Variable Object)에 등록된 변수를 `메모리에 할당`한다. 이 단계에서 변수는 undefined로 초기화된다.
  - `할당 단계(Assignment phase)`
    - undefined로 초기화된 변수에 실제값을 할당한다.

- `var 키워드로 선언된 변수는 선언 단계와 초기화 단계가 한번에 이루어 진다.`
- 변수 선언문 이전에 변수에 접근하여도 Variable Object에 변수가 존재하기 때문에 에러가 발생하지 않는다. 이것을 변수 호이스팅이라 한다.

- `let 키워드로 선언된 변수는 선언 단계와 초기화 단계가 분리되어 진행된다.`
- 스코프에 변수가 선언단계에 등록되지만 초기화 단계는 변수 선언문을 도달했을 때 이루어진다.
- 초기화 이전에 변수에 접근하려고 하면 ReferenceError 에러가 발생한다.

> 일시적 사각지대에 들어오면 ReferenceError가 발생한다.

### 1.4 클로저
- Block-level scope를 지원하는 let은 var보다 직관적이다.

```javascript
var funcs = [];

// 함수의 배열을 생성한다
// i는 전역 변수이다
for (var i = 0; i < 3; i++) {
  funcs.push(function () { console.log(i); });
}

// 배열에서 함수를 꺼내어 호출한다
for (var j = 0; j < 3; j++) {
  funcs[j]();
}

```
- 위 코드의 실행 결과로 0, 1, 2를 기대할 수도 있지만 결과는 3이 3번 출력된다. 그 이유는 for문의 var i가 전역 변수이기 때문이다. 0, 1, 2를 출력시키기 위해서는 아래와 같은 코드가 필요하다

```javascript
var funcs = [];

// 함수의 배열을 생성한다
// i는 전역 변수이다
for (var i = 0; i < 3; i++) {
  (function (index) { // index는 자유변수이다.
    funcs.push(function () { console.log(index); });
  }(i));
}

// 배열에서 함수를 꺼내어 호출한다
for (var j = 0; j < 3; j++) {
  funcs[j]();
}

```
- JavaScript의 Function-level scope로 인하여 for loop의 초기화식에 사용된 변수가 전역 스코프를 갖게되어 발생하는 문제를 회피하기 위해 `클로저를 활용한 방법이다.`

```javascript
var funcs = [];

// 함수의 배열을 생성한다
// i는 for loop에서만 유효한 지역변수이면서 자유변수이다
for (let i = 0; i < 3; i++) {
  funcs.push(function () { console.log(i); });
}

// 배열에서 함수를 꺼내어 호출한다
for (var j = 0; j < 3; j++) {
  funcs[j]();
}

```
- for loop의 let i는 for loop에서만 유효한 지역 변수이다의

### 1.5 전역 객체와 let
- 전역 객체는 모든 객체의 유일한 최상위 객체를 의미하며 일반적으로 Browser-side에서는 window 객체, Server-side(Node.js)에서는 global 객체를 의미한다.

- var 키워드로 선언된 변수를 전역 변수로 사용하면 전역 객체(Global Object)의 프로퍼티가 된다.

```javascript
var foo = 123; // 전역변수

console.log(window.foo); // 123

```
- let 키워드로 선언된 변수를 전역 변수로 사용하는 경우, `let 전역 변수는 전역 객체의 프로퍼티가 아니다.` 즉 window.foo와 같이 접근할 수 없다.

```javascript
let foo = 123; // 전역변수

console.log(window.foo); // undefined

```

## 2. const
- const는 상수(변하지 않는 값)를 위해 사용한다. 하지만 반드시 상수만을 위해 사용하지는 않는다.
- const는 let과 대부분 동일한 특징을 갖는다.

> 규칙을 정해줄때 사용한다. 암묵적으로 대문자로 사용한다.

### 2.1 선언과 초기화

- let은 초기화 이후 다른 값으로 재할당이 자유로우나 const는 초기화 이후 재할당이 금지된다.

```javascript
const FOO = 123;
FOO = 456; // TypeError: Assignment to constant variable.

```
- `주의할 것은 const는 반드시 선언과 동시에 초기화가 이루어져야 한다는 것이다.`

```javascript
const FOO; // SyntaxError: Missing initializer in const declaration

```

- 또한 const는 let과 마찬가지로 Block-level scope를 갖는다.

```javascript
{
  const FOO = 10;
  console.log(FOO); //10
}
console.log(FOO); // ReferenceError: FOO is not defined
```

### 2.2 상수
- 상수는 가독성의 향상과 유지보수의 편의를 위해 적극적으로 사용해야한다.

```javascript
// Low readability
if (x > 10) {
}

// Better!
const MAXROWS = 10;
if (x > MAXROWS) {
}
```
- 네이밍이 적절한 상수로 선언하면 가독성과 유지보수성이 대폭 향상된다.
- const는 객체에도 사용할 수 있다. 물론 재할당은 금지된다.

```javascript
const obj = { foo: 123 };
obj = { bar: 456 }; // TypeError: Assignment to constant variable.
```

### 2.3 const와 객체
- const는 재할당이 금지된다. 이는 const 변수의 값이 객체인 경우, 객체에 대한 참조의 변경을 금지한다는 것을 의미한다.

- `객체의 프로퍼티는 보호되지 않는다.` 다시 말하자면 재할당을 불가능하지만 할당된 객체의 내용(property)은 변경할 수 있다.


```javascript
const user = {
  name: 'Lee',
  address: {
    city: 'Seoul'
  }
};

// const 변수는 재할당이 금지된다.
// user = {}; // TypeError: Assignment to constant variable.

// 프로퍼티 값의 재할당은 허용된다!
user.name = 'Kim';

console.log(user); // { name: 'Kim', address: { city: 'Seoul' } }
```
- `객체 타입 변수 선언에는 const를 사용하는 것이 좋다. 이유는 아래와 같다.`
  - 객체에 대한 참조는 변경될 필요가 없다. 즉, 재할당이 필요없다. 만일 새로운 객체에 대한 참조를 변수에 할당해야 한다면 새로운 변수를 사용하면 된다.
  - const를 사용한다 하더라도 객체의 프로퍼티를 변경할 수 있다.


## 3. var vs. let vs. const
- 아래와 같이 var, let, const 사용하는 것을 추천한다.

  - ES6를 사용한다면 var 키워드는 사용하지 않는다.
  - 변경이 발생하지 않는(재할당이 필요없는) primitive형 변수와 객체형 변수에는 const를 사용한다.
  - 재할당이 필요한 primitive형 변수에는 let를 사용한다.
