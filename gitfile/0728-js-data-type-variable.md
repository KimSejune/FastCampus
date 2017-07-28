170728

# Javascript Data type & Variable

- 자료형은 데이터의 성질을 나타낸다.
- javascript 영역이 입력되는 값을 판단하여서 메모리에 저장한다.
- JavaScript는 `동적 타이핑 언어`로 변수의 Type annotation이 필요없이 값이 `할당되는 과정에서 자동으로 자료형이 결정`된다.
- 할당되기 전에는 undefined형이다.
- `typeof`를 통하여 변수의 type을 알 수 있다.

```
var str  = 'Hello';
var num  = 1;
var bool = true;

var foo = 'string';
console.log(typeof foo); // string
foo = 1;
console.log(typeof foo); // number

```

## 1.Data Type (자료형)
- 기본 자료형
  - Boolean
  - null
  - undefined
  - Number
  - String
  - Symbol(ECMAScript 6 추가)

- 객체형
  - object

### 1.1 Primitive Data Type (기본자료형)
- 기본자료형의 값은 변경 불가능한 값이다.

#### 1.1 Boolean
- true, false 두가지의 값을 가질 수 있다.
  - 비어있는 문자열, null, undefined, 0은 false로 간주된다.

#### 1.1.2 null
- 값을 할당한 이후에 그 값의 관계를 끊는다.
- JavaScript는 case-sensitive(대소문자구분)하므로 null은 항상 소문자로 작성해야한다.

> var foo = null; 을하면 typeof가 null이 나와야하는데 object가 나온다 설계상의 오류이다. 즉 typeof로 check하면 안되고 (foo === null)로 체크해야한다.

#### 1.1.3 undefined
- 값을 할당하지 않은 변수는 undefined값을 가진다.

```
var foo;
console.log(foo); // undefined

foo = {
  name: 'Lee',
  gender: 'male'
}
console.log(foo.bar); // bar가 존재하지 않아서 undefined가 나온다. 

```