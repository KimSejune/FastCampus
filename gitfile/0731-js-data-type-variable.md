170731

# Javascript Data type & Variable
- `변수란? `: 메모리 주소에 접근하기 위해 사람이 이해할 수 있는 언어로 지정한 식별자이다.
- 자료형은 데이터의 성질을 나타낸다.
- javascript 영역이 입력되는 값을 판단하여서 메모리에 저장한다.
- JavaScript는 `동적 타이핑 언어`로 변수의 Type annotation이 필요없이 값이 `할당되는 과정에서 자동으로 자료형이 결정`된다.
- 할당되기 전에는 undefined형이다.
- `typeof`를 통하여 변수의 type을 알 수 있다.


```javascript
var str  = 'Hello';
var num  = 1;
var bool = true;

var foo = 'string';
console.log(typeof foo); // string
foo = 1;
console.log(typeof foo); // number

```

## 1.Data Type (자료형)
- 기본 자료형(변경 불가능)
  - Boolean
  - null
  - undefined
  - Number
  - String
  - Symbol(ECMAScript 6 추가)

- 객체형(변경 가능)
  - object

### 1.1 Primitive Data Type (기본자료형)
- 기본자료형의 값은 `변경 불가능한 값`이다. (pass-by- value)

#### 1.1.1 Boolean
- true, false 두가지의 값을 가질 수 있다.
  - 비어있는 문자열, null, undefined, 숫자 0은 false로 간주된다.

#### 1.1.2 null
- 값을 할당한 이후에 그 값의 관계를 끊는다.
- JavaScript는 case-sensitive(대소문자구분)하므로 null은 항상 소문자로 작성해야한다.

> var foo = null; 을하면 typeof가 null이 나와야하는데 object가 나온다 설계상의 오류이다. 즉 typeof로 check하면 안되고 (foo === null)로 체크해야한다.

#### 1.1.3 undefined
- 값을 할당하지 않은 변수는 undefined값을 가진다.

```javascript
var foo;
console.log(foo); // undefined

foo = {
  name: 'Lee',
  gender: 'male'
}
console.log(foo.bar); // bar가 존재하지 않아서 undefined가 나온다. 

```

#### 1.1.4 Number
- 자바스크립트는 Number인 하나의 숫자 자료형만 존재한다.
  - +/- Infinity, NaN(not-a-number)
  - 정수를 +0으로 나누면 + Infinity, -0으로 나누면 - Infinity이다.
  - NaN은 연산은 가능하지만 숫자로 표시를 못하는 경우

#### 1.1.5 String
- String은 텍스트 데이터를 나타내는데 사용한다.
- '', ""사이에 값을 넣을 수 있지만 주로 ''를 사용한다.

```javascript
var str = "string";
console.log(str[0]);  // s 
console.log(typeof str);  // type = string
console.log(str[3]);  // i
```

- 자바스크립트의 문자열은 변경 불가능(immutable)하다. 이것은 한 번 문자열이 생성되면, 그 문자열을 변경할 수 없다는걸 의미한다.

- 변경 불가능(immutable) 한번 생성된 문자열은 read only로서 수정되지 않는다.

- 새로운 문자를 할당하는 것은 가능하다 += 를 사용한다.
  - 재할당은 그 부분에다가 하는 것이아닌 새로운 부분에다가 만들고 변수가 그곳을 알려주는 것이다.

```javascript
var str = 'string';
console.log(str); // string

str = 'String';    // 재할당
console.log(str); // String

str += ' test';
console.log(str); // String test

str.substring(0, 3);
console.log(str); // Str

str = str.toUpperCase();
console.log(str); // STR
```
> 재할당이란? 기존에 string을 따로두고 새로운 곳에 String으로 만들어 둔다. 

> 메서드란? .앞에는 기본적으로 객체이고 뒤에는 함수인데 이것을 합쳐서 이야기한다.

> 기본자료형은 안에 wrapper가 존재하기에 객체의 역할을 할 수 있다.

#### 1.1.6 Symbol
- Symbol은 애필리케이션 전체에서 유일하며 변경 불가능한(immutable) 기본 자료형(primitive)이다.
  - 주로 객체의 프로퍼티 키(property key)로 사용한다.
  - 자료형을 symbol이라는 함수로 나타내며 이값은 에플리케이션에서 `유일한 값`으로 나타난다.

```javascript
var key = Symbol('key');
console.log(typeof key); // symbol

var obj = {};
obj[key] = 'value';
console.log(obj[key]); // value
```

### 1.2 객체형 (object type, 참조형)
- `객체`는 이름과 값을 가지는 데이터를 의미하는 프로퍼티와 동작을 의미하는 메서드를 포함하고 있는 독립적 주체이다.(pass-by-reference)
- 변경가능한 데이터이다.
- 데이터를 의미하는 `프로퍼티(property)`와 동작을 의미하는 `메서드(method)`를 포함하고 있는 독립적 주체이다.

- 객체의 종류
  - 함수
  - 배열
  - 날짜
  - 정규식

## 2. 변수(Varible)
- 값을 유지할 필요가 있을 때 사용한다.

- 변수명 생성 규칙
  - 반드시 영문자(특수문자 제외), underscore ( _ ), 또는 달러 기호($)로 시작하여야 한다. 이어지는 문자에는 숫자(0~9)도 사용할 수 있다.
  - JavaScript는 대/소문자를 구별하므로 사용할 수 있는 문자는 “A” ~ “Z” (대문자)와 “a” ~ “z” (소문자)이다.
  - `var keyword`를 사용하여서 선언을한다.  

```javascript
var name;     // 변수 name 선언
name = 'Lee'; // 변수 name에 값 'Lee'가 저장(할당)되었다.

var age = 30; // 선언과 할당

var person = 'Lee',
    address = 'Seoul',
    price = 200;

var price = 10;
var tax   = 1;
var total = price + tax;
```

- 선언이 안되어 있는 값에 접근하면 Reference Error 예외가 발생한다.
```javascript
var x;
console.log(x); // undefined
console.log(y); // ReferenceError

```
### 2.1 변수의 중복 선언
- 변수는 중복 선언이 가능하다.
```javascript
var x = 1;
console.log(x); // 1

// 변수의 중복 선언
var x = 100;
console.log(x); // 100
```
- 이기능은 기존의 선언된 값이 의도되지않게 재할당이 될 위험이 있다.(협업시 문제 발생 가능성 증가)

### 2.2 변수 선언 시 var 키워드 생략 허용

```javascript
x = 1;
console.log(x); // 1
```
- var를 사용하지 않았기 때문에 전역 변수로 선언이 된다.

> 전역 변수란? 소스코드 모든 영역에서 변수를 사용할 수 있다.

### 2.3 동적 타이핑 (Dynamic Typing)
- Typing 변수의 type을 설정하는 것을 나타낸다.
- 변수의 Type annotation이 필요없이 값이 할당되는 과정에서 자동으로 자료형이 결정된다.
  - 같은 변수에 여러 data type의 값을 대입할 수 있다.

  > type을 선언하지 않았다면 runtime에러가 발생할 확률이 높다.

```javascript
var foo;

console.log(typeof foo);  // undefined

foo = null;
console.log(typeof foo);  // object

foo = {};
console.log(typeof foo);  // object

foo = 3;
console.log(typeof foo);  // number
foo = 3.14;
console.log(typeof foo);  // number

foo = 'Hi';            
console.log(typeof foo);  // string

foo = true;                  
console.log(typeof foo);  // boolean
```

> 하나의 변수로 여러개의 type을 설정할 수 있지만 위험할 수 있다.

### 2.4 변수 호이스팅 (Variable Hoisting)
- 자바스크립트의 `모든 선언문은 호이스팅`된다.
- 호이스팅이란 var 선언문이나 function 선언문을 해당 `Scope의 선두로 옮겨진것 처럼 `보여지는 것을 말한다.
- javascript의 변수는 `function-level scope`를 가진다.
  > Function-level scope : `함수 내부에서 선언한 변수는 지역변수이며`, 함수 외부에서 선언한 변수는 모두 전역 변수이다. `즉 함수 블록만 지역이다`. 함수내에서 선언된 변수는 함수 내에서만 유효하며 함수 외부에서는 참조할 수 없다. 
  함수 외부에서 선언한 변수는 함수내부에서 사용가능하다.

```javascript
console.log(foo); // ① undefined
var foo = 123;
console.log(foo); // ② 123
{
  var foo = 456;
}
console.log(foo); // ③ 456

```
  - 1. undefined인 이유는 `변수 호이스팅으로 인해서` 밑에 foo가 선언된 값이 `선두로 옮겨진 것 처럼 보여지는 것`이라서 그렇다.

- 변수의 생성단계
  - 선언 단계 : 변수 객체에 변수를 등록한다. 이 변수 객체는 scope가 참조하는 대상이 된다.
  - 초기화 단계 : 변수 객체에 등록된 변수를 메모리에 할당한다. 이 단계에서 변수는 undefined로 초기화된다.
  - 할당 단계 : undefined로 초기화된 변수에 실제값을 할당한다.

  - var keyword로 선언된 변수는 선언 단계와 초기화 단계가 한번에 이루어진다.


> 타언어에서는 if, for문 등의 { ~~ } 안에는 또다른 scope(지역 범위)으로 구분이 되지만 `javascript에서는 구분이 되지 않는다.` javascript는 함수만 scope로 구분한다.

### 2.5 var keyword로 선언된 변수의 문제점
- 1. `Function-level scope`
  - 전역 변수의 남발가능성 농후
  - for loop 초기화식에서 사용한 변수를 for loop 외부 or 전역에서 참조할 수 있다.
- 2. var keyword 생략 허용
  - 의도하지 않은 변수의 전역화
- 3. 중복 선언 허용
  - 의도하지 않은 변수값 변경
- 4. 변수 호이스팅
  - 변수를 선언하기 전에 참조가 가능하다.

- 변수의 범위는 좁을수록 좋다.
