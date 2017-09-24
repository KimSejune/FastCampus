# ECMA SCRIPT 6 - MODULE
## 1. INTRODUCTION
MODULE : 애플리케이션을 구성하는 개별적 요소
- 구현된 세부사항을 캡슐화하고 공개가 필요한 API를 외부에 노출해 다른 코드에서 로드하고 사용할 수 있도록 작성된 재사용 가능한 코드조각
- 모듈은 캡슐화가 되는 것이 기본적
- 공개할 것만 공개하는 것이 캡슐화이다.
- 모듈만의 개별적인 전역을 가져야한다.
- private은 함수내의 지역변수로 선언된 것으로 사용된다.
> COMMONJS 와 AMD(Asynchronous Module Definition) : 클라이언트 사이드에 국한되지 않고 범용적으로 사용하고자 하는 움직임이 생기면서 제안된 것

## 2. EXPORT & IMPORT
모듈안에 선언한 모든 것들은 기본적으로 해당 모듈 안에서만 참조가능하다.
> 모듈안에 선언한 항목을 외부에 공개해 다른 모듈들이 사용할 수 있게 하고 싶다면 export해야 한다.
```javascript
// lib.js
export const pi = Math.PI; //공개하겠다

export function square(x) { // 공개하겠다
  return x * x;
}

export class Person { // 공개하겠다
  constructor(name) {
    this.name = name;
  }
}
```
선언문 앞에 매번 키워드를 붙이는 것이 싫다면 대상을 한번에 모아 export할 수 있다.
```javascript
// lib.js
const pi = Math.PI;

function square(x) {
  return x * x;
}

class Person {
  constructor(name) {
    this.name = name;
  }
}

export { pi, square, Person };
```
import : export된 이름으로 import한다.
```javascript
// main.js
import { pi, square, Person } from './lib';
console.log(pi);         // 3.141592653589793
console.log(square(10)); // 100
console.log(new Person('Lee')); // Person { name: 'Lee' }
```
각각의 이름을 지정하지 않고 하나로 한꺼번에 import할 수 있다.
```javascript
// main.js
import * as lib from './lib';
console.log(lib.pi);         // 3.141592653589793
console.log(lib.square(10)); // 100
console.log(new lib.Person('Lee')); // Person { name: 'Lee' }
```
이름을 변경해 import 할 수 도 있다.
```javascript
// main.js
import { pi as PI, square as sq, Person as P } from './lib';
console.log(PI);    // 3.141592653589793
console.log(sq(2)); // 4
console.log(new P('Kim')); // Person { name: 'Kim' }
```
모듈에서 하나만을 export하는 경우, default 키워드를 사용할 수 있다.
```javascript
// lib.js
function (x) {
  return x * x;
}
export default;

//축약형
// lib.js
export default function (x) {
  return x * x;
}
```
default 키워드와 함께 export한 모듈은 {}없이 임의의 이름으로 import한다.
```javascript
// main.js
import square from './lib';

console.log(square(3)); // 9
```