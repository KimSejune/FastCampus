170814

# Js Event

## 1. Introduction

## 2. 동기식 처리 모델 vs 비동기식 처리 모델
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

## 3. 이벤트 루프(Event Loop)와 동시성(Concurrency)
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

## 4. 이벤트의 종류

### 4.1 UI Event
- 웹페이지가 로드될때
  - load	웹페이지의 로드가 완료되었을 때
  - unload	웹페이지가 언로드될 때(주로 새로운 페이지를 요청한 경우)
  - error	브라우저가 자바스크립트 오류를 만났거나 요청한 자원이 존재하지 않는 경우
  - resize	브라우저 창의 크기를 조절했을 때
  - scroll	사용자가 페이지를 위아래로 스크롤할 때
  - select	텍스트를 선택했을 때

> script문을 제일 하단에 써줘야하는 이유는 html이 전부다가 load되면 js를 실행하게 하기위해서이다.

### 4.2 Keyboard Event
  - keydown	키를 누르고 있을 때
  - keyup	누르고 있던 키를 뗄 때
  - keypress 키를 누르고 뗏을 때

### 4.3 Mouse Event
  - click	마우스 버튼을 클릭했을 때
  - dbclick	마우스 버튼을 더블 클릭했을 때
  - mousedown	마우스 버튼을 누르고 있을 때
  - mouseup	누르고 있던 마우스 버튼을 뗄 때
  - mousemove	마우스를 움직일 때 (터치스크린에서 동작하지 않는다)
  - mouseover	마우스를 요소 위로 움직였를 때 (터치스크린에서 동작하지 않는다) // hover와 비슷
  - mouseout	마우스를 요소 밖으로 움직였를 때 (터치스크린에서 동작하지 않는다)

### 4.4 Focus Event
  - focus/focusin	요소가 포커스를 얻었을 때
  - blur/foucusout	요소가 포커스를 잃었을 때


### 4.5 Form Event
  - input	input 또는 textarea 요소의 값이 변경되었을 때, contenteditable 어트리뷰트를 가진 요소의 값이 변경되었을 때
  - change	select box, checkbox, radio button의 상태가 변경되었을 때
  - submit	form을 submit할 때 (버튼 또는 키)
  - reset	reset 버튼을 클릭할 때 (최근에는 사용 안함)

### 4.6 Clipboard Event
  - cut	콘텐츠를 잘라내기할 때
  - copy	콘텐츠를 복사할 때
  - paste	콘텐츠를 붙여넣기할 때

## 5. Event Binding

### 5.1 HTML Event Handler
- HTML 요소의 이벤트 어트리뷰트에 이벤트 핸들러를 대응시키는 방법이다.
  - 자주 사용되지 않는다.

```html
<!DOCTYPE html>
<html>
<body>
  <button onclick="myFunction()">Click me</button>
  <script>
    function myFunction() {
      alert('Button clicked!');
    }
  </script>
</body>
</html>
```

### 5.2 전통적(Traditional) DOM Event Handler
- HTML Event Handler처럼 HTML과 Javascript가 혼용되는 문제는 해결되었으나 이벤트 핸들러에 하나의 함수만을 바인딩할 수 있으며 `함수에 인수를 전달할 수 없는 단점이 있다.`
- 추천하는 방식이 아니다. EventHandler방식을 사용한다.

```html
<!DOCTYPE html>
<html>
<body>
  <button id="btn">Click me</button>
  <script>
    var btn = document.getElementById('btn');

    // 첫번째 바인딩된 이벤트 핸들러 => 실행되지 않는다.
    btn.onclick = function () {
      alert('Button clicked 1');
    };

    // 두번째 바인딩된 이벤트 핸들러
    btn.onclick = function () {
      alert('Button clicked 2');
    };

    // 첫번째 바인딩된 이벤트 핸들러 !!! 이것을 추천한다.
    btn.addEventListener('click', function () {
      alert('Button clicked 1');
    });

    // 두번째 바인딩된 이벤트 핸들러
    btn.addEventListener('click', function () {
      alert('Button clicked 2');
    });
  </script>
</body>
</html>

```
### 5.3 DOM Level 2 Event Listener(최근 트렌드)
- addEventListener() 함수를 이용하여 대상 요소에 이벤트를 바인딩하고 해당 이벤트가 발생했을 때 실행될 콜백 함수를 지정한다.  

![Event Listener](../images/event_listener.png)
  - Bubbling은 event를 발생한 곳에서부터 위로 올라가는 방식이다.
  - capturing은 처음부터 아래로 내려오는 방식이다.

- addEventListener()는 이전에 방식에 비해 보다 나은 장점을 갖는다.
  -하나의 이벤트에 대해 하나 이상의 핸들러를 추가할 수 있다.
  -캡처링과 버블링를 지원한다.
  - HTML 요소뿐만아니라 모든 DOM 요소에 대해 동작한다.

- `addEventListener()` 함수는 IE9 이상에서 동작한다. IE 8 이하에서는 `attachEvent()` 함수를 사용한다.

- IE 버전에 대한 방어코드이다.
```javascript
if (elem.addEventListener) {    // IE 9 ~
  elem.addEventListener('click', func); 
} else if (elem.attachEvent) {  // ~ IE 8
  elem.attachEvent('onclick', func);
}
```

- addEventListener()의 사용 예제를 살펴보자.

```html
<!DOCTYPE html>
<html>
<body>
  <script>
    addEventListener('click', function() {
      alert('Clicked!');
    });
  </script>
</body>
</html>
```
- 위와 같이 대상요소(target)를 지정하지 않으면 click 이벤트는 전역객체 window에 바인딩된다.


```html

```