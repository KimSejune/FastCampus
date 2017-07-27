170725

# CSS3 Responsive Web Design

- 문제점1 : 화면폭을 좁히면 아래 그림과 같이 화면이 망가지는데 이것는 HTML 요소에 고정폭을 지정하여 가로 스크롤을 발생시키지 않으면 해결이 어렵다.
- 문제점2: 모바일과 같이 작은 해상도의 디바이스에서 접근했을 때 화면이 너무 작아져 가시성에 문제가 발생한다.

## 1. Responsive web Design 개요
- 사용자가 어떤 디바이스로 웹사이트를 방문할 지 알 수 없다.
- One Source Multi Use를 목적으로 한다.
  - 소스코드 1개로써 모든 디바이스를 대응한다.
- 화면의 크기마다 breakpoint를 설정하여서 그에 맞는 css를 입힌다.  
[ionic](http://ionicframework.com/)  
[Electron](https://electron.atom.io/)  
[PhoneGap](https://phonegap.com/)  
[Sencha Touch](https://www.sencha.com/)

### 1.1 viewport meta tag
- viewport란 웹페이지의 가시영역을 의미한다.
  - 기본적으로 모바일은 resize가 되지 않는다.
- meta tag는 브라우저 혹은 검색엔진최적화를 위해 검색엔진에게 메타데이터를 전달하기 위해 사용된다.
- viewport meta tag는 브라우저의 화면 설정과 관련된 정보를 제공한다.
  - width=device-width, initial-scale=1.0, maximum-scale=2.0, minimum-scale=1.0
```
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

### 1.2 @media
- screen, print에 따라 각각의 style을 지정하는 것을 가능하게 한다.
```
    @media screen {
      * { color: red; }
    }
    @media print {
      * { color: blue; }
    }
```

- 반응형 웹디자인에 사용되는 핵심 기술은 `@media`이다.
- @media를 사용하여 미디어 별로 style을 지정하는 것을 Media Query라 한다. 디바이스를 지정하는 것뿐만 아니라 디바이스의 크기나 비율까지 구분할 수 있다.
- 대부분  `width property` 를 사용한다.
```
@media screen and (min-width: 480px) {
  body {
    background-color: lightgreen;
  }
}
```
> min-width: 480px이 되면 background-color: lightgreen으로 바꿔라.

[media query property](http://poiemaweb.com/css3-responsive-web-design)

- mobile first인경우 min-width, non-mobile first인 경우 max-width를 사용한다. 순서가 중요하다.

> min-width는 작은 수 부터, max-width는 큰 수 부터 작성한다.
```
/*==========  Mobile First Method  ==========*/
/* All Device */

/* Custom, iPhone Retina : 320px ~ */
@media only screen and (min-width : 320px) {

}
/* Extra Small Devices, Phones : 480px ~ */
@media only screen and (min-width : 480px) {

}  
/* Small Devices, Tablets : 768px ~ */
@media only screen and (min-width : 768px) {

}
/* Medium Devices, Desktops : 992px ~ */
@media only screen and (min-width : 992px) {

}
/* Large Devices, Wide Screens : 1200px ~ */
@media only screen and (min-width : 1200px) {

}

/*==========  Non-Mobile First Method  ==========*/
/* All Device */

/* Large Devices, Wide Screens : ~ 1200px */
@media only screen and (max-width : 1200px) {

}
/* Medium Devices, Desktops : ~ 992px */
@media only screen and (max-width : 992px) {

}
/* Small Devices, Tablets : ~ 768px */
@media only screen and (max-width : 768px) {

}
/* Extra Small Devices, Phones : ~ 480px */
@media only screen and (max-width : 480px) {

}
/* Custom, iPhone Retina : ~ 320px */
@media only screen and (max-width : 320px) {

}
```

## 2. Responsive Navigation Bar
- 디바이스 해상도에 따라 반응할 수 있도록 viewport meta tag와 media query를 추가한다.
- 각각의 breakpoint 설정을 잘해두어야한다.

### 2.1 Responsive Navigation Bar - Tablet
- 데스크탑 layout에서 화면이 작아질 때 header navigation bar가 header 영역 아래로 내려오는 현상이 발생하였다. 이를 보완하기 위해 다음과 같이 태블릿에서의 layout을 정의한다.

- header부분의  header-menu 영역을 float: none;으로 설정하여서 밑으로 내려준다.

### 2.2 Responsive Navigation Bar - Smartphone
- header-menu 요소 내에 클릭할 수 있는 navigation icon을 만들기 위한 html tag를 추가한다. `label tag의 for 프로퍼티값과 input tag의 id 프로퍼티값이 일치`하여야 한다.

- span의 class는 햄버거의 위 아래를 생성하는데 필요하다.
- input의 id는 label의 for에 입력해 줌으로써 서로 연결한다. 
- input의 class는 checked의 여부를 확인하기 위해서 
```
<nav>
  <input class="nav-toggle" id="nav-toggle" type="checkbox">
  <label class="navicon" for="nav-toggle"><span class="navicon-bar"></span></label>
  <ul class="nav-items">
    <li><a href="#home">Home</a></li>
...
```
- navigation icon은 input checkbox 요소와 연동되어야 하므로 label 요소를 사용하였다. 즉 navigation icon을 클릭하면 checkbox input tag도 checked 상태가 된다.

```
<nav>
  <input class="nav-toggle" id="nav-toggle" type="checkbox">
  <label class="navicon" for="nav-toggle"><span class="navicon-bar"></span></label>
  <ul class="nav-items">
    <li><a href="#home">Home</a></li>
...
```

- checkbox에 checked 상태여부를 판단할 수 있게된다.

```
.navicon-bar::before,
.navicon-bar::after {
  background-color: #333;
  content: "";
  display: block;
  height: 100%;
  width: 100%;
  position: absolute;
}
.navicon-bar::before {
  top: -7px;
}
.navicon-bar::after {
  top: 7px;
}

.navicon-bar {
  position: relative ; /*추가하기*/
}

```

- 햄버거 모양으로 만든 것을 누르면 x 로 표시되게한다.

> 회전시 위치가 틀어짐으로써 top:0; 으로 지정해준다.
```
.nav-toggle:checked ~ .navicon > .navicon-bar {
  background: transparent;
}

.nav-toggle:checked ~ .navicon > .navicon-bar::after {
  transform: rotate(45deg);
  top: 0;
}

.nav-toggle:checked ~ .navicon > .navicon-bar::before {
  transform: rotate(-45deg);
  top: 0;
}
```

- transition property는 property, duration, delay 순으로 정의한다.

```
.navicon-bar {
  background-color: #333;
  display: block;
  position: relative;
  transition: background-color .2s ease-out;
  width: 20px;
  height: 3px;
}
.navicon-bar::before,
.navicon-bar::after {
  background-color: #333;
  content: "";
  display: block;
  height: 100%;
  width: 100%;
  position: absolute;
  transition: all .2s ease-out;
}
```

- navigation icon을 클릭하면 의도하지 않게 이미지가 선택되는 현상이 발생할 수 있다.
  - 이것은 navigation icon이 텍스트이기 때문에 발생하는 문제이다. 이 문제는 텍스트 선택을 차단하는 방법인 user-select: none; 프로퍼티를 지정하여 회피할 수 있다.

  ```
  .navicon {
  cursor: pointer;
  position: absolute;
  height: 60px;
  padding: 28px 15px;
  top: 0;
  right: 0;
  -webkit-user-select: none;
  /* Chrome all / Safari all */
  -moz-user-select: none;
  /* Firefox all */
  -ms-user-select: none;
  /* IE 10+ */
  user-select: none;
  /* Likely future */
  }
  ```



- navigation icon과 checkbox input tag는 스마트폰 layout 이외의 경우, 화면에 표시되어서는 않된다. 따라서 display: none;으로 화면에 표시되지 않도록 한다.

- display: none;은 해당 공간조차 점유하지 않지만 visibility: hidden;을 사용하면 해당 공간은 남아있고 표시만 되지 않는다.

- CSS 적용 우선 순위 (Cascading Order)를 고려하여 가장 마지막에 정의하는 것이 안전하다. 일반적으로 media query를 가장 마지막에 정의하므로 media query 정의부 직전에 위치시킨다.


```
.nav-toggle {
  display: none;
}
.navicon {
  display: none;
}
```

- 스마트폰 layout에서는 .header-menu > ul > li 가 초기상태에서 비표시되어야 한다. 그리고 navigation icon은 표시되어야 한다. 아직 navigation icon을 완성하지 않았으므로 표시되지 않는다.

```
@media screen and (max-width: 480px) {
  header {
    height: 60px;
  }
  .nav-items {
    display: none;
  }
  .navicon {
    display: block;
  }
}
```

- 콘텐츠 영역이 아직 tablet layout에 맞추어 아래로 내려가 있다. header 영역 바로 아래로 다시 끌어 올린다.

```
@media screen and (max-width: 480px) {
  /*...*/
  #wrap {
    margin-top: 60px;
  }
  aside {
    top: 60px;
  }
  /*...*/
}
```

- 마지막으로 navigation icon을 클릭하면 navigation item이 표시되도록 한다.



```
@media screen and (max-width: 480px) {
  ...

  .nav-toggle:checked ~ .nav-items {
    display: block;
    width: 100%;
    background-color: #fff;
    box-shadow: 0 2px 2px rgba(0, 0, 0, 0.05), 0 1px 0 rgba(0, 0, 0, 0.05);
  }
  .nav-items > li  {
    display: block;
  }
  .nav-items > li > a {
    line-height: 50px;
  }
}
```

## 3. Section & Aside & Footer
- article을 한 행에 2개씩 존재하게 만든다.