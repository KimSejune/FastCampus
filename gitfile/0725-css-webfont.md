170725

# CSS3 webfont
- local에 font가 존재하지 않아도 서버에서 font를 제공한다
  - 시간이 더 걸린다는 단점이 발생한다.
- 예전에는 포토샵으로 이미지로 만들었었다.
  - SEO(검색)이 안된다는 단점이 발생한다.

## 1. CDN(Content Delivery Network)링크 방식
- 웹폰트를 사용하는 방법 중 가장 간단한 방법이다.
- 회사에서 font를 보관하고 있다가 연결을 해준다.  
[Google Font](https://fonts.google.com/)

```
@import url(http://fonts.googleapis.com/earlyaccess/nanumgothic.css);

* { font-family: 'Nanum Gothic', sans-serif; }
```

> import는 css내에서 다른 css를 불러오는 것이다.

## 2. 서버 폰트 로딩 방식
- 나의 폰트를 내가 가지고 있다가 요청하면 준다.
  - 구현은 복잡하지만 속도는 빠르다

- @font-face규칙으로 폰트를 등록하고 font-family porperty로 폰트를 선택하여 사용할 수 있다.

```
/* IE 9~ & all browsers */
@font-face {
  font-family: myFontName;
  src: url("myFont.woff");
}

* { font-family: myFontName, sans-serif; }
```

- 밑의 방법은 검증된 웹폰트 사용 방법이다.
```
@font-face {
  font-family:"Nanum Gothic";
  src:url("NanumGothic.eot"); /* IE 9 호환성 보기 모드 대응 */
  src:local("☺"),             /* local font 사용 방지. 생략 가능 */
      url("NanumGothic.eot?#iefix") format('embedded-opentype'), /* IE 6~8 */
      url("NanumGothic.woff") format('woff'); /* 표준 브라우저 */
}

* { font-family: "Nanum Gothic", sans-serif; }
```
- 영문과 한글을 혼용하는 경우 먼저 영문 폰트, 그 다음 한글 폰트를 지정하여야 한다. 한글 폰트부터 지정하면 영문에도 한글 폰트가 지정된다.

```
font-family: 'Lora', 'KoPub Batang', 'Times New Roman', serif;
```