170815

# Jq Ajax & JSON


## 7. Ajax with jQuery
- jQuery는 Ajax 요청과 응답을 위해 유용한 메소드들을 제공한다.

### 7.1 Low-Level Interface

- settings는 Ajax 요청 설정 정보로서 key/value의 쌍으로 이루어진 객체이다. 모든 settings는 옵션이다.

  - url	요청이 전송될 url	 
  - method	http 요청 방식 (default: ‘GET’)	version added: 1.9.0
  - type	method의 alias (default: ‘GET’)	1.9.0 이전 버전에서 사용
  - data	서버로 전달될 데이터	 
  - dataType	서버로부터 반환될 데이터의 type. default: Intelligent Guess (xml, json, jsonp, script, html)	 
  - async	요청 시 동기화 여부. 기본은 비동기(asynchronous) 요청 (default: true)	 
  - timeout	요청 제한 시간. 제한 시간 안에 요청이 완료되지 않으면 요청을 취소하거나 error 콜백을 호출.	  
  - jsonpCallback	JSONP 요청을 위한 콜백 함수 이름	 
  - success	요청 성공 이벤트 핸들러	 
  - error	요청 실패 이벤트 핸들러	 
  - complete	요청 완료 이벤트 핸들러	 

####  7.1.1 Load HTML

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="http://poiemaweb.com/assets/css/ajax.css">
  </head>
  <body>
    <div id='content'></div>

    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script>
    <script>
    $.ajax({
      url: "data/data.html",
      cache: false
    })
      .done(function(data, textStatus, jqXHR) {
        $("#content").html(data);
      })
      .fail(function(jqXHR, textStatus, errorThrown){
        console.log("fail: ", jqXHR);
      })
      .always(function(data, textStatus, jqXHR){
        console.log("always: ", data);
      });
    </script>
  </body>
</html>

```
- promise로 통신의 여부를 확인하는데 done(성공), fail(실패), always(후속처리의미) 실시한다.
  - data는 성공했을때 첫번째 요소로 들어온다.

### 7.1.2 Load JSON

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="http://poiemaweb.com/assets/css/ajax.css">
  </head>
  <body>
    <div id='content'></div>

    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script>

    <script>
    $.ajax({
      url: "data/data.json",
      dataType: "json"
    })
      .done(function(data) {
        var newContent = '';
        newContent += '<div id="tours">';
        newContent += '<h1>Guided Tours</h1>';
        newContent += '<ul>';
        for (var i = 0; i < data.tours.length; i++) {
          newContent += '<li class="' + data.tours[i].region + ' tour">';
          newContent += '<h2>' + data.tours[i].location + '</h2>';
          newContent += '<span class="details">' + data.tours[i].details + '</span>';
          newContent += '<button class="book">Book Now</button>';
          newContent += '</li>';
        }
        newContent += '</ul></div>';

        $("#content").html(newContent);
      })
      .fail(function(jqXHR, textStatus, errorThrown){
        console.log("fail: ", jqXHR);
      })
      .always(function(data, textStatus, jqXHR){
        console.log("always: ", data);
      });
    </script>
  </body>
</html>
```

### 7.2 Shorthand Method

####  7.2.1 jQuery.get()
- HTTP GET request를 사용하여 서버로부터 데이터를 로드한다.

```javascript
jQuery.get( url [, data ] [, success ] [, dataType ] ) // Returns: jqXHR
```

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="http://poiemaweb.com/assets/css/ajax.css">
  </head>
  <body>
    <div id='content'></div>

    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script>
    <script>
      $.get("data/data.html", function(data){
        $("#content").html(data);
      });
    </script>
  </body>
</html>

```

####  7.2.2 jQuery.getJSON()

- HTTP GET request를 사용하여 서버로부터 JSON-encoded 데이터를 로드한다.

```html
jQuery.getJSON( url [, data ] [, success ] ) // Returns: jqXHR

<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="http://poiemaweb.com/assets/css/ajax.css">
  </head>
  <body>
    <div id='content'></div>

    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script>
    <script>
      $.getJSON("data/data.json", function(data){

        var newContent = '';
        newContent += '<div id="tours">';
        newContent += '<h1>Guided Tours</h1>';
        newContent += '<ul>';
        for (var i = 0; i < data.tours.length; i++) {

          newContent += '<li class="' + data.tours[i].region + ' tour">';
          newContent += '<h2>' + data.tours[i].location + '</h2>';
          newContent += '<span class="details">' + data.tours[i].details + '</span>';
          newContent += '<button class="book">Book Now</button>';
          newContent += '</li>';
        }
        newContent += '</ul></div>';

        $("#content").html(newContent);
      });
    </script>
  </body>
</html>
```
#### 7.2.3 jQuery.getScript()

- HTTP GET request를 사용하여 서버로부터 JavaScript 파일을 로드한 후 실행한다.

```javascript
jQuery.getScript( url [, success ] ) // Returns: jqXHR
```

#### 7.2.4 jQuery.post()

- HTTP GET request를 사용하여 서버로부터 데이터를 로드한다.

```javascript
jQuery.post( url [, data ] [, success ] [, dataType ] ) // Returns: jqXHR
```

####  7.2.5 .load()

- 서버로부터 HTML 데이터를 로드하고 매치드셋에 적용한다.

```javascript
.load( url [, data ] [, complete ] ) // Returns: jQuery
```

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="http://poiemaweb.com/assets/css/ajax.css">
  </head>
  <body>
    <div id='content'></div>

    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script>
    <script>
      $("#content").load("data/data.html", function(){
        console.log("Load was performed.");
      })
    </script>
  </body>
</html>
```