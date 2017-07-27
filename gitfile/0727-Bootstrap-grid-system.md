170727

# Bootstrap-Grid-System

## 1. Media Query 
- Bootstrap은 Mobile-first 방식을 기본 지원하므로 Media query에 포함되지 않은 모든 정의는 768px 미만 디바이스를 위한 것이다.
- Bootstrap은 기본적으로 4개의 breakpoint로 구간을 나눈다.

```
/* Small devices (tablets, 768px and up) */
@media (min-width: @screen-sm-min) {
  /* ... */
}

/* Medium devices (desktops, 992px and up) */
@media (min-width: @screen-md-min) {
  /* ... */
}

/* Large devices (large desktops, 1200px and up) */
@media (min-width: @screen-lg-min) {   
  /* ... */
}
```

> @는 LESS의 변수를 의미한다. LESS는 CSS 프리프로세서(Preprocessor)로서 Bootstrap의 소스코드는 LESS를 기반으로 작성되었다.

## 2. Container
- Bootstrap은 콘텐츠를 감싸는 wrapping 요소(container)를 포함해야 한다. container는 그리드 시스템의 필수 요소이다.

- container에는 2가지 종류가 있다.
  - .container class : fixed width container로서 responsive fixed layout(반응형 고정폭 레이아웃)을 제공한다.
  - .container-fluid class : full width container로서 fluid layout(유동 최대폭 레이아웃)을 제공한다.

### 2.1 fixed width container (responsive fixed layout)
- responsive fixed layout(반응형 고정폭 레이아웃)을 만들 때 사용한다. Media query에 의해 반응형으로 동작하며 동일 breakpoint내에서는 viewport 너비가 늘어나거나 줄어들어도 고정폭을 갖는다.

```
.container {
  padding-right: 15px;
  padding-left: 15px;
  margin-right: auto;
  margin-left: auto;
}
/* Extra small devices (phones, less than 768px) */
/* No media query since this is the default in Bootstrap */

/* Small devices (tablets, 768px and up) */
@media (min-width: 768px) {
  .container {
    width: 750px;
  }
}
/* Medium devices (desktops, 992px and up) */
@media (min-width: 992px) {
  .container {
    width: 970px;
  }
}
/* Large devices (large desktops, 1200px and up) */
@media (min-width: 1200px) {
  .container {
    width: 1170px;
  }
}
```


### 2.2 full width container (fluid layout)
- fluid layout(유동 최대폭 레이아웃)을 만들 때 사용한다. viewport 너비에 상관없이 언제나 콘텐츠 요소를 화면에 꽉차는 너비를 갖게 한다.

```
.container-fluid {
  padding-right: 15px;
  padding-left: 15px;
  margin-right: auto;
  margin-left: auto;
}
```

> container 내부에는 container를 padding의 문제가 발생하기 때문이며 container 내부에는 row가 온다.

## 3. Grid-System
- 그리드 시스템은 열을 나누어 콘텐츠를 원하는 위치에 배치하는 방법(Layout)을 말한다. Bootstrap은 반응형 12열 그리드 시스템을 제공한다.

> 그리드 레이아웃을 구성 시에는 반드시 .row(행)를 먼저 배치하고 행 안에 .col-*-*(열)을 필요한 갯수만큼 배치한다. 즉 container 내에 .row(행)을 먼저 배치하고 그 안에 .col-*-*(열)을 배치한다. 그리고 콘텐츠는 .col-*-* 내에 배치한다.

### 3.1 행(.row)의 구성
- container(.container 또는 .container-fluid) 내에 .row class를 사용하여 행을 배치한다.

### 3.2 열(.col-*-*)의 구성
- 열은 행(.row) 내에 배치하여야 한다. .col-*-* class로 열을 배치하는데 첫번째 *에는 `xs, sm, md, lg` 중의 하나를 지정한다.

> col-size-count 이런 형식으로 나타난다.

- 무조건 범위에 있는 것 1개만 선택된다.
  - 800인 경우 xs, sm은 적용이된다 하지만 여기서 800이 sm의 범위 안에 있어서 sm이 선택된다.


#### 3.2.1 .col-xs-* class
- viewport width와 관계없이 .col-xs-* 클래스는 언제나 적용되어 .col-xs-* 틀래스가 선언된 요소는 항상 수평으로 정렬된다.

#### 3.2.2 .col-sm-* class
- viewport width가 768px 이상(768px ~)일 때 .col-sm-* class는 적용된다. `768px 미만`일 때는 media query에 의해 .col-sm-* class가 적용되지 않고 `div 요소의 block 특성에 의해 100%의 너비를 가지며 수직으로 쌓이게 된다`.

#### 3.2.3 .col-md-* class

- viewport width가 992px 이상(992px ~)일 때 .col-md-* class는 적용된다. 992px 미만일 때는 media query에 의해 .col-md-* class가 적용되지 않고 div 요소의 block 특성에 의해 100%의 너비를 가지며 수직으로 쌓이게 된다.

#### 3.2.4 .col-lg-* class

- viewport width가 1200px 이상(1200px ~)일 때 .col-lg-* class는 적용된다. 1200px 미만일 때는 media query에 의해 .col-lg-* class가 적용되지 않고 div 요소의 block 특성에 의해 100%의 너비를 가지며 수직으로 쌓이게 된다.

### 3.3 col- class의 복합 구성

- 위와 같이 정의하면 아래와 같이 동작한다.
    - viewport 너비가 768px 미만(~ 768px)이면 .col-xs-12 class가 적용된다.
    - viewport 너비가 768px 이상(768px ~)이면 .col-sm-6 class가 적용된다.
    - 하지만 col-xs-* class는 언제나 적용된다고 하였다.
```
<div class="row">
  <div class="col-sm-12 col-md-8">.col-sm-12 .col-md-8</div>
  <div class="col-sm-6">.col-sm-6</div>
</div>
```
- 위의 경우, viewport width가 992px 이상일 때 첫번째 div 요소는 col-md-8가 지정되어 있으므로 col-md-8 class가 적용되지만 두번째 div 요소에는 col-md-이 지정되어 있지 않다. 따라서 viewport 너비가 992px 이상이더라도 col-sm-6 class가 적용된다.

#### 3.3.1 Mobile and Desktop
- Mobile의 경우 breakpoint는 768px 미만(~ 768px)이며 class prefix는 .col-xs-*이다.
- Desktop의 경우, breakpoint는 992px(992px ~) 이상이며 class prefix는 .col-md-*이다.

```
      <div class="col-xs-12 col-md-8">.col-xs-12 .col-md-8</div>

      <div class="col-xs-12 col-md-4">.col-xs-12 .col-md-4</div>
```

#### 3.3.2 Mobile, tablet, desktop
- Mobile의 경우 breakpoint는 768px 미만이며 class prefix는 .col-xs-*이다.
- tablet의 경우 breakpoint는 768px 이상이며 class prefix는 .col-sm-*이다.
- Desktop의 경우, breakpoint는 992px 이상이며 class prefix는 .col-md-*이다.

### 3.4 Nesting columns
- 열 내부에 그리드를 추가하면 자식 그리드의 전체 너비는 부모 열의 너비와 같다.

### 3.5 Offsetting columns
- 열에 .col-*-offset-* class를 추가하면 오른쪽으로 열을 이동시킬 수 있다.

- 예를 들어 `<div class="col-md-2 col-md-offset-4">`의 경우, viewport 너비가 992px 이상이면 .col-md-4 만큼 오른쪽으로 이동한 후 .col-md-2 만큼의 너비를 갖는 열을 표시한다.

### 3.6 Column ordering
- .col-*-push-* 와 .col-*-pull-* 클래스를 사용하여 열의 순서를 변경할 수 있다
```
  <div class="col-xs-9 col-xs-push-3">.col-xs.col-xs-push-3</div>
  <div class="col-xs-3 col-xs-pull-9">.col-xs.col-xs-pull-9</div>
```
- 서로 자리를 변경한다.