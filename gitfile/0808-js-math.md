170808

# Js Math

## 1. Math Property
- 정적(static) 프로퍼티로 Math 객체를 생성할 필요없이 Math.propertyName의 형태로 사용한다.
- 대문자로 써져있으면 상수이다 즉 변하면 안되는 값이다.
- Math는 생성자 함수가 아닌 객체이다.
- 객체라서 prototype이 존재하지 않는다.

### 1.1 Math,PI
- PI 값(π ≈ 3.141592653589793)을 반환한다.

```javascript
PI 값(π ≈ 3.141592653589793)을 반환한다.
```

## 2. Math Method

### 2.1 Math.abs()
- 절대값을 반환한다.

```javascript
Math.abs('-1');     // 1
Math.abs(-2);       // 2
Math.abs(null);     // 0
Math.abs('string'); // NaN
Math.abs();         // NaN

```

### 2.2 Math.round()
- 숫자를 가장 인접한 정수로 `반올림`한다.

```javascript
var x;

// Returns the value 20
x = Math.round(20.49);

// Returns the value 21
x = Math.round(20.5);

// Returns the value -20
x = Math.round(-20.5);

// Returns the value -21
x = Math.round(-20.51);
```

### 2.3 Math.sqrt()
- 양의 제곱근을 반환한다.

```javascript
Math.sqrt(9); // 3

```

### 2.4 Math.ceil()
- 지정된 숫자를 자신보다 큰, 가장 가까운 정수로 `올림`한다.

```javascript
Math.ceil(1.4); // 2

```

### 2.5 Math.floor()
- 지정된 숫자를 자신보다 작은, 가장 가까운 정수로 `내림`한다.

```javascript
Math.floor(1.6); // 1

```
### 2.6 Math.random()
- 0과 1 사이의 임의의 숫자를 반환한다. 이때 0은 포함되지만 1은 포함되지 않는다.

```javascript
Math.random();

var randomNum = Math.floor((Math.random() * 10) + 1); // 1 ~ 10
console.log(randomNum);
```
### 2.7 Math.pow()
- 첫번째 인수를 밑(base), 두번째 인수를 지수(exponent)로하여 거듭제곱을 반환한다.

```javascript
Math.pow(7, 2);    // 49
Math.pow(7, 3);    // 343
Math.pow(2, 10);   // 1024
```

### 2.8 Math.max()
- `숫자 중 가장 최대수를 반환한다.`
- `중요하게 사용된다.`

```javascript
Math.max( 1, 2, 3 );  // 3

var arr = [1, 2, 3];
var max = Math.max.apply(null, arr); // 3 

// ES6
var max = Math.max(...arr); // 3 
```

> apply는 this의 호출 패턴으로써 사용된다. `func.apply(thisArg, [argsArray])`
// thisArg: 함수 내부의 this에 바인딩할 객체
// argsArray: 함수에 전달할 인자 배열

> ...은 spread연산자로써 array의 요소값을 (1,2,3)으로 풀어준다.

### 2.9 Math.min()
- 숫자 중 가장 최소수를 반환한다.

```javascript
Math.min( 1, 2, 3 );  // 1

var arr = [1, 2, 3];
var min = Math.min.apply(null, arr); // 1

// ES6
var min = Math.min(...arr); // 1
```