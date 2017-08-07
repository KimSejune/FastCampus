170803

# Sass-Basics

## 1. Introduction
- Sass는 Css pre-processor로서 css의 한계와 단점을 보완하여 보다 가독성이 높고 코드의 재사용에 유리한 CSS를 생성하기 위한 CSS의 확장(extension)이다.
- Sass의 추가 기능과 유용한 도구
  - 변수의 사용
  - 조건문과 반복문
  - Import
  - Nesting
  - Mixin
  - Extend/Inheritance

- CSS와 비교하여 Sass는 아래와 같은 장점이 있다.
  - CSS보다 심플한 표기법으로 CSS를 구조화하여 표현할 수 있다.
  - 스킬 레벨이 다른 팀원들과의 작업 시 발생할 수 있는 구문의 수준 차이를 평준화할 수 있다.
  - CSS에는 존재하지 않는 Mixin 등의 강력한 기능을 활용하여 CSS 유지보수 편의성을 큰 폭으로 향상시킬 수 있다.

## 2. Install
  - node-sass -> npm install -g node-sass
  - ruby-sass

## 3. Command
- dist는 배포용으로 쓰인다.

```bash
$ cd my-project

## 특정 파일을 특정 파일 이름으로 컴파일
## Compile foo.scss to bar.css
$ node-sass foo.scss > bar.css

## 폴더 내의 모든 파일을 컴파일
## node-sass input-folder-path -o output-folder-path
$ node-sass src/sass --output dist/css

## watch src/sass/foo.scss -> dist/css  browser-sync같은거다.
$ node-sass --watch --output-style expanded src/sass/foo.scss --output dist/css 
```

### 3.3 style
- nested
  - sass 형식과 유사하게 nested된 css 파일이 생성된다. 기본값으로 옵션을 추가하지 않아도 기본 적용된다.

- expanded
  - 표준적인 스타일의 css 파일이 생성된다.
  `$ node-sass --output-style expanded src/sass --output dist/css`

- compact
  - 여러 룰셋을 한줄로 나타내는 스타일의 css 파일이 생성된다.
  `node-sass --output-style compact src/sass --output dist/css`

- compressed
  - 가능한 빈공간이 없는 압축된 스타일의 css 파일이 생성된다.
  `node-sass --output-style compressed src/sass --output dist/css`