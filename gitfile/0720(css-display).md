2017.07.20

# CSS3 display
- `block요소` width를 100%를 가지는 것
  - ex) li, p 등
- `inline요소` width를 설정할 수 있다.
  - ex) input 요소, span 등
- `inline-block 요소` inline의 요소를 가지며 block의 요소도 가진다.
- none 해당 요소를 화면에 표시하지 않는다.
  - 감춰져 있다가 어떤 상황에 나타난다. ex) 로그인시 id에 한글을 쓰면 안될 때 알린다.

> display는 상속되지 않는다.

## 1.1 block 레벨 요소
- 항상 새로운 라인에서 시작한다.
- 화면 크기 전체의 가로폭을 차지한다. (width: 100%)
- width, height, margin, padding 프로퍼티 지정이 가능하다.
- block 레벨 요소 내에 inline 레벨 요소를 포함할 수 있다
- block 레벨 요소 예
  - div, h1 ~ h6, p, ol, ul, li, hr, table, form

## 1.2 inline 레벨 요소
- 새로운 라인에서 시작하지 않으며 문장의 중간에 들어갈 수 있다.  
`즉, 줄을 바꾸지 않고 다른 요소와 함께 한 행에 위치한다.`
- content의 너비만큼 가로폭을 차지한다.
- `width, height, margin-top, margin-bottom 프로퍼티를 지정할 수 없다.` 상, 하 여백은 line-height로 지정한다.
- inline 레벨 요소 뒤에 공백(엔터, 스페이스 등)이 있는 경우, 정의하지 않은 space(4px)가 자동 지정된다.
- inline 레벨 요소 내에 block 레벨 요소를 포함할 수 없다. inline 레벨 요소는 일반적으로 block 레벨 요소에 포함되어 사용된다.
- inline 레벨 요소 예
  - span, a, strong, img, br, input, select, textarea, button

## 1.3 `inline-block` 레벨 요소
- inline 레벨 요소와 같이 한 줄에 표현되면서 `width, height, margin Property`를 모두 지정할 수 있다.

```
<ul>
  <li> </li>
  <li> </li>
</ul>
```
이것을 좌우로 놓고 싶다면 li를 가져와서 display : inline-block으로 한다.

[4px을 회피하는 방법](https://css-tricks.com/fighting-the-space-between-inline-block-elements/)
```
    .wrapper {
      font-size: 0; /*요소간 간격을 제거*/
    }
```
## 2. Visibility Property
- 요소를 보이게하고 안보이게 한다 
  - visible	해당 요소를 보이게 한다 (기본값)
  -	해당 요소를 보이지 않게 한다. `display: none;`은 해당 요소의 공간까지 사라지게 하지만 `visibility: hidden;`은 해당 요소의 공간은 사라지지 않고 남아있게 된다.

## 3. opacity Property
- 요소의 투명도를 0.0 ~ 1.0 사이로 지정한다. 0.0은 투명, 1.0은 불투명
  - 이미지와 색상에 적용가능
> transition : opacity 1s;  opacity를 1초에 걸려서 시켜라.

---