170731

# Javascript Control Flow

## 1. 블록 구문(Block statement)
- 중괄호로 범위가 정해진 구문을 블록 구문이라고 한다.

```javascript
// 함수
function foo() {
  var x = 1, y = 2;
  console.log(x + y);
}
foo();

// 객체리터럴
var obj = {
  x: 1,
  y: 2
};
console.log(obj.x + obj.y);

// 흐름 제어 구문(control flow statement)
var x = 0;
while (x < 10) {
  x++;
}
console.log(x);
```

## 2. 조건문 (Conditional statement)
- 조건식을 가지고 코드블럭을 실행할지 않할지에 대한 의사결정을 하는 것이다.
- 프로그래밍은 요구사항의 집합을 분석하여 적절한 자료구조와 함수의 집합으로 변환한 후 그 흐름을 제어하는 것이다.

### 2.1 if 문
- if문을 통하여 논리적 참, 거짓을 구별한다.

```javascript
if(조건문) {
  // 조건식이 참이면 이 코드블록이 실행된다.
} else {
  // 조건식이 거짓이면 이 코드블록이 실행된다.
}
```

```javascript
var hour = 20;
var greeting;

// if 문
if (hour < 18) {
  greeting = 'Good day';
}

console.log(greeting);

// if-else 문
if (hour < 18) {
  greeting = 'Good day';
} else {
  greeting = 'Good evening';
}

console.log(greeting);

// if-else if 문
if (hour < 10) {
  greeting = 'Good morning';
} else if (hour < 20) {
  greeting = 'Good day';
} else {
  greeting = 'Good evening';
}

console.log(greeting);
```

### 2.2 switch 문
- switch변수의 값과 일치되는 case문으로 실행 순서가 이동하게 된다. 일치하는 값이 없다면 default로 이동한다.

```javascript
var color = 'red';

// color = switch 변수
switch (color) {
  // color == 'yellow'인 경우
  case 'yellow':
    console.log('yellow color');
  // color == 'red'인 경우
  case 'red':
    console.log('red color');
  // color == 'blue'인 경우
  case 'blue':
    console.log('blue color');
  // 그외의 경우
  default:
    console.log('unknown color');
}
```
> 이렇게 하면 break를 선언하지 않았기 때문에 red,blue,unknown까지 출력이된다.

```javascript
var color = 'red';

switch (color) {
  case 'yellow':
    console.log('yellow color');
    break;
  case 'red':
    console.log('red color');
    break;
  case 'blue':
    console.log('blue color');
    break;
  default:
    console.log('unknown color');
}
```

## 3. 반복문(Loop)
- 주어진 조건식이 참인 경우 코드 블록을 반복해서 실행한다.

### 3.1 for 문
- for문은 특정 조건이 거짓으로 판별될 때까지 반복한다.

```javascript
for ([초기문]; [조건문]; [증감문]) {
  구문;
}
```
- 여러 종류의 for문이 존재한다.

```javascript
var array = ['one', 'two', 'three', 'four'];

for (var i = 0; i < array.length; i++) {
  // console.log(array[i]);
  console.log('[' + i + '] = ' + array[i]);
}

// for-in
for (var index in array) {
  console.log('[' + index + '] = ' + array[index]);
}

// foreach
array.forEach(function (element, index, arr) {
  console.log('[' + index + '] = ' + element);
});

// for-of (ES6)
for (const element of array) {
  console.log(element);
}
// array.entries(): 배열의 key/value의 쌍을 반환하는 iterator를 반환
for (const [index, value] of array.entries()) {
  console.log('[' + index + '] = ' + value);
}
```

- for문에 어떤 식도 선언하지 않으면 무한루프가 된다.

### 3.2 while 문
- 조건문이 거짓이 되면 실행을 종료하고 반복문을 빠져나간다.
- 조건문이 언제나 참이면 무한루프가 된다.
- 무한루프를 탈출하기 위해서는 break문을 사용한다. break문을 감싸는 반복문 하나를 탈출한다.

```javascript
var i = 0;
// 무한루프
while (true) {
  console.log(i);
  i++;
  // i가 10이면 exit!
  if (i === 10) break;
}
```

### 3.3 do-while 문
- 코드블록은 조건문을 확인하기 전에 무조건 1회 실행된다. 그후 조건문을 확인한다.

```javascript
var i = 0;
do {
  console.log(i);
  i++;
} while (i < 3);
```

### 3.4 continue
- continue문은 이후 구문의 `실행을 스킵`하고 반복문의 조건문으로 이동한다.
  - 예참조 ->  짝수에서는 console.log를 안한다.
  ```javascript
    for (var i = 0; i < 5; i++) {
      if (i % 2 == 0) continue;
      console.log(i);
  }
  ```

## 4. 평가(Evaluating)
- 일반적 표현식외에도 문자열, 숫자, 변수, 내장값등을 조건식으로 사용할 수 있다.

```javascript
if (1) { // true
  console.log('1');
}

if ('str') { // true
  console.log('2');
}

if (true) { //true
  console.log('3');
}

if (null) { // false
  console.log('4');
}

var x = '';

if (x) { // false
  console.log('5');  
}

if (!x) { //true
  console.log('6');  
}
```

### 4.1 암묵적 강제 형 변환(Type coercion)
- context를 고려하여 내부적으로 자료형을 강제 형변환시킨다.

```javascript
console.log('1' > 0);            // true
console.log(1 + '2');            // '12'
console.log(2 - '1');            // 1
console.log('10' == 10);         // true
console.log('10' === 10);        // false -> type이 다르다.
console.log(undefined == null);  // true
console.log(undefined === null); // false -> type이 다르다.
```

### 4.2 Type Conversion Table
- 부정적 값은 = 0, false, undefined 등으로 나타내진다.
- 긍정적 값은 = 1, true 등으로 나타내진다.

### 4.3 Data type conversion
- 형 변환시 편리하다.

```javascript
var val = '123';
console.log(typeof val + ': ' + val); // string: 123

// sting -> number
val *= 1;   // string에 수를 곱하면 type이 number로 변환된다.
// val = Number(val);
// val = parseInt(val);
console.log(typeof val + ': ' + val); // number: 123

// number -> sting 
val += '';  // 숫자에 빈문자열을 더해준다.
// val = String(val);
console.log(typeof val + ': ' + val); // string: 123
```

> val *= 1;   // string에 수를 곱하면 type이 number로 변환된다.
string->number

> val += '';  // 숫자에 빈문자열을 더해준다. number->string

### 4.4 Truthy & Falsy values
- 아래 값들은 Boolean context에서 false로 평가된다.
  - false
  - undefined
  - null
  - 0
  - NaN (Not a Number)
  - '' (빈문자열)

### 4.5 Checking equality
- 동등비교시 (==, !=)이 아닌 일치연산자(===, !==)을 사용해야한다.
```javascript
// logs false !!!
console.log(null == false);
console.log(undefined == false);
console.log(null == 0);
console.log(undefined == 0);
console.log(undefined === null);
console.log(NaN == null);
console.log(NaN == NaN);

```

### 4.6 Checking existence
- 객체나 배열(배열도 객체이다)이 값을 가지고 있으면 truthy value로 취급된다.

```javascript
if (document.getElementById('header')) {
  // 요소가 존재함 : 필요한 작업을 수행
} else {
  // 요소가 존재하지 않음 : 필요한 작업을 수행
}
```

- 객체의 존재를 boolean으로 비교하면 안된다.
```javascript
if (document.getElementById('header') == true) // false
```

- 주의 사항 : b가 false라는 값을 가진 객체가 된다. 
```javascript
var b = new Boolean(false);
if (b) // true 
```