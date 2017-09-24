170814

# Js RESTAPI

REST의 기본 원칙을 성실히 지킨 서비스 디자인을 “RESTful”이라고 표현한다.  

## 1. REST API 중심 규칙

URI는 자원을 표현하는 데에 집중하고 행위에 대한 정의는 HTTP Method를 통해 하는 것이 REST한 API를 설계하는 중심 규칙이다.  

1. URI는 정보의 자원을 표현해야 한다.   
리소스명은 동사보다는 명사를 사용한다. URI는 자원을 표현하는데 중점을 두어야 한다.  

```bash
# good
GET /books/1
```

> URI = 통합 자원 식별자(Uniform Resource Identifier, URI)는 인터넷에 있는 자원을 나타내는 유일한 주소이다.  

2. 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE 등)으로 표현한다.

```bash
# good
DELETE /books/1
```

## 2. HTTP Method

<table>
  <tr>
    <th>Method</th>
    <th>Action</th>
    <th>역할</th>
  </tr>
  <tr>
    <td>GET</td>
    <td>index/retrieve</td>
    <td>모든/특정 리소스를 조회</td>
  </tr>
  <tr>
    <td>POST</td>
    <td>create</td>
    <td>리소스를 생성</td>
  </tr>
  <tr>
    <td>PUT</td>
    <td>update</td>
    <td>리소스를 갱신</td>
  </tr>
  <tr>
    <td>DELETE</td>
    <td>delete</td>
    <td>리소스를 삭제</td>
  </tr>        
</table> 

## 3. REST API의 구성
REST API는 자원(Resource), 행위(Verb), 표현(Representations)의 3가지 요소로 구성된다.  

<table>
  <tr>
    <th>구성 요소</th>
    <th>내용</th>
    <th>표현 방법</th>
  </tr>
  <tr>
    <td>Resource</td>
    <td></td>
    <td>HTTP URI</td>
  </tr>
  <tr>
    <td>Verb</td>
    <td>자원에 대한 행위</td>
    <td>HTTP Method</td>
  </tr>
  <tr>
    <td>Representations</td>
    <td>자원에 대한 행위의 내용</td>
    <td>HTTP Message Pay Load</td>
  </tr>
</table>

## 4. Rest API의 Example

### 4.1 PUT

books 리소스에서 특정 책을 조회(retrieve)한다.

```js
var req = new XMLHttpRequest()
req.open('GET', '/books/1')
req.send()
```

### 4.2 POST

books 리소스에 책을 생성한다.  

```js
var req = new XMLHttpRequest()
req.open('POST', '/books')
req.setRequestHeader('Content-type', 'application/json')
req.send(JSON.stringify({
  title: "ES6",
  author: "kim"
}))

```

### 4.3 PUT

books 리소스의 책의 타이틀을 “ES6”에서 “ECMAScript6”로 갱신한다.

```js
var req = new XMLHttpRequest()
req.open('PUT', 'books/1')
req.setRequestHeader('Content-type', 'application/json')
req.send(JSON.stringify({
  title:'ecamscript6',
  author:'kim'
}))
```

### 4.4 DELETE
books 리소스에서 책을 삭제한다.

```js
var req = new XMLHttpRequest()
req.open('DELETE', 'books/1')
req.send()
```