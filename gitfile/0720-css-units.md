2017.07.20

# CSS - Units

## 1. 키워드
property에 따라서 지정해 줄 수 있는 값이 있다.

```
h1{color:red; font-size: 12px;}
```

> display property는 block, inline, inline-block, none이 존재한다.


---

## 2. 크기단위
CSS에서 사용하는 대표적인 크기 단위는 px, em, %이다.
> em, %는 상대적인 크기 px은 절대적인 크기

### 2.1 px
- px(화소)단위이다. 1px은 화소 1개 크기를 의미한다.  
- 픽셀수가 많으면 화질이 또렷하고 선명한 것이다. 단) 데이터의 수는 늘어난다.
- 현재 1px을 1/96인치이다.
> px은 font의 크기,  img의 크기에 사용한다.

### 2.2 %
- %는 요소에 지정된 사이즈에 상대적인 사이즈이다. 
  - ex) 50%은 1/2배의 크기를 나타낸다.
### 2.3 em
- em은 요소에 지정된 사이즈에 상대적인 사이즈이다.
  - ex) 2em은 (상속된, 디폴트 사이즈) 2배의 크기를 나타낸다.

```
  <div class='box1'>
    Font size: 1.2em ⇒ 14px * 1.2 = 16.8px
    <div class='box2'>
      Font size: 1.2em ⇒ 16.8px * 1.2 = 20.16px
      <div class='box3'>
        Font size: 1.2em ⇒ 20.16px * 1.2 = 24.192px
      </div>
    </div>
  </div>
```

> 중첩된 요소의 em을 사용하면 지속적으로 커진다. // sol-> rem

### 2.4 rem
- rem은 최상위 요소(html)의 사이즈를 기준으로 삼는다. 
  - r은 root를 나타낸다.
```
html{
  font-size: 14px; // 이것을 기준으로 잡는다.
}
```

### 2.5 Viewport단위(vh, vw, vmin, vmax)
- viewport 단위 : viewport를 기준으로 한 상대적 사이즈를 의미
  - vw = viewport 너비의 1/100
  - vh = viewport 높이의 1/100
  - vmin = viewport 너비 또는 높이 중 작은 쪽의 1/100
  - vmax = viewport 너비 또는 높이 중 큰 쪽의 1/100

  > viewport는 보고있는 화면을 나타낸다.
<br>

## 3. 색상 표현 단위
- 다양한 방법을 통하여 색상을 세밀하게 표현 가능

  - HEX 코드 단위 (Hexadecimal Colors)	#000000   
  - RGB (Red, Green, Blue)	rgb(255, 255, 0)  
  - RGBA (Red, Green, Blue, Alpha/투명도)	rgba(255, 255, 0, 1)  

[htmlcolorcodes](www.htmlcolorcodes.com) color Information check  

### 3.1 color keywords
- black, white, red etc..

---