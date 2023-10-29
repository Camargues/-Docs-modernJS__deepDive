# 6장 - 데이터 타입

- 자바스크립트의 모든 값은 데이터 타입을 갖는다.

| 구분 | 데이터 타입 | 설명 |
| --- | --- | --- |
| 원시 타입 | 숫자(number) 타입 | 숫자. 정수와 실수 구분 없이 하나의 숫자 타입만 존재 |
|  | 문자열(string) 타입 | 문자열 |
|  | 불리언(boolean) 타입 | 논리적 참(true)과 거짓(false) |
|  | undefined 타입 | var 키워드로 선언된 변수에 암죽적으로 할당되는 값 |
|  | null 타입 | 값이 없다는 것을 의도적으로 명시할 때 사용하는 값 |
|  | 심벌(symbol) 타입 | ES6에서 추가된 7번째 타입 |
| 객체 타입 |  | 객체, 함수, 배열 등 |

## 6.1 숫자 타입

- 자바스크립트는 하나의 숫자 타입만 존재하며, 모든 수를 실수로 처리한다

```jsx
// 모두 숫자 타입이다.
var integer = 10;   // 정수
var double = 10.12; // 실수
var negative = -20; // 음의 정수

var binary = 0b01000001; // 2진수
var octal = 0o101;       // 8진수
	var hex = 0x41;          // 16wlstn

// 표기법만 다를 뿐 모두 같은 값이다.
console.log(binary); // 65
console.log(octal);  // 65
console.log(hex);    // 65
console.log(binary === octal); // true
console.log(octal === hex);    // true

// 숫자 타입은 모두 실수로 처리된다.
console.log(1 === 1.0); // true
console.log(4 / 2); // 2
console.log(3 / 2); // 1.5

// 숫자 타입의 세 가지 특별한 값
console.log(10 / 0);       // Infinity
console.log(10 / -0);      // -Infinity
console.log(1 * 'String'); // Nan

// 자바스크립트는 대소문자를 구별한다
var x = nan; // ReferenceError: nan is not defined
```

## 6.2 문자열 타입

- 문자열(string) 타입은 텍스트 데이터를 나타내는데 사용한다. 유니코드 문자(UTF-16)의 집합으로 전 세계 대부분의 문자를 표현할 수 있다.
- 문자열은 작은따옴표(’ ’), 큰따옴표(” “), 백틱(\` \`)으로 텍스트를 감싼다.

```jsx
// 문자열 타입
var string;
string = '문자열'; // 작은따옴표
string = "문자열"; // 큰따옴표
string = `문자열`; // 백틱(ES6)
string = '작은 따옴표로 감싼 문자열 내의 "큰따옴표"는 문자열로 인식된다.';
string = "큰따옴표로 감싼 문자열 내의 '작은따옴표'는 문자열로 인식된다.";

// 따옴표로 감싸지 않는 hello를 식별자로 인식한다.
var string = hello; // ReferenceError: hello is not defined
```

## 6.3 템플릿 리터럴

> `템플릿 리터럴(template literal)`은 `멀티라인 문자열(multi-line string)`, `표현식 삽입(experssion interpolation)`, `태그드 템플릿(tagged template)`등 편리한 문자열 처리 기능을 제공하며, 백틱(` `)을 사용해 표현한다.
> 

```jsx
var template = `Template literal`;
console.log(template); // Template literal
```

### 6.3.1 멀티라인 문자열

- 일반 문자열 내에서는 줄바꿈(개행)이 허용되지 않는다. 일반 문자열 내에서 줄바꿈 등의 `공백(white space)`을 표현하려면 백슬래시(\)로 시작하는 `이스케이프 시퀀스(escape sequence)`를 사용해야 한다.

| 이스케이프 시퀀스 | 의미 |
| --- | --- |
| \0 | Null |
| \b | 백스페이스 |
| \f | 폼 피드(Form Feed): 프린터로 출력 할 경우 다음 페이지의 시작 지점으로 디오한다. |
| \n | 개행(LF Line Feed): 다음 행으로 이동 |
| \r | 개행(CR Carriage Return): 커서를 처음으로 이동 |
| \t | 탭(수평) |
| \v | 탭(수직) |
| \uXXXX | 유니코드 |
| \’ | 작은따옴표 |
| \” | 큰따옴표 |
| \\ | 백슬래시 |

```jsx
var template = '<ul>\n\t<li><a href="#">Home</a></li>\n</ul>';

console.log(template);

// 출력 결과
<ul>
	<li>
		<a href="#">Home</a>
	</li>
</ul>

var template = `<ul>
	<li>
		<a href="#">Home</a>
	</li>
</ul>`;

console.log(template);

// 출력 결과
<ul>
	<li>
		<a href="#">Home</a>
	</li>
</ul>
```

### 6.3.2 표현식 삽입

- 문자열은 문자열 연산자 +를 사용해 연결할 수 있다. + 연산자는 피연사자 중 하나 이상이 문자열인 경우 문자열 연결 연산자로 동작한다.

```jsx
var first=. 'Ung-mo';
var last = 'Lee';

// ES5: 문자열 연결
console.log('My name is ' + first + ' ' + last + '.'); // My name is Ung-mo Lee.
```

- 템플릿 리터럴 내에서는 표현식 삽입(expression interpolation)을 통해 문자열을 삽입할 수 있다.

```jsx
var first = 'Ung-mo';
var last = 'Lee';

// ES6: 표현식 삽입
consoel.log(`My name is ${first} ${last}.`); // My name is Ung-mo Lee.

// 표현식의 평가 결과가 문자열이 아니더라도 문자열로 타입이 강제 변환되어 삽입된다.
console.log(`1 + 2 = ${1 + 2}`); // 1 + 2 = 3

// 표현식 삽입은 템플릿 리터럴이 아닌 일반 문자열에서 사용하면 문자열로 취급된다.
console.log('1 + 2 = ${1 + 2)'); // 1 + 2 = ${1 + 2}
```

## 6.4 불리언 타입

- 불리언 타입의 값은 논리적 참, 거짓을 나타내는 true와 false뿐이다.

```jsx
var foo = true;
console.log(foo); // true

foo = false;
console.log(foo) // false
```

## 6.5 undefined 타입

- undefined 타입의 값은 undefined가 유일하다.
- 변수 선언 후 값을 할당하지 않은 변수를 참조하면 undefined가 반환된다.

```jsx
var foo;
console.log(foo); // undefined
```

## 6.6 null 타입

- null 타입의 값은 null이 유일하다.

```jsx
var foo = 'Lee';

// 이전 참조를 제거. foo 변수는 더 이상 'Lee'를 참조하지 않는다.
// 유용해 보이지는 않는다. 변수의 스코프를 좁게 만들어 변수 자체를 재빨리 소멸시키는 편이 낫다.
foo = null;
```

- 함수가 유효한 값을 반환할 수 없는 경우 명시적으로 null을 반환한다.

```html
<!DOCTYPE html>
<html>
<body>
	<script>
		var element = document.querySelector('.myClass');

		// HTML 문서에 myClass 클래스를 갖는 요소가 없다면 null을 반환한다.
		console.log(element); // null
	</script>
</body>
</html>
```

## 6.7 심벌 타입

- `심벌(symbol)`은 ES6에서 추가된 7번째 타입으로, 변경 불가능한 원시 타입의 값이다.
- 심벌은 Symbol 함수를 호출해 생성한다. 값이 외부에 노출되지 않으며, 다른 값과 절대 중복되지 않는다.

```jsx
// 심벌 값 생성
var key = Symbol('key');
console.log(typeof key); // symbol

// 객체 생성
var obj = {};

// 이름이 충돌할 위험이 없는 유일무이한 값인 심벌을 프로퍼티 키로 사용한다.
obj[key] = 'value';
console.log(obj[key]); // value
```

## 6.8 객체 타입

- 자바스크립트는 객체 기반의 언어이며, 자바스크립트를 이루고 있는 거의 모든 것이 객체다.

## 6.9 데이터 타입의 필요성

### 6.9.1 데이터 타입에 의한 메모리 공간의 학보와 참조

- 값은 메모리에 저장하고 참조할 수 있어야 한다.

```jsx
var score = 100;
```

- 위 코드가 실행되면 숫자 타입의 값 100을 저장하기 위해 8바이트 메모리 공간을 확보한 뒤 100을 2진수로 저장한다.
- 위 변수를 불러올때 자바스크립트 엔진이 score 변수의 타입을 인식하여 숫자 타입인 8바이트 단위로 메모리 공간에 저장된 값을 읽어 들인다.

### 6.9.2 데이터 타입에 의한 값의 해석

- 자바스크립트의 모든 값은 데이터 타입을 갖는다.
    - 값을 저장할 때 확보해야 하는 메모리 공간의 크기를 결정하기 위해
    - 값을 참조할 때 한 번에 읽어 들여야 할 메모리 공간의 크기를 결정하기 위해
    - 메모리에서 읽어 들인 2진수를 어떻게 해석할지 결정하기 위해

## 6.10 동적 타이핑

### 6.10.1 동적 타입 언어와 정적 타입 언어

- C나 자바 같은 `정적 타입(static/strong type) 언어`는 변수를 선언할때 `명시적 타입 선언(explicit type declaration)`을 하여 데이터 타입을 사전에 선언해야 한다.

```c
// c 변수에는 1바이트 정수 타입의 값(-128 ~ 127)만 할당할 수 있다.
char c;

// num 변수에는 4바이트 정수 타입의 값(-2,124,483,648 ~ 2,124,483,647)만 할당할 수 있다.
int num;
```

- 정적 타입 언어는 변수의 타입을 변경할 수 없으며, 선언한 타입에 맞는 값만 할당할 수 있다.
- 정적 타입 언어는 컴파일 시점에 타입 체크를 수행하여 통과하지 못하면 에러를 발생시킨다.
- 대표적인 정적 타입 언어로 `C`, `C++`, `자바(Java)`, `코틀린(Kotlin)`, `고(Go)`, `하스켈(Haskell)`, `러스트(Rust)`, `스칼라(Scala)` 등이 있다.
- 자바스크립트는 변수 선언할 때 타입을 선언하는게 아닌 `키워드(var, let ,const)`를 사용해 변수를 선언한다.
- 자바스크립트의 변수는 어떠한 데이터 타입의 값이라도 자유롭게 할당할 수 있다.

```jsx
var foo;
console.log(typeof foo); // undefined

foo = 3;
console.log(typeof foo); // number

foo = 'Hello';
console.log(typeof foo); // string

foo = true;
console.log(typeof foo); // boolean

foo = null;
console.log(typeof foo); // object

foo = Symbol(); // 심벌
console.log(typeof foo); // symbol

foo = {}; // 객체
console.log(typeof foo); // object

foo = []; // 배열
console.log(typeof foo); // object

foo = function () {}; // 함수
console.log(typeof foo); // function
```

- typeof 연산자로 변수를 연산하면 변수에 할당된 값의 데이터 타입을 반환한다.
- 자바스크립트의 변수는 선언이 아닌 `할당에 의해 타입이 결정(타입 추론 type inference)`된다.
- 재할당에 의해 변수의 타입은 언제든지 동적으로 변할 수 있다.
- 위와 같은 특징을 `동적 타이핑(dynamic typing)`이라 하며, 이러한 언어를 `동적 타입(dynamic/weak type) 언어`라 한다,
- 대표적인 동적 타입 언어로 `자바스크립트`, `파이썬(Python)`, `PHP`, `루비(Ruby)`, `리스프(Lisp)`, `펄(Perl)` 등이 있다.

### 6.10.2 동적 타입 언어와 변수

- 동적 타입 언어는 변수에 어떤 데이터 타입의 값이라도 자유롭게 할당할 수 있다.
- 동적 타입 언어의 변수는 값을 확인하기 전에는 타입을 확신할 수 없다.
- 동적 타입 언어는 `유언성(flexibility)`은 높지만 `신뢰성(reliability)`은 떨어진다.
- 변수 사용시 주의 사항
    - 변수는 꼭 필요한 경우에 한해 제한적으로 사용한다. 변수 값은 재할당에 의해 언제든지 변경될 수 있으며, 변수의 개수가 많으면 오류가 발생할 확률도 높아진다.
    - `변수의 유효 범위(스코프)`는 최대한 좁게 만들어 변수의 부작용을 억제해야 한다. 변수의 유효 범위가 넓으면 넓을수록 변수로 인해 오류가 발생할 확률이 높아진다.
    - 전역 변수는 최대한 사용하지 않도록 한다. 전역 변수는 의도치 않게 값이 변경될 가능성이 높고 다른 코드에 영향을 줄 가능성도 높다.
    - 변수보다는 상수를 사용해 값의 변경을 억제한다.
    - 변수 이름은 변수의 목적이나 의미를 파악할 수 있도록 네이밍한다.
- 코드는 오해하지 않도록 작성해야 한다. 코드는 동작하는 것만이 존재 목적은 아니라 개발자를 위한 문서이기도 하다. 따라서 `가독성이 좋은 코드가 좋은 코드다.`
