170814

# Js Asynchronous processing model

## 1. 브라우저의 동작 원리


## 2. Ajax
- server에서 ajax를 통해서 데이터를 던지면 그것을 client가 받는 방식을 나타낸다.
- 전통적으로는 새로운 HTML을 불러와서 load부터 다시한다.
- 현재는 DOM Manipulation(조작)을 통하여서 ajax 통신을 한다.
  - 서버가 존재해야한다.


## 3. 동기식 처리 모델 vs 비동기식 처리 모델
- 동기식 : 커피를 주문하고 커피가 나올때까지 대기한다.
  - 직렬적으로 작업을 수행한다 즉 순차적으로 실행되며 작업이 수행중이면 다음 작업은 대기하게 된다.
  - `Blocking방식이다.`

- 비동기식 : 커피를 주문하고 할일을 하고 있다가 커피를 받는다.
  - 병렬적으로 작업을 수행한다  즉 작업이 종료되지 않은 상태라도 대기하지 않고 다음 작업을 실행한다는 의미이다.
  - `Non-Blocking방식이다.`

```javascript
function func1() {
  console.log('func1');
  func2();
}

function func2() {
  setTimeout(function() {
    console.log('func2');
  }, 0);

  func3();
}

function func3() {
  console.log('func3');
}

func1();
```

> setTimeout을 서버에 요청을 하고 바로 func3를 실행하기에 func1, func3, func2순서로 나온다. setTimeout은 모든 동기식이 실행된 후에 실행된다.

## 4. 이벤트 루프와 동시성(Concurrency)
- 브라우저는 `단일 쓰레드(single-thread)`에서 `이벤트 드리븐(event-driven)` 방식으로 동작한다.

- 자바스크립트의 동시성(Concurrency)을 지원하는 것이 바로 `이벤트 루프(Event Loop)`이다.

- `js는 비동기를 못하지만 그것을 browser가 한다.`

> thread란 컴퓨터가 일을 할때 한번에 일을 할 수 있는 정도를 나타낸다.

> 이벤트 드리븐(event-driven) 방식이란? 모든 application이 이벤트 방식으로 동작한다.

  - 이벤트루프와 브라우저의 환경  
![이벤트루프와 브라우저의 환경](../images/event-loop.png)

  - Web API는 browser의 영역으로써 Ajax, DOM Events, Timer등이 있다.

- 구글의 V8을 비롯한 대부분의 자바스크립트 엔진은 크게 2개의 영역으로 나뉜다.
  - Call Stack(호출 스택) == 실행 컨텍스트
    - 작업이 요청되면(함수가 실행되면) 요청된 작업은 순차적으로 Call Stack에 쌓이게 되고 순차적으로 실행된다. 자바스크립트는 단 하나의 Call Stack을 사용하기 때문에 해당 task가 종료하기 전까지는 다른 어떤 task도 수행될 수 없다.
  - Heap
    - 동적으로 생성된 객체 인스턴스가 할당되는 영역이다.

-  자바스크립트 엔진은 단순히 작업이 요청되면 요청된 작업을 Call Stack을 사용하여 순차적으로 실행할 뿐이다. 앞에서 언급한 동시성(Concurrency)을 지원하기 위해 필요한 비동기 요청(이벤트를 포함) 처리는 자바스크립트 엔진을 구동하는 환경 `즉 브라우저(또는 Node.js)가 담당한다.`

- Event Queue(Task Queue)
  - 비동기 처리 함수의 콜백 함수, 비동기식 이벤트 핸들러, Timer 함수(setTimeout(), setInterval())가 보관되는 영역으로 이벤트 루프(Event Loop)에 의해 특정 시점(Call Stack이 비어졌을 때)에 순차적으로 Call Stack으로 이동되어 실행된다.
- Event Loop(이벤트 루프)
  - Call Stack내에서 현재 실행중인 task가 있는지 그리고 Event Queue에 task가 있는지 반복하여 확인한다.