# ECMA SCRIPT 6 - PROMISE
## 1. PROMISE & CALLBACK HELL
비동기식 처리모델 
- 장점 
  - 병럴로 처리해 다른 요청이 BLOCKING 되지 않는다.
- 단점
  - CALLBACK HELL : 여러개의 콜백함수가 순서를 보장하기 위해 NESTING 되어 복잡도가 높아지는 것
```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Promise example</title>
</head>
<body>
  <h1>Promise example</h1>
  <script>
    function get(url) {
      // XMLHttpRequest 객체의 생성
      var req = new XMLHttpRequest();
      // 비동기 방식으로 Request를 오픈한다
      req.open('GET', url);
      // Request를 전송한다
      req.send();

      // Event Handler
      req.onreadystatechange = function () {
        // 서버 응답 완료 && 정상 응답
        if (req.readyState === XMLHttpRequest.DONE) {
          if (req.status == 200) {
            console.log(req.response);
            // 비동기 함수는 실행 완료를 기달리지 않고 다음 task를 실행한다. 따라서 비동기 함수 내에서 처리 결과를 return(또는 전역변수에의 할당)하면 기대한 대로 동작하지 않는다.
            return req.response;
            // 비동기 함수의 결과에 대한 처리는 이곳에서 진행하여야 한다.
          } else {
            // 서버의 응답이 정상이 아니면
            console.log(Error(req.statusText));
          }
        }
      };
    }

    var url = 'http://jsonplaceholder.typicode.com/posts/1';

    // get 함수는 비동기 함수이므로 실행 완료를 기달리지 않고 다음 task를 수행한다.
    // 즉, 함수의 실행이 완료하여 함수의 반환값을 받기 이전에 다음 task로 진행된다. 따라서 res는 undefined이다.
    var res = get(url);
    console.log(res); // undefined
  </script>
</body>
</html>
```
> 비동기 함수 내에서 처리결과를 return(또는 전역 변수에 할당)하면 기대한 대로 동작하지 않는다.

- CALLBACK HELL 문제점
  - 가독성이 매우 나쁘게한다.
  - 복잡도를 증가시켜 실수를 유발 시킬 확률이 높아진다.
  - 에러처리가 안된다.
```javascript
try {
  setTimeout(function(){
    throw 'Error!';
  }, 1000);
} catch(e) {
  console.log('에러를 캐치하지 못한다..');
  console.log(e);
}
```
## 3. PROMISE 상태
비동기 처리가 성공하였는지 실패하였는지 등의 상태정보를 갖는다.
- PENDING
  - 비동기 처리가 아직 수행되지 않은 상태
  - RESOLVE 또는 REJECT함수가 아직 호출되지 않은 상태이다.
- FULFILLED
  - 비동기 처리가 수행된 상태(성공)
  - RESOLVE 함수가 호출된 상태
- REJECTED
  - 비동기 처리가 수행된 상태(실패)
  - REJECT 함수가 호출된 상태
- SETTLED
  - 비동기 처리가 수행된 상태(성공 또는 실패)
  - RESOLVED 또는 REJECT 함수가 호출된 상태

### 1. PROMISE 생성
PROMISE 생성자를 통해 인스턴스화한다.
```javascript
var promise = new Promise(function(resolve, reject) {
  // 비동기 작업 수행

  if (/* 비동기 작업 수행 성공 */) {
    resolve('resolved!');
  }
  else { /* 비동기 작업 수행 실패 */
    reject(Error('rejected!'));
  }
});
```
> promise 생성자는 비동기 작업을 수행할 콜백함수를 인자로 전달받는데 이 콜백함수는 resolve 와 reject 콜백함수를 인수로 전달받는다.
- Promise 생성자가 인자로 전달받은 콜백함수는 비동기작업을 수행한다.
- 이때, 비동기 작업이 성공하면 resolve를 호출
- 실패하면 reject호출

### 2. PROMISE 후속처리 함수 THEN, CATCH
PROMISE 생성자가 인자로 전달받은 콜백함수에서 비동기작업을 실행한 예제
```javascript
// 비동기 함수
function asyncFunc(param) {
  // Promise 객체 선언과 반환
  return new Promise(function(resolve, reject) {
    setTimeout(function() { // 비동기 함수
      param ? resolve('resolved!') : reject('rejected!');
    }, 2000);
  });
};
```
- then 
  - 두개의 콜백함수를 인자로 전달받는다.
  - 첫번째 함수는 성공시 호출되는 함수
  - 두번째 함수는 실패시 호출되는 함수
- catch
  - 예외 발생시 호출
```javascript
// 비동기 함수
function asyncFunc(param) {
  // Promise 객체 선언과 반환
  return new Promise(function(resolve, reject) {
    setTimeout(function() { // 비동기 함수
      param ? resolve('resolved!') : reject('rejected!');
    }, 2000);
  });
};

// asyncFunc 함수를 호출하면 Promise 객체를 생성하고 반환한다.
// 인자에 true를 전달 : resolve 메소드 호출
asyncFunc(true)
  .then(function(data) {
    // resolve가 실행된 경우(성공), resolve 함수에 전달된 값이 data에 저장된다
    console.log(data);  // resolved!
  },function(reason) {
    // reject가 실행된 경우(실패), reject 함수에 전달된 값이 reason에 저장된다
    console.log(reason); // rejected!
    throw 'Error:' + reason;
  }).catch(function(error) {
    // 예외 발생 시 호출된다.
    console.error(error);
  });

// asyncFunc 함수를 호출하면 Promise 객체를 생성하고 반환한다.
// 인자에 false를 전달 : reject 메소드 호출
asyncFunc(false)
  .then(function (data) {
    // resolve가 실행된 경우(성공), resolve 함수에 전달된 값이 data에 저장된다
    console.log(data);
  }, function (reason) {
    // reject가 실행된 경우(실패), reject 함수에 전달된 값이 reason에 저장된다
    console.log(reason);
    throw 'Error:' + reason;
  }).catch(function (error) {
    // 예외 발생 시 호출된다.
    console.error(error);
  });
```
- asyncFunc 함수는 함수 내부에서 Promise 객체를 생성하고 반환한다.
- 이 함수를 실행하면 
  - asyncFunc 함수는 Promise 객체를 반환하는데 이 객체를 상태를 갖는다.
  - Promise 객체의 상태에 따라 후속 처리함수를 체이닝 방식을 호출한다.
```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Promise example</title>
</head>
<body>
  <h1>Promise example</h1>
  <script>
    function get(url) {
      // promise 생성과 반환
      return new Promise(function (resolve, reject) {
        // XMLHttpRequest 객체의 생성
        var req = new XMLHttpRequest();
        // 비동기 방식으로 Request를 오픈한다
        req.open('GET', url);
        // Request를 전송한다
        req.send();

        // Event Handler
        req.onreadystatechange = function () {
          // 서버 응답 완료 && 정상 응답
          if (req.readyState === XMLHttpRequest.DONE) {
            if (req.status == 200) {
              // resolve 메소드에 전달한 처리 결과는 then 메소드의 첫번째 콜백함수에서 취득 가능
              resolve(req.response); // then이 캐치
            } else {
              // 서버의 응답이 정상이 아니면
              // reject 메소드에 전달한 처리 결과는 then 메소드의 두번째 콜백함수에서 취득 가능
              reject(req.statusText); //실패 이유
            }
          }
        };
      });
    }

    var url = 'http://jsonplaceholder.typicode.com';

    get(url + '/posts/1')
      .then(function (response) { //데이터가 들어간다.
        console.log('Success 1', response);
        // Ajax 요청 결과에 의해 또 다른 Ajax 요청을 실행한다.
        // Request: /posts?userId=1
        // JSON.parse(): JSON 문자열 => 객체.
        // 반대의 경우 : stringDefine
        console.log(JSON.parse(response).userId);
        
        return get(url + '/posts?userId=' + JSON.parse(response).userId); //promise 객체를 리턴
        // then 메소드의 콜백 함수가 반환하는 값은 자동으로 다음에 오는 then 또는 catch 메소드로 전달된다.
      })
      .then(function (response) {
        // Request: /posts?userId=1의 처리 결과를 수신
        console.log('Success 2', response);
      });
  </script>
</body>
</html>
```
> 위의 코드는 바닐라코드이다. 프레임워크를 사용하면 이러한 부분은 해소 가능하다.
> 앵귤러, 리엑트, 뷰: 대표적 프레임워크