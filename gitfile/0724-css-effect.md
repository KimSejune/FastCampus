170724

# CSS3 Effect

## 1. 벤더 프리픽스 (Vender Prefix)
- CSS3 표준으로 확정되기 이전 또는 브라우저 개발사가 실험적으로 제공하는 기능을 사용하기 위해서는 벤더 프리픽스를 사용하여야 한다.

```
* {
  -webkit-user-select: none;  /* Chrome all / Safari all / 다된다. */
  -moz-user-select: none;     /* Firefox all */
  -ms-user-select: none;      /* IE 10+ */
  user-select: none;          /* Likely future */
}
```  

- 라이브러리를 사용하는 것은 매우 유용한 방법이다.
[Prefix Free 라이브러리](http://leaverou.github.io/prefixfree/)
```
<script src="prefixfree.min.js"></script>
```

## 2. 그림자(shadow)
- 텍스트나 요소에 그림자 효과를 부여하기 위한 프로퍼티를 선언한다.

### 2.1 text-shadow
- 텍스트에 그림자 효과를 부여하는 프로퍼티이다.
```
선택자 { text-shadow: Horizontal-offset Vertical-offset Blur-Radius Shadow-Color; }
```

### 2.2 box-shadow
- 요소에 그림자 효과를 부여하는 프로퍼티이다.

## 3. 그레이디언트(Gradient)
- 2가지 이상의 색상을 혼합하여 부드러운 색감의 배경 등을 생성하는 것이다.
  - 선형 그레이디언트
  - 방사형 그레이디언트
[그레이디언트 작성 툴](http://www.colorzilla.com/gradient-editor/)
[codepen](https://codepen.io/search/pens?q=gradient&limit=all&order=popularity&depth=everything&show_forks=false)
> browser의 속성을 많이 탄다. 그래서 기본 백그라운드를 설정해준다.

## 4. 트랜지션(Transition)
- CSS Property가 변경되면 Property 변경에 따른 표시의 변화를 표현한다.
- `transition: all 2s;` 이것에 포함된 모든 것들이 2초 동안 변경된다.
  - 부모에다가 이 코드를 쓰면 모든 경우에 변화한다.
  - 자식에다가 이 코드를 쓰면 올렸을 때는 변화하지만 내리면 변화하지 않는다.
- transition은 자동으로 발동되지 않는다. 
  - 가상 클래스 선택자 또는 JavaScript onclick이벤트를 사용해야 발동한다.

### 4.1 transition-property
- transition-property 프로퍼티는 트랜지션의 대상이 되는 CSS 프로퍼티명을 지정한다
- 여러개를 지정할 때는 , 로 연결한다.
- `transition-duration`은 반드시 지정해야한다.
> display property는 변경할 수 없다.
- layout에 영향을 주는 트랜지션 효과는 회피하기 위한 노력이 필요하다.
- layout에 영향을 주는 프로퍼티는 다음과 같다.
```
width height padding margin border
display position float overflow
top left right bottom
font-size font-family font-weight
text-align vertical-align line-height
clear white-space
```
### 4.2 transition-duration
- duration을 초 단위로 지정한다.
  - 값을 지정하지 않을 경우 기본값 0s가 적용되어 어떠한 효과도 볼 수 없다.
```
div {
  /* shorthand syntax */
  transition: width 2s, opacity 4s;
}
```

### 4.3 transition-timing-function
- 트랜지션 효과의 변화 흐름, 시간에 따른 변화 속도와 같은 일종의 변화의 리듬을 지정한다.
  - eage(default) : 기본값. 느리게 시작하여 점점 빨라졌다가 느리지면서 종료한다.
  - linear : 시작부터 종료까지 등속 운동을 한다.
  - ease-in : 느리게 시작한 후 일정한 속도에 다다르면 그 상태로 등속 운동한다.
  - ease-out : 일정한 속도의 등속으로 시작해서 점점 느려지면서 종료한다.
  - ease-in-out : ease와 비슷하게 느리게 시작하여 느리지면서 종료한다.

### 4.4 transition-delay
- transition이 바로 발동하는 것이 아닌 대기를 하였다가 시작한다.

### 4.5 transition
- shorthand 방법 : `transition: property duration function delay`

## 5. 애니메이션(Animation)
- 애니메이션은 browser에 부담을 주기 때문에 조심해서 사용해야 한다.
- 비교적 작은 효과나 CSS만으로도 충분한 효과를 볼 수 있는 것은 CSS를 사용한다. 예를 들어 요소의 width 변경 애니메이션은 자바스크립트를 사용하는 것보다 훨씬 간편하며 효과적이다.
  - css로 만들기 힘들다면 javascript로 만드는 것이 났다.
- 세밀한 제어를 위해서는 자바스크립트 사용이 바람직하다. 예를 들어 바운스, 중지, 일시 중지, 되감기 또는 감속과 같은 고급 효과는 자바스크립트가 훨씬 유용하다.

## 5.1 @keyframs
- 애니메이션의 흐름중의 여러 시점에서 CSS property값을 지정할 수 있다.
```
    div {
      position: absolute;
      width: 100px;
      height: 100px;
      background-color: red;
      animation-name: move;
      animation-duration: 5s;
      animation-iteration-count: infinite;
    }
    @keyframes move {
      /* keyframe 시작 */
      from {
        left: 0;
      }
      /* keyframe 종료 */
      to {
        left: 300px;
      }
    }
```
  - from, to 대신 %를 사용할 수 있다.
  ```
  @keyframes move {
    0%   { left: 0; }
    50%  { left: 100px; }
    100% { left: 300px; }
  }
  ```
### 5.2 animation-name
- @keyframes rule을 생성할 때 이름을 생성해준다.
- animation-name을 여러개 넣을 때 ,를 사용한다.

### 5.3 animation-duration
- 한 싸이클에 animation에 소요되는 시간을 초 단위로 지정한다.

### 5.4 animation-timing-funtion
- 애니메이션 효과를 위한 수치 함수를 지정한다.
> 트랜지션 transition-timing-function 프로퍼티 을 참조하기 바란다.

### 5.5 animation-delay
- 요소가 로드된 시점과 애니메이션이 실제로 시작하는 사이에 대기하는 시간을 초 단위로 지정한다.

### 5.6 animation-iteration-count
- animation의 반복여부를 지정할 수 있다.
  - `animation-iteration-count: infinite;` 하면 무한반복한다.

### 5.7 animation-direction
- 애니메이션이 종료된 이후 반복될 때 진행하는 방향을 지정한다.  
  - normal :	기본값으로 from(0%)에서 to(100%) 방향으로 진행한다.  
  - reverse :	to에서 from 방향으로 진행한다.  
  - alternate	: 홀수번째는 normal로, 짝수번째는 reverse로 진행한다.  
  - alternate-reverse :	홀수번째는 reverse로, 짝수번째는 normal로 진행한다.  

### 5.8 animation-fill-mode
- 애니메이션 미실행 시(대기 또는 종료) 요소의 스타일을 지정한다.
  - none, forwards, backwords, both
  [참조](http://poiemaweb.com/css3-effect) 

### 5.9 animation-play-state
- 애니메이션 재생 상태(재생 또는 중지)를 지정한다. 기본값은 running이다.

### 5.10 animation
- 모든 애니메이션 프로퍼티를 한번에 지정한다. 값을 지정하지 않은 프로퍼티에는 기본값이 지정된다. 지정 방법은 다음과 같다.
- `animation: name duration timing-function delay iteration-count direction fill-mode play-state`
  - duration은 반드시 지정해야 한다.


## 6. 트랜스폼(Transform)
- 트랜스폼은 요소에 이동(translate), 회전(rotate), 확대축소(scale), 비틀기(skew) 효과를 부여하기 위한 함수를 제공한다.
 [Transform codepen 활용](https://codepen.io/search/pens?q=transform&limit=all&type=type-pens)

### 6.1 2D Transform
- 2D 트랜스폼은 프로퍼티값으로 변환함수(transform function)를 사용한다. 
  - trnaslate(x,y) : 이동
  - scale(x,y) : 확대
  - skew(x-angle,y-angle) : 기울기
  - rotate(angel) : 회전
[변환함수 참조](http://poiemaweb.com/css3-effect)

### 6.1.1 transform
- 변환함수를 프로퍼티값으로 쉼표없이 나열한다. 나열순서에 따라 차례대로 효과가 적용된다.

### 6.1.2 transform-origin
- 요소의 기준점을 설정할 때 사용된다.
  - 좌상단 0,0, 중앙 center

## 6.2 3D Transform
- 3D 트랜스폼은 프로퍼티값으로 변환함수(transform function)를 사용한다.
[변환함수 참조](http://poiemaweb.com/css3-effect)
