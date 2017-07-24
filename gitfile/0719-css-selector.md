170719

# CSS-Selector
- , 를 사용하여서 여러개의 selector를 지정할 수 있다.
```
h1, p {color: red; }
```

## 1. Universal Selector (전체 셀렉터)

- * 를 사용하여서 모든 selector를 선택한다.
```
/* 모든 요소를 선택 */
* { color: red; }
```
## 2. Tag Selector (태그 셀렉터)

- 태그명을 사용하여서 해당되는 selector를 선택한다.
```
/* 모든 p 태그 요소를 선택 */
p { color: red; }
```

## 3. ID Selector(ID Selector)

- #id 을 사용하여서 해당 id를 가진 요소를 선택한다. 
- id attribute 값은 중복될 수 없는 유일한 값이다.
```
/* id 어트리뷰트 값이 p1인 요소를 선택 */
#p1 { color: red; }
``` 

## 4. Class Selector(클래스 셀렉터)

- .class를 통하여 일치하는 요소를 선택한다.
- class attribute 값은 중복될 수 있다.
```
/* class 어트리뷰트 값이 container인 모든 요소를 선택 */
/* color 어트리뷰트는 자식 요소에 상속된다. */
.container { color: red; }
/* not supported in IE */
#p2 { color: initial; }
```

## 5. Attribute Selector(어트리뷰트 셀렉터)

- selector[attribute] 지정된 어트리뷰트를 갖는 모든 요소를 선택한다.
```
/* a 요소 중에 href 어트리뷰트를 갖는 모든 요소 */
a[href] { color: red; }
```

- selector[attribure="value"] 지정된 어트리뷰트를 가지며 지정된 값과 어트리뷰트의 값이 일치하는 모든 요소를 선택한다.

```
/* a 요소 중에 target 어트리뷰트의 값이 "_blank"인 모든 요소 */
a[target="_blank"] { color: red; }
```

- selector[attribute~="value"] 지정된 어트리뷰트의 값이 지정된 값을 (`공백으로 분리된`) 단어로 포함하는 요소를 선택한다.

```
/* h1 요소 중에 title 어트리뷰트 값에 "first"를 단어로 포함하는 요소 */
h1[title~="first"] { color: red; }
```

- selector[attribute|="value"] 지정된 어트리뷰트의 값과 일치하거나 지정 어트리뷰트 값 뒤 연이은 `하이픈(“값-“)`으로 시작하는 요소를 선택한다.
```
/* p 요소 중에 lang 어트리뷰트 값이 "en"과 일치하거나 "en-"로 시작하는 요소 */
p[lang|="en"] { color: red; }
```

- selector[attribute^="value"] 지정된 어트리뷰트 값으로 `시작하는 요소`를 선택한다.

```
/* a 요소 중에 href 어트리뷰트 값이 "https://"로 시작하는 요소 */
a[href^="https://"] { color: red; }
```

- selector(attribute$="value") 지정된 어트리뷰트 값으로 `끝나는 요소`를 선택한다.
```
/* a 요소 중에 href 어트리뷰트 값이 ".html"로 끝나는 요소 */
a[href$=".html"] { color: red; }
```

- selector[attribute*="value"] 지정된 어트리뷰트 값을 `포함하는 요소`를 선택한다.
```
/* div 요소 중에서 class 어트리뷰트 값에 "test"를 포함하는 요소 */
div[class*="test"] { color: red; }
/* div 요소 중에서 class 어트리뷰트 값에 "test"를 단어로 포함하는 요소 */
div[class~="test"] { background-color: yellow; }
```

## 6. Combinator(복합 셀렉터)

### 6.1 후손 셀렉터(Descendant Combinator)
- space로 구분한다.
```
/* div 요소의 후손요소 중 p 요소 */
div p { color: red; }
  <div>
    <p>paragraph 1</p>
    <p>paragraph 2</p>
    <span><p>paragraph 3</p></span>
  </div>

/* 3개다 허용이다 */
```

### 6.2 자식 셀렉터(Child Combinator)
- SelectorA > SelectorB A의 모든 자식 요소 중 B와 일치하는 요소를 선택한다.
```
/* div 요소의 자식요소 중 p 요소 */
div > p { color: red; }

  <div>
    <p>paragraph 1</p>
    <p>paragraph 2</p>
    <span><p>paragraph 3</p></span> => 애만 아니다.
  </div>
```

### 6.3 동위 셀렉터(Sibling Combinator)
- 동위 셀렉터는 동위 관계에서 뒤에 위치하는 요소를 선택할 때 사용한다.

#### 6.3.1 인접 형제 셀렉터
- SelectorA + SelectorB A바로 뒤에 나오는 B만 선택된다.
```
/* p 요소의 형제 요소 중에 p 요소 바로 뒤에 위치하는 ul 요소를 선택한다. */
p + ul { color: red; }

<body>
  <div>A div element.</div>
  <ul>
    <li>Coffee</li>
    <li>Tea</li>
    <li>Milk</li>
  </ul>

  <p>The first paragraph.</p>
/* 이 부분 바로 밑에 ul만 선택 */
  <ul>
    <li>Coffee</li>
    <li>Tea</li>
    <li>Milk</li>
  </ul>

  <h2>Another list</h2>
  <ul>
    <li>Coffee</li>
    <li>Tea</li>
    <li>Milk</li>
  </ul>
</body>
```

#### 6.3.2 일반 형제 셀렉터
- SelectorA ~ SelectorB A 뒤에 위치하는 B 요소를 모두 선택한다.
```
/* p 요소의 형제 요소 중에 p 요소 뒤에 위치하는 ul 요소를 모두 선택한다.*/
p ~ ul { color: red; }

<body>
  <div>A div element.</div>
  <ul>
    <li>Coffee</li>
    <li>Tea</li>
    <li>Milk</li>
  </ul>

  <p>The first paragraph.</p>
  /* 이 밑에 ul 다 선택된다. */
  <ul>
    <li>Coffee</li>
    <li>Tea</li>
    <li>Milk</li>
  </ul>

  <h2>Another list</h2>
  <ul>
    <li>Coffee</li>
    <li>Tea</li>
    <li>Milk</li>
  </ul>
</body>
```

## 7. 가상 클래스 셀렉터
- 요소의 특정 상태에 따라 스타일을 정의할 때 사용된다.

### 7.1 링크 셀렉터, 동적 셀렉터
- 마우스가 올라와 있을 때 :hover
- 방문하지 않은 링크일 때 :link
- 방문한 링크일 때 :visited
- 클릭된 상태일 때 :active
- 포커스가 들어와 있을 때 :focus

### 7.2 UI 요소 상태 셀렉터
- 체크 상태일 때 :checked
- 사용 가능한 상태일 때 :enabled
- 사용 불가능한 상태일 때 :disabled

```
    /* input 요소가 사용 가능한 상태일 때, 
       input 요소 바로 뒤에 위치하는 인접 형제 span 요소를 선택 */
    input:enabled + span {
      color: blue;
    }
    /* input 요소가 사용 불가능한 상태일 때, 
       input 요소 바로 뒤에 위치하는 인접 형제 span 요소를 선택 */
    input:disabled + span {
      color: gray;
      text-decoration: line-through;
    }
    /* input 요소가 체크 상태일 때, 
       input 요소 바로 뒤에 위치하는 인접 형제 span 요소를 선택 */
    input:checked + span {
      color: red;
    }
```

### 7.3 구조 가상 클래스 셀렉터
- first-child 셀렉터에 해당하는 모든 요소 중 첫번째 자식인 요소를 선택한다.
- last-child 셀렉터에 해당하는 모든 요소 중 마지막 자식인 요소를 선택한다.

```
/* p 요소 중에서 첫번째 자식을 선택 */
p:first-child { color: red; }

/* p 요소 중에서 마지막 자식을 선택 */
/* body 요소의 두번째 p 요소는 마지막 자식 요소가 아니다.
body 요소의 마지막 자식 요소는 div 요소이다. */
p:last-child { color: blue; }

<body>
  <p>This paragraph is the first child of its parent (body).</p>

  <h1>Welcome to My Homepage</h1>
  <p>This paragraph is not the first child of its parent.</p>

  <div>
    <p>This paragraph is the first child of its parent (div).</p>
    <p>This paragraph is not the first child of its parent.</p>
  </div>
</body>

```

- nth-child(n) 셀렉터에 해당하는 모든 요소 중 앞에서 n번째 자식인 요소를 선택한다.
- nth-last-child(n)	셀렉터에 해당하는 모든 요소 중 뒤에서 n번째 자식인 요소를 선택한다.

> n은 0부터 시작하는 정수이다. 0과 음수는 생략되기 때문에 2n+1, 2n-1은 결과적으로 같은 수열을 생성한다.

```
    /* ol 요소의 자식 요소인 li 요소 중에서 짝수번째 요소만을 선택 */
    ol > li:nth-child(2n)   { color: orange; }
    /* ol 요소의 자식 요소인 li 요소 중에서 홀수번째 요소만을 선택 */
    ol > li:nth-child(2n+1) { color: green; }

    /* ol 요소의 자식 요소인 li 요소 중에서 첫번쨰 요소만을 선택 */
    ol > li:first-child     { color: red; }
    /* ol 요소의 자식 요소인 li 요소 중에서 마지막 요소만을 선택 */
    ol > li:last-child      { color: blue; }

    /* ol 요소의 자식 요소인 li 요소 중에서 4번째 요소 요소만을 선택 */
    ol > li:nth-child(4)    { background: brown; }

    /* ul 요소의 모든 자식 요소 중에서 뒤에서부터 시작하여 홀수번째 요소만을 선택 */
    ul > :nth-last-child(2n+1) { color: red; }
    /* ul 요소의 모든 자식 요소 중에서 뒤에서부터 시작하여 짝수번째 요소만을 선택 */
    ul > :nth-last-child(2n)   { color: blue; }
```

- :first-of-type 셀렉터에 해당하는 요소의 부모 요소의 자식 요소 중 첫번째 등장하는 요소를 선택한다.
- :last-of-type	셀렉터에 해당하는 요소의 부모 요소의 자식 요소 중 마지막에 등장하는 요소를 선택한다.
- :nth-of-type(n)	셀렉터에 해당하는 요소의 부모 요소의 자식 요소 중 앞에서 n번째에 등장하는 요소를 선택한다.
- :nth-last-of-type(n)	셀렉터에 해당하는 요소의 부모 요소의 자식 요소 중 뒤에서 n번째에 등장하는 요소를 선택한다.

```
    /* p 요소의 부모 요소의 자식 요소 중 첫번째 등장하는 p 요소 */
    p:first-of-type  { color: red; }
    /* p 요소의 부모 요소의 자식 요소 중 마지막 등장하는 p 요소 */
    p:last-of-type   { color: blue; }
    /* p 요소의 부모 요소의 자식 요소 중 앞에서 2번째에 등장하는 p 요소 */
    p:nth-of-type(2) { color: green; }
    /* p 요소의 부모 요소의 자식 요소 중 뒤에서 2번째에 등장하는 p 요소 */
    p:nth-last-of-type(2) { color: orange;}

    /* p 요소 중에서 첫번째 자식을 선택 */
    p:first-child { background: brown;}
```

### 7.4 부정 셀렉터

- :not(셀렉터)	셀렉터에 해당하지 않는 모든 요소를 선택한다.

```
/* input 요소 중에서 type 어트리뷰트의 값이 password가 아닌 요소를 선택 */

input:not([type=password]) 
{background: yellow;}
``` 

## 8. 가상 요소 셀렉터

- 특정 부분에 스타일을 적용하기 위하여 사용된다.
  - 요소 콘텐츠의 첫글자 또는 첫줄
  - 요소 콘텐츠의 앞 또는 뒤 

> 가상 요소에는 ::를 사용한다.

- ::first-letter	콘텐츠의 첫글자를 선택한다.
- ::first-line	콘텐츠의 첫줄을 선택한다. 블록 요소에만 적용할 수 있다.
- ::after	콘텐츠의 뒤에 위치하는 공간을 선택한다. 일반적으로 content 어트리뷰트와 함께 사용된다.
- ::before	콘텐츠의 앞에 위치하는 공간을 선택한다. 일반적으로 content 어트리뷰트와 함께 사용된다.
- ::selection	드래그한 콘텐츠를 선택한다. iOS Safari 등 일부 브라우저에서 동작 않는다.