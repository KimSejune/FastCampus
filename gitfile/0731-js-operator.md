170731

# Javascript Operator

## 1. 산술 연술자 (Arithmetic Operators)

```javascript
var x = 5;
var y = 2;
var z;

z = x + y;  // 7
z = x - y;  // 3
z = x * y;  // 10
z = x / y;  // 2.5
z = x % y;  // 1
z = x++;    // 5 선대입후증가  즉 먼저 z에게 값을준다 그래서 z= 5 그 뒤에 x=6이된다.
z = ++x;    // 7 선증가후대입 x=6인 값에 ++하니 z=7이된다.
z = x--;    // 7 선대입후감소 
z = --x;    // 5 선감소후대입

var str1 = '5' + 5;      // '55'
var str2 = 5 + '5';      // '55'
var str3 = 'Hello' + 5;  // 'Hello5'
```
- `+ 연산자는` 덧셈 연산과 문자열 연결 연산을 수행한다.
  - 연산 대상이 모두 숫자인 경우 : 덧셈 연산
  - 그 외의 경우 : 문자열 연결 연산


## 2. 대입 연산자 (Assignment Operators)
```javascript
var x;

x = 10;   // 10
x += 5;   // 15
x -= 5;   // 10
x *= 5;   // 50
x /= 5;   // 10
x %= 5;   // 0

var txt1 = 'Good';
var txt2 = 'Morning';
var txt3 = txt1 + ' ' + txt2; // Good Morning

txt1 = 'What a very ';
txt1 += 'nice day'; // What a very nice day
```

## 3. 비교 연산자 (Comparison Operators)

- == : 동등비교 형변환 후, 비교한다.
- === : 일치비교 타입까지 일치하여라  true를 반환
- != : 부등비교
- !== : 불일치비교
- ? : 삼항 연산자

```javascript
var x = 5

x == 5    // true
x == '5'  // true   '5'를 숫자로 형변환을 해버려서  true로 나타낸다.
x == 8    // false

x === 5   // true
x === '5' // false

x != 8    // true
x != 5    // false
x != '5'  // false

x !== 8   // true
x !== 5   // false
x !== '5' // true

x > 0     // true
x > 5     // false
x > 8     // false

x < 0     // false
x < 5     // false
x < 8     // true

x >= 0    // true
x >= 5    // true
x >= 8    // false

x <= 0    // false
x <= 5    // true
x <= 8    // true

//삼항연산자(ternary operator)
// 조건 ? 조건이 ture일때 반환할 값 : 조건이 false일때 반환할 값

var condition = true;
var result = condition ? 'true' : 'false';
console.log(result); // 'true'

var now = new Date();
var greeting = 'Good' + ((now.getHours() > 17) ? ' evening.' : ' day.');

// id의 길이가 INPUT_ID_MIN_LEN보다 작으면 에러 메시지를 출력한다.
var id = 'lee';
var INPUT_ID_MIN_LEN = 5;
var errMsg = id.length < INPUT_ID_MIN_LEN ? '아이디는 5자리 이상으로 입력하세요' : '성공';
console.log(errMsg); // '아이디는 5자리 이상으로 입력하세요'

```

## 4. 논리 연산자 (Logical Operator)
```javascript
// && (논리곱) 연산자
var a1 =  true && true;     // t && t returns true
var a2 =  true && false;    // t && f returns false
var a3 = false && true;     // f && t returns false
var a4 = false && (3 == 4); // f && f returns false
var a5 = 'Cat' && 'Dog';    // t && t returns Dog
var a6 = false && 'Cat';    // f && t returns false
var a7 = 'Cat' && false;    // t && f returns false

// || (논리 합) 연산자
var o1 =  true || true;     // t || t returns true
var o2 = false || true;     // f || t returns true
var o3 =  true || false;    // t || f returns true
var o4 = false || (3 == 4); // f || f returns false
var o5 = 'Cat' || 'Dog';    // t || t returns Cat
var o6 = false || 'Cat';    // f || t returns Cat
var o7 = 'Cat' || false;    // t || f returns Cat

// ! (논리 부정) 연산자
var n1 = !true;  // false
var n2 = !false; // true
var n3 = !'Cat'; // false
```

## 5. 단축 평가
- 논리연산자가 Boolean 값과 함께 사용되지 않을 경우, 둘중 1개가 반환된다.
  - true || anything	true
  - false || anything	anything
  - true && anything	anything
  - false && anything	false

  > JavaScript는 빈문자열을 true로 인식한다.


## 6. 타입 연산자 (Type Operator)
- typeof : 변수의 자료형을 문자열로 반환한다.
- instanceof : 객체가 동일 객체형의 인스터스이면 true를 반환한다.
```javascript
typeof 'John'                 // returns string
typeof 3.14                   // returns number
typeof NaN                    // returns number
typeof false                  // returns boolean
typeof [1, 2, 3, 4]           // returns object
typeof {name:'John', age:34}  // returns object
typeof new Date()             // returns object
typeof function () {}         // returns function 
typeof myCar                  // returns undefined (설계적 결함)
typeof null                   // returns object (설계적 결함)


function Person(){}
var me = new Person()
me instanceof Person // true
```

## 7. !!
- !!은 피연산자를 boolen으로 변환하는 것이다.
```
console.log(!!1);         // true
console.log(!!0);         // false
console.log(!!'string');  // true
console.log(!!'');        // false
console.log(!!null);      // false
console.log(!!undefined); // false
console.log(!!{});        // true
console.log(!![]);        // true
```

- 객체(배열 포함)의 경우 빈 객체라도 존재하기만하면 true로 변환된다.

> 객체의 존재 확인 후 그 결과를 반환해야 하는 경우, !!를 사용하면 `강제로 피연산자를 boolean으로 형 변환 할 수 있다.`

```
function checkExist(obj) {
  return !!obj;
}

var obj;
console.log(checkExist(obj)); // false

obj = {};
console.log(checkExist(obj)); // true
```
