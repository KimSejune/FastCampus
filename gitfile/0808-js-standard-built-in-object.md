170808

# Js Standard Built-in Object

## 1. Global Object
- 전역 객체(Global Object)는 모든 객체의 유일한 최상위 객체를 의미하며 일반적으로 Browser-side에서는 window, Server-side(Node.js)에서는 global 객체를 의미한다.

```javascript
// in browser console
this === window // true

// in Terminal
node
this === global // true
```
- 전역 객체는 실행 컨텍스트에 컨트롤이 들어가기 이전에 생성이 되며 constructor가 없기 때문에 new 연산자를 이용하여 새롭게 생성할 수 없다. 즉, 개발자가 전역 객체를 생성하는 것은 불가능하다.
- 전역 객체는 전역 스코프(Global Scope)를 갖게 된다.
- 전역 객체의 자식 객체를 사용할 때 전역 객체의 기술은 생략할 수 있다. 예를 들어 document 객체는 전역 객체 window의 자식 객체로서 window.document…와 같이 기술하여도 좋으나 일반적으로 전역 객체의 기술은 생략한다.

```javascript
document.getElementById('foo').style.display = 'none';
// window.document.getElementById('foo').style.display = 'none';
```

- 그러나 사용자가 정의한 변수와 전역 객체의 자식 객체 이름이 충돌할 때 명확히 명확히 전역 객체를 기술하여 혼동을 방지할 수 있다.

```javascript
function moveTo(url) {
  var location = {'href':'move to '};
  alert(location.href + url);
  // location.href = url;
  window.location.href = url;  // BOM에 들어 있는 location이다.
}
moveTo('http://www.google.com');

```

- 전역 객체는 전역 변수(Global variable)를 프로퍼티로 가지게 된다.
```javascript
var ga = 'Global variable';
console.log(ga);
console.log(window.ga);

```
- 글로벌 영역에 선언한 함수도 전역 객체의 프로퍼티로 접근할 수 있다.

```javascript
function foo() {
  console.log('invoked!');
}
window.foo();
```

- Standard Built-in Objects(표준 빌트인 객체)도 역시 전역 객체의 자식 객체이다. 전역 객체의 자식 객체를 사용할 때 전역 객체의 기술은 생략할 수 있으므로 표준 빌트인 객체도 전역 객체의 기술을 생략할 수 있다.

```javascript
// window.alert('Hello world!');;
alert('Hello world!');
```

### 1.1 Global property (전역 프로퍼티)

#### 1.1.1 Infinity
- 양/음의 무한대를 나타내는 숫자값이다.

```javascript
console.log(3/0);  // Infinity
console.log(-3/0); // -Infinity
console.log(Number.MAX_VALUE * 2); // 1.7976931348623157e+308 * 2 // Infinity로 나온다.
console.log(typeof Infinity); // number

```

#### 1.1.2 NaN
- 숫자가 아님(Not-a-Number)을 나타내는 숫자값이다. 전역개체의 NaN 프로퍼티는 Number.NaN 프로퍼티와 같다.

```javascript
console.log(Number('xyz')); // NaN
console.log(1 * 'string');  // NaN
console.log(typeof NaN);    // number
```

#### 1.1.3 undefined
- 변수에 값이 대입되지 않았음을 나타내는 값이다. 초기값은 기본 자료형(primitive data type) undefined이다.

```javascript
var foo;
console.log(foo); // undefined
console.log(typeof undefined); // undefined

```

### 1.2 Global function (전역 함수)
- Global function(전역 함수)는 전역에서 호출할 수 있으며 호출한 곳(caller)으로 결과값을 반환한다.
- Global function(전역 함수)는 모두 Global Object(전역 객체)의 함수 프로퍼티이다.


#### 1.2.1 eval()
- 사용자로 부터 입력받은 Contents(untrusted data)를 eval()로 실행하는 것은 `보안에 매우 취약하다.`

```javascript
eval(string)
// string: code 또는 표현식을 나타내는 문자열. 표현식은 존재하는 객체들의 프로퍼티들과 변수들을 포함할 수 있다.
var foo = eval('2 + 2');
var x = 5,
    y = 4;
console.log(foo); // 4
console.log(eval('x * y')); // 20
```

#### 1.2.2 isFinite()
- 매개변수(parameter)로 전달된 값이 유한수인지, 정상적인 수인지를 검사하여 그 결과를 Boolean으로 반환한다. 
- 매개변수가 숫자가 아닌 경우, 숫자로 변환한 후 검사를 수행한다.

```javascript
isFinite(testValue)
// testValue: 검사 대상 값
console.log(isFinite(Infinity));  // false
console.log(isFinite(NaN));       // false
console.log(isFinite('Hello'));   // false
console.log(isFinite('2005/12/12'));   // false

console.log(isFinite(0));         // true
console.log(isFinite(2e64));      // true
console.log(isFinite(null));      // true: null->0

Number(null)  // 0 null을 Number로 형변환 시도
Boolean(null) // false null을 Boolean로 형변환 시도
```

- 숫자가 아닌놈이 오면 무조건 false이다.
- 상태를 알려주는 녀석은 is를 사용한다.

#### 1.2.3 isNaN()
- NaN이 들어오면 true, 아니면 false이다.

```javascript
isNaN(testValue)
// testValue: 검사 대상 값
isNaN(NaN)       // true
isNaN(undefined) // true: undefined -> NaN
isNaN({})        // true: {} -> NaN
isNaN('blabla')  // true: 'blabla' -> NaN

isNaN(true)      // false: true -> 1
isNaN(null)      // false: null -> 0
isNaN(37)        // false

// strings
isNaN('37')      // false: '37' -> 37
isNaN('37.37')   // false: '37.37' -> 37.37
isNaN('')        // false: '' -> 0
isNaN(' ')       // false: ' ' -> 0

// dates
isNaN(new Date())             // false: new Date() -> Number
isNaN(new Date().toString())  // true:  String -> NaN
```
- 두수를 비교를 할 때 수인지 아닌지 isNaN으로 비교해준다.

#### 1.2.4 parseFloat()
- 매개변수(parameter)로 전달된 문자열을 부동소수점숫자(floating point number)로 변환하여 반환한다.

```javascript
parseFloat(string)
// string: 변환 대상 문자열
parseFloat('3.14');     // 3.14
parseFloat('10.00');    // 10
parseFloat('34 45 66'); // 34
parseFloat(' 60 ');     // 60
parseFloat('40 years'); // 40
parseFloat('He was 40') // NaN
```

- 매개변수 문자열의 첫 숫자만 반환되며 전후 공백은 무시된다. 그리고 첫문자를 숫자로 변환할 수 없다면 NaN을 반환한다.

#### 1.2.5 parseInt()
- 매개변수(parameter)로 전달된 문자열을 정수형 숫자(Integer)로 변환하여 반환한다.

```javascript
parseInt(string, radix);
// string: 변환 대상 문자열
// radix: 진법을 나타내는 기수(2 ~ 36, 기본값 10)

parseInt('10');       // 10
parseInt('10.33');    // 10
parseInt('34 45 66'); // 34
parseInt(' 60 ');     // 60
parseInt('40 years'); // 40
parseInt('He was 40') // NaN

parseInt('0x20');     // 32
parseInt('10', 16);   // 16 
parseInt('10', 8);    // 8 
```

#### 1.2.6 encodeURI() / decodeURI()

- encodeURI()은 매개변수로 전달된 URI(Uniform Resource Identifier)를 인코딩한다.

```javascript
encodeURI(URI)
// URI: 완전한 URI
decodeURI(encodedURI)
// encodedURI: 인코딩된 완전한 URI
var uri = 'http://www.test.com/자바스크립트/test.php?who=나&target=너#전역 객체';
var enc = encodeURI(uri);
var dec = decodeURI(enc);
console.log(enc);
// http://www.test.com/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8/test.php?who=%EB%82%98&target=%EB%84%88#%EC%A0%84%EC%97%AD%20%EA%B0%9D%EC%B2%B4
console.log(dec);
// http://www.test.com/자바스크립트/test.php?who=나&target=너#전역 객체
```

#### 1.2.7 encodeURIComponent() / decodeURIComponent()
- encodeURIComponent()은 매개변수로 전달된 URI(Uniform Resource Identifier) component(구성 요소)를 인코딩한다.
- 일부분만 띄어서 encode한다.
- 단 아래의 문자는 이스케이프 처리에서 제외된다.
  - 알파벳, 0~9의 숫자, - _ . ! ~ * ‘ ( )
- encodeURIComponent()는 인수를 쿼리스트링의 일부라고 간주한다. 따라서 `=, ?, &`를 인코딩한다. 반면 encodeURI()는 인수를 URI 전체라고 간주하며 파라미터 구분자인 =, ?, &를 인코딩하지 않는다.

```javascript
encodeURIComponent(URI)
// URI: URI component(구성 요소)
decodeURIComponent(encodedURI)
// encodedURI: 인코딩된 URI component(구성 요소)
var uriComp = 'who=나&target=너#전역 객체';
var enc = encodeURIComponent(uriComp);
var dec = decodeURIComponent(enc);
console.log(enc);
// who=%EB%82%98&target=%EB%84%88#%EC%A0%84%EC%97%AD%20%EA%B0%9D%EC%B2%B4
console.log(dec);
// who=나&target=너#전역 객체

```

## 2. Standard Built-in Objects (Global objects)
- Javascript는 프로그램 전체의 영역에서 `공통적으로 필요한 기능`을 사용자 각자가 일일히 작성하는 수고를 줄이기 위해 `Standard Built-in Objects(표준 빌트인 객체)`를 제공한다.

### 2.1 Object
- 객체 생성자(Object constructor)는 레퍼(wrapper) 객체를 생성한다. 만약 생성자 인수값이 null이거나 undefined이면 빈 객체를 반환한다.

```javascript
// 변수 o에 빈 객체를 저장한다
var o = new Object();
console.log(typeof o + ': ', o);

o = new Object(undefined);  //  빈객체 생성
console.log(typeof o + ': ', o);

o = new Object(null);       // 빈객체 생성
console.log(typeof o + ': ', o);
```

- 생성자 함수의 인수값에 따라 강제 형변환된 객체가 반환된다.

```javascript
// String 객체를 반환한다
// var o = new String('String');과 동치이다
var obj = new Object('String');
console.log(typeof obj + ': ', obj);
console.dir(obj);

var strObj = new String('String');
console.log(typeof strObj + ': ', strObj);

// Number 객체를 반환한다
// var o = new Number(123);과 동치이다
var obj = new Object(123);
console.log(typeof obj + ': ', obj);

var numObj = new Number(123);
console.log(typeof numObj + ': ', numObj);

// Boolean 객체를 반환한다.
// var o = new Boolean(true);과 동치이다
var obj = new Object(true);
console.log(typeof obj + ': ', obj);

var boolObj = new Boolean(123);
console.log(typeof boolObj + ': ', boolObj);
```
- 객체를 생성할 경우 특수한 상황이 아니라면 `객체리터럴 방식을 사용하는 것이 일반적이다`.
  - `var o = {};`

### 2.2 Function
- 자바스크립트의 모든 함수는 Function 객체이다. 다른 모든 객체들처럼 Function 객체는 new 연산자을 사용해 생성할 수 있다.

### 2.3 Boolean
- Boolean 객체는 기본자료형 boolean을 위한 레퍼(wrapper) 객체이다. Boolean 생성자 함수로 Boolean 객체를 생성할 수 있다.

```javascript
var x = new Boolean(false);
if (x) { // x는 객체로서 존재한다. 따라서 참으로 간주된다.
  // . . . 이 코드는 실행된다.
}
```
- x자체가 false라는 값을 가지는 객체가 생성되기에 코드가 실행된다.

### 2.4 Number
- [Number](http://poiemaweb.com/js-number)

### 2.5 Math
- [Math](http://poiemaweb.com/js-math)

### 2.6 Date
- [Date](http://poiemaweb.com/js-date)

### 2.7 String
- [String](http://poiemaweb.com/js-string)

### 2.8 RegExp
- [RegExp](http://poiemaweb.com/js-regexp)

### 2.9 Array
- [Array](http://poiemaweb.com/js-array)

### 2.10 Error
- Error 생성자는 error 객체를 생성한다. error 객체의 인스턴스는 런타임 에러가 발생하였을 때 throw된다.

```javascript
try {
  // foo();
  throw new Error('Whoops!');
} catch (e) {
  console.log(e.name + ': ' + e.message);
}
```
- 요청의 실패할경우 에러메세지를 사전에 약속을 해둬야한다.
- Error 이외에 Error에 관련한 객체는 아래와 같다.
  - EvalError
  - InternalError
  - RangeError
  - ReferenceError
  - SyntaxError
  - TypeError
  - URIError

### 2.11 Symbol
- Symbol은 ECMAScript 6(Javascript 2015) 에서 추가된 `유일하고 변경 불가능한(immutable) 기본자료형`으로 Symbol 객체는 기본자료형 Symbol을 위한 `레퍼(wrapper) 객체를 생성한다.`

## 3. 기본자료형과 래퍼객체 (Wrapper Object)
- Standard Built-in Object는 각자의 프로퍼티와 메소드를 가진다.
- 정적(static) 프로퍼티, 메소드는 해당 인스턴스를 생성하지 않아도 사용할 수 있고 prototype에 속해있는 메소드는 해당 prototype을 상속받은 인스턴스가 있어야만 사용할 수 있다. 그런데 기본자료형의 값에 대해 Standard Built-in Object의 메소드를 호출하면 정상적으로 작동한다.

```javascript
var str = 'Hello world!';
var res = str.toUpperCase();
console.log(res); // 'HELLO WORLD!'

var num = 1.5;
console.log(num.toFixed()); // 2
```

- 기본자료형의 값에 대해 Standard Built-in Object의 메소드를 호출할 때, `기본자료형의 값은 연관된 객체(Wrapper 객체)로 일시 변환` 되기 때문에 가능한 것이다. 