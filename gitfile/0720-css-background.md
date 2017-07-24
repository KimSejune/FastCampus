2017.07.20

# CSS3 Backgroud
## 1. background-image property  
  - 절대경로, 상대경로를 넣으면 된다.
  ```
      body {
      background-image: url("http://poiemaweb.com/img/bg/dot.png");
    }
  ```
## 2. background-repeat property
  - background-repeat을 통하여 반복을 설정한다.
    - no-repeat, x-repeat, y-repeat

  - 이미지는 여러개를 넣을 수 있다.
      - 먼저 선언한 이미지가 위로 올라온다. 반드시 , 로 구분을 한다.
```
    body {
      background-image: url("http://poiemaweb.com/img/bg/dot.png");
      background-repeat: repeat-x;
    }
```

## 3. background-size property
- px 원하는 크기를 설정할 수 있다. 
- % 화면을 줄이거나 늘리면 찌그러지는 현상이 발생한다.
- `cover` 비율을 유지한 상태에서 화면을 채운다. 단) 안보이는 영역이 발생한다.
- contain 비율을 유지한 상태에서 모든 부분이 보이게 채운다. 단) 공백이 발생한다.

```
body {
  background-image: url("front.png"), url("back.png");
  background-repeat: no-repeat, no-repeat;
  background-size: 100%, 500px;
}
```
> size를 하나만 지정해주는 것은 width를 의미하게 되며 height는 auto가 된다.

## 4. background-attachment
- scroll을 할 때 배경은 움직이지 않게 한다.  
    ```
    background-attachment: fixed
    ```
  
>margin 상쇄문제 해결 코드
        https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing

```
아래의 방법으로 해결가능
overflow: auto; 
/* or padding: 0.1px; */
 ```

## 5. background-position property
- 이미지의 좌표(xpos, ypos)를 지정할 수 있다.
  - %, px로 위치를 지정할 수 있다.  
[MDN:background-position](https://developer.mozilla.org/en-US/docs/Web/CSS/background-position)

- 이미지가 2개 이상 있을 때 , 로 구분한다
```
.example8 {
    background-image: url("http://poiemaweb.com/img/bg/dot.png"), url("http://poiemaweb.com/img/bg/dot.png");
    background-position: 0px 0px, center;
 }
```

## 6. background-color property
- 원하는 색을 지정할 수 있다.

## 7. background shorthand
- 여러가지의 속성을 한번에 지정하는 방법이다. 
  - background: color image repeat attachment position
  >space로 구분되며 비워둬도 된다.  

`img를 채울 때 div영역에 background-image로 채우는 것이 좋다.`

---
