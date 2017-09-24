170808

# Js Number

## 1. Number Constructor
- Number 객체는 Number() 생성자 함수를 통해 생성할 수 있다.

```javascript
new Number(value);

var x = new Number(123);
var y = new Number('123');
var z = new Number('str');

console.log(x); // 123
console.log(y); // 123
console.log(z); // NaN
```

- new와 함께 사용하지 않는다면 형변환을 한다.

```javascript
var x = Number('123');

console.log(typeof x, x); // number 123

var x = 123; // type이 number이다.
var y = new Number(123); // type이 object이다.

console.log(x == y);  // true
console.log(x === y); // false 형과 값을 본다.

console.log(typeof x); // number
console.log(typeof y); // object
```

## 2. Number Property

### 2.1 Number.EPSILON
- Number.EPSILON은 JavaScript에서 표현할 수 있는 가장 작은 수이다.
- 2진수의 형태로다저장되기에 모든 부동소수점은 산술 연산 비교는 정확한 값을 기대하기 어렵다.
- 부동소수점의 비교는 Number.EPSILON을 사용하여 비교 기능을 갖는 함수를 작성하여야 한다.
- ex) 0.1와 0.1보다 가장작은 것과의 차이가 EPSILON이다.
```javascript
console.log(0.1 + 0.2);        // 0.30000000000000004
console.log(0.1 + 0.2 == 0.3); // false!!!

function isEqual(a, b){
  // Math.abs는 절대값을 반환한다.
  // 즉 a와 b의 차이가 JavaScript에서 표현할 수 있는 가장 작은 수인 Number.EPSILON보다 작으면 같은 수로 인정할 수 있다.
  return Math.abs(a - b) < Number.EPSILON;
}

console.log(isEqual(0.1 + 0.2, 0.3));
```

### 2.2 Number.MAX_VALUE
- 자바스크립트에서 사용 가능한 가장 큰 숫자(1.7976931348623157e+308)를 반환한다. `MAX_VALUE보다 큰 숫자는 Infinity이다.`

```javascript
Number.MAX_VALUE; // 1.7976931348623157e+308

var num = 10;
num.MAX_VALUE;    // undefined

console.log(Infinity > Number.MAX_VALUE); // true
```

### 2.3 Number.MIN_VALUE
- 자바스크립트에서 사용 가능한 가장 작은 숫자(5e-324)를 반환한다. MIN_VALUE는 0에 가장 가까운 양수 값이다. MIN_VALUE보다 `작은 숫자는 0으로 변환된다.`

```javascript
Number.MIN_VALUE; // 5e-324

var num = 10;
num.MIN_VALUE;    // undefined

console.log(Number.MIN_VALUE > 0); // true
```

### 2.4 Number.POSITIVE_INFINITY
- 양의 무한대 Infinity를 반환한다.

```javascript
Number.POSITIVE_INFINITY // Infinity

var num = 10;
num.POSITIVE_INFINITY;   // undefined
```
### 2.5 Number.NEGATIVE_INFINITY
- 음의 무한대 -Infinity를 반환한다.

```javascript
Number.NEGATIVE_INFINITY // -Infinity

var num = 10;
num.NEGATIVE_INFINITY;   // undefined
```

### 2.6 Number.NaN
- 숫자가 아님(Not-a-Number)을 나타내는 숫자값이다. Number.NaN 프로퍼티는 NaN 프로퍼티와 같다.

```javascript
console.log(Number('xyz')); // NaN
console.log(1 * 'string');  // NaN
console.log(typeof NaN);    // number
```

## 3. Number Method
- Number 안에 Method들은 형변환을 하지 않는다.

### 3.1 Number.isFinite()
- 매개변수를 통해 전달된 값이 유한수인지, 정상적인 수인지를 검사하여 그 결과를 Boolean으로 반환한다.
- Number 생성자 함수의 property들이다.(static method 정적)

```javascript
Number.isFinite(Infinity)  // false
Number.isFinite(NaN)       // false
Number.isFinite('Hello')   // false
Number.isFinite('2005/12/12')   // false

Number.isFinite(0)         // true
Number.isFinite(2e64)      // true
Number.isFinite(null)      // false. isFinite(null) => true
```

### 3.2 Number.isInteger()
- 매개변수를 통해 전달된 값이 정수(Integer)인지 검사하여 그 결과를 Boolean으로 반환한다. 검사전에 인수를 숫자로 변환하지 않는다.
- Number 생성자 함수의 property들이다.(static method 정적)

```javascript
Number.isInteger(testValue)
// testValue: 검사 대상 값
Number.isInteger(123)   //true
Number.isInteger(-123)  //true
Number.isInteger(5-2)   //true
Number.isInteger(0)     //true
Number.isInteger(0.5)   //false
Number.isInteger('123') //false
Number.isInteger(false) //false
Number.isInteger(Infinity)  //false
Number.isInteger(-Infinity) //false
Number.isInteger(0 / 0) //false

```
### 3.3 Number.isNaN()
- 매개변수를 통해 전달된 값이 NaN인지를 검사하여 그 결과를 Boolean으로 반환한다.
- Number 생성자 함수의 property들이다.(static method 정적)

```javascript
Number.isNaN(testValue)
// testValue: 검사 대상 값
Number.isNaN(NaN)       // true
Number.isNaN(undefined) // false. undefined->NaN. isNaN(undefined) -> true.
Number.isNaN({})        // false. {}->NaN.        isNaN({}) -> true.
Number.isNaN('blabla')  // false. 'blabla'->NaN.  isNaN('blabla') -> true.

Number.isNaN(true)      // false
Number.isNaN(null)      // false
Number.isNaN(37)        // false
Number.isNaN('37');     // false
Number.isNaN('37.37');  // false
Number.isNaN('');       // false
Number.isNaN(' ');      // false
Number.isNaN(new Date())             // false
Number.isNaN(new Date().toString())  // false. String->NaN. isNaN(String) -> true.
```
- NaN이 아니면 전부다 false이다.

### 3.4 Number.isSafeInteger()
- javascript로 표현할 수 있는 정수 범위 안에 있는가?
- 매개변수를 통해 전달된 값이 안전한(safe) 정수값인지 검사하여 그 결과를 Boolean으로 반환한다.
- 검사전에 인수를 숫자로 변환하지 않는다.
- Number 생성자 함수의 property들이다.(static method 정적)

```javascript
Number.isSafeInteger(testValue)
// testValue: 검사 대상 값
Number.isSafeInteger(123)   //true
Number.isSafeInteger(-123)  //true
Number.isSafeInteger(5-2)   //true
Number.isSafeInteger(0)     //true
Number.isSafeInteger(1000000000000000)  // true
Number.isSafeInteger(10000000000000001) // false
Number.isSafeInteger(0.5)   //false
Number.isSafeInteger('123') //false
Number.isSafeInteger(false) //false
Number.isSafeInteger(Infinity)  //false
Number.isSafeInteger(-Infinity) //false
Number.isSafeInteger(0 / 0) //false
```

### 3.5 Number.prototype.toExponential()
- 대상을 지수 표기법으로 변환하여 문자열로 반환한다. 
- 객체에 대해서 호출한다.

```javascript
numObj.toExponential([fractionDigits])
// fractionDigits: 0~20 사이의 정수값으로 소숫점 이하의 자릿수를 나타낸다. 옵션으로 생략 가능하다.  
var numObj = 77.1234;

console.log(numObj.toExponential());  // logs 7.71234e+1
console.log(numObj.toExponential(4)); // logs 7.7123e+1  소수점 이하 4자리를 표시하라
console.log(numObj.toExponential(2)); // logs 7.71e+1
console.log((77.1234).toExponential()); // logs 7.71234e+1
console.log(77 .toExponential());     // logs 7.7e+1 스페이스를 띄어야지 된다.
```

### 3.6 Number.prototype.toFixed()

- 매개변수로 지정된 `소숫점자리`를 반올림하여 `문자열로 반환한다.`

```javascript
numObj.toFixed([digits])
// digits: 0~20 사이의 정수값으로 소숫점 이하 자릿수를 나타낸다. 기본값은 0이며 옵션으로 생략 가능하다.
var numObj = 12345.6789;

numObj.toFixed();       // '12346': 소수점 이하를 반올림
numObj.toFixed(1);      // '12345.7'  소수점 1자리를 유지
numObj.toFixed(6);      // '12345.678900' 소수점 6자리를 유지
(1.23e+20).toFixed(2);  // '123000000000000000000.00'
(1.23e-10).toFixed(2);  // '0.00': 0.00000001의 소수점 2자리 이후를 반올림
2.34.toFixed(1);        // '2.3'
2.35.toFixed(1);        // '2.4'. Note that it rounds up in this case.
-2.34.toFixed(1);       // -2.3: 가로 안에 음수를 넣어두지 않으면 문자열을 반환하지 않는다
(-2.34).toFixed(1);     // '-2.3'
```

### 3.7 Number.prototype.toPrecision()
- 매개변수로 지정된 `전체 자릿수`까지 유효하도록 나머지 자릿수를 반올림하여 문자열로 반환한다.
- 지정된 전체 자릿수로 표현할 수 없는 경우 지수 표기법으로 결과를 반환한다.


```javascript
numObj.toPrecision([precision])
// precision: 1~21 사이의 정수값으로 전체 자릿수를 나타낸다. 옵션으로 생략 가능하다.
var numObj = 5.123456;

numObj.toPrecision()    // '5.123456'
numObj.toPrecision(5)   // '5.1235' // 전체 자리수를 나타낸다.
numObj.toPrecision(2)   // '5.1'
numObj.toPrecision(1)   // '5'

(1234.5).toPrecision(2) // `1.2e+3`
```

### 3.8 Number.prototype.toString()
- `숫자를 문자열로 변환하여 반환한다.`

```javascript
numObj.toString([radix])
// radix: 2~36 사이의 정수값으로 진법을 나타낸다. 옵션으로 생략 가능하다.
var count = 10;
console.log(count.toString());   // '10'
console.log((17).toString());    // '17'
console.log(17 .toString());     // '17'
console.log((17.2).toString());  // '17.2'

var x = 16;
console.log(x.toString(2));       // '10000'  2진수
console.log(x.toString(8));       // '20' 8진수
console.log(x.toString(16));      // '10' 16진수로

console.log((254).toString(16));  // 'fe'
console.log((-10).toString(2));   // '-1010'
console.log((-0xff).toString(2)); // '-11111111'

```

### 3.9 Number.prototype.valueOf()
- Number 객체의 기본자료형 값(primitive value)을 반환한다.

```javascript
numObj.valueOf()


var numObj = new Number(10);
console.log(typeof numObj); // object

var num = numObj.valueOf();
console.log(num);           // 10
console.log(typeof num);    // number

```

Number를 String로 바꾸는 방법 
  - 1.''+num
  - 2.toString사용
  - 3.String(num) new를 사용하지않고 만든다. 쓰지말것.

String을 Number로 바꾸는 방법
  - 1.1 * str  ex) 1*'12' 단 str이 숫자로 변환될 수 있다는 전재
  - 2.parseInt
  - 3.Number(str) 
