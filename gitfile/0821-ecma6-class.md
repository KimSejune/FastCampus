170821

# ECMAScript6 - Class
- Javascript는 `프로토타입 기반(prototype-based) 객체지향형 언어다.`
- 프로토타입 기반 프로그래밍은 클래스가 필요없는(class-free) 객체지향 프로그래밍 스타일로 프로토타입 체인과 클로저 등으로 객체 지향 언어의 상속, 캡슐화(정보 은닉) 등의 개념을 구현할 수 있다.
- class는 함수 객체이다.

```javascript
// ES5
var Person = (function () {
  // Constructor
  function Person(name) {
    this._name = name;
  }

  // method
  Person.prototype.sayHi = function () {
    console.log('Hi! ' + this._name);
  };

  // return constructor
  return Person;
}());

var me = new Person('Lee');
me.sayHi(); // Hi! Lee.

console.log(me instanceof Person); // true
```
- ES6의 클래스가 새로운 객체지향 모델을 제공하는 것이 아니며 사실 클래스도 함수이고 기존 프로토타입 기반 패턴의 Syntactic sugar일 뿐이다.

## 1. 클래스 정의 (Class Definition)

- ES6 클래스는 class 키워드를 사용하여 정의한다. 위에서 살펴본 Person 생성자 함수를 Person 클래스로 정의해 보자.

```javascript
class Person {
  constructor(name) {  // 생성자 함수
    this._name = name;
  }

  sayHi() {
    console.log(`Hi! ${this._name}`);
  }
}

const me = new Person('Lee');
me.sayHi(); // Hi! Lee

console.log(me instanceof Person); // true
```
- `property의 생성은 항상 constructor내부에서 해야한다.`
- New 생성자를 붙여주지 않으면 error가 발생한다.
- `_name의 의미는 private이라는 의미를 가진다.`

```javascript
const Foo = class MyClass {};

const foo = new Foo();
console.log(foo);  // MyClass {}

new MyClass(); // ReferenceError: MyClass is not defined
```
- 표현식으로는 자주사용하지않기에 선언식 즉 위에것을 자주 사용한다.

## 2. 인스턴스의 생성

- new 연산자를 사용하지 않고 인스턴스를 생성하면 에러가 발생한다.

```javascript
class Foo {}

const foo = Foo(); // TypeError: Class constructor Foo cannot be invoked without 'new'
```

## 3. constructor

- `constructor`는 인스턴스를 생성하고 초기화하기 위한 특수한 메소드이다.
- `property를 만드는 역활을 한다.`
- constructor 메소드는 생략할 수 있다. constructor를 생략하면 constructor() {}를 포함한 것과 동일하게 동작하지만 `객체의 생성과 동시에 초기화는 할 수 없다.`

```javascript
class Foo {}

const foo = new Foo();
console.log(foo); // Foo {}

foo.num = 1;      // 동적 프로퍼티 추가
console.log(foo); // Foo { num: 1 }

class Bar {
  constructor(num) {
    this.num = num;
  }
}

console.log(new Bar(1)); // Bar { num: 1 }
```

## 4. 멤버 변수
- 클래스 바디에는 메소드만을 포함할 수 있다. 클래스 바디에 멤버 변수를 선언하면 SyntaxError가 발생한다.

```javascript
class Foo {
  let name = ''; // SyntaxError

  constructor() {}
}
```
- 따라서 멤버 변수의 선언과 초기화는 반드시 constructor 내부에서 실시한다.

```javascript
class Foo {
  constructor(name) {
    this.name = name; // OK
  }
}

console.log(new Foo('Lee')); // Foo { name: 'Lee' }

```
- constructor 내부에서 선언한 멤버 변수 name은 this(클래스의 인스턴스)에 바인딩되어 있으므로 언제나 public이다.
  - _name과 다르다.

```javascript
class Foo {
  constructor(name) {
    this.name = name; // OK
  }
}

const foo = new Foo('Lee');
console.log(foo.name); // Lee
```

## 5. 호이스팅
- 클래스는 let, const와 같이 호이스팅되지 않는 것처럼 동작한다. 즉 class 선언문 이전에 class를 참조하면 ReferenceError가 발생한다.

```javascript
const foo = new Foo(); // ReferenceError: Foo is not defined
class Foo {}
```
- 클래스는 스코프의 선두에서 class의 선언까지 일시적 사각지대(Temporal Dead Zone; TDZ)에 빠지게 되기 때문에 class 선언문 이전에 class를 참조하면 ReferenceError가 발생한다.

## 6. getter, setter 

### 6.1 getter 
- getter는 어떤 프로퍼티에 접근할 때마다 프로퍼티를 조작하는 행위가 필요할 때 사용한다. 사용 방법은 아래와 같다
- `getter은 반드시 무언가를 반환하여야 한다.`
```javascript
class Foo {
  constructor(arr = []) {
    this._arr = arr;
  }

  // getter: firstElem은 프로퍼티 이름과 같이 사용된다.
  // getter는 반드시 무언가를 반환하여야 한다.
  get firstElem() {
    if (this._arr.length === 0) { return null; }
    return this._arr[0];
  }
}

const foo = new Foo([1, 2]);
// 프로퍼티 firstElem에 접근하면 getter가 호출된다.
console.log(foo.firstElem); // 1
```
### 6.2 setter

- setter는 어떤 프로퍼티에 값을 할당할 때마다 프로퍼티를 조작하는 행위가 필요할 때 사용한다. 사용 방법은 아래와 같다.

```javascript
class Foo {
  constructor(arr = []) {
    this._arr = arr;
  }

  // getter: firstElem은 프로퍼티 이름과 같이 사용된다.
  // getter는 반드시 무언가를 반환하여야 한다.
  get firstElem() {
    if (this._arr.length === 0) { return null; }
    return this._arr[0];
  }

  // setter: firstElem은 프로퍼티 이름과 같이 사용된다.
  set firstElem(elem) {
    // ...this._arr은 this._arr를 개별 요소로 분리한다
    this._arr = [elem, ...this._arr];
  }
}

const foo = new Foo([1, 2]);

// 프로퍼티 lastElem에 값을 할당하면 setter가 호출된다.
foo.firstElem = 100;

console.log(foo.firstElem); // 100
```
