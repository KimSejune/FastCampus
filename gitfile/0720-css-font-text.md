2017.07.20

# CSS3 Font & Text
## 1. font-size 
- text의 크기를 지정한다.

## 2. font-family property
- pc에 특정 font가 존재해야지 적용이된다.
  - 기본으로 존재하는 font를 넣어준다.
```
    .serif {
      font-family: "Times New Roman", Times, serif;
    }

    .sans-serif {
      font-family: Arial, Helvetica, sans-serif;
    }

    .monospace {
      font-family: "Courier New", Courier, monospace;
    }
```

## 3. font-style / font-weight property
- font-style은 이탤리체의 지정, font-weihgt은 폰트 굵기 지정에 사용한다.

## 4. font-shorthand
- font : font-style(optional) font-variant(optional) font-weight(optional) font-size(mandatory) line-height(optional) font-family(mandatory)
  - optional : 생략가능, mandatory : 생략불가

```
/* size | family */
font: 2em "Open Sans", serif;

/* style | size | family */
font: italic 2em "Open Sans", sans-serif;

/* style | variant | weight | size/line-height | family */
font: italic small-caps bolder 16px/1.2 monospace;

/* style | variant | weight | size/line-height | family */
/* font-variant: small-caps; 소문자를 대문자로 만든다. 단 크기는 일반 대문자에 비해 더 작다.*/
font: italic small-caps bolder 16px/3 cursive;
```


## 5. line-height property
- text의 행간을 지정한다. text 수직 정렬에도 응용되어 사용한다.
    - default : 110% ~ 120% 줄어들 수 록 서로 점점 붙는다.

`수직 중앙 정렬 하는 방법이다.`
```
    .button {
      width: 150px;
      height: 70px;
      background-color: #FF6A00;
      border-radius: 30px;
      box-shadow: 5px 5px 5px #A9A9A9;
    }
    .button > a {
      display: block;
      font: italic bold 2em/70px Arial, Helvetica, sans-serif;
      text-decoration: none;
      text-align: center; 
    }
``` 
> `부모요소의 height와 같게 해야한다.`

## 6. letter-spacing property
- 글자간 사이의 간격을 지정한다.

## 7. text-align property
- 텍스트의 수평 정렬을 정의한다 
```
text-align: center;
```
> inline요소를 정렬할려면 display를 바꿔줘야한다.

## 8. text-decoration property
- link의 underline을 제거하거나 텍스트에 underline, overline, line-through를 추가할 수 있다.

## 9. white-space property
- 공백(space), 들여쓰기(tab), 줄바꿈(line break)을 의미하며 기본 동작을 제어한다.

## 10. text-overflow property
- 부모 영역을 벗어난 wrapping(자동줄바꿈)이 되지 않은 텍스트의 처리 방법을 정의한다.
    - overflow property에 반드시 'visible' 이외의 값이 지정되어 있어야 한다.
    - width property가 지정되어 있어야하며, block 요소로 변경해야한다.
    - 자동 줄바꿈을 방지하려면 white-space property를 nowrap으로 설정한다.

- clip : 영역의 벗어난 부분을 표시하지 않는다.(default)
- ellipsis : 영역을 벗어난 부분을 잘라내어 보이지 않게 하고 말 줄임표(...)를 표시한다.
- <string> : 값으로 지정한 임의의 문자열을 출력한다. firefox만 지원한다.

## 11. word-wrap property
- 한단어의 길이가 길어서 부모 영역을 벗어난 텍스트의 처리 방법을 정의한다.
```
word-wrap: break-word; 를 사용해서 넘어간 text를 맞춰준다.
```
## 12. word-break property
- word-wrap property는 단어를 어느 정도 고려해서 개행하지만 word-break는 단어를 고려하지 않고 부모 영역에 맞추어 강제 개행한다.  
```
word-break: break-all;
```