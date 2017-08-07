170803

# Javascript scoep

## 3.Function scope  

자바스크립트의 Scope 종류
- 전역Scope(Global scope)
  - 코드 어디에서든지 참조할 수 있다.
- 지역Scope(Local scope or Function-level scope)
  - 정의된 함수 내에서만 참조할 수 있다.

변수의 Scope 종류
- 전역 변수 (Global variable)
  - 전역 Scope를 갖는 변수.
- 지역 변수 (Local variable)
  - 지역 Scope를 갖는 변수

- `변수는 선언 위치(전역 또는 지역)에 의해 Scope를 가지게 된다. 즉 전역에서 선언된 변수는 전역 Scope를 갖는 전역 변수이고, 지역(자바스크립트의 경우 함수 내부)에서 선언된 변수는 지역 Scope를 갖는 지역 변수가 된다.`

- `전역 Scope를 갖는 전역 변수는 전역(코드 어디서든지)에서 참조할 수 있다. 지역(함수 내부)에서 선언된 지역 변수는 그 지역과 그 지역의 하부 지역에서만 참조할 수 있다.`

- javascript는 함수 코드블럭만 지역Scope로 인식하며, 그 외는 전역 Scope이다.

```javascript
var x = 0;  // global
{
  var x = 1;  // global
  console.log(x); // 1
}
console.log(x);   // 1

let y = 0;  // global
{
  let y = 1;  // local
  console.log(y); // 1
}
console.log(y);   // 0

```
> let은 block-level-scope를 지원한다.

## 1. Global scope
- `전역 변수는 전역 객체 window의 프로퍼티이다.`
```javascript
var global = 'global'; // 전역 변수

function foo() {  // 전역 함수
  var local = 'local'; // this로 선언하면 함수외부에서도 참조가가능하다 but var는 안된다.
  console.log(global);
  console.log(local);
}
foo();

console.log(global); // window.global을 해도 같은 값이 나온다. 편의상 없앴다.
console.log(local); // Uncaught ReferenceError: local is not defined

```
> `함수내부에 this로 선언한 변수들은 public 외부에서 참조가 가능하며 var로 선언한 변수들은 private하여 외부에서 참조가 불가능하다.`

## 2. Non block-level scope -> Function-level scope

```javascript
if (true) {
  var x = 5; // function이 아니니깐 global하다.
}
console.log(x); // 5가 나온다.
```





## 3. Function scope

```javascript
var a = 10;     // 전역변수

(function () {  // IIFE 즉시실행함수이다.
  var b = 20;   // 지역변수
})();

console.log(a); // 10
console.log(b); // "b" is not defined
```
- 자바스크립트는 function-level scope를 사용한다. 즉 함수 내에서 선언된 매개변수와 변수는 함수 외부에서는 유효하지 않다. 따라서 `변수 b는 지역 변수이다.`


```javascript
var x = 'global';

function foo() {
  var x = 'local';
  console.log(x);

  function bar() {  // 내부함수
    console.log(x); // local
  }

  bar();
}
foo();
console.log(x); // global

```
- Scope 체이닝이 발생한다. = `실행 컨텍스트`
- `내부함수는 자신을 포함하고 있는 외부함수의 변수에 접근할 수 있다.` 이는 매우 유용하다. 클로저에서와 같이 내부함수가 더 오래 생존하는 경우, 타 언어와는 다른 움직임을 보인다.


```javascript
var x = 'global';

function foo() {
  var x = 'local';
  console.log(x);
}

foo();          // local
console.log(x); // global 
```

```javascript
var x = 10;

function foo() {
  x = 100;
  console.log(x);
}
foo();  // 100
console.log(x); // 100 Q. 왜 100인가요?? 숫자는 지역값을 가져오나요? 
// A. 내부함수에 var가아닌 전역으로 선언해서 그렇다.

```

```javascript
var foo = function ( ) {

  var a = 3, b = 5;

  var bar = function ( ) {
    var b = 7, c = 11;
// 이 시점에서 a는 3, b는 7, c는 11
    a += b + c;
// 이 시점에서 a는 21, b는 7, c는 11
  };
// 이 시점에서 a는 3, b는 5, c는 not defined
  bar( );
// 이 시점에서 a는 21, b는 5  -> a가 참조되어서 bar안에서 변경되서 a=21이며 b는 내부함수껏을 사용못하니깐 5이다.

};
```
## 4. 암묵적 전역
- var 키워드없이 선언을 하면 암묵적으로 전역번수가 된다.

## 5. Lexical scoping (Static scoping)

```javascript
var i = 5;

function foo() {
  var i = 10;
  bar();
}

function bar() { // 선언된 시점에서의 scope를 갖는다!
  console.log(i);
}

foo(); // 5  bar와 foo가 각각 scope이기에 bar는 전역변수 i=5를 가져와서 출력한다.

```

## 6. 변수명의 중복

- i값이 서로 전역변수로 중복이 되기에 조심해야한다.

- `전역변수를 반드시 사용하여야 할 이유를 찾지 못한다면 지역변수를 사용하여야 한다. 변수의 범위인 스코프는 좁을수록 좋다.`

## 7. 최소한의 전역변수 사용

- 전역변수 사용을 최소화하는 방법 중 하나는 애플리케이션에서 전역변수 사용을 위해 다음과 같이 전역변수 객체 하나를 만들어 사용하는 것이다.

```javascript
var MYAPP = {};

MYAPP.student = {
  name: 'Lee',
  gender: 'male'
};

console.log(MYAPP.student.name);
```

## 8. 즉시실행함수를 이용한 전역변수 사용 억제
- 전역변수 사용을 억제하기 위해, 즉시 실행 함수(IIFE, Immediately-Invoked Function Expression)를 사용할 수 있다.

- 즉시 실행 함수는 즉시 실행되고 그 후 전역에서 바로 사라진다.

```javascript
(function () {
  var MYAPP = {};

  MYAPP.student = {
    name: 'Lee',
    gender: 'male'
  };

  console.log(MYAPP.student.name); //사용가능
}());

console.log(MYAPP.student.name); // 여기서 사용안된다.

```