170814

# Js DOM(Document Object Model)

## 1. DOM(Document Object Model)
- 브라우저는 웹 문서(HTML, XML, SVG)를 로드하고 파싱하여 DOM(문서 객체 모델)을 생성한다.
  - 브라우저 동작 원리
![브라우저 동작 원리](../images/client-server.png)

- DOM이란? 
  - 브라우저의 렌더링 엔진은 웹 문서를 로드하고 파싱하여 웹 문서를 `브라우저가 이해할 수 있는 구조로 구성하여 메모리에 적재하는 것을 나타낸다.`
  - 모든 요소와 요소의 어트리뷰트, 텍스트를 각각의 객체로 만들고 이들 `객체를 부자 관계를 표현할 수 있는 트리 구조로 구성`한 것이 DOM이다
  - DOM은 자바스크립트를 통해 동적으로 변경할 수 있으며 변경된 DOM은 렌더링에 반영된다.

- DOM API(Application Programming Interface)이란?
  - 웹 문서의 동적 변경을 위해 DOM은 프로그래밍 언어가 자신에 접근하고 수정할 수 있는 방법을 제공하는데 일반적으로 프로퍼티와 메소드를 갖는 JavaScript 객체로 제공된다.
  - 정적인 웹페이지에 접근하여 동적으로 웹페이지를 변경하기 위한 유일한 방법은 메모리 상에 존재하는 DOM을 변경하는 것이고, 이때 필요한 것이 `DOM에 접근하고 변경하는 프로퍼티와 메소드의 집합인 DOM API이다.`

- DOM의 2가지 기능
  - `HTML 문서에 대한 모델 구성` : 브라우저는 HTML 문서를 로드한 후 해당 문서에 대한 모델을 메모리에 생성한다. 이때 모델은 객체의 트리로 구성되는데 이것을 `DOM tree`라 한다.
  - `HTML 문서 내의 각 요소에 접근 / 수정` : DOM은 모델 내의 각 객체에 접근하고 수정할 수 있는 프로퍼티와 메소드를 제공한다. DOM이 수정되면 브라우저를 통해 사용자가 보게 될 내용 또한 변경된다.

## 2. DOM tree
- DOM tree는 브라우저가 HTML 문서를 로드한 후 생성하는 모델을 의미하는데 객체의 트리로 구조화되어 있기 때문에 DOM tree라 부른다.

```javascript
<!DOCTYPE html>
<html>
  <head>
    <style>
      .red  { color: #ff0000; }
      .blue { color: #0000ff; }
    </style>
  </head>
  <body>
    <div>
      <h1>Cities</h1>
      <ul>
        <li id="one" class="red">Seoul</li>
        <li id="two" class="red">London</li>
        <li id="three" class="red">Newyork</li>
        <li id="four">Tokyo</li>
      </ul>
    </div>
  </body>
</html>
```
  - DOM tree
![DOM tree](../images/dom-tree.png)

- DOM에서 모든 요소, 어트리뷰트, 텍스트는 하나의 객체이며 Document 객체의 자식이다.

- DOM tree의 4가지 노드
  - `문서 노드(Document Node)` : 트리의 최상위에 존재하며 각각 요소, 어트리뷰트, 텍스트 노드에 접근하려면 문서 노드를 통해야 한다. 즉 DOM tree에 접근하기 위한 `시작점(entry point)`이다.

  - `요소 노드(Element Node)` : 요소 노드는 `HTML` 요소를 표현한다. HTML 요소는 중첩에 의해 `부자 관계를 가지며` 이 부자 관계를 통해 정보를 구조화한다. 따라서 `요소 노드는 문서의 구조를 서술한다`고 말 할 수 있다. 어트리뷰트, 텍스트 노드에 접근하려면 먼저 요소 노드를 찾아 접근해야 한다. 모든 요소 노드는 요소별 특성을 표현하기 위해 HTMLElement 객체를 상속한 객체로 구성된다. (그림: DOM tree의 세부 구성 참고)

  - `어트리뷰트 노드(Attribute Node)` : 어트리뷰트 노드는 HTML 요소의 어트리뷰트를 표현한다. 어트리뷰트 노드는 해당 어트리뷰트가 지정된 요소의 자식이 아니라 해당 요소의 일부로 표현된다. 따라서 해당 요소 노드를 찾아 접근하면 어트리뷰트를 참조, 수정할 수 있다.

  - `텍스트 노드(Text Node)` : 텍스트 노드는 HTML 요소의 텍스트를 표현한다. 텍스트 노드는 요소 노드의 자식이며 자신의 자식 노드를 가질 수 없다. 즉 `텍스트 노드는 DOM tree의 최종단이다.`

> 모든 요소는 attribute, text가 올 수 도있고 안올 수 도있다. DOM tree에서 요소노드와 어트리뷰트노드는 형제이며 텍스트노드는 자식이다.

- DOM tree의 객체 구성
![DOM tree의 객체 구성](../images/HTMLElement.png)

- DOM을 통해 웹페이지를 조작(manipulate)하기 위해서는 다음과 같은 수순이 필요하다.
  - 조작하고자하는 요소를 선택 또는 탐색한다.
  - 선택된 요소의 콘텐츠 또는 어트리뷰트를 조작한다.
- JavaScript는 이것에 필요한 수단(API)을 제공한다.

## 3. DOM Query / Traversing(요소에의 접근)

### 3.1 하나의 요소 노드 선택(DOM Query)

- `document.getElementById(id)`
  - 요소의 id 어트리뷰트 값으로 해당 요소를 선택한다. 복수개가 선택된 경우, 첫번째 요소만 반환한다.
  - Return: HTMLElement를 상속받은 객체
  - 모든 브라우저에서 동작

```javascript
// id로 하나의 요소를 선택한다.
var elem = document.getElementById('one');
// 클래스 어트리뷰트의 값을 변경한다.
elem.className = 'blue';

// 그림: DOM tree의 세부 구성 참고
console.log(elem.__proto__);           // HTMLLIElement
console.log(elem.__proto__.__proto__); // HTMLElement
console.log(elem.__proto__.__proto__.__proto__);           // Element
console.log(elem.__proto__.__proto__.__proto__.__proto__); // Node

```

> onfocus focus가 들어가면 지정한 함수를 한다.

- `document.querySelector(cssSelector)`
  - CSS 셀렉터를 이용해 요소를 선택한다. 복수개가 선택된 경우, 첫번째 요소만 반환한다.
  - Return: HTMLElement를 상속받은 객체
  - IE8 이상의 브라우저에서 동작

```javascript
// CSS 셀렉터를 이용해 요소를 선택한다
var elem = document.querySelector('li.red');
// 클래스 어트리뷰트의 값을 변경한다.
elem.className = 'blue';
```

### 3.2 여러개의 요소 노드 선택(DOM Query)
- `document.getElementsByClassName(class)`
  - 지정된 class를 가지는 요소를 모두 선택한다. 공백으로 구분하여 여러개의 class를 지정할 수 있다.
  - Return: HTMLCollection (live)
  - IE9 이상의 브라우저에서 동작

```javascript
// HTMLCollection을 반환한다.
var elems = document.getElementsByClassName('red'), i;

for (i = 0; i < elems.length; i++) {
  // 클래스 어트리뷰트의 값을 변경한다.
  elems[i].className = 'blue';
}
```

- 위 예제를 실행해 보면 예상대로 동작하지 않는다. (두번째 요소만 클래스 변경이 되지 않는다.)

- getElementsByClassName 메소드의 반환값은 `HTMLCollection`이다. 이것은 반환값이 복수인 경우, HTMLElement의 리스트를 담아 반환하기 위한 객체로 배열과 비슷한 사용법을 가지고 있지만 배열은 아닌 `유사배열(array-like object)`이다. 
- HTMLCollection은 `실시간으로 Node의 상태 변경을 반영한다. (live HTMLCollection)`

- 위 예제가 예상대로 동작하지 않은 이유를 알아보자.
  - 1.i가 0일때, elems의 첫 요소(li#one.red)의 class 어트리뷰트 값이 className 프로퍼티에 의해 red에서 blue로 변경된다. 이때 첫째 요소는 class명이 변경됨으로 제외된다.(실시간으로 Node의 상태 변경을 반영한다.)
  
  - 2.i가 1일때, elems에서 첫째 요소는 제거되었으므로 elems[1]은 3번째 요소(li#three.red)가 된다. li#three.red의 class 어트리뷰트 값이 blue로 변경되고 마찬가지로 HTMLCollection에서 제외된다.

  - 3.i가 2일때, HTMLCOllection의 1,3번째 요소가 실시간으로 제거되었으므로 2번째 요소(li#two.red)만 남았다. elems[2]는 undefined이다.

- 해결책1. 반복문을 역방향으로 돌린다.

```javascript
var elems = document.getElementsByClassName('red'), i;
for (i = elems.length - 1; i >= 0; i--) {
  elems[i].className = 'blue';
}
```
- 해결책2. while 반복문을 사용한다. 이때 elems에 요소가 남아 있지 않을 때까지 무한반복하기 위해 index는 0으로 고정시킨다.

```javascript
var elems = document.getElementsByClassName('red');
var i = 0;
while (elems.length > i) { // elems에 요소가 남아 있지 않을 때까지 무한반복
  elems[i].className = 'blue';
  // i++;
}
```

- 해결책3. `HTMLCollection을 배열로 변경한다.`

```javascript
var elems = document.getElementsByClassName('red'), i;

// 유사배열을 배열로 변환
var arr = [].slice.call(elems);

console.log(arr); 
// [li#one.red, li#two.red, li#three.red]
// 각 요소는 HTMLLIElement

for (i = 0; arr.length > 0; i++) {
  arr[i].className = 'blue';
}
```

- 해결책4. querySelectorAll 메소드를 사용하여 non-live NodeList를 반환하게 한다.

```javascript
// Nodelist(non-live)를 반환한다. IE8+
var elems = document.querySelectorAll('.red'), i;
for (i = 0; i < elems.length; i++) {
  elems[i].className = 'blue';
}
```

- 해결책5. document.getElementsByTagName(tagName)
  - 지정된 태그명을 가지는 요소를 모두 선택한다.
  - Return: HTMLCollection (live)
  - 모든 브라우저에서 동작

```javascript
// HTMLCollection을 반환한다.
var elems = document.getElementsByTagName('li'), i;
for (i = 0; i < elems.length; i++) {
  elems[i].className = 'blue';
}
```

> Q. getElementByTagName도 live이면 유사배열 아닌가요?? 에러가나야하지 않나요?
A. Tag가 변경될일이 없기때문에 에러가나지 않는다.

- `document.querySelectorAll(selector)`
  - 지정된 CSS 선택자와 일치하는 요소를 모두 선택한다.
  - Return: NodeList (non-live)
  - IE8 이상의 브라우저에서 동작

```javascript
// Nodelist를 반환한다.
var elems = document.querySelectorAll('li.red'), i;
for (i = 0; i < elems.length; i++) {
  elems[i].className = 'blue'; // color는 상속이되니 li도 blue를 가진다.
}
```

### 3.3 DOM Traversing(탐색)
![탐색](../images/traversing.png)

- `parentNode`
  - 부모 요소를 탐색한다.
  - Return: HTMLElement를 상속받은 객체
  - 모든 브라우저에서 동작

```javascript
var elem = document.getElementById('two');
var parentNode = elem.parentNode;
parentNode.className = 'blue';
```

- `firstChild, lastChild`
  - 자식 요소를 탐색한다.
  - Return: HTMLElement를 상속받은 객체
  - IE9 이상의 브라우저에서 동작
  - 권장하지 않는다. `공백이나 줄바꿈 문자를 텍스트 노드로 취급하기 때문이다.`

```javascript
var elem = document.getElementsByTagName('ul')[0];

// first Child
elem.firstChild.className = 'blue';
// last Child
elem.lastChild.className = 'blue';
```
- 위 예제를 실행해 보면 예상대로 동작하지 않는다. 그 이유는 IE를 제외한 대부분의 브라우저들은 요소 사이의 공백 또는 줄바꿈 문자를 텍스트 노드로 취급하기 때문이다. 이것을 회피하기 위해서는 HTML에 공백을 제거하거나 `jQuery: .prev`()와 `jQuery: .next()`를 사용한다.

```javascript
<ul><li
  id='one' class='red'>Seoul</li><li
  id='two' class='red'>London</li><li
  id='three' class='red'>Newyork</li><li
  id='four'>Tokyo</li></ul>
```

- `hasChildNodes()`
  - 자식 노드가 있는지 확인하고 Boolean 값을 반환한다.
  - Return: Boolean 값
  - 모든 브라우저에서 동작

- `childNodes`
  - 자식 노드의 컬렉션을 반환한다.
  - Return: NodeList (non-live)
  - 모든 브라우저에서 동작

```javascript
var elem = document.querySelector('ul');
console.log(elem); // ul

if (elem.hasChildNodes()) {
  console.log(elem.childNodes);
  // [text, li#one.red, text, li#two.red, text, li#three.red, text, li#four, text] text는 공백을 나타낸다.
  elem.childNodes[1].className = 'blue';
}
```

- `previousSibling, nextSibling`
  - 형제 요소를 탐색한다.
  - Return: HTMLElement를 상속받은 객체
  - IE9 이상의 브라우저에서 동작

```javascript
var elem = document.getElementsByTagName('ul')[0];

// first Child
elem.firstChild.className = 'blue';
// 2nd Child
elem.firstChild.nextSibling.className = 'blue';
// 3rd Child
elem.lastChild.previousSibling.className = 'blue';
// last Child
elem.lastChild.className = 'blue';
```


## 4. DOM Manipulation (조작)

### 4.1 텍스트 노드에의 접근/수정
- 요소의 텍스트는 텍스트 노드에 저장되어 있다. 텍스트 노드에 접근하려면 아래와 같은 수순이 필요하다.

  - 1.해당 텍스트 노드의 부모 요소 노드를 선택한다. 텍스트 노드는 요소 노드의 자식이다.
  - 2.firstChild 프로퍼티를 사용하여 텍스트 노드를 탐색한다.
  - 3.텍스트 노드의 유일한 프로퍼티(`nodeValue`)를 이용하여 텍스트를 취득한다.
  - 4.`nodeValue`를 이용하여 텍스트를 수정한다.

- `nodeValue`
  - 노드의 값을 반환한다.
  - Return: 문자열
  - IE6 이상의 브라우저에서 동작한다.


```javascript
// 해당 텍스트 노드의 부모 요소 노드를 선택한다.
var one = document.getElementById('one');
console.dir(one); // HTMLLIElement: li#one.red

// firstChild 프로퍼티를 사용하여 텍스트 노드를 탐색한다.
var textNode = one.firstChild;

// nodeValue 프로퍼티를 사용하여 노드의 값을 취득한다.
console.log(textNode.nodeValue); // Seoul

// nodeValue 프로퍼티를 이용하여 텍스트를 수정한다.
textNode.nodeValue = 'Pusan';
```
- nodeName, nodeType을 통해 노드의 정보를 취득할 수 있다.

### 4.2 어트리뷰트 노드에의 접근/수정

- `className`
  - `class 어트리뷰트의 값을 취득 또는 변경한다`. class 어트리뷰트가 존재하지 않으면 class 어트리뷰트를 생성하고 지정된 값을 설정한다. class 어트리뷰트의 값이 여러개일 경우, 공백으로 구분된 문자열이 반환되므로 String 메소드 `split(' ')`를 사용하여 배열로 변경하여 사용한다.
  - 모든 브라우저에서 동작한다.

```javascript
var elems = document.getElementsByTagName('li');

for (var i = elems.length - 1; i >= 0; i--) {
  // class 어트리뷰트의 값을 취득하여 확인
  if (elems[i].className === 'red') {
    // class 어트리뷰트의 값을 변경한다.
    elems[i].className = 'blue';
  } else {
    // class 어트리뷰트의 값을 변경한다.
    elems[i].className = 'red';
  }
}
```

- `id`
  - id 어트리뷰트의 값을 취득 또는 변경한다. id 어트리뷰트가 존재하지 않으면 id 어트리뷰트를 생성하고 지정된 값을 설정한다.
  - 모든 브라우저에서 동작한다.

```javascript
// h1 태그 요소 중 첫번째 요소를 취득
var heading = document.getElementsByTagName('h1')[0];
console.dir(heading); // HTMLHeadingElement: h1
console.log(heading.firstChild.nodeValue); // Cities

// id 어트리뷰트의 값을 변경
heading.id = 'heading';
console.log(heading.id); // heading

```
- `hasAttribute()`
  - 지정한 어트리뷰트를 가지고 있는지 검사한다.
  - Return : Boolean
  - IE8 이상의 브라우저에서 동작한다.

- `getAttribute()`
  - 어트리뷰트의 값을 취득한다.
  - Return : 문자열
  - 모든 브라우저에서 동작한다.

- `setAttribute()`
  - 어트리뷰트와 어트리뷰트의 값을 설정한다.
  - Return : undefined
  - 모든 브라우저에서 동작한다.

- `removeAttribute()`
  - 지정한 어트리뷰트를 제거한다.
  - Return : undefined
  - 모든 브라우저에서 동작한다.

```javascript
var four = document.getElementById('four');

// four에 class 어트리뷰트가 존재하지 않으면
if (!four.hasAttribute('class')) {
  // four에 name 어트리뷰트를 추가하고 값으로 'user'를 설정
  four.setAttribute('class', 'blue');
} else { // four에 class 어트리뷰트가 존재하면
  four.className = 'blue';
}

// four에 lang 어트리뷰트의 값을 취득
console.log(four.getAttribute('class')); // blue

// four에서 name 어트리뷰트를 제거
four.removeAttribute('class');

// inputUser에서 name 어트리뷰트의 존재를 확인
console.log(four.hasAttribute('class')); // false
```


### 4.3 HTML 콘텐츠 조작(Manipulation)
- HTML 콘텐츠를 조작(Manipulation)하기 위해 아래의 프로퍼티 또는 메소드를 사용할 수 있다. 
- 마크업이 포함된 콘텐츠를 추가하는 행위는 `크로스 스크립팅 공격(XSS: Cross-Site Scripting Attacks)`에 취약하므로 주의가 필요하다.
- content가 문자열로 이루어져있을때만 사용한다.

- `textContent`
  - 요소의 텍스트 콘텐츠를 취득 또는 변경한다. 이때 마크업은 무시된다. textContent를 통해 요소에 새로운 텍스트를 할당하면 텍스트를 변경할 수 있다. 이때 `순수한 텍스트만 지정해야 하며 마크업을 포함시키면 문자열로 인식되어 그대로 출력된다.`
  - IE9 이상의 브라우저에서 동작한다.

```javascript
var ul = document.getElementsByTagName('ul')[0];

// 요소의 텍스트 취득
console.log(ul.textContent);
// IE를 제외한 대부분의 브라우저들은 요소 사이의 공백 또는 줄바꿈 문자를 텍스트 노드로 취급한다
/*
        Seoul
        London
        Newyork
        Tokyo
*/

var one = document.getElementById('one');

// 요소의 텍스트 취득
console.log(one.textContent); // Seoul

// 요소의 텍스트 변경
one.textContent += ', Korea';

console.log(one.textContent); // Seoul, Korea

// 요소의 마크업이 포함된 콘텐츠 변경.
one.textContent = '<h1>Heading</h1>';

// 마크업이 문자열로 표시된다.
console.log(one.textContent); // <h1>Heading</h1>
```

- `innerText`
  - innerText 프로퍼티를 사용하여도 요소의 텍스트 콘텐츠에만 접근할 수 있다. 하지만 아래의 이유로 사용하지 않는 것이 좋다.
    - 비표준이다.
    - CSS에 순종적이다. 예를 들어 CSS에 의해 비표시(visibility: hidden;)로 지정되어 있다면 텍스트가 반환되지 않는다.
    - CSS를 고려해야 하므로 textContent 프로퍼티보다 느리다
- `innerHTML`
  - innerHTML 프로퍼티를 사용하면 해당 요소의 모든 자식 요소를 포함하는 `모든 콘텐츠를 하나의 문자열로 취득할 수 있다. 이 문자열은 마크업을 포함한다.`

```javascript
var ul = document.getElementsByTagName('ul')[0];

// innerHTML 프로퍼티는 모든 자식 요소를 포함하는 모든 콘텐츠를 하나의 문자열로 취득할 수 있다. 이 문자열은 마크업을 포함한다.
console.log(ul.innerHTML);
// IE를 제외한 대부분의 브라우저들은 요소 사이의 공백 또는 줄바꿈 문자를 텍스트 노드로 취급한다
/*
        <li id="one" class="red">Seoul</li>
        <li id="two" class="red">London</li>
        <li id="three" class="red">Newyork</li>
        <li id="four">Tokyo</li>
*/

```
- innerHTML 프로퍼티를 사용하여 마크업이 포함된 새로운 콘텐츠를 지정하면 새로운 요소를 DOM에 추가할 수 있다.

```javascript
var one = document.getElementById('one');

// 마크업이 포함된 콘텐츠 취득
console.log(one.innerHTML); // Seoul

// 마크업이 포함된 콘텐츠 변경
one.innerHTML += '<em class="blue">, Korea</em>';

// 마크업이 포함된 콘텐츠 취득
console.log(one.innerHTML); // Seoul <em class="blue">, Korea</em>
```

- 위와 같이 마크업이 포함된 콘텐츠를 추가하는 것은 `크로스 스크립팅 공격(XSS: Cross-Site Scripting Attacks)에 취약`하다.

```javascript
// 크로스 스크립팅 공격 사례

// 스크립트 태그를 추가하여 자바스크립트가 실행되도록 한다.
// HTML5에서 innserHTML로 삽입된 <script> 코드는 실행되지 않는다.
// 크롬, 파이어폭스 등의 브라우저나 최신 브라우저 환경에서는 작동하지 않을 수도 있다.
elem.innerHTML = '<script>alert("XSS!")</script>';

// 에러 이벤트를 발생시켜 스크립트가 실행되도록 한다.
one.innerHTML = '<img src="#" onerror="alert('XSS')">';
```

### 4.4 DOM 조작 방식

- innerHTML 프로퍼티를 사용하지 않고 새로운 콘텐츠를 추가할 수 있는 방법은 DOM을 직접 조작하는 것이다. 한개의 요소를 추가하는 경우 사용한다. 이 방법은 다음의 수순에 따라 진행한다.

  - 1.요소 노드 생성
  createElement() 메소드를 사용하여 새로운 요소 노드를 생성한다. createElement() 메소드의 인자으로 태그 이름을 전달한다.
  - 2.텍스트 노드 생성
  createTextNode() 메소드를 사용하여 새로운 텍스트 노드를 생성한다. 경우에 따라 생략될 수 있지만 생략하는 경우, 콘텐츠가 비어 있는 요소가 된다.
  - 3.생성된 요소를 DOM에 추가
  appendChild() 메소드를 사용하여 생성된 노드를 DOM tree에 추가한다. 또는 removeChild() 네서드를 사용하여 DOM tree에서 노드를 삭제할 수도 있다.

- `createElement(tagName)`
  - 태그이름을 인자로 전달하여 요소를 생성한다.
  - Return: HTMLElement를 상속받은 객체
  - 모든 브라우저에서 동작한다.

- `createTextNode(text)`
  - 텍스트를 인자로 전달하여 텍스트 노드를 생성한다.
  - Return: Text 객체
  - 모든 브라우저에서 동작한다.

- `appendChild(Node)`
  - 인자로 전달한 노드를 자식 요소로 DOM 트리에 추가한다.
  - Return: 추가한 노드
  - 모든 브라우저에서 동작한다.

- `removeChild(Node)`
  - 인자로 전달한 노드를 DOM 트리에 제거한다.
  - Return: 추가한 노드
  - 모든 브라우저에서 동작한다.

```javascript
// 태그이름을 인자로 전달하여 요소를 생성
var newElem = document.createElement('li');
// var newElem = document.createElement('<li>test</li>');
// Uncaught DOMException: Failed to execute 'createElement' on 'Document': The tag name provided ('<li>test</li>') is not a valid name.

// 텍스트 노드를 생성
var newText = document.createTextNode('Beijing');

// 텍스트 노드를 newElem 자식으로 DOM 트리에 추가
newElem.appendChild(newText);

var container = document.getElementsByTagName('ul')[0];

// newElem을 container의 자식으로 DOM 트리에 추가
container.appendChild(newElem);

var removeElem = document.getElementById('one');

// container의 자식인 removeElem 요소를 DOM 트리에 제거한다.
container.removeChild(removeElem);
```

### 4.5 insertAdjacentHTML()

- `insertAdjacentHTML()`
  - 인자로 전달한 텍스트를 HTML로 파싱하고 그 결과로 생성된 노드를 DOM 트리의 지정된 위치에 삽입한다. 첫번째 인자는 삽입 위치, 두번째 인자는 삽입할 요소를 표현한 문자열이다. 첫번째 인자로 올 수 있는 값은 아래와 같다.
    - ‘beforebegin’
    - ‘afterbegin’
    - ‘beforeend’
    - ‘afterend’
  - 모든 브라우저에서 동작한다.
  
  ![insertAdjacentHTML 메소드의 position 파라미터](../images/insertAdjacentHTML-position.png)

```javascript
var one = document.getElementById('one');

// 마크업이 포함된 요소 추가
one.insertAdjacentHTML('beforeend', '<em class="blue">, Korea</em>');

```

### 4.6 innerHTML vs. DOM 조작 방식 vs. insertAdjacentHTML()

- `innerHTML`
  - 장점 
    - DOM 조작 방식에 비해 빠르고 간편하다. 
    - 간편하게 문자열로 정의 여러 요소를 DOM에 추가할 수 있다. 해당 요소의 내용을 덮어 쓴다. 즉 HTML을 로드하고 다시 파싱한다. 이것은 비효율적이다.
    - 콘텐츠를 취득할 수 있다.
  - 단점
    - XSS공격에 취약점이 있기 때문에 사용자로 부터 입력받은 콘텐츠(untrusted data: 댓글, 사용자 이름등)를 추가할 때 사용해서는 않된다.

- `DOM 조작 방식`
  - 장점 
    - 특정 노드 한개(노드, 텍스트, 데이터 등)를 DOM에 추가할 때 적합하다.
  - 단점
    - innerHTML보다 느리고 더 많은 코드가 필요하다.

- `insertAdjacentHTML()`
  - 장점 
    - 간편하게 문자열로 정의된 여러 요소를 DOM에 추가할 수 있다.
    - 삽입되는 위치를 선정할 수 있다.
  - 단점
    - XSS공격에 취약점이 있기 때문에 사용자로 부터 입력받은 콘텐츠(untrusted data: 댓글, 사용자 이름등)를 추가할 때 사용해서는 않된다.

- `결론`
  - innerHTML과 insertAdjacentHTML()은 크로스 스크립팅 공격(XSS: Cross-Site Scripting Attacks)에 취약하다. 따라서 `untrusted data의 경우, 주의하여야 한다. 텍스트를 추가 또는 변경시에는 textContent`, `새로운 요소의 추가 또는 삭제시에는 DOM 조작 방식을 사용하도록 한다.`


## 5. style
- style 프로퍼티를 사용하면 inline 스타일 선언을 생성한다. 특정 요소에 inline 스타일을 지정하는 경우 사용한다.

```javascript
var four = document.getElementById('four');

// inline 스타일 선언을 생성
four.style.color = 'blue';

// font-size와 같이 '-'으로 구분되는 프로퍼티는 카멜케이스로 변환하여 사용한다.
four.style.fontSize = '2em';
```
