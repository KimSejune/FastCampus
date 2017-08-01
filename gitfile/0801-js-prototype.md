170801

# Javascript prototype

## 1. 프로포타입 객체

- 자바스크립트의 모든 객체는 부모가 존재한다.
- `Prototype 기반 객체로` 나타낸다.

```javascript
var student = {
  name: 'Lee',
  score: 90
};

// student에는 hasOwnProperty 메서드가 없지만 아래 구문은 동작한다.
console.log(student.hasOwnProperty('name')); // true

console.dir(student);
```

> hasOwnProperty는 obejct 객체안에 존재하기에 사용가능하다.

- 함수가 아니여서 prototype이 존재하지 않는다.
