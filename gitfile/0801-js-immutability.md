170801

# Javascript Immutability
Immutability(변경불가성)이란? 객체가 생성된 이후 그 상태를 변경할 수 없는 디자인 패턴을 의미한다.
레퍼런스를 참조한 다른 객체에서 객체를 변경하는 상황을 해결하는 방법
  - 객체를 불변객체로 만들어 프로퍼티의 변경을 방지하며 객체의 변경이 필요한 경우에는 참조가 아닌 객체의 방어적 복사(defensive copy)를 통해 새로운 객체를 생성한 후 변경한다. 또는 Observer 패턴으로 객체의 변경에 대처할 수도 있다.
  -  `Observer` 패턴으로 객체의 변경에 대처할 수도 있다.
[Observer](https://ko.wikipedia.org/wiki/%EC%98%B5%EC%84%9C%EB%B2%84_%ED%8C%A8%ED%84%B4);

> 데이터 타입이 필요한이유 ? 메모리를 효율적으로 사용하기 위해서

## 1. immutable value vs. mutable value
- Javascript의 기본 자료형(primitive data type)은 변경 불가능한 값(immutable value)이다.
  - Boolean
  - null
  - undefined
  - Number
  - String
  - Symbol (New in ECMAScript 6)

- 객체 타입은 변경 가능한 값(mutable value)이다. 즉 `객체는 새로운 값을 다시 만들 필요없이 직접 변경이 가능하다는 것이다.`

```javascript
var statement = 'I am an immutable value'; // string은 immutable value

var otherStr = statement.slice(8, 17);

console.log(otherStr);   // 'immutable'
console.log(statement);  // 'I am an immutable value'
```
- slice() 메서드는 statement 변수에 저장된 문자열을 변경하는 것이 아니라 사실은 `새로운 문자열을 생성하여 반환하고 있다.(immutable value)`

```javascript
var arr = [];
console.log(arr.length); // 0

var v2 = arr.push(2);    // arr.push()는 메서드 실행 후 arr의 length를 반환
console.log(arr.length); // 1
```
- 처리 후 결과의 복사본을 리턴하는 문자열의 메서드 slice()와는 달리 배열(객체)의 메서드 push()는 직접 대상 배열을 변경한다. 그 이유는 배열은 `객체이고 객체는 immutable value가 아닌 변경 가능한 값이기 때문이다.`

```javascript
var user = {
  name: 'Lee',
  address: {
    city: 'Seoul'
  }
};

var myName = user.name; // 변수 myName은 string 타입이다.
// myName은 기본형이라서 user.name을 참조가아닌 복사를한다. 

user.name = 'Kim'; 
console.log(myName); // Lee -> myName은 참조가아닌 복사를 하기때문에 kim이 반영이안됬다.

myName = user.name;  // 재할당
console.log(myName); // Kim

```
- user.name의 값을 변경했지만 변수 myName의 값은 변경되지 않았다. `이는 user.name의 타입 string이 변경 불가능하기 때문이다.`
- myName은 기본형으로써 값을 pass-by-value(복사)하기 때문에 user.name='kim'이 바로 반영되지 않는다.


```javascript
var user1 = {
  name: 'Lee',
  address: {
    city: 'Seoul'
  }
};

var user2 = user1; // user1이라는 객체를 pass-by-reference한것이다 변수 user2는 객체 타입이다.

user2.name = 'Kim';

console.log(user1.name); // Kim
console.log(user2.name); // Kim
```
- var user2 = user1으로 인해서 user2가 `객체 타입으로 변했기에 참조형으로 반영된다.`
- 객체를 변경못하게 불변객체로 만들어야한다.

## 2. 불변 데이터 패턴(immutable data pattern)
- 의도하지 않은 객체의 변경을 막는 방법 : 객체를 불변객체로 만들어 프로퍼티의 변경을 방지하며 객체의 `변경이 필요한 경우에는 참조가 아닌 객체의 방어적 복사(defensive copy)를 통해 새로운 객체를 생성한 후 변경한다.`

### 2.1 Obejct.assign
- Object.assign은 타킷 객체로 소스 객체의 프로퍼티를 복사한다.
- 소스 객체의 프로퍼티와 동일한 프로퍼티를 가진 타켓 객체의 프로퍼티들은 소스 객체의 프로퍼티로 덮어쓰기된다. 
  - 리턴값으로 타킷 객체를 반환한다.

  > copy의 역할을 한다.

```javascript
// Copy
const obj = { a: 1 };
const copy = Object.assign({}, obj);
console.log(copy); // { a: 1 }
console.log(obj == copy); // false

// Merge
const o1 = { a: 1 };
const o2 = { b: 2 };
const o3 = { c: 3 };

const merge1 = Object.assign(o1, o2, o3);

console.log(merge1); // { a: 1, b: 2, c: 3 }
console.log(o1);     // { a: 1, b: 2, c: 3 }, 타겟 객체가 변경된다!

// Merge
const o4 = { a: 1 };
const o5 = { b: 2 };
const o6 = { c: 3 };

const merge2 = Object.assign({}, o4, o5, o6);

console.log(merge2); // { a: 1, b: 2, c: 3 }
console.log(o4);     // { a: 1 }
```

- Object.assign을 사용하여 기존 객체를 변경하지 않고 객체를 복사하여 사용할 수 있다.

```javascript
const user1 = {
  name: 'Lee',
  address: {
    city: 'Seoul'
  }
};

const user2 = Object.assign({}, user1); // user1을 {}에 Copy

user2.name = 'Kim';

// 상기 2행은 아래와 동치이다.
// {name: 'Kim'}은 user1에 병합되는 것이 아니라 첫번째 인자인 {}에 병합된다.
// const user2 = Object.assign({}, user1, {name: 'Kim'});

console.log(user1.name); // Lee
console.log(user2.name); // Kim
```
- user1 객체를 빈객체에 복사하여 새로운 객체 user2를 생성하였다. user1과 user2는 어드레스를 공유하지 않으므로 한 객체를 변경하여도 다른 객체에 `아무런 영향을 주지 않는다.`

- 주의할 것은 user1 객체는 const로 선언되어 재할당은 할 수 없지만 객체의 프로퍼티는 보호되지 않는다. `다시 말하자면 객체의 내용은 변경할 수 있다.`

### 2.2 Objet.freeze
- Object.freeze()를 사용하여 불변(immutable) 객체로 만들수 있다.
  > 객체 내부의 객체는 얼리지 못한다.
  
```javascript
const user1 = {
  name: 'Lee',
  address: {
    city: 'Seoul'
  }
};

const user2 = Object.assign({}, user1, {name: 'Kim'});

console.log(user1.name); // Lee
console.log(user2.name); // Kim

Object.freeze(user1);

user1.name = 'Kim'; // 무시된다!

console.log(user1); // { name: 'Lee', address: { city: 'Seoul' } }

console.log(Object.isFrozen(user1)); // true
```
- 하지만 객체 내부의 객체(Nested Object)는 변경가능하다.
  - 즉 메소드의 내부내용은 변경가능하다.

```javascript
const user = {
  name: 'Lee',
  address: {
    city: 'Seoul'
  }
};

Object.freeze(user);

user.address.city = 'Busan'; // 변경된다!
console.log(user); // { name: 'Lee', address: { city: 'Busan' } }
```

- 내부 객체까지 변경 불가능하게 만들려면 Deep freeze를 하여야 한다.

```javascript
function deepFreeze(obj) {
  const props = Object.getOwnPropertyNames(obj);

  props.forEach((name) => {
    const prop = obj[name];
    if(typeof prop === 'object' && prop !== null) {
      deepFreeze(prop);
    }
  });
  return Object.freeze(obj);
}

const user = {
  name: 'Lee',
  address: {
    city: 'Seoul'
  }
};

deepFreeze(user);

user.name = 'Kim';           // 무시된다
user.address.city = 'Busan'; // 무시된다

console.log(user); // { name: 'Lee', address: { city: 'Seoul' } }

```

### 2.3 Immutable.js

- 또 다른 대안으로 Facebook이 제공하는 Immutable.js를 사용하는 방법이 있다.
- Immutable.js는 List, Stack, Map, OrderedMap, Set, OrderedSet, Record와 같은 영구 불변 (Permit Immutable) 데이터 구조를 제공한다.
  - npm으로 설치한다.

  ```git
  npm install immutable
  ```

  - Immutable.js의 Map 모듈을 임포트하여 사용한다.

  ```javascript
  const { Map } = require('immutable')
  const map1 = Map({ a: 1, b: 2, c: 3 })
  const map2 = map1.set('b', 50)
  map1.get('b') // 2
  map2.get('b') // 50
  ```

  - map1.set(‘b’, 50)의 실행에도 불구하고 map1은 불변하였다. map1.set()은 결과를 반영한 새로운 객체를 반환한다.