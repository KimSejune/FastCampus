170809

# Js String

## 1. String Constructor
- String 객체는 String() 생성자 함수를 통해 생성할 수 있다. 이때 전달된 인자는 모두 문자열로 변환된다.
  - new를 넣지 않는다면 그냥 문자로만 변환한다.

```javascript
var x = 'Lee';
var y = new String('Lee');

console.log(x == y);  // true
console.log(x === y); // false

console.log(typeof x); // string
console.log(typeof y); // object
```

## 2. String Property

### 2.1 String.length

- 문자열 내의 문자 갯수를 반환한다.

```javascript
var str = 'Hello';
console.log(str.length); // 5

str = '안녕하세요';
console.log(str.length); // 5
```

## 3. String Method

### 3.1 String.prototype.charAt()

- 매개변수로 전달한 index 번호에 해당하는 위치의 문자를 반환한다. 
- index 번호는 0 ~ (문자열 길이 - 1) 사이의 정수이다.

```javascript
str.charAt(index)

var str = 'Hello';

console.log(str.charAt(0)); // H
console.log(str.charAt(1)); // e
console.log(str.charAt(2)); // l
console.log(str.charAt(3)); // l
console.log(str.charAt(4)); // o
// 지정한 index가 범위(0 ~ str.length-1)를 벗어난 경우 빈문자열을 반환한다.
console.log(str.charAt(5)); // ''

for (var i = 0; i < str.length; i++) {
  console.log(str.charAt(i));
}
```

### 3.2 String.prototype.indexOf()

- 문자열 내에 매개변수로 전달된 문자 또는 문자열이 처음 발견된 곳의 index를 반환한다. 
- `발견하지 못한 경우 -1을 반환한다.`

```javascript
str.indexOf(searchValue[, fromIndex])
// searchValue: 검색할 문자 또는 문자열
// fromIndex : 검색 시작 index (생략할 경우, 0)

var str = 'Hello World';

console.log(str.indexOf('l'));  // 2
console.log(str.indexOf('or')); // 7
console.log(str.indexOf('or' , 8)); // -1
```

### 3.3 String.prototype.lastIndexOf()

- 문자열 내에 매개변수로 전달된 문자 또는 문자열이 마지막으로 발견된 곳의 index를 반환한다. 발견하지 못한 경우 -1을 반환한다.

- 2번째 인수(fromIndex)가 전달되면 검색 시작 위치를 fromIndex으로 이동하여 역방향으로 검색을 시작한다. 이때 검색 범위는 0 ~ fromIndex이다.



```javascript
var str = 'Hello World';

console.log(str.lastIndexOf('World')); // 6
console.log(str.lastIndexOf('l'));     // 9
console.log(str.lastIndexOf('o', 5));  // 4
console.log(str.lastIndexOf('o', 8));  // 7
console.log(str.lastIndexOf('l', 10)); // 9

console.log(str.lastIndexOf('H', 0));  // 0
console.log(str.lastIndexOf('W', 5));  // -1
console.log(str.lastIndexOf('x', 8));  // -1
```
### 3.4 String.prototype.replace()

- 첫번째 인수로 전달된 문자열 또는 정규표현식을 대상 문자열에서 검색하여 두번째 인수로 전달된 문자열로 대체한다. 
  - 검색된 문자열이 복수 존재할 경우 첫번째로 검색된 문자열만 대체된다.
- `기본자료형이라서 원본은 변경되지 않는다.`

```javascript
var str = 'Hello Hello';

var replacedStr = str.replace('Hello', 'Lee');
console.log(replacedStr);  // Lee Hello
console.log(str); // Hello Hello

replacedStr = str.replace(/hello/gi, 'Lee'); // 정규표현식
console.log(replacedStr); //  Lee Lee
console.log(str); //  Hello Hello

```
> /hello/의 패턴을 검색하는데 (g반복해서 계속) (i 대소문자를 구분하지 말라)해서 찾는다.

### 3.5 String.prototype.split()

- 첫번째 인수로 전달된 문자열 또는 정규표현식을 대상 문자열에서 검색하여 문자열을 구분한 후 분리된 각 문자열로 이루어진 `배열을 반환한다`.

- 인수가 없는 경우, 대상 문자열 전체를 단일 요소로 하는 배열을 반환한다.


```javascript
str.split([separator[, limit]])
// separator: 구분 대상 문자열 또는 정규표현식
// limit: 구분 대상수의 한계를 나타내는 정수

var str = 'How are you doing?';

var splitStr = str.split(' ');
console.log(splitStr); // [ 'How', 'are', 'you', 'doing?' ]

splitStr = str.split();
console.log(splitStr); // [ 'How are you doing?' ]

splitStr = str.split('');
console.log(splitStr); // [ 'H','o','w',' ','a','r','e',' ','y','o','u',' ','d','o','i','n','g','?' ]

splitStr = str.split(' ', 3);  // 앞에서 부터 3개만 가져와.
console.log(splitStr); // [ 'How', 'are', 'you' ]

splitStr = str.split('o');
console.log(splitStr); // [ 'H', 'w are y', 'u d', 'ing?' ]

```

### 3.6 String.prototype.substring()

- 첫번째 인수로 전달된 index에 해당하는 문자부터 두번째 인수로 전달된 index에 해당하는 문자의 `바로 이전 문자까지`를 모두 반환한다. 이때 첫번째 인수 < 두번째 인수의 관계가 성립된다.
  - 첫번째 인수 > 두번째 인수 : 두 인수는 교환된다. ex) 4,1이면 1,4로 변경된다.
  - 두번째 인수가 생략된 경우 : 해당 문자열의 끝까지 반환한다.
  - 인수 < 0 또는 NaN인 경우 : 0으로 취급된다. ex) -2를 주면 전체를 애기한다.
  - 인수 > 문자열의 길이(str.length) : 인수는 문자열의 길이(str.length)으로 취급된다. 빈문자를 출력한다.

```javascript
var str = 'Hello World'; // str.length == 11

var res = str.substring(1, 4);
console.log(res); // ell

// 첫번째 인수 > 두번째 인수 : 두 인수는 교환된다.
res = str.substring(4, 1);
console.log(res); // ell

// 두번째 인수가 생략된 경우 : 해당 문자열의 끝까지 반환한다.
res = str.substring(4);
console.log(res); // o World

// 인수 < 0 또는 NaN인 경우 : 0으로 취급된다.
res = str.substring(-2);
console.log(res); // Hello World

// 인수 > 문자열의 길이(str.length) : 인수는 문자열의 길이(str.length)으로 취급된다.
res = str.substring(1, 12);
console.log(res); // ello World

res = str.substring(11);
console.log(res); // ''

res = str.substring(20);
console.log(res); // ''

res = str.substring(0, str.indexOf(' '));
console.log(res); // 'Hello'

res = str.substring(str.indexOf(' ') + 1, str.length);
console.log(res); // 'World'
```


### 3.7 String.prototype.toLowerCase()

- 문자열의 문자를 모두 소문자로 변경한다.

### 3.8 String.prototype.toUpperCase()

- 문자열의 문자를 모두 대문자로 변경한다.

### 3.9 String.prototype.trim()

- 문자열 양쪽 끝에 있는 공백 문자를 제거한 문자열을 반환한다.

```javascript
var str = '   foo  ';
var trimmedStr = str.trim();
console.log(trimmedStr);
console.log(str);
```
- 이때 해당 `문자열 자신은 변경되지 않는다`. 문자열은 변경 불가능한 값(immutable value)이기 때문이다.

```javascript

```