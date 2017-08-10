170809

# Js Date
- 생성자 함수로 반드시 생성해야한다 리터럴 방식이 없다.

## 1. Date Constructor
- Date 생성자를 사용하여 날짜와 시간을 가지는 인스턴스를 생성한다. 

```javascript
new Date()
new Date(milliseconds)
new Date(dateString)
new Date(year, month[, day, hour, minute, second, millisecond])
```
- Date() 생성자 함수를 new 연산자없이 사용하면 Date 객체를 반환하지 않고 결과값을 문자열로 반환한다.

```javascript
var date = new Date();
console.log(typeof date, date); //object Thu May 12 2016 00:51:36 GMT+0900 (KST)

date = Date();
console.log(typeof date, date); // string Thu May 12 2016 00:51:36 GMT+0900 (KST)

console.dir(Date);
```

### 1.1 new Date()
- 매개변수가 없는 경우 현재 날짜와 시간을 가지는 인스턴스를 반환한다.

```javascript
var d = new Date();
console.log(d); // Thu May 12 2016 15:38:39 GMT+0900 (KST)
```

### 1.2 new Date(milliseconds)

- 매개변수에 밀리초를 전달하면 1970년 1월 1일 00:00(UTC)을 기점으로 전달된 밀리초만큼 경과한 날짜와 시간을 가지는 인스턴스를 반환한다.

```javascript
var d = new Date(0);
console.log(d); // Fri Jan 01 1970 09:00:00 GMT+0900 (KST)

var d = new Date(86400000);
console.log(d); // Fri Jan 02 1970 09:00:00 GMT+0900 (KST)
```
- 86400000ms는 1day를 의미한다.

### 1.3 new Date(dateString)
- 매개변수에 날짜와 시간을 나타내는 `문자열`을 전달하면 지정된 날짜와 시간을 가지는 인스턴스를 반환한다.
  - 문자열로 나타내진다.

```javascript
var d = new Date('2017/08/08/20:00:00');
console.log(d); // Tue Aug 08 2017 20:00:00 GMT+0900 (KST)
```

### 1.4 new Date(year, month[, day, hour, minute, second, millisecond])
- 매개변수에 년, 월, 일, 시, 분, 초, 밀리초를 의미하는 숫자를 전달하면 지정된 날짜와 시간을 가지는 인스턴스를 반환한다. `이때 년, 월을 반드시 지정하여야 한다. `
  - 숫자로 나타내진다.
  - year	1900년 이후의 년
  - month	월을 나타내는 `0 ~ 11까지의 정수 (주의: 0부터 시작, 0 = 1월)`
  - day	일을 나타내는 1 ~ 31까지의 정수
  - hour	시를 나타내는 0 ~ 23까지의 정수
  - minute	분을 나타내는 0 ~ 59까지의 정수
  - second	초를 나타내는 0 ~ 59까지의 정수
  - millisecond	밀리초를 나타내는 0 ~ 999까지의 정수

```javascript
var d = new Date(1999);
console.log(d); // Thu Jan 01 1999 09:00:01 GMT+0900 (KST)

var d = new Date(1999, 10, 3, 11, 33, 30, 0);
console.log(d); // Wed Nov 03 1999 11:33:30 GMT+0900 (KST)

var d = new Date(1999, 10);
console.log(d); // Mon Nov 01 1999 00:00:00 GMT+0900 (KST)

var d = new Date('1999/10/3/11:33:00:00');
console.log(d); // Mon Nov 01 1999 00:00:00 GMT+0900 (KST)
```

## 2. Date Method

### 2.1 Date.now()

- 1970년 1월 1일 00:00:00(UTC)을 기점으로 현재 시간까지 경과한 밀리초를 숫자로 반환한다.

```javascript
var n = Date.now();
console.log(n);

```
### 2.2 Date.parse()

- 1970년 1월 1일 00:00:00(UTC)을 기점으로 매개변수로 전달된 지정 시간(new Date(dateString)의 인수와 동일한 형식)까지의 밀리초를 숫자로 반환한다.
  - UTC로 지정을 안해주면 컴퓨터의 로컬을 기준으로 반영한다.

```javascript
var d = Date.parse('Jan 2, 1970 00:00:00 UTC'); // UTC
console.log(d); // 86400000

var d = Date.parse('Jan 2, 1970 09:00:00'); // KST
console.log(d); // 86400000

var d = Date.parse('1970/01/02/09:00:00'); // KST
console.log(d); // 86400000
```

### 2.3 Date.UTC()

- 1970년 1월 1일 00:00:00(UTC)을 기점으로 매개변수로 전달된 지정 시간(new Date(year, month[, day, hour, minute, second, millisecond]))의 인수와 동일한 형식)까지의 밀리초를 숫자로 반환한다.

- UTC() 메소드는 new Date(year, month[, day, hour, minute, second, millisecond])와 같은 형식의 인수를 사용한다. 하지만 UTC() 메소드의 인수는 local time(KST)가 아닌 UTC로 인식된다.


```javascript
var d = Date.UTC(1970, 0, 2);
console.log(d); // 86400000

var d = Date.UTC('1970/1/2');
console.log(d); // NaN
```

### 2.4 Date.prototype.getFullYear()

- 해당 연도를 나타내는 4자리 숫자를 반환한다.

```javascript
var today = new Date();
var year = today.getFullYear();

console.log(today); // Tue Aug 08 2017 20:53:24 GMT+0900 (KST)
console.log(year);  // 2017

```

### 2.5 Date.prototype.setFullYear()

- 해당 연도를 나타내는 4자리 숫자를 설정한다. 연도 이외 월, 일도 설정할 수 있다.

```javascript
dateObj.setFullYear(yearValue[, monthValue[, dayValue]])


var today = new Date();
today.setFullYear(2000);
var year = today.getFullYear();

console.log(today); // Tue Aug 08 2000 20:54:21 GMT+0900 (KST)
console.log(year);  // 2000

today.setFullYear(1900, 0, 1);
year = today.getFullYear();

console.log(today); // Mon Jan 01 1900 20:54:21 GMT+0900 (KST)
console.log(year);  // 1900
```

### 2.6 Date.prototype.getMonth()

- 해당 월을 나타내는 0 ~ 11의 정수를 반환한다. 1월은 0, 12월은 11이다.

### 2.7 Date.prototype.setMonth()

- 해당 월을 나타내는 0 ~ 11의 정수를 설정한다. 1월은 0, 12월은 11이다. 월 이외 일도 설정할 수 있다.

### 2.8 Date.prototype.getDate()

- 해당 날짜(1 ~ 31)를 나타내는 정수를 반환한다.


### 2.9 Date.prototype.setDate()

- 해당 날짜(1 ~ 31)를 나타내는 정수를 설정한다.


###2.10 Date.prototype.getDay()

- 해당 요일(0 ~ 6)를 나타내는 정수를 반환한다. 반환값은 아래와 같다.
  - 0은 일요일 6은 토요일이다.

```javascript
var today = new Date();
var day = today.getDay();

console.log(today); // Tue Aug 08 2017 20:58:22 GMT+0900 (KST)
console.log(day);   // 2
```

### 2.11 Date.prototype.getHours()

- 해당 시간(0 ~ 23)를 나타내는 정수를 반환한다.

### 2.12 Date.prototype.setHours()

- 해당 시간(0 ~ 23)를 나타내는 정수를 설정한다. 시간 이외 분, 초, 밀리초도 설정할 수 있다.

### 2.13 Date.prototype.getMinutes()

- 해당 분(0 ~ 59)를 나타내는 정수를 반환한다.

### 2.14 Date.prototype.setMinutes()

- 해당 분(0 ~ 59)를 나타내는 정수를 설정한다. 분 이외 초, 밀리초도 설정할 수 있다.

### 2.15 Date.prototype.getSeconds()

- 해당 초(0 ~ 59)를 나타내는 정수를 반환한다.


### 2.16 Date.prototype.setSeconds()

- 해당 초(0 ~ 59)를 나타내는 정수를 설정한다. 초 이외 밀리초도 설정할 수 있다.

### 2.17 Date.prototype.getMilliseconds()

- 해당 밀리초(0 ~ 999)를 나타내는 정수를 반환한다.


### 2.18 Date.prototype.setMilliseconds()

- 해당 밀리초(0 ~ 999)를 나타내는 정수를 설정한다.

### 2.19 Date.prototype.getTime()

- 1970년 1월 1일 00:00:00(UTC)를 기점으로 현재 시간까지 경과된 밀리초를 반환한다.

### 2.20 Date.prototype.setTime()

- 1970년 1월 1일 00:00:00(UTC)를 기점으로 현재 시간까지 경과된 밀리초를 설정한다.

### 2.21 Date.prototype.getTimezoneOffset()

- UTC와 지정 로케일(Locale) 시간과의 차이를 분단위로 반환한다.

### 2.22 Date.prototype.toDateString()

- 사람이 읽을 수 있는 형식의 문자열로 날짜를 반환한다.

```javascript
var d = new Date('1988/8/17/13:30');

console.log(d.toString());     // Sat Sep 17 1988 13:30:00 GMT+1000 (KDT)
console.log(d.toDateString()); // Sat Sep 17 1988
```

### 2.23 Date.prototype.toTimeString()

- 사람이 읽을 수 있는 형식의 문자열로 시간을 반환한다.

```javascript
var d = new Date('1988/8/17/13:30');

console.log(d.toString());     // Wed Aug 17 1988 13:30:00 GMT+1000 (KDT)
console.log(d.toTimeString()); // 13:30:00 GMT+1000 (KDT)
```

### 3. Date Example

- 현재 날짜와 시간을 초단위로 반복 출력하는 예제이다.

```javascript
(function printNow() {
  var today = new Date();

  var dayNames = ['(일요일)', '(월요일)', '(화요일)', '(수요일)', '(목요일)', '(금요일)', '(토요일)'];
  // getDay: 해당 요일(0 ~ 6)를 나타내는 정수를 반환한다.
  var day = dayNames[today.getDay()];

  var year   = today.getFullYear(),
      month  = today.getMonth() + 1,
      date   = today.getDate(),
      hour   = today.getHours(),
      minute = today.getMinutes(),
      second = today.getSeconds();
      ampm   = hour >= 12 ? 'PM' : 'AM';

  // 12시간제로 변경
  hour = hour % 12;
  hour = hour ? hour : 12; // 0 => 12

  // 10미만인 분과 초를 2자리로 변경
  minute = minute < 10 ? '0' + minute : minute;
  second = second < 10 ? '0' + second : second;

  var now = year + '년 ' + month + '월 ' + date + '일 ' + day + ' ' + hour + ':' + minute + ':' + second + ' ' + ampm;

  console.log(now);
  setTimeout(printNow, 1000);
}());
```

```javascript

```

```javascript

```