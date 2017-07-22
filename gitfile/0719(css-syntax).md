170719

#CSS-Syntax
- CSS는 HTML요소의 style을 표현한다.

## 1.Selector(선택자)
- styling하려는 요소를 선택한다.
- 태그명, id(#), class(.) 명으로 가져올 수 있다.

## 2. Property(속성)
- ;를 사용하여 여러개의 property를 지정할 수 있다.

## 3. Value(속성 값)
- property에 따라서 특정 값을 입력할 수 있다.

## 4. HTML과 CSS의 연동
- Rendering Engine이란?? HTML file을 읽는 능력이 있어야한다.<순차적으로 읽는다.>
Html file 읽히는 도중에 CSS file을 서버에서 loading한다.
HTML file 읽히는 도중에 JavaScript file도 읽는다 단! Js Engine으로 읽는다. 
한줄 씩 읽는 것을 parsing 이라고 하며 그 기계를 parser라고하며 Rendering Engine안에 parser, loader가 존재한다.  
Html 이 parsing을 하면 DOM이 컴퓨터의 메모리에 올라가 있는다. 
Css 이 parsing을 하면 CSSOM이 컴퓨터의 메모리에 올라가 있는다.   
결과론 적으로는 DOM + CSSOM = Render Tree가 생성된다.

[browser 동작원리](http://d2.naver.com/helloworld/59361)


### 4,1 Link style
- HTML에서 외부에 있는 CSS 파일을 로드하는 방식이다.
  - ```<link rel="stylesheet" href="css/style.css">```

### 4.2 Embedding style
- style tag 안에다가 입력하는 방식이다.

### 4.3 Inline style
- HTML 요소의 style property에 css를 기술하는 방식이다. 
> Link style을 사용하는 것이 좋다.

## 5. Reset CSS 사용하기

- 기본적인 HTML 요소의 CSS를 초기화하는 용도로 사용한다.

- bootstrap등의 framework를 사용하면 Reset CSS를 사용하지 않아도 된다.  

[Reset CSS](http://meyerweb.com/eric/tools/css/reset/)
 
## 6. CSS Version
- CSS1 : 1996, CSS2 : 1998, CSS3 : 2005

