170728

# Snippet Centering

## 1. 수평 정렬

### 1.1 inline/inline-block 요소
- margin-top, bottom 을 줄 수 없다.
- margin-left, right 을 줄 수 있다.

  ```
  text-align: center;
  ```
### 1.2 block 요소
- width가 100%가 아니라는 전제하에 margin을 auto로 주면된다.  

  ```
  width: 200px;
  margin: 0 auto;
  ```

### 1.3 복수의 block 요소
- 복수의 block 요소는 기본적으로 수직 정렬된다. 이것을 수평정렬하기 위해서는 정렬 대상 block 요소를 inline-block 요소로 변경한 후 부모 요소에 text-align: center;를 지정한다.
- width도 지정해 두어야 한다.

```
.container {
  text-align: center;
}
.item {
  width: 150px;
  display: inline-block;
}
```
### 1.4 FlexBox
-flexbox를 사용할 수도 있다. 정렬 대상의 부모 요소에 아래의 룰셋을 선언한다.
```
.flex-center {
  display: flex;
  justify-content: center;
}
```

## 2. 수직 정렬

### 2.1 inline/inline-block 요소

#### 2.1.1 Single line
- 정렬 대상의 부모 요소에 padding-top과 padding-bottom 프로퍼티값을 동일하게 적용한다.

- height와 line-heigth를 맞춘다 단> 1줄 짜리 텍스트 일때만 가능하다.

#### 2.1.2 Multiple lines
- 여러 줄의 텍스트의 경우, padding-top과 padding-bottom 프로퍼티값을 동일하게 적용하는 방법도 가능하다.

- vertical-align 프로퍼티를 사용한 방법도 가능하다. 이 방법은 table 속성을 사용하여야 한다.

```
.parent {
  display: table;
  height: 100px;
}
.child {
  display: table-cell;
  vertical-align: middle;
}
```

> div로 잡아서 center로 하는 것이 더 났다.

### 2.2 block 요소

#### 2.2.1 요소의 높이가 고정되어 있는 경우
- 부모 요소를 기준으로 절대 위치를 지정한다.
```
.parent {
  position: relative;
}
.child {
  position: absolute;
  top: 50%;
  height: 100px;
  /*요소의 높이(100px)의 반 만큼 위로 이동*/
  margin-top: -50px;
}
```

#### 2.2.2 요소의 높이가 불확정 상태의 경우
- 부모 요소를 기준으로 절대 위치를 지정한다.
```
.parent {
  position: relative;
}
.child {
  position: absolute;
  top: 50%;
  /*요소의 높이의 반(50%) 만큼 위로 이동*/
  transform: translateY(-50%);
}
```

## 3. 수평/수직 정렬
- 요소의 너비와 높이가 고정되어 있는 경우, 요소의 너비와 높이가 불확정 상태의 경우 모두 사용 가능한 방법이다

```
.parent {
  position: relative;
}
.child {
  position: absolute;
  top: 50%;
  left: 50%;
  /*요소의 높이/너비의 반(50%)만큼 위/왼쪽으로 이동*/
  transform: translate(-50%, -50%);
}
```