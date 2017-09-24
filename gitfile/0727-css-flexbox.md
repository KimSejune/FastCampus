170727

# CSS3 flexbox

## 1. Introduction
- 복잡한 레이아웃이라도 적은 코드로 보다 간단하게 표현할 수 있다.
- 부모에게 `display: flex;` 를 해주고 자식들에게 속성을 지정해줘야한다.
- Flexbox의 장점 
  - 1줄의 코드 추가로 수평 정렬이 가능하다.
  - 요소의 상하좌우 정렬, 순서 변경이 간단하다.
  - 요소가 간격 조절이 간단하다.
  - 서로 다른 height를 갖는 요소의 수평정렬 시, 간단히 상하중앙 정렬이 가능하다.
> 아직까지 지원하는 브라우저가 적으니 사용시 주의해야한다.

## 2. Usage
- Flexbox 레이아웃은 부모 : `flex-container`, 자식 : `flex item`로 구성된다.

- flexbox를 사용하기 위해서 HTML 부모 요소의 display 속성에 flex를 지정한다.
```
.flex-container {
  display: flex;
}
```

- 부모 요소가 inline 요소인 경우 inline-flex을 지정한다.
```
.flex-container {
  display: inline-flex;
}
```

## 3. Flexbox container 속성

### 3.1 flex-direction
- flex-direction 속성은 flex 컨테이너의 주축(main axis) 방향을 설정한다.
  - `flex-direction: row;`
   - 좌에서 우로(ltr) 수평 배치된다. flex-direction 속성의 기본값이다.
  - `flex-direction: row-reverse;`
    - 우에서 좌로(rtl) 수평 배치된다.
  - `flex-direction: column;`
    - 위에서 아래로 수직 배치된다.
  - flex-direction: column-reverse;
    - 아래에서 위로 수직 배치된다.

### 3.2 flex-wrap
- flex-wrap 속성은 flex 컨테이너의 복수 flex item을 1행으로 또는 복수행으로 배치한다. flex-wrap 속성은 flex 컨테이너의 width보다 flex item들의 width의 합계가 더 큰 경우, 한줄로 표현할 것인지, 여러줄로 표현할 것인지를 지정한다.
  - `flex-wrap: nowrap;`
   - flex item을 개행하지 않고 1행에 배치한다. flex-wrap 속성의 기본값이다.
>  flex item들의 width의 합계가 flex 컨테이너의 width보다 큰 경우 flex 컨테이너를 넘치게 된다. 이때 `overflow: auto;`를 지정하면 가로 스크롤이 생기며 컨테이너를 넘치지 않는다.

  - flex-wrap: wrap;
    - flex item들의 width의 합계가 flex 컨테이너의 width보다 큰 경우, flex item을 복수행에 배치한다. 기본적으로 좌에서 우로, 위에서 아래로 배치된다.
  
  - flex-wrap: wrap-reverse;
    - flex-wrap: wrap;과 동일하나 아래에서 위로 배치된다.

### 3.3 flex-flow
- flex-flow 속성은 flex-direction 속성과 flex-wrap 속성을 설정하기 위한 shorthand이다. 기본값은 row nowrap이다.

```
.flex-container {
  flex-flow: <flex-direction> || <flex-wrap>;
}
```

### 3.4 justify-content
- flex container의 main axis를 기준으로 flex item을 수평 정렬한다.

- justify-content: flex-start;
  - main start(좌측)를 기준으로 정렬한다. justify-content 속성의 기본값이다.
- justify-content: flex-end;
  - main end(우측)를 기준으로 정렬한다.
- justify-content: center;
  - flex container의 중앙에 정렬한다.
- justify-content: space-between;
  - 첫번째와 마지막 flex item은 좌우 측면에 정렬되고 나머지와 균등한 간격으로 정렬된다.
- justify-content: space-around;
  - 모든 flex item은 균등한 간격으로 정렬된다.

### 3.5 align-items
- flex item을 flex container의 수직 방향(cross axis)으로 정렬한다. align-items 속성은 모든 flex item에 적용된다.
- align-items: stretch;
  - 모든 flex item은 flex container의 높이(cross start에서 cross end까지의 높이)에 꽉찬 높이를 갖는다. align-items 속성의 기본값이다
- align-items: flex-start;
  - 모든 flex item은 flex container의 cross start(부모의 윗부분) 기준으로 정렬된다.
- align-items: flex-end;
  - 모든 flex item은 flex container의 cross end(부모의 밑부분) 기준으로 정렬된다.
- align-items: center;
  - 모든 flex item은 flex container의 cross axis의 중앙에 정렬된다.
- align-items: baseline;
  - 모든 flex item은 flex container의 baseline을 기준으로 정렬된다.(글자를 기준으로 정렬)

### 3.6 align-content
- flex container의 cross axis를 기준으로 flex item을 수직 정렬한다.
- align-content: stretch;
  - 모든 flex item은 flex item의 행 이후에 균등하게 분배된 공간에 정렬되어 배치된다. align-content 속성의 기본값이다.
- align-content: flex-start;
  - 모든 flex item은 flex container의 cross start 기준으로 stack 정렬된다.
- align-content: flex-end;
  - 모든 flex item은 flex container의 cross end 기준으로 stack 정렬된다.
- align-content: center;
  - 모든 flex item은 flex container의 cross axis의 중앙에 stack 정렬된다.
- align-content: space-between;
  - 첫번째 flex item의 행은 flex container의 상단에 마지막 flex item의 행은 flex container의 하단에 배치되며 나머지 행은 균등 분할된 공간에 배치 정렬된다.
- align-content: space-around;
  - 모든 flex item은 균등 분할된 공간 내에 배치 정렬된다.
## 4. Flexbox item 속성
  - float, clear, vertical-align 속성은 flex item에 영향을 주지 않는다.

### 4.1 order
- 0은 원래위치, 음수는 앞으로, 양수는 뒤로 이동한다.
```
.flex-item {
  order: 정수값;
}
```
### 4.2 flex-grow
- flex item의 너비에 대한 확대 인자(flex grow factor)를 지정한다. 기본값은 0이고 음수값은 무효하다.

- 모든 flex item이 동일한 flex-grow 속성값을 가지면 모든 flex item은 동일한 너비를 갖는다.
- 두번째 flex item의 flex-grow 속성값을 3으로 지정하면 다른 flex item보다 더 넓은 너비를 갖는다두
```
.flex-item {
  flex-grow: 양의 정수값;
}
```
### 4.3 flex-shrink
- flex item의 너비에 대한 축소 인자(flex shrink factor)를 지정한다. 기본값은 1이고 음수값은 무효하다. 0을 지정하면 축소가 해제되어 원래의 너비를 유지한다.
- 기본적으로 모든 flex item은 축소된 상태로 지정(기본값 1)하고 두번째 flex item만 축소를 해제(flex-shrink: 0;)하면 원래의 너비를 유지한다.
```
.flex-item {
  flex-shrink: 양의 정수값;
}
```
### 4.4 flex-basis
- flex item의 너비 기본값을 px, % 등의 단위로 지정한다. 기본값은 auto이다.
```
.flex-item {
  flex-basis: auto | <width>;
}
```

### 4.5 flex
- flex-grow, flex-shrink, flex-basis 속성의 shorthand이다. 기본값은 0 1 auto이다.
```
.flex-item {
  flex: none | auto | [ <flex-grow> <flex-shrink>? || <flex-basis> ];
}
```
### 4.6 align-self
- align-items 속성(flex container속성으로 flex item을 flex container의 수직 방향(cross axis)으로 정렬한다.)보다 우선하여 개별 flex item을 정렬한다. 기본값은 auto이다.

```
.flex-item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```
## 5. Flexbox playground
[Flexbox Playground](https://demos.scotch.io/visual-guide-to-css3-flexbox-flexbox-playground/demos/)