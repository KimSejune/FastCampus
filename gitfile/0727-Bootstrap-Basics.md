170727

# Bootstrap-Basics

## 1.Introduction
- Bootstrap은 빠르고 간편한 반응형 웹 디자인(responsive web design)을 위한 open-source front-end framework이다.
- mobile-first로 구성된다.

### 1.1 코드재사용
- 중복을 제거하여서 코드를 수정할 경우에 1번만 수정가능하게 한다.

### 1.2 Framework의 장점
- Framework란 1. 뼈대, 2. 틀, 3. 체제, 체계의 의미를 가진다.
- 팀원간의 대화가 잘된다.

### 1.3 Bootstrap의 장점
- Easy to use : HTML과 CSS에 대한 기본 지식이 있다면 쉽게 사용할 수 있다.
- Responsive features : 스마트폰, 테블릿, 데스크탑에 적합한 responsive CSS를 제공한다.
- Mobile-first approach : Bootstrap 3부터 mobile-first style을 기본으로 지원한다.
- Browser compatibility : 대부분의 브라우저(Chrome, Firefox, Internet Explorer, Safari, Opera)를 지원한다.

## 2. Bootstrap 설치
- Bootstrap을 사용하기 위한 방법은 Bootstrap을 다운로드 받은 후 자신의 환경에 위치시킨 후 사용하는 방법과 CDN(Content Delivery Network)을 사용하는 방법이 있다. 물론 npm을 통해 설치하는 방법도 가능하다.

### 2.1 Bootstrap Download

### 2.2 Bootstrap CDN
```
<!-- Latest compiled and minified CSS -->
<link rel="stylesheet" href="http://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css">

<!-- jQuery library -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.0/jquery.min.js"></script>

<!-- Latest compiled JavaScript -->
<script src="http://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>
```
### 2.3 npm
- 프로젝트 폴더로 이동한 후, npm 명령어를 사용하여 bootstrap을 설치한다.
```
$ cd <project-folder>
## package.json이 존재하지 않는 경우
$ npm init --y
$ npm install --save bootstrap
```
## 3. Browser support
- Bootstrap은 중요 플랫폼의 기본 브라우저의 최신 버전을 지원한다. 단, Opera, Opera Mobile, UC Browser Mini, Amazon Silk는 지원하지 않는다.

## 4. Hello World
- javascript 파일을 2개 포함시켰다. 하나는 bootstrap의 자바스크립트 파일이고 또 다른 하나는 bootstrap이 사용할 jQuery이다. jQuery는 bootstrap의 자바스크립트가 사용하므로 bootstrap 자바스크립트 파일 로드 전에 로드하여야 한다. 그리고 body tag가 끝나기 직전 javascript 파일을 로드하였는데 이 방법은 웹페이지 로딩 속도 향상에 효과적이다.