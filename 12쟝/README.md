# 12장 - 함수
## 12.1 함수란?

> 프로그래밍 언어의 함수는 일련의 과정을 `문(statement)`으로 구현하고 코드 블록으로 감싸서 하나의 실행 단위로 정의한 것이다.
> 
- 프로그래밍 언어의 함수도 입력을 받아서 출력을 내보낸다. 함수 내부로 입력을 전달받는 변수를 `매개변수(parameter)`, 입력을 `인수(argument)`, 출력을 `반환값(return value)`라 한다.
- 함수는 값이며, 여러개 존재할 수 있으므로 특정 함수를 구별하기 위해 식별자인 함수 이름을 사용할 수 있다.
- 함수는 `함수 정의(function definition)`를 통해 생성한다.

```jsx
// 함수 정의
function add(x, y) {
	return x + y;
}
```

- 함수를 실행하려면 `인수(argument)`를 매개변수를 통해 함수에 전달하면서 함수의 실행을 명시적으로 지시해야 한다. 이를 `함수 호출(function call/invoke)`이라 한다.

```jsx
// 함수 호출
var result = add(2, 5);

// 함수 add에 인수 2, 5를 전달하면서 호출하면 반환값 7을 반환한다.
console.log(result); // 7
```

## 12.2 함수를 사용하는 이유

- 함수는 필요할 때 몇 번이든 호출할 수 있으므로 코드의 재사용이라는 측면에서 매우 유용하다.
- 코드의 중복을 억제하고 재사용성을 높이는 함수는 유지보수의 편의성을 높이고 실수를 줄여 코드의 신뢰성을 높이는 효과가 있다.
- 적절한 함수 이름은 함수의 내부 코드를 이해하지 않고도 함수의 역할을 파악할 수 있게 돕는다. 이는 코드의 가독성을 향상시킨다.

## 12.3 함수 리터럴

- 자바스크립트의 함수는 객체 타입의 값이다. 따라서 함수 리터럴로 생성할 수 있으며, 함수 리터럴은 function 키워드, 함수 이름, 매개 변수 목록, 함수 몸체로 구성된다

```jsx
var f = function add(x, y) {
	return x + y;
};
```

| 구성 요소 | 설명 |
| --- | --- |
| 함수 이름 | - 함수 이름은 식별자다. 따라서 식별자 네이밍 규칙을 준수해야 한다. <br> - 함수 이름은 함수 몸체 내에서만 참조할 수 있는 식별자다. <br> - 함수 이름은 생략할 수 있다. 이름이 있는 함수를 기명 함수(named function), 이름이 없는 함수를 무명/익명 함수(anonymous function)라 한다. |
| 매개변수 목록 | - 0개 이상의 매개변수를 소괄호로 감싸고 쉼표로 구분한다. <br> - 각 매개변수에는 함수를 호출할 때 지정한 인수가 순서대로 할당된다. 즉, 매개변수 목록은 순서에 의미가 있다.<br> - 매개변수는 함수 몸체 내에서 변수와 동일하게 취급된다. 따라서 매개변수도 변수와 마찬가지로 식별자 네이밍 규칙을 준수해야 한다. |
| 함수 몸체 | - 함수가 호출되었을 때 일괄적으로 실행될 문들을 하나의 실행 단위로 정의한 코드 블록이다.<br>- 함수 몸체는 함수 호출에 의해 실행된다. <br>- 일반 객체는 호출할 수 없지만 함수는 호출할 수 있다.

## 12.4 함수 정의

| 함수 정의 방식 | 예시 |
| --- | --- |
| 함수 선언문 | function add(x, y) { <br>    return x + y; <br> } |
| 함수 표현식 | var add = function (x, y) { <br>    return x + y; <br> } |
| Function 생성자 함수 | var add = new Function(’x’, ‘y’, ‘return x + y’); |
| 화살표 함수(ES6) | var add = (x, y) => x + y; |
- 변수 선언과 함수 정의
    - 변수는 `선언(declaration)` 한다고 했지만 함수는 `정의(definition)`한다고 표현한다.
    - 함수 선언문이 평가되면 식별자가 암묵적으로 생성되고 함수 객체가 할당된다. 따라서 `변수 선언(variable declaration)`, `함수 정의(function definition)`라고 표현 한다.

### 12.4.1 함수 선언문

```jsx
// 함수 선언문
function add(x, y) {
	return x + y;
}

// 함수 참조
// console.dir은 console.log와는 달리 함수 객체의 프로퍼티까지 출력한다.
// 단, Node.js 환경에서는 console.log와 같은 결과가 출력된다.
console.dir(add); // ƒ add(x, y)

// 함수 호출
console.log(add(2, 5)); // 7
```

- 함수 리터럴은 함수 이름은 생략할 수 있으나 함수 선언문은 함수 이름을 생략할 수 없다.

```jsx
// 함수 선언문은 함수 이름을 생략할 수 없다.
function (x, y) {
	return x + y;
}
// SyntaxError: Function statements require a function name
```

- 함수 선언문은 표현식이 아닌 문이다.

```jsx
// 함수 선언문은 표현식이 아닌 문이므로 변수에 할당할 수 없다.
// 하지만 함수 선언문이 변수에 할당되는 것처럼 보인다.
var add = function add(x, y) {
	return x + y;
};

// 함수 호출
console.log(add(2, 5)); // 7

// 기명 함수 리터럴을 단독으로 사용하면 함수 선언문으로 해석된다.
// 함수 선언문에서는 함수 이름을 생략할 수 없다.
function foo() { console.log('foo'); }
foo(); // foo

// 함수 리터럴을 피연산자로 사용하면 함수 선언문이 아니라 함수 리터럴 표현식으로 해석된다.
// 함수 리터럴에서는 함수 이름을 생략할 수 있다.
(function bar() { console.log('bar'); });
bar(); // ReferenceError: bar is not defined
```

- 자바스크립트 엔진은 생성된 함수를 호출하기 위해 함수 이름과 동일한 이름의 식별자를 암묵적으로 생성하고, 거기에 함수 객체를 할당한다.

```jsx
// 식별자 add에 함수가 할당
var add = function add(x, y) {
	return x + y;
}

// 식별자 add 호출
console.log(add(2, 5));
```

- 함수는 함수 이름으로 호출하는 것이 아니라 함수 객체를 가리키는 식별자로 호출한다.

### 12.4.2 함수 표현식

- 함수는 값처럼 변수에 할당 할 수도 있고 프로퍼티 값이 될 수도 있으며 배열의 요소가 될 수도 있다.
- 값의 성질을 갖는 객체를 일급 객체라고 하며, 자바스크립트의 함수는 일급 객체다.
- 함수는 일급 객체이므로 함수 리터럴로 생성한 함수 객체를 변수에 할당할 수 있는데, 이러한 함수 정의 방식을 `함수 표현식(function expression)`이라 한다.

```jsx
// 함수 표현식
var add = function (x, y) {
	return x + y;
};

console.log(add(2, 5)); // 7
```

- 함수 리터럴의 함수 이름은 생략할 수 있으며, 익명 함수라 한다.
- 함수를 호출할 때는 함수 이름이 아니라 함수 객체를 가리키는 식별자를 사용해야 한다.
- 함수 이름은 함수 몸체 내부에서만 유효한 식별자이므로 함수 이름으로 함수를 호출할 수 없다.

```jsx
// 기명 함수 표현식
var add = function foo (x, y) {
	return x + y;
};

// 함수 객체를 가리키는 식별자로 호출
console.log(add(2, 5)); // 7

// 함수 이름으로 호출하면 ReferenceError가 발생한다.
// 함수 이름은 함수 몸체 내부에서만 유효한 식별자다.
console.log(foo(2, 5)); // ReferenceError: foo is not defined
```

- 함수 선언문은 “표현식이 아닌 문”이고 함수 표현식은 “표현식인 문“이다.

### 12.4.3 함수 생성 시점과 함수 호이스팅

```jsx
// 함수 참조
console.dir(add); // ƒ add(x, y)
console.dir(sub); // undefined

// 함수 호출
console.log(add(2, 5)); // 7
console.log(sub(2, 5)); // TypeError: sub is not a function

// 함수 선언문
function add(x, y) {
	return x + y;
}

// 함수 표현식
var sub = function (x, y) {
	return x - y;
};
```

- 함수 선언문으로 정의한 함수와 함수 표현식으로 정의한 함수의 생성 시점이 다르다.
- 함수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징을 `함수 호이스팅(function hoisting)`이라 한다.
- 변수 할당문의 값은 할당문이 실행되는 시점, 즉 런타임에 평가되므로 함수 표현식의 함수 리터럴도 할당문이 실행되는 시점에 평가되어 함수 객체가 된다.
- 함수 표현식으로 함수를 정의하면 함수 호이스팅이 발생하는 것이 아니라 변수 호이스팅이 발생한다.
- 함수 호이스팅은 함수를 호출하기 전에 반드시 함수를 선언해야 한다는 당연한 규칙을 무시한다.

### 12.4.4 Function 생성자 함수

- Function 생성자 함수에 매개변수 목록과 함수 몸체를 문자열로 전달하면 함수 객체를 생성해서 반환한다. (new 생략 가능)
- 생성자 함수(constructor function)
    - 생성자 함수는 객체를 생성하는 함수를 말한다.

```jsx
var add = new Function('x', 'y', 'return x + y');

console.log(add(2, 5)); // 7
```

- Function 생성자 함수로 생성한 함수는 `클로저(closure)`를 생성하지 않는 등, 함수 선언문이나 함수 표현식으로 생성한 함수와 다르게 동작한다.

```jsx
var add1 = (function () {
	var a = 10;
	return function (x, y) {
		return x + y + a;
	};
}());

console.log(add1(1, 2)); // 13

var add2 = (function () {
	var a = 10;
	return new Function('x', 'y', 'return x + y + a;');
}());

console.log(add2(1, 2)); // ReferenceError: a is not defined
```

### 12.4.5 화살표 함수

- 화살표 함수(arrow function)는 function 키워드 대신 화살표(fat arrow) =>를 사용해 선언할 수 있으며, 항상 익명 함수로 정의한다.

```jsx
// 화살표 함수
const add = (x, y) => x + y;
console.log(add(2, 5)); // 7
```

- 화살표 함수는 생성자 함수로 사용할 수 없으며, 기존 함수와 this 바인딩 방식이 다르고, prototype 프로퍼티가 없으며 arguments 객체를 생성하지 않는다.

## 12.5 함수 호출

- 함수는 식별자와 함수 호출 연산자인 소괄호로 호출한다.
- 호출 연산자 내에는 0개 이상의 인수를 쉼표로 구분하여 나열한다.

### 12.5.1 매개변수와 인수

- 함수를 실행하기 위해 필요한 값을 함수 내부로 전달할 필요가 있는 경우, `매개변수/인자(parameter)`를 통해 `인수(argument)`를 전달한다.
- 인수는 함수를 호출할 때 지정한다.

```jsx
// 함수 선언문
function add(x, y) {
	return x + y;
}

// 함수 호출
// 인수 1과 2가 매개변수 x와 y에 순선대로 할당되고 함수 몸체의 문들이 실행된다.
var result = add(1, 2);
```

- 매개변수는 함수를 정의할 때 선언하며, 함수 내부에서 변수와 동일하게 취급된다.

```jsx
function add(x, y) {
	console.log(x, y); // 2 5
	return x + y;
}

add(2, 5);

// add 함수의 매개변수 x, y는 함수 몸체 내부에서만 참조할 수 있다.
console.log(x, y); // ReferenceError: x is not defined
```

- 함수를 호출할 때 매개변수의 개수만큼 인수를 전달하지 않아도 에러가 발생하지는 않는다.

```jsx
function add(x, y) {
	return x + y;
}

// x + y = 2 + undefined = NaN
console.log(add(2)); // NaN
```

- 매개변수보다 인수가 더 많은 경우 초과된 인수는 무시된다.

```jsx
function add(x, y) {
	return x + y;
}

console.log(add(2, 5, 10)); // 7
```

- 모든 인수는 암묵적으로 arguments 객체의 프로퍼티로 보관된다.

```jsx
function add(x, y) {
	console.log(arguments);
	// Arguments(3) [2, 5, 10, callee: ƒ, Symbol(Symbol.iterator): ƒ]

	return x + y;
}

add(2, 5, 10);
```

- arguments 객체는 함수를 정의할 때 매개변수 개수를 확정할 수 없는 가변 인자 함수를 구현할 때 유용하게 사용된다.

### 12.5.2 인수 확인

```jsx
function add(x, y) {
	return x + y;
}

// 자바스크립트 함수는 매개변수와 인수의 개수가 일치하는지 확인하지 않는다.
console.log(add(2)); // NaN
// 자바스크립트는 동적 타입 언어라 매개변수의 타입을 사전에 지정할 수 없다.
console.log(add('a', 'b')); // 'ab'
```

- 함수를 정의할 때 적절한 인수가 전달되었는지 확인할 필요가 있다.

```jsx
function add(x, y) {
	if (typeof x !== 'number' || typeof y !== 'number') {
		// 매개변수를 통해 전달된 인수의 타입이 부적절한 경우 에러를 발생시킨다.
		throw new TypeError('인수는 모두 숫자 값이어야 합니다.');
	}

	return x + y;
}

console.log(add(2)); // TypeError: 인수는 모두 숫자 값이어야 합니다.
console.log(add('a', 'b')); // TypeError: 인수는 모두 숫자 값이어야 합니다.
```

- 인수가 전달되지 않은 경우 단축 평가를 사용해 매개변수에 기본값을 할당하는 방법도 있다.

```jsx
function add(a, b, c) {
	a = a || 0;
	b = b || 0;
	c = c || 0;
	return a + b + c;
}

console.log(add(1, 2, 3)); // 6
console.log(add(1, 2)); // 3
console.log(add(1)); // 1
console.log(add()); // 0
```

- ES6에서 도입된 매개변수 기본값을 사용하면 인수 체크 및 초기화를 간소화할 수 있다.
- 매개변수 기본값은 매개변수에 인수를 전달하지 않았을 경우와 undefined를 전달한 경우에만 유효하다.

```jsx
function add(a = 0, b = 0, c = 0) {
	return a + b + c;
}

console.log(add(1, 2, 3)); // 6
console.log(add(1, 2)); // 3
console.log(add(1)); // 1
console.log(add()); // 0
```

### 12.5.3 매개변수의 최대 개수

- 매개변수의 최대 개수에 대해 명시적으로 제한하고 있지 않지만, 적을수록 좋다.
- 이상적인 함수는 한 가지 일만 해야 하며 가급적 작게 만들어야 한다.
- 매개변수는 최대 3개 이상을 넘지 않는 것을 권장하며, 객체를 인수로 전달하는 것이 유리하다.

```jsx
$.ajax({
	method: 'POST',
	url: '/user'/,
	data: { id: 1, name: 'Lee' },
	cache: false
});
```

- 객체를 인수로 사용하는 경우 프로퍼티 키만 정확히 지정하면 매개변수의 순서를 신경 쓰지 않아도 된다.

### 12.5.4 반환문

- 함수는 return 키워드와 표현식(반환값)으로 이뤄진 반환문을 사용해 실행 결과를 함수 외부로 반환(return)할 수 있다.

```jsx
function multiply(x, y) {
	return x * y; // 반환문
}

// 함수 호출은 반환값으로 평가된다.
var result = multiply(3, 5);
console.log(result); // 15
```

- 함수 호출은 표현식이기 때문에 return 키워드가 반환한 반환값으로 평가된다.
- 반환문은 함수의 실행을 중단하고 함수 몸체를 빠져나간다.

```jsx
function multiply(x, y) {
	return x * y; // 반환문
	// 반환문 이후에 다른 문이 존재하면 그 문은 실행되지 않고 무시된다.
	console.log('실행되지 않는다.');
}

console.log(multiply(3, 5)); // 15
```

- 반환문은 return 키워드 뒤에 오는 표현식을 평가해 반환한다.
- return 키워드 뒤에 반환값으로 표현식을 명시적으로 지정하지 않으면 undefined가 반환된다.

```jsx
function foo() {
	return;
}

console.log(foo()); // undefined
```

- 반환문은 생략할 수 있으며, 함수의 마지막 문까지 실행한 후 undefined를 반환환다.

```jsx
function foo() {
	// 반환문을 생략하면 암묵적으로 undefined가 반환된다.
}

console.log(foo()); // undefined
```

- return 키워드와 반환값으로 사용할 표현식 사이에 줄바꿈이 있으면 세미콜론 자동 삽입 기능에 의해  undefined가 반환된다.

```jsx
function multiply(x, y) {
	// return 키워드와 반환값 사이에 줄바꿈이 있으면
	return // 세미콜론 자동 삽입 기능(ASI)에 의해 세미콜론이 추가된다.
	x * y; // 무시된다.
}

console.log(multiply(3, 5)); // undefined
```

- 전역에서 반환문을 사용하면 문법 에러(SyntaxError: Illegal return statement)가 발생한다.

```html
<!DOCTYPE html>
<html>
<body>
	<script>
		return;
	</script>
</body>
</html>
```

## 12.6 참조에 의한 전달과 외부 상태의 변경

- 함수를 호출하면서 매개변수에 값을 전달하는 방식을 값에 의한 호출, 참조에 의한 호출로 구별해 부르는 경우도 있으나 동작 방식은 값에 의한 전달, 참조에 의한 전달과 동일하다.

```jsx
// 매개변수 primitive는 원시 값을 전달받고, 매개변수 obj는 객체를 전달받는다.
function changeVal(primitive, obj) {
	primitive += 100;
	obj.name = 'Kim';
}

// 외부 상태
var num = 100;
var person = { name: 'Lee' };

console.log(num);
console.log(person); // {name: "Lee"}

// 원시 값은 값 자체가 복사되어 전달되고 객체는 참조 값이 복사되어 전달된다.
changeVal(num, person);

// 원시 값은 원본이 훼손되지 않는다.
console.log(num); // 100

// 객체는 원본이 훼손된다.
console.log(person); // {name: "Kim"}
```

- 원시 값은 변경 불가능한 값이므로 직접 변경할 수 없기에 재할당을 통해 할당된 원시 값을 새로운 원시 값으로 교체한다.
- 객체는 변경 가능한 값이므로 직접 변경할 수 있기 때문에 재할당 없이 직접 할당된 객체를 변경한다.
- 함수가 외부 상태를 변경하면 상태 변화를 추적하기 어려워진다.
- 객체의 변경을 추적하려면 `옵저버(Observer)` 패턴등을 통해 객체를 참조를 공유하는 모든 이들에게 통지하고 대처하는 추가 대응이 필요하다.
- 객체를 `불변 객체(immutable object)`로 만들어 사용하면 오부 상태가 변경되는 부수 효과를 없앨 수 있다.
- 외부 상태를 변경하지 않고 외부 상태에 의존하지도 않는 함수를 순수 함수라 한다.

## 12.7 다양한 함수의 형태

### 12.7.1 즉시 실행 함수

> 함수 정의와 동시에 즉시 호출되는 함수를 `즉시 실행 함수(IIFE, Immediately Invoked Function Expression)`라고 한다. 실행 함수는 단 한 번만 호출되며 다시 호출할 수 없다.
> 

```jsx
// 익명 즉시 실행 함수
(function () {
	var a = 3;
	var b = 5;
	return a * b;
}());
```

- 즉시 실행 함수는 익명 함수를 사용하는 것이 일반적이다.
- 그룹 연산자 ( … ) 내의 기명 함수는 함수 선언문이 아니라 함수 리터럴로 평가되며 함수 이름은 함수 몸체에서만 참조할 수 있는 식별자이므로 즉시 실행 함수를 다시 호출할 수는 없다.

```jsx
// 기명 즉시 실행 함수
(function foo() {
	var a = 3;
	var b = 5;
	return a * b;
}());

foo(); // ReferenceError: foo is not defined
```

- 즉시 실행 함수는 그룹 연산자 ( … )로 감싸야 한다.

```jsx
function () { // SyntaxError: Function statements require a function name
	// ...
}();

function foo() {
	// ...
	// 함수 코드 블록의 닫는 중괄호 뒤에 ";"이 암묵적으로 추가되어 에러가 발생
}(); // SyntaxError: Unexpected token ')'

function foo() {} (); // => function foo() {};();

// 그룹 연산자의 피연산자는 값으로 평가되므로
// 기명 또는 무명 함수를 그룹 연산자로 감싸면 함수 리터럴로 평가되어 함수 객체가 된다.
(); // SyntaxError: Inexpected token ')'

console.log(typeof (function f(){})); // function
console.log(typeof (function(){})); // function
```

- 그룹 연산자로 함수를 묶은 이유는 먼저 함수 리터럴을 평가해서 함수 객체를 생성하기 위해서다.
- 함수 리터럴을 평가해서 함수 객체를 생성할 수 있다면 그룹 연산자 의외의 연산자를 사용해도 된다.

```jsx
(function () {
	// ...
}());

(function () {
	// ...
})();

!function () {
	// ...
}();

+function () {
	// ...
}();
```

- 즉시 실행 함수도 일반 함수처럼 값을 반환하거나 인수를 전달할 수도 있다.

```jsx
// 즉시 실행 함수도 일반 함수처럼 값을 반환할 수 있다.
var res = (fnction () {
	var a = 3;
	var b = 5;
	return a * b;
}());

console.log(res); // 15

// 즉시 실행 함수에도 일반 함수처럼 인수를 전달할 수 있다.
res = (function (a, b) {
	return a * b;
}(3, 5));

console.log(res);
```

- 즉시 실행 함수 내에 코드를 모아 두면 변수나 함수 이름의 충돌을 방지할 수 있다.

### 12.7.2 재귀 함수

> 함수가 자기 자신을 호출하는 것을 `재귀 호출(recursive call)`이라 한다. `재귀 함수(recursive function)`는 자기 자신을 호출하는 재귀 호출을 수행하는 함수를 말한다.
> 
- 재귀 함수는 반복되는 처리를 위해 사용한다.

```jsx
// 반복문을 사용하여 구현
function countdown(n) {
	for (var i = n; i >= 0; i--) console.log(i);
}

countdown(10);

// 재귀함수를 사용하여 구현
function countdown(n) {
	if (n < 0) return;
	console.log(n);
	countdown(n - 1); // 재귀 호출
}

countdown(10);
```

- 재귀 함수를 사용하면 반복되는 처리를 반복문 없이 구현할 수 있다.

```jsx
// 팩토리얼(계승)은 1부터 자신까지의 모든 양의 정수의 곱이다.
// n! = 1 * 2 * ... * (n-1) * n
function factorial(n) {
	// 탈출 조건: n이 1 이하일 때 재귀 호출을 멈춘다.
	if (n <= 1) return 1;
	// 재귀 호출
	return n * factorial(n - 1);
}

console.log(factorial(0)); // 0! = 1
console.log(factorial(1)); // 1! = 1
console.log(factorial(2)); // 2! = 2 * 1 = 2
console.log(factorial(3)); // 3! = 3 * 2 * 1 = 6
console.log(factorial(4)); // 4! = 4 * 3 * 2 * 1 = 24
console.log(factorial(5)); // 5! = 5 * 4 * 3 * 2 * 1 = 120
```

- 함수 내부에서 함수 이름을 사용해 자기 자신을 호출할 수 있다.
- 함수 외부에서 함수를 호출할 때는 반드시 함수를 가리키는 식별자로 해야 한다.

```jsx
// 함수 표현식
var factorial = function foo(n) {
	// 탈출 조건: n이 1 이하일 때 재귀 호출을 멈춘다.
	if (n <= 1) return 1;
	// 함수를 가리키는 식별자로 자기 자신을 재귀 호출
	return n * factorial(n - 1);

	// 함수 이름으로 자기 자신을 재귀 호출할 수도 있다.
	// console.log(factorial === foo); // true
	// return n * foo(n - 1);
};

console.log(factorial(5)); // 5! = 5 * 4 * 3 * 2 * 1 = 120
```

- 재귀 함수는 자신을 무한 재귀 호출하기 때문에 재귀 호출을 멈출 수 있는 탈출 조건을 반드시 만들어야 한다.
- 탈출 조건이 없으면 함수가 무한 호출되어 `스택 오버플로(stack overflow)`에러가 발생한다.
- 대부분의 재귀 함수는 for 문이나 while 문으로 구현 가능하다.

```jsx
function factorial(n) {
	if (n <= 1) return 1;

	var res = n;
	while (--n) res *= n;
	return res;
}

console.log(factorial(0)); // 0! = 1
console.log(factorial(1)); // 1! = 1
console.log(factorial(2)); // 2! = 2 * 1 = 2
console.log(factorial(3)); // 3! = 3 * 2 * 1 = 6
console.log(factorial(4)); // 4! = 4 * 3 * 2 * 1 = 24
console.log(factorial(5)); // 5! = 5 * 4 * 3 * 2 * 1 = 120
```

- 재귀 함수는 반복처리를 반복문 없이 구현할 수 있다는 장점이 있지만 무한 반복에 빠질 위험이 있으므로 주의해서 사용해야 한다.

### 12.7.3 중첩 함수

> 함수 내부에 정의된 함수를 `중첩 함수(nested function)`또는 `내부 함수(inner function)`라 한다. 중첩 함수를 포함하는 함수는 `외부 함수(outer function)`라 부른다. 중첩 함수는 외부 함수 내부에서만 호출할 수 있다. 일반적으로는 중첩 함수는 자신을 포함하는 외부 함수를 돕는 `헬퍼 함수(helper function)`의 역할을 한다.
> 

```jsx
function outer() {
	var x = 1;

	// 중첩 함수
	function inner() {
		var y = 2;
		// 외부 함수의 변수를 참조할 수 있다.
		console.log(x + y); // 3
	}

	inner();
}

outer();
```

- ES6부터 함수 정의는 문이 위치할 수 있는 문맥이라면 어디든지 가능하다.

### 12.7.4 콜백 함수

```jsx
// 외부에서 전달받는 f를 n만큼 반복 호출한다.
function repeat(n, f) {
	for (var i = 0; i < n; i++) {
		f(i); // i를 전달하면서 f를 호출
	}
}

var logAll = function (i) {
	console.log(i);
};

// 반복 호출할 함수를 인수로 전달한다.
repeat(5, logAll); // 0 1 2 3 4

var logOdds = function (i) {
	if (i % 2) console.log(i);
};

// 반복 호출할 함수를 인수로 전달한다.
repeat(5, logOdds); // 1 3
```

- 함수의 매개변수를 통해 다른 함수의 내부로 전달되는 함수를 `콜백 함수(callback function)`라고 하며, 매개 변수를 통해 함수의 외부에서 콜백 함수를 전달받은 함수를 `고차 함수(Higher-Order Function, HOF)`라고 한다.
- 고차 함수는 콜백 함수를 자신의 일부분으로 합성한다.
- 고차 함수는 매개변수를 통해 전달받은 콜백 함수의 호출 시점을 결정해서 호출한다.
- 콜백 함수는 고차 함수에 의해 호출되며 이때 고차 함수는 필요에 따라 콜백 함수에 인수를 전달할 수 있다.

```jsx
// 익명 함수 리터럴을 콜백 함수로 고차 함수에 전달한다.
// 익명 함수 리터럴은 repeat 함수를 호출할 때마다 평가되어 함수 객체를 생성한다.
repeat(5, function (i) {
	if (i % 2) console.log(i);
}); // 1 3
```

- 콜백 함수로서 전달된 함수 리터럴은 고차 함수가 호출될 때마다 평가되어 함수 객체를 생성한다.
- 콜백 함수를 다른 곳에서도 호출하거나, 콜백 함수를 전달받는 함수가 자주 호출된다면 함수 외부에서 콜백 함수를 정의한 후 함수 참조를 고차 함수에 전달하는 편이 효율적이다.

```jsx
// logOdds 함수는 단 한 번만 생성된다.
var logOdds = function (i) {
	if (i % 2) console.log(i);
};

// 고차 함수에 함수 참조를 전달한다.
repeat(5, logOdds); // 1 3
```

- 콜백 함수는 비동기 처리에 활용되는 중요한 패턴이다.

```jsx
// 콜백 함수를 사용한 이벤트 처리
// myButton 버튼을 클릭하면 콜백 함수를 실행한다.
document.getElementById('myButton').addEventListener('click', function () {
	console.log('button clicked!');
});

// 콜백 함수를 사용한 비동기 처리
// 1초 후에 메시지를 출력한다.
setTimeout(function () {
	console.log('1초 경과');
}, 1000);
```

- 콜백 함수는 배열 고차 함수에서도 사용된다.

```jsx
// 콜백 함수를 사용하는 고차 함수 map
var res = [1, 2, 3].map(function (item) {
	return item * 2;
});

console.log(res); // [2, 4, 6]

// 콜백 함수를 사용하는 고차 함수 filter
res = [1, 2, 3].filter(function (item) {
	return item % 2;
});

console.log(res); // [1, 3]

// 콜백 함수를 사용하는 고차 함수 reduce
res = [1, 2, 3].reduce(function (acc, cur) {
	return acc + cur;
}, 0);

console.log(res); // 6
```

### 12.7.5 순수 함수와 비순수 함수

> 함수형 프로그래밍에서는 어떤 외부 상태에 의존하지도 않고 변경하지도 않는 함수를 `순수 함수(putre function)`라 하고, 외부 상태에 의존하거나 외부 상태를 변경하는 함수를 `비순수 함수(impure function)`라고 한다.
> 
- 순수 함수는 동일한 인수가 전달되면 언제나 동일한 값을 반환하는 함수다.
- 비순수 함수는 외부 상태에 따라 반환값이 달라진다.
- 외부 상태에는 전역 변수, 서버 데이터, 파일, Console, DOM 등이 있다.
- 순수 함수는 일반적으로 최소 하나 이상의 인수를 전달받는다. 인수를 전달받지 않는 순수 함수는 상수와 마찬가지라 의미가 없다.
- 순수 함수는 인수를 변경하지 않는 것이 기본이라 인수의 불변성을 유지한다.
- 순수 함수는 함수의 외부 상태를 변경하지 않는다.

```jsx
var count = 0; // 현재 카운트를 나타내는 상태

// 순수 함수 increase는 동일한 인수가 전달되면 언제나 동일한 값을 반환한다.
function increase(n) {
	return ++n;
}

// 순수 함수가 반환한 결과값을 변수에 재할당해서 상태를 변경
count = increase(count);
console.log(count); // 1

count = increase(count);
console.log(count); // 2
```

- 비순수 함수는 외부 상태를 변경하는 `부수 효과(side effect)`가 있다.

```jsx
var count = 0; // 현재 카운트를 나타내는 상태: increase 함수에 의해 변화한다.

// 비순수 함수
function increase() {
	return ++count; // 외부 상태에 의존하며 외부 상태를 변경한다.
}

// 비순수 함수는 외부 상태(count)를 변경하므로 상태 변화를 추적하기 어려워진다.
increase();
console.log(count); // 1

increase();
console.log(count); // 2
```
