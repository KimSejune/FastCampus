# ECMA6 - CLASS
프로토타입 기반 프로그래밍은 클래스가 필요없는(class-free) 객체지향 프로그래밍 스타일로 프로토타입 체인과 클로저 등으로 객체 지향 언어의 상속, 캡슐화(정보 은닉) 등의 개념을 구현할 수 있다.
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
> class도 함수이고 기존 프로토타입 기반 패턴의 syntactic sugar일 뿐이다.
## 1. 클래스 정의
class 키워드를 사용해 정의한다.
```javascript
class Person {
  constructor(name) {
    this._name = name; //_name : private
  }
//constructor 내부에서 선언한 멤버변수 name은 this에 바인딩 되어 있으므로 언제나 public이다.
  sayHi() {
    console.log(`Hi! ${this._name}`);
  }
}

const me = new Person('Lee');
me.sayHi(); // Hi! Lee

console.log(me instanceof Person); // true
```
>표현식으로도 클래식을 정의할 수 있다.
```javascript
const Foo = class MyClass {};

const foo = new Foo();
console.log(foo);  // MyClass {}

new MyClass(); // ReferenceError: MyClass is not defined
```
## 2. 인스턴스의 생성
new 연산자를 사용하지 않고 인스턴스를 생성하면 에러가 발생한다.
```javascript
class Foo {}

const foo = Foo(); // TypeError: Class constructor Foo cannot be invoked without 'new'
```

## 3. constructor
constructor : 인스턴스를 생성하고 초기화하기 위한 특수한 메소드이다.
> 클래스내에 한개만 존재할 수 있으며 만약 클래스가 2개 이상의 constructor 메소드를 포함하면 syntaxerror가 발생한다.
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
constructor를 생략하면 cosntructor(){}를 포함한 것과 동일하게 동작하지만 객체의 생성과 동시에 초기화는 할 수 없다.
> 프로퍼티를 만드는데도 사용된다.
## 4. 멤버 변수
클래스 바디에는 메소드만을 포함할 수 있다.
> 클래스 바디에 멤버변수를 선언하면 syntaxerror가 발생한다.
```javascript
class Foo {
  let name = ''; // SyntaxError

  constructor() {}
}
```
수정 : 멤버변수의 선언과 초기화는 반드시 constructor 내부에서 실시한다.
```javascript
class Foo {
  constructor(name) {
    this.name = name; // OK
  }
}

console.log(new Foo('Lee')); // Foo { name: 'Lee' }
```
> 자바스크립트의 프로퍼티 : 메소드를 담고 있는 프로퍼티, 데이터를 담고 있는 프로퍼티
## 5. 호이스팅
클래스는 let,const와 같이 호이스팅 되지 않는 것 처럼 동작한다.
> class 선언문 이전에 class를 참조하면 referenceerror가 발생한다.
```javascript
const foo = new Foo(); // ReferenceError: Foo is not defined
class Foo {}
```
모든 선언을 호이스팅한다.
> 하지만 클래스는 스코프의 선두에서 class 선언까지 일시적 사각지대(TDZ : temporal dead zone)에 빠지기 때문에 class 선언문 이전에 class를 선언하면 reference 에러가 발생한다.
## 6. GETTER, SETTER
### 1. GETTER
어떤 프로퍼티에 접근할 때마다 프로퍼티를 조작하는 행위가 필요할 때 사용한다.
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
### 2. SETTER
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
## 7. 정적 메소드
static : 클래스의 정적 메소들르 정의
> 정적 메소드 : 클래스의 인스턴스화없이 호출하며 `클래스의 인스턴스로 호출할 수 없다.`
```javascript
//ES5
var Foo = (function () {
  function Foo(prop) {
    this.prop = prop;
  }
  Foo.staticMethod = function () {
    return 'staticMethod';
  };
  Foo.prototype.prototypeMethod = function () {
    return 'prototypeMethod';
  };
  return Foo;
}());

var foo = new Foo(123);

console.log(Foo.staticMethod());
console.log(foo.staticMethod()); // Uncaught TypeError: foo.staticMethod is not a function

//ES6
class Foo {
  constructor(prop) {
    this.prop = prop;      
  }
  static staticMethod() {
    return 'staticMethod';
  }
  prototypeMethod() {
    return 'prototypeMethod';
  }
}

const foo = new Foo(123);

console.log(Foo.staticMethod());
console.log(foo.staticMethod()); // Uncaught TypeError: foo.staticMethod is not a function
```
> 정적 메소드는 어플리케이션을 위한 유틸리티 함수를 생성하는데 주로 사용된다.

## 8. 클래스 상속
### 1. Extends 키워드
부모클래스를 상속하는 자식 클래스의 생성을 위해 클래스 선언에 사용된다.
```javascript
// Base Class
class Animal {
  constructor(weight) {
    this._weight = weight;
  }

  weight() {
    console.log(this._weight);
  }

  eat() { console.log('Animal eat.'); }
}

// Sub Class
class Human extends Animal {
  constructor(weight, language) {
    super(weight);
    this._language = language;
  }

  // 부모 클래스의 eat 메소드를 오버라이드하였다
  eat() { console.log('Human eat.'); }

  speak() {
    console.log(`Koreans speak ${this._language}.`);
  }
}

const korean = new Human(70, 'Korean');
korean.weight(); // 70
korean.eat();    // Human eat.
korean.speak();  // Koreans speak Korean.

console.log(korean instanceof Human);  // true
console.log(korean instanceof Animal); // true
//instanceOf : 연산자 // korean은 human의 인스턴스이냐?는 질문을 한다.
```
> 프로토타입 체인 : 특정 객체의 프로퍼티나 메소드에 접근하려고 할 때 해당 객체에 접근하려는 프로퍼티 또는 메소드가 없다면 [[Prototype]]프로퍼티가 가리키는 링크를 따라 자신의 부모 역할을 하는 프로토타입 객체의 프로퍼티나 메소드를 차례대로 검색한다.

### 2. super 키워드
부모 클래스 프로퍼티를 참조할 때 또는 부모 클래스의 constructor를 호출할 때 사용한다.
```javascript
class Parent {
  constructor(x, y) {
    this._x = x;
    this._y = y;
  }

  toString() {
    return `${this._x}, ${this._y}`;
  }
}

class Child extends Parent {
  constructor(x, y, z) {
    // super 메소드는 자식 class의 constructor 내부에서 부모 클래스의 constructor(super-constructor)를 호출한다.
    super(x, y);
    this._z = z;
  }

  toString() {
    // super 키워드는 부모 클래스(Base Class)에 대한 참조이다. 부모 클래스의 프로퍼티 또는 메소드를 참조하기 위해 사용한다.
    return `${super.toString()}, ${this._z}`; // B
  }
}

const child = new Child(1, 2, 3);
console.log(child.toString()); // 1, 2, 3
```
>자식 클래스의 constructor에서 super()를 호출하지 않으면 refernece error가 발생
```javascript
class Parent {
  constructor(x) {
    this._x = x;
  }
}

class Child extends Parent {
  constructor(x, y) {
    // console.log(this); // ReferenceError: this is not defined
    super(x);
    this._y = y;
    console.log(this); // Child { _x: 1, _y: 2 }
  }
}

const child = new Child(1, 2);
```
> super()를 호출하기 이전에는 this를 참조할 수 없다.
### 3. static 메소드와 prototype메소드의 상속
