170809

# Js RegExp

## 1. 정규표현식 (Regulat Expression)
- 정규표현식(Regular Expression)은 문자열에서 특정 내용을 찾거나 대체 또는 발췌하는데 사용한다.

```javascript
var tel = '0101234567팔';

var myRegExp = /^[0-9]+$/;

console.log(myRegExp.test(tel)); // false
```

```javascript
var myRegExp = /regexr/i;
```
- regexr = 패턴(pattern), i = 플래그(Flag)

### 1.2 플래그
- 플래그는 여러가지 종류가 있다.
  - i	Ignore Case	대소문자를 구별하지 않고 검색한다.
  - g	Global	문자열 내의 모든 패턴을 검색한다.
  - m	Multi Line	문자열의 행이 바뀌더라도 검색을 계속한다.


```javascript
var targetStr = 'Is this all there is?';
var regexr = /is/;

console.log(targetStr.match(regexr)); // [ 'is', index: 5, input: 'Is this all there is?' ]

regexr = /is/ig;

console.log(targetStr.match(regexr)); // [ 'Is', 'is', 'is' ]
```
- match() method를 사용하면 배열로 반영한다.
- test() method를 통하여 있는지 없는지를 찾아내기만 한다.

### 1.2 패턴
- 패턴에는 찾고자 하는 대상을 문자열로 지정한다.
- 패턴은 특별한 의미를 가지는 메타문자(Metacharacter) 또는 기호로 표현할 수 있다. 

```javascript
var targetStr = 'AA BB Aa Bb';
// 임의의 문자 3개
var regexr = /.../;
```
- .를 3개 연속하여 패턴을 생성하였으므로 패턴과 일치하는 3자리 문자를 추출한다.
- 반복하기 위해서는 플래그 g를 사용한다.

```javascript
var targetStr = 'AA BB Aa Bb';
// 임의의 문자 3개를 반복하여 검색
var regexr = /.../g;
console.log(targetStr.match(regexr)); // [ 'AA ', 'BB ', 'Aa ' ]

```

- 대소문자를 구별하지 않게 하려면 플래그 i를 사용한다.

```javascript
var targetStr = 'AA BB Aa Bb';
// 'A'를 대소문자 구분없이 반복 검색
var regexr = /A/ig;
console.log(targetStr.match(regexr)); // [ 'A', 'A', 'A', 'a' ]
```

- 앞선 패턴을 최소 한번 반복하려면 앞선 패턴 뒤에 +를 붙인다.

```javascript
var targetStr = 'AA AAA BB Aa Bb';
// 'A'가 한번이상 반복되는 문자열을 반복 검색 / 1번도 대상이다.
var regexr = /A+/g;
console.log(targetStr.match(regexr)); // [ 'AA', 'AAA', 'A' ]
```

- |를 사용하면 or의 의미를 가지게 된다.

```javascript
var targetStr = 'AA BB Aa Bb';
// 'A' 또는 'B'를 반복 검색
var regexr = /A|B/g;
console.log(targetStr.match(regexr)); // [ 'A', 'A', 'B', 'B', 'A', 'B' ]
```

- 분해되지 않은 단어 레벨로 추출하기 위해서는 +를 같이 사용하면 된다.

```javascript
var targetStr = 'AA AAA BB Aa Bb';
// 'A' 또는 'B'가 한번이상 반복되는 문자열을 반복 검색
var regexr = /A+|B+/g;
console.log(targetStr.match(regexr)); // [ 'AA', 'AAA', 'BB', 'A', 'B' ]
```

-  []내의 문자는 or로 동작한다 위의 | 와 같다.

```javascript
var targetStr = 'AA BB Aa Bb';
// 'A' 또는 'B'가 한번이상 반복되는 문자열을 반복 검색
var regexr = /[AB]+/g;
console.log(targetStr.match(regexr)); // [ 'AA', 'BB', 'A', 'B' ]

```
- 범위를 지정하려면 []내에 -를 사용한다. 아래의 경우 대문자 알파벳을 추출한다범.

```javascript
var targetStr = 'AA BB ZZ Aa Bb';
// 'A' ~ 'Z'가 한번이상 반복되는 문자열을 반복 검색
var regexr = /[A-Z]+/g;
console.log(targetStr.match(regexr)); // [ 'AA', 'BB', 'ZZ', 'A', 'B' ]
```

- 대소문자를 구별하지 않고 알파벳을 추출하려면 아래와 같이 한다.

```javascript
var targetStr = 'AA BB Aa Bb';
// 'A' ~ 'Z' 또는 'a' ~ 'z'가 한번이상 반복되는 문자열을 반복 검색
var regexr = /[A-Za-z]+/g;
console.log(targetStr.match(regexr)); // [ 'AA', 'BB', 'Aa', 'Bb' ]

```

- 숫자를 추출하는 방법이다.

```javascript
var targetStr = 'AA BB Aa Bb 24,000';
// '0' ~ '9'가 한번이상 반복되는 문자열을 반복 검색
var regexr = /[0-9]+/g;
console.log(targetStr.match(regexr)); // [ '24', '000' ]
```

- 컴마 때문에 결과가 분리되므로 패턴에 포함시킨다.

```javascript
var targetStr = 'AA BB Aa Bb 24,000';
// '0' ~ '9' 또는 ','가 한번이상 반복되는 문자열을 반복 검색
var regexr = /[0-9,]+/g;
console.log(targetStr.match(regexr)); // [ '24,000' ]
```

- \d는 숫자를 의미한다. \D는 \d와 반대로 동작한다.
  - `\D는 숫자말고 다른 것을 다 포함한다.`

```javascript
var targetStr = 'AA BB Aa Bb 24,000';
// '0' ~ '9' 또는 ','가 한번이상 반복되는 문자열을 반복 검색
var regexr = /[\d,]+/g;
console.log(targetStr.match(regexr)); // [ '24,000' ]

// '0' ~ '9'가 아닌 문자(숫자가 아닌 문자) 또는 ','가 한번이상 반복되는 문자열을 반복 검색
var regexr = /[\D,]+/g;
console.log(targetStr.match(regexr)); // [ 'AA BB Aa Bb ', ',' ]

```

- \w는 알파벳과 숫자를 의미한다. \W는 \w와 반대로 동작한다.
  - `\W는 알파벳과 숫자가 아닌것을 찾는다.`

```javascript
var targetStr = 'AA BB Aa Bb 24,000';
// 알파벳과 숫자 또는 ','가 한번이상 반복되는 문자열을 반복 검색
var regexr = /[\w,]+/g;
console.log(targetStr.match(regexr)); // [ 'AA', 'BB', 'Aa', 'Bb', '24,000' ]

// 알파벳과 숫자가 아닌 문자 또는 ','가 한번이상 반복되는 문자열을 반복 검색
var regexr = /[\W,]+/g;
console.log(targetStr.match(regexr)); // [ ' ', ' ', ' ', ' ', ',' ]
```

### 1.3 자주 사용하는 정규표현식
- 특정 단어로 시작하는지 검사한다.
  -  `^`를 사용한다.

```javascript
var targetStr = 'abcdef';
// 'abc'로 시작하지 검사
var regexr = /^abc/;
console.log(regexr.test(targetStr)); // true

```

- 특정 단어로 끝나는지 검사한다.
  - `$`를 사용한다.

```javascript
var targetStr = 'abcdef';
// 'ef'로 끝나는지 검사
var regexr = /ef$/;
console.log(regexr.test(targetStr)); // true

```
- 숫자인지 검사한다.
  - `/^\d+$/`를 사용한다.

```javascript
var targetStr = '12345';
// 모두 숫자인지 검사
var regexr = /^\d+$/;
console.log(regexr.test(targetStr)); // true
```

- 공백으로 시작하는지 검사한다.
  - ^[\s]+/; 를 사용한다.

```javascript
var targetStr = ' Hi!';
// 1개 이상의 공백으로 시작하는지 검사
var regexr = /^[\s]+/;
console.log(regexr.test(targetStr)); // true
```

- 아이디로 사용 가능한지 검사한다. (영문자, 숫자만 허용, 4~10자리)
  - `/^[A-Za-z0-9]{4,10}$/`  알파벳 대소문자 또는 숫자로 시작하고 끝나며 4 ~10자리인지 검사의 조건을 사용한다.

```javascript
var targetStr = 'abc123';
// 알파벳 대소문자 또는 숫자로 시작하고 끝나며 4 ~10자리인지 검사 
var regexr = /^[A-Za-z0-9]{4,10}$/
console.log(regexr.test(targetStr)); // true
```

- 메일 주소 형식에 맞는지 검사한다.
  - `/^[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*\.[a-zA-Z]{2,3}$/i`;를 사용한다.
```javascript
var targetStr = 'ungmo2@gmail.com';
var regexr =  /^[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*\.[a-zA-Z]{2,3}$/i;
console.log(regexr.test(targetStr)); // true
```

- 핸드폰 번호 형식에 맞는지 검사한다.
  - `/^\d{3}-\d{3,4}-\d{4}$/;`를 사용한다.

```javascript
var targetStr = '010-1234-5678';
var regexr = /^\d{3}-\d{3,4}-\d{4}$/;
console.log(regexr.test(targetStr)); // true
```

- 특수 문자 포함 여부를 검사한다.
  - /[\{\}\[\]\/?.,;:|\)*~`!^\-_+<>@\#$%&\\\=\(\'\"]/gi 를 사용한다.
  - 특수문자가 있으면 true 없으면 false이다.
```javascript
var targetStr = 'abc#123';
var regexr = /[\{\}\[\]\/?.,;:|\)*~`!^\-_+<>@\#$%&\\\=\(\'\"]/gi
console.log(regexr.test(targetStr)); // true
```

## 2. Javascript Regular Expression

### 2.1 RegExp Constructor

-  RegExp 객체를 생성하기 위해서는 리터럴 방식과 RegExp 생성자 함수를 사용할 수 있다.
  - 일반적인 방법은 리터럴 방식이다.

```javascript
// 정규식 리터럴
var myRegExp = /ab+c/i;

var myRegExp = new RegExp('ab+c', 'i');

var myRegExp = new RegExp(/ab+c/, 'i');

var myRegExp = new RegExp(/ab+c/i); // ECMAScript 6
```


### 2.2 RegExp Method

#### 2.2.1 RegExp.prototype.exec()
- 문자열을 검색하여 매칭 결과를 반환한다. 반환값은 배열 또는 null이다.

```javascript
var target = 'Is this all there is?';
var regExp = /is/;

var res = regExp.exec(target);
console.log(res); // [ 'is', index: 5, input: 'Is this all there is?' ]
```

#### 2.2.2 RegExp.prototype.test()
- 문자열을 검색하여 매칭 결과를 반환한다. 반환값은 true 또는 false이다.

```javascript
var target = 'Is this all there is?';
var regExp = /is/;

var res = regExp.test(target);
console.log(res); // true
```