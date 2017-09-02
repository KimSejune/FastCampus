170901

# Data Structure

## Data Structures in Web Development

Array & Hash(Dictionary) - indexing post

```json
in RDB
[articleId, title, body, userId, view]
[{
	userId: 1,
	articleId: 1,
	view: 100,
	title: "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
	body: "quia et suscipit suscipit recusandae consequuntur expedita et cum reprehenderit molestiae ut ut quas totam nostrum rerum est autem sunt rem eveniet architecto"
}, 
...

]
```

## Data Structures in Web Development

Tree - DOM rendering performance, reply  

```html
<html>
<head></head>
<body>
<h1></h1>
<p></p>
</body>
</html>
```

- div로 영역을 나누어서 묶으면 더욱 빠른 접근이 가능하다.

## Data Structures in Web Development

- Binary Tree Search  
  - Queue(BFS, Breadth First Search)  = 너비우선탐색
  - Stack(DFS, Depth First Search) = 깊이우선탐색

## We'll Learn about..

- Stack  
- Queue  
- Linked-list  
- Tree  

## Stack

A stack is an abstract data type that serves as a collection of elements, with two principal operations.  

- push: which adds an element to the collection (값을 add)
- pop: which removes the most recently added element that was not yet removed (값을 remove)

`LIFO` = Last In First Out

## pusj & pop & peek & isEmpty & size & clear & print

```js
function Stack(){
  var items = [];

  this.push = function(element){
    return items.push(element);
  };

  this.pop = function(){
    return items.pop();
  };

  this.peak = function(){
    return items[items.length-1];
  };

  this.isEmpty = function(){
    return items.length === 0;
  };

  this.size = function(){
    return items.length;
  };

  this.clear = function(){
    items = [];
  };

  this.print = function(){
    console.log(items.toString());
  };
}
```

- 10진수를 2진수로 변경하는 함수 구현

```js
function binaryConverter(x) {
  var stack = [];
  var y = 0;
  var last = '';
  while (x > 0) {
    y = Math.floor(x % 2);
    stack.push(y);
    x = Math.floor(x / 2);
  }

  while (stack.length > 0) {
    last += stack.pop();
  }
  return console.log(last);
}

binaryConverter(10);
```

##  Queue
들어온 순서대로 나가게 도와주는 자료구조이다. 선입선출(FIFO)


## Enqueue & Dequeue

- Enqueue: addition of entities to the rear terminal position  
- Dequeue: removal of entities from the front terminal position  


## Enqueue & Dequeue & front & isEmpty & clear & size & print

```js
function Queue() {
	//properties, methods
	var items = [];

	this.enqueue = function(element) {
		items.push(element);
	};
	this.dequeue = function() {
		return items.shift();
	};

	this.front = function() {
		return items[0];
	};
	this.isEmpty = function() {
		return items.length == 0;
	};

	this.clear = function() {
		items = [];
	};
	this.size = function() {
		return items.length;
	};
	this.print = function() {
		console.log(items.toString());
	};
}
```


## Gulp

## Task runner

- 매우 귀찮은 루틴한 작업들을 자동화 할 수 있는 툴  
- 현재 2735 + a 개의 패키지가 존재  
  - 따라서 필요한 기능을 골라 설치할 필요가 있음!!  


## task flow

- 코드작성 - JS test(jshint) - JS Minify - JS Merge(concat) - CSS Minify - CSS Merge - 결과물

```bash
$ npm install gulp --global
$ npm install gulp --save-dev
$ touch gulpfile.js

var gulp = require("gulp");

//hello라는 gulp task를 등록
gulp.task("hello", function () {
	return console.log("hello gulpworld");
});

$ gulp hello
```

## gulp 기본 문법

- gulp.task : gulp의 작업단위  
- gulp.src : gulp 실행의 대상  
- gulp.dest : gulp 실행 후 목적지  
- gulp.watch : 변화 감지 후 자동 실행  


## 기본값 설정하기

```git
$ gulpfile.js

var gulp = require("gulp");

//hello라는 gulp task를 등록
gulp.task("hello", function () {
	return console.log("hello gulpworld");
});

gulp.task("default", ["hello"]);

$ gulp
```
- gulp 만 실행하면 default랑 다른 task들이 실행된다.
- gulp hello 만 실행하면 이것만 실행된다.

## 우선순위 설정하기

```git
$touch gulpfile.js

var gulp = require("gulp");

//hello라는 gulp task를 등록
gulp.task("hello", function () {
	return console.log("hello");
});

gulp.task("gulpworld", ["hello"], function () {
	return console.log("gulpworld");
});

gulp.task("default", ["gulpworld"]);

$ gulp

```

## 자주쓰는 목적지 설정하기

```js
var publicPath = {
	src  : './public/src/',
	dest : './public/dist/'
};
```
[uglify(gulp-uglify)](https://github.com/terinjokes/gulp-uglify): js uglify

- npm install --save-dev gulp-uglify
- npm install --save-dev pump
```js
gulp.task("uglify", function(){
	pump([
		gulp.src(publicPath.src + 'js/uglify.js'),
		uglify(),
		gulp.dest(publicPath.dest + 'js/')
	]);
});
```
