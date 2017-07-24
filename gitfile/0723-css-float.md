170723

# CSS3 float
- float property는 주로 layout을 구성하기 위해 사용되며 요소를 원하는 위치에 정렬시키는 것이 목적이다.
- float는 수평정렬이다.

> float property를 사용할 때 요소의 위치를 고정시키는 position `absolute`를 사용하면 안된다.

- none: 요소를 떠 있게 하지 않는다(default)
- right: 요소를 오른쪽으로 이동시킨다.
- left: 요소를 왼쪽으로 이동시킨다.

## 1. 정렬
- float 프로퍼티를 사용하지 않은 블록 요소들은 수직으로 정렬된다. float:left; 프로퍼티를 사용하면 왼쪽부터 정렬되고, float:right; 프로퍼티를 사용하면 오른쪽부터 정렬된다.

> float는 좌우 정렬만 가능 중앙정렬은 margin을 이용해야한다.

> block 레벨 요소에 float 프로퍼티가 선언되면 width가 `inline 요소와 같이 content에 맞게 최소화`되고 다음 요소 위에 떠 있게(부유하게) 된다.

## 2. float property 관련 문제 해결 방법

### 2.1 float 프로퍼티가 선언된 요소와 float 프로퍼티가 선언되지 않은 요소간 margin이 사라지는 문제
- float property를 선언하지 않은 요소에 `overflow: hidden`을 선언한다.
  - 만약 둘다 float property를 선언했다면 overflow를 할 필요 없다.

### 2.2 float 프로퍼티를 가진 자식 요소를 포함하는 부모 요소의 높이가 정상적으로 반영되지 않는 문제

- 자식 요소를 포함하는 부모 요소의 높이가 정상적인 값을 가지지 못하는 문제가 발생한다.
  - 부모 요소 이후에 위치하는 요소의 정렬에 문제를 발생시킨다.
  - 해결책 1 : 부모요소에 `overflow: hidden`을 선언한다.`비추천`
  - 해결책 2 : `::after` 가상요소선택자 이용한다. `이 방법을 사용하라.`
  ```
  .clearfix:after {
      content: "";
      display: block;
      clear: both;
  }
      /* or */

  selector:after {
     content: "";
    display: block;
     clear: both;
  }
  ```

  - 해결책 3 : float property대신에 `display: inline-block;`을 선언한다.
  > 좌우에 정의하지 않은 space를 신경써야한다.
  ```
    .wrapper {
      font-size: 0; /*요소간 간격을 제거*/
    }
  ```