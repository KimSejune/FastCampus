170803

# Sass-SassScript

## 1. Data Type
- 변수를 선언시 $를 붙이고 변수명을 쓰고 : 뒤에다가 값을 쓴다.
  - 숫자형
  - 문자열
  - 컬러
  - boolean
  - null
  - list
  - map : JSON과 유사한 방식으로 map-get 함수를 사용하여 원하는 값은 추출할 수 있다.


```css
// map
$foundation-palette: (
  primary: #E44347,
  mars: #D7525C,
  saturn: #E4B884,
  neptune: #5147D7
);

.mars {
  color: map-get($foundation-palette, mars); 
}

// => .mars { color: #D7525C; }

```

## 2. 변수

```css
$width: 960px;

header {
  width: $width;
  margin: 0 auto;
}

#main {
  width: $width;
  margin: 20px auto;
}

footer {
  width: $width;
  margin: 0 auto;
}
```
- sass를 compile하면 아래와 같이 바뀐다.

```css
header {
  width: 960px;
  margin: 0 auto; }

#main {
  width: 960px;
  margin: 20px auto; }

footer {
  width: 960px;
  margin: 0 auto; }
```
- 어떤것을 변수화 할 것인지 생각해두어야하고 sass변수를 맨앞에다가 가져다 두어야 편하다.

## 3. 변수의 Scope
- 전역변수와 지역변수를 알 수 있다.

```css
$width: 960px; // global variable

header {
  width: $width;
  margin: 0 auto;
}

#main {
  $color: #333; // local variable
  width: $width;
  margin: 20px auto;
  section {
    p {
      color: $color;

      a:link {
        color: $color;
      }
    }
  }
}

footer {
  width: $width;
  margin: 0 auto;
  color: $color;   /*error가 발생한다.*/
}
```

- 지역변수를 전역변수로 하는방법은 뒤에 !global을 하면된다.

## 4. 연산자

### 4.1 숫자 연산자
- +,-,*,/,%,==,!=
 - 상대적인값은 더할 수 없다.
 - 왼쪽을 기준으로 계산한다.
   - em은 해당요소에 적용된 사이즈를 바탕으로 계산된다.
   - %는 부모의 사이즈를 바탕으로 계산된다.
   - rem은 html에 적용된 사이즈를 바탕으로 계산되며 단) 적용이 안되어 있으면 기본값인 16으로 적용된다.
 - 절대값과 상대값을 계산할 일이 있다면 calc함수를 사용한다.
```css
  #foo {
    width: calc(25% - 5px);
  }
```
- Sass의 / 연산자를 사용하기 위해서는 몇가지 조건이 필요하다.
  - 변수에 대해 사용
  - 괄호 내에서 사용
  - 다른 연산의 일부로서 사용

```css
p {
  // font와 border-radius의 '/'는 CSS문법에 맞는 표현이므로 연산되지 않는다.
  font: italic bold 12px/30px Georgia, serif;
  // 타원형 둥근 모서리
  border-radius: 10px 20px/20px;

  $width: 1000px;

  width: $width / 2;            // 변수에 대해 사용 →　width: 500px;
  height: (500px / 2);          // 괄호 내에서 사용 →　height: 250px;
  margin-left: 5px + 8px / 2px; // 다른 연산의 일부로서 사용 →　margin-left: 9px;
}
```

- 변수를 CSS의 /와 함께 사용하고자 하는 경우 `#{}(Interpolation)를 사용한다.`
  - 연산을 하고싶지 않을때 사용한다.

```css
p {
  $font-size: 12px;
  $line-height: 30px;
  font: #{$font-size}/#{$line-height};  // 12px/30px
}
```

### 4.2 컬러 연산자
- 모든 산술 연산자는 컬러 값에도 사용할 수 있다.

```css
p {
  color: #010203 + #040506;
  // R: 01 + 04 = 05
  // G: 02 + 05 = 07
  // B: 03 + 06 = 09
  // => #050709
}

p {
  color: #010203 * 2;
  // R: 01 * 2 = 02
  // G: 02 * 2 = 04
  // B: x03 * 2 = 06
  // => #020406
}

p {
  color: rgba(255, 0, 0, 0.75) + rgba(0, 255, 0, 0.75);
  // alpha 값은 연산되지 않는다 opacity 계산 안된다.
  // color: rgba(255, 255, 0, 0.75);
}

```

- alpha 값은 연산되지 않는다. alpha 값의 연산을 위해서는 `opacify 함수 또는 transparentize 함수를 사용한다.`
  - opacify 함수: 첫번째 argument의 alpha값에 두번째 argument를 `더해` 불투명도를 증가시킨다.(더 불투명해진다)
  - transparentize 함수: 첫번째 argument의 alpha값에 두번째 argument를 `빼서` 불투명도를 감소시킨다.(더 투명해진다)

```css
$translucent-red: rgba(255, 0, 0, 0.5);

p {
  color: opacify($translucent-red, 0.3);
  // => color: rgba(255, 0, 0, 0.8);

  background-color: transparentize($translucent-red, 0.25);
  // => background-color: rgba(255, 0, 0, 0.25);
}
```

### 4.3 문자열 연산자
- `+` 연산자는 자바스크립트와 같이 문자열을 연결할 수 있다.
- 따옴표가 있는 문자열과 없는 문자열을 함께 사용하는 경우,  `좌항의 문자열을 기준으로 따옴표를 처리한다.`

```css
p:before {
  content: "Foo " + Bar;        // "Foo Bar"
  font-family: sans- + "serif"; // sans-serif
}
```

### 4.4 불린 연산자
- if
- @if

### 4.5 list 연산자
- built-in function 참고

## 5. 함수
- built-in function 참고

## 6. Interpolation: #{}
- 인터폴레이션은 변수의 값을 문자열 그대로 삽입한다
- #{}을 사용하면 프로퍼티값은 물론 셀렉터와 프로퍼티명에도 사용할 수 있다.

```css
$name: foo;
$attr: border;

p.#{$name} {            // p.foo
  #{$attr}-color: blue; // border-color: blue;
}

.someclass {
  $font-size: 12px;
  $line-height: 30px;
  // 연산의 대상으로 취급되지 않도록
  font: #{$font-size} / #{$line-height}; // 12px / 30px
}
```

## 7. Ampersand(&)
- &는 부모요소를 참조하는 셀렉터이다.

```css
a {
  color: #ccc;

  &.home {
    color: #f0f;
  }

  &:hover {
    text-decoration: none;
  }

  /* & > span (X) */
  > span {
    color: blue;
  }

  span {
    color: red;
  }
}
```

위 Sass의 컴파일 결과는 아래와 같다.
```css
a {
  color: #ccc;
}

a.home {
  color: #f0f;
}

a:hover {
  text-decoration: none;
}

a > span {
  color: blue;
}

a span {
  color: red;
}
```

## 8. !default
- !default flag는 할당되지 않은 변수의 초기값을 설정한다.

```css

$content: null;
$content: "Non-null content" !default;

#main {
  content: $content; // "Non-null content"
}
```

- 이미 값이 할당되어 있는 변수에 !default flag를 사용하면 적용되지 않는다.
  - 이러한 특성은 `partial에 매우 유용하다.`
  - compile을 할 파일들을 합친뒤에 한번에 compile한다.

```css
// font.scss
$font-size: 16px !default;
$line-height: 1.5 !default;
$font-family: "Helvetica Neue", "Helvetica", "Arial", sans-serif !default;

body {
  font: #{$font-size}/$line-height $font-family;
}
```

```css
// main.scss
$font-family: "Lucida Grande", "Lucida Sans Unicode", sans-serif;

@import "font";
```
- !default를 사용하게되면 font-family부분을 실행하면 그 부분을 사용하지 않겠다는거다.
- _를 붙인것과 안붙인것의 차이
  - _붙이면 compile을 할 파일들을 합친뒤에 한번에 compile한다.
  - 안붙이면 각자 compile후에 붙인다.
