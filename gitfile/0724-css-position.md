170724

# CSS3 Position(요소의 위치를 지정하는 레이아웃의 기본)

## 1. Position Property
- Position Property는 요소의 위치를 정의한다. top, bottom, left, right property와 함께 사용하여 위치를 지정한다.
> 부모의 좌상단에 붙는다.

### 1.1 static(기본위치)
- static은 position property의 기본값이다.
- 배치 순서는 위에서 아래로, 왼쪽에서 오른쪽으로 순서에 따라서 배치되며 부모요소내에 자식 요소로서 존재할 때는 `부모 요소의 위치를 기준으로 배치된다.`
- 이미 설정된 position을 무력화하기 위해 사용될 수 있다.
> position을 무력화하기 위해 사용하면 좋다. property를 줘도 무시한다.

### 1.2 relative(상대위치)
- 기본 위치를 기준으로 좌표 property(top, bottom, left, right)를 사용하여 위치를 이동시킨다.
-  static을 선언한 요소와 relative를 선언한 요소의 차이점은 좌표 Property의 동작 여부 뿐이며 그외는 동일하게 동작한다.
> width를 따로 설정하지 않으면 부모 요소와 동일한 값이 적용된다. `무조건 부모 기준이다`.

### 1.3 absolute(절대위치)
- 부모 요소 또는 가장 가까이 있는 조상 요소(static 제외)를 기준으로 좌표 property만큼 이동한다. 
- `relative, absolute, fixed`가 선언되어 있는 `부모 또는 조상 요소를 기준`으로 위치가 결정된다.
- 부모 또는 조상 요소가 `static`인 경우, `document body를 기준`으로 하여 좌표 프로퍼티대로 위치하게 된다.
- 따라서 부모 요소를 배치의 기준으로 삼기 위해서는 부모 요소에 relative를 정의하여야 한다.
- absolute 선언 시, block 레벨 요소의 width는 inline 요소와 같이 content에 맞게 변화되므로 `적절한 width를 지정`하여야 한다.

> relative 프로퍼티와 absolute 프로퍼티의 차이점
relative 프로퍼티는 기본 위치(static으로 지정되었을 때의 위치)를 기준으로 좌표 프로퍼티(top, bottom, left, right)을 사용하여 위치를 이동시킨다. 따라서 `무조건 부모를 기준으로 위치`하게 된다.
absolute 프로퍼티는 부모에 static 이외의 position 프로퍼티이 지정되어 있을 경우에만 부모를 기준으로 위치하게 된다. 만일 부모, 조상이 모두 static 프로퍼티인 경우, document body를 기준으로 위치하게 된다.
따라서 `absolute 프로퍼티 요소는 부모 요소의 영역을 벗어나 자유롭게 어디든지 위치할 수 있다.`

> `나를 움직이고 싶다면 부모에 relative를 주고 나를 absolute를 준다.` 

### 1.4 fixed(고정위치)
- 스크롤이 되더라도 화면에서 사라지지 않고 항상 같은 곳에 위치한다.
- fixed선언시, block 요소의 `width는 inline 요소와 같이 content에 맞게 변화되므로 적절한 width를 지정`하여야 한다.

## 2. z-index property
- z-index property에 큰 숫자값을 지정할 수록 화면 전면에 출력된다.

## 3. overflow property
- 자식 요소가 부모 요소의 영역을 벗어났을 때 처리 방법을 정의한다.
  - visible(default) : 영역이 벗어난 부분을 표시한다.
  - hidden : 영역을 벗어난 부분을 잘라내어 보이지 않게 한다.
  - scroll : 영역을 벗어난 부분이 없어도 스크롤 표시한다.
  - auto : 영역을 벗어난 부분이 있을때만 스크롤 표시한다.

  > overflow:auto; 는 margin 상쇄의 역할도 한다.
