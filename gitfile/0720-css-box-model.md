2017.07.20

# CSS Box Model
- 모든 HTML요소는 BOX 형태의 영역을 가지고 있다.
- Margin, Padding, Border, Contents로 구성된다.
  - 요소의 영역은 Margin까지로 표현된다.

  > background-color를 사용하면 Padding까지 색이 들어간다.
- 크게 HTML요소는 Inline, Block 요소를 가지고 있다.

`웹 디자인이란? `  박스 모델을 정의하고 CSS Property를 통해 스타일과 위치 및 정렬을 지정한다.

Content :	요소의 텍스트나 이미지 등의 실제 내용이 위치하는 영역이다.  
Padding	: 테두리(Border) 안쪽에 위치하는 요소의 내부 여백 영역이다.  
Border :	테두리 영역으로 border 프로퍼티 값은 테두리의 두께를 의미한다.  
Margin :	테두리(Border) 바깥에 위치하는 요소의 외부 여백 영역이다.


## 1. width / height Property
-  기본적으로 width는 부모의 100%, height는 contents가 들어갈 영역의 크기이다.

## 2. Margin / Padding Property
- 4방면(top, right, bottom, left)을 따로따로 지정할 수 있다.

> margin 0 auto; 를 통해서 가운데로 위치하게 한다.
- max-width는 너비의 최대값 지정 `요소의 width가 browser보다 커지면 자동으로 요소의 너비가 줄어든다.`
- min-width는 너비의 최솟값 지정 `아무리 browser가 작아져도 요소의 width를 유지한다.`

## 3. border Property

### 3.1 border-style
- Property의 테두리 선의 스타일을 지정한다.
    - solid : 실선

### 3.2 border-width
- border-style과 함께 사용해야한다.

### 3.3 border-color
- border-style과 함께 사용해야한다.

### 3.4 border-radius
- border radius가 커질수록 더 원형에 가까워진다.
```
  border-top-left-radius:     10px;
  border-top-right-radius:    40px;
  border-bottom-right-radius: 40px;
  border-bottom-left-radius:  10px;
```
### 3.5 border
- border: border-width border-style border-color; 

## 4. box-sizing Property
- `border까지 box의 영역으로 만들 수 있다.` 
```
html {
  box-sizing: border-box;
}
*, *:before, *:after {
  box-sizing: inherit;
}
```
> inherit은 상속을 의미한다.

---
