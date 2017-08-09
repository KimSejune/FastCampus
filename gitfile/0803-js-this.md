170803

# Javascript this

- 자바스크립트의 함수는 호출될 때, 매개변수로 전달되는 인자값 이외에, `arguments 객체와 this를 암묵적으로 전달 받는다.`

```javascript
function square(number) {

  console.log(arguments);
  console.log(this);  // browser에서는 window로 node에서는 global로 출력된다.
  // 전역이다.

  return number * number;
}

var result = square();
```


- `This는 특별한 상황 2가지를 제외한 경우는 모두 전역변수를 의미한다.`
  - 예외 1. method로 호출될때 호출한 것이 this로 사용된다./ method의 내부함수도 전역 변수이다.
  - 예외 2. 생성자 함수에서 생성된 객체의 경우 `this는 생성자 함수가 생성할 객체를 가르킨다.`  

- 자바스크립트의 경우 자바와 같이 this에 바인딩되는 객체는 한가지가 아니라 `해당 함수 호출 패턴에 따라 this에 바인딩되는 객체가 달라진다.`

## 함수 호출 패턴과 this 바인딩
  - 메소드 호출 패턴(Method Invocation Pattern)
  - 함수 호출 패턴(Function Invocation Pattern)
  - 생성자 호출 패턴(Constructor Invocation Pattern)
  - apply 호출 패턴(Apply Invocation Pattern)  
 
## 1. 메소드 호출 패턴(Method Invocation Pattern)
- this는 그 method를 소유한 객체를 가르킨다. `즉 그 method를 호출한 객체를 가르킨다.`

```javascript
var obj1 = {
  name: 'Lee',
  sayName: function() {
    console.log(this.name);
  }
}

var obj2 = {
  name: 'Kim'
}

obj2.sayName = obj1.sayName;

obj1.sayName();  // Lee
obj2.sayName();  // kim

```

- 프로토타입 객체도 메소드를 가질 수 있다. 프로토타입 객체 메소드 내부에서 사용된 this도 일반 메소드 방식과 마찬가지로 해당 메소드를 호출한 객체에 바인딩된다.

> 즉 함수를 부른 객체에 적용이된다.

Q. obj2에는 sayName함수가없는데 이것은 obj2__proto__, obj1__proto__가 같아서인가요?? 아니면 무슨이유인가요?

A. `this의 특징인 method를 호출한 객체를 가르키기 때문이다.`


```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.getName = function() {
  return this.name;
}

var me = new Person('Lee');
console.log(me.getName()); // Lee -> method를 호출한 객체를 가르키기 때문이다.

Person.prototype.name = 'Kim';
console.log(Person.prototype.getName()); // kim

```

![method prototype this](../images/prototype_metthod_invocation_pattern.png)

## 2. 함수 호출 패턴(Function Invocation Pattern)
- 전역객체(Global Object)는 모든 객체의 유일한 최상위 객체를 의미하며 일반적으로 Browser-side에서는 window, Server-side(Node.js)에서는 global 객체를 의미한다.

- 기본적으로 this는 전역객체(Global object)에 바인딩된다. 전역함수는 물론이고 심지어 내부함수의 경우도 this는 외부함수가 아닌 전역객체에 바인딩된다.

- method 내부의 내부함수의 this도 전역을 가르킨다. (설계상 결점) 
```javascript
var value = 1;

var obj = {
  value: 100,
  foo: function() {
    console.log("foo's this: ",  this);  // obj
    console.log("foo's this.value: ",  this.value); // 100
    function bar() {
      console.log("bar's this: ",  this); // window
      console.log("bar's this.value: ", this.value); // 1
    }
    bar();
  }
};

obj.foo();
```

- 콜백함수의 경우에도 this는 전역객체에 바인딩된다.(설계적 결함)
```javascript
var value = 1;

var obj = {
  value: 100,
  foo: function() {
    setTimeout(function() {
      console.log("callback's this: ",  this);  // window
      console.log("callback's this.value: ",  this.value); // 1
    }, 100);
  }
};

obj.foo();
```

- this의 전역객체 회피방법
```javascript
var value = 1;

var obj = {
  value: 100,
  foo: function() {
    var that = this;  // Workaround : this === obj

    console.log("foo's this: ",  this);  // obj
    console.log("foo's this.value: ",  this.value); // 100
    function bar() {
      console.log("bar's this: ",  this); // window
      console.log("bar's this.value: ", this.value); // 1

      console.log("bar's that: ",  that); // obj
      console.log("bar's that.value: ", that.value); // 100
    }
    bar();
  }
};
```

> var that = this; 여기서 this는 obj이다 즉 that은 obj이므로 이상해지면 that을 써준다.

## 3. 생성자 호출 패턴(Constructor Invocation Pattern)
- 생성자 함수를 생성시 `new를 쓴것과 안쓴것은 차이가 있다.`

### 3.1 생성자 함수 동작 방식

- 빈 객체 생성 및 this 바인딩
- this를 통한 프로퍼티 생성
- 생성된 객체 반환
  - 생성자 함수 내부에는 return을 안써주는 것이다. 암묵적으로 해주기에 안써주는것이다 쓰면 코드가 꼬인다.
  - `this는 생성자 함수가 생성할 객체를 가르킨다.`

```javascript
var Person = function(name) {
  // 생성자 함수 코드 실행 전 -------- 1
  this.name = name;  // --------- 2
  // 생성된 함수 반환 -------------- 3
}

var me = new Person('Lee');
console.log(me.name);
```
![this constructor](../images/constructor.png)

## 3.3 생성자 함수에 new 연산자를 붙이지 않고 호출할 경우

```javascript
var Person = function(name) {
  // 전역객체에 name 프로퍼티를 추가
  this.name = name;
};

// 일반 함수로서 호출되었기 때문에 객체를 생성하여 반환하지 않는다.
// 일반 함수의 this는 전역객체를 가리킨다.
var me = Person('Lee');

console.log(me); // undefined
console.log(window.name); // Lee
```
- me에다가 값이 들어가지 않고 window에 값이 들어간다.
- `방어코드를 작성해서 new를 빼먹는 경우를 방어한다.`

```javascript
// Scope-Safe Constructor Pattern
function A(arg) {
  // 생성자 함수가 new 연산자와 함께 호출되면 함수의 선두에서 빈객체를 생성하고 this에 바인딩한다.

  /*
  this가 호출된 함수(arguments.callee, 본 예제의 경우 A)의 인스턴스가 아니면 new 연산자를 사용하지 않은 것이므로 이 경우 new와 함께 생성자 함수를 호출하여 인스턴스를 반환한다.
  arguments.callee는 호출된 함수의 이름을 나타낸다. 이 예제의 경우 A로 표기하여도 문제없이 동작하지만 특정함수의 이름과 의존성을 없애기 위해서 arguments.callee를 사용하는 것이 좋다.
  */
  if (!(this instanceof arguments.callee)) { // A에 의해 생성된 객체가 아니라면
    return new arguments.callee(arg); // 강제로 new를 붙인다.
  }

  this.value = arg ? arg : 0;
}

var a = new A(100);
var b = A(10);

console.log(a.value);
console.log(b.value);

```
- argument.callee는 생성자의 이름이 나타난다.

## 4. apply 호출 패턴(Apply Invocation Pattern)

> 유사배열 : 유사배열은 배열이아닌 객체라서 배열처럼 불를수있지만 `원래의 순서가 보장이 안된다.`

- func.apply는 func의 양부인 Function.prototype 객체의 메소드이다.
- []는 option을 나타낸다.

```javascript
func.apply(thisArg, [argsArray])

// thisArg: 함수 내부의 this에 바인딩할 객체
// argsArray: 함수에 전달할 인자 배열
```

```javascript
var Person = function (name) {
  this.name = name;
};

var foo = {};

// apply 메소드는 생성자함수 Person을 호출한다. 이때 this에 객체 foo를 바인딩한다.
Person.apply(foo, ['name']); // this로 쓸 객체 = foo, name은 Person의 인자배열 / call은 , 로 구분해서준다.

console.log(foo); // { name: 'name' }
```

```javascript
function convertArgsToArray() {
  console.log(arguments);

  // arguments 객체를 배열로 변환
  // slice: 배열의 특정 부분에 대한 복사본을 생성한다.
  var arr = Array.prototype.slice.apply(arguments); // arguments.slice
  // var arr = [].slice.apply(arguments);
  // argument를 Array로 변환해서 arr에 저장해준다.

  console.log(arr);
  return arr;
}

convertArgsToArray(1, 2, 3);

```

- argumetns 객체는 배열 객체는 아닌데 slice를 쓰게해달라고 해주는게 apply이다 그래서 배열객체의.prototype에 .apply를 통해서 argument가 쓰게해준다.

```javascript
Person.apply(foo, [1, 2, 3]);

Person.call(foo, 1, 2, 3);
```
- call과 apply의 차이는 배열이냐 , 이냐의 차이이다.

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.doSomething = function(callback) {
  if(typeof callback == 'function') {
    // --------- 1 여기서 this는 method안에서 작동하니 Person을 가르킨다.
    callback();
  }
};

function foo() {
  console.log(this.name); // --------- 2 전역 this
}

var p = new Person('Lee');
p.doSomething(foo);  // undefined
```

- callback함수에다가 직접적으로 call에 this를 명시해줘서 일반함수가 callback을 사용할 수 있게 해준다.

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.doSomething = function(callback) {
  if(typeof callback == 'function') {
    callback.call(this);
  }
};

function foo() {
  console.log(this.name);
}

var p = new Person('Lee');
p.doSomething(foo);  // 'Lee'

```