# 13장 - 스코프

## 13.1 스코프란?

- `스코프(scope)`는 매개변수를 참조할 수 있는 유효범위를 뜻함

```tsx
function add(x, y) {
	// 매개변수는 ㅎ마수 몸체 내부에서만 참조할 수 있다.
	// 즉, 매개변수의 스코프(유효범위)
	console.log(x, y); // 2 5
	reutnr x + y;
}

add(2, 5);

// 매개변수는 함수 몸체 내부에서만 차모할 수 있다.
console.log(x, y); // ReferenceError: x is not defined
```

- 변수는 코드의 바깥 영역뿐 아니라 코드 블록이나 함수 몸체 내에서도 선언할 수 있으며, 코드블록이나 함수는 중첩될 수 있다.

```tsx
var var1 = 1; // 코드의 가장 바깥 영역에서 선언한 변수

if (true) {
	var var2 = 2; // 코드 블록 내에서 선언한 변수
	if (true) {
		var var3 = 3; // 중첩된 코드 블록 내에서 선언한 변수
	}
}

function foo() {
	var var4 = 4; // gkatn sodptj tjsdjsgks qustn

	function bar() {
		var var5 = 5; // 중첩된 함수 내에서 선언한 변수
	}
}

console.log(var1); // 1
console.log(var2); // 2
console.log(var3); // 3
console.log(var4); // ReferenceError: var4 is not defined
console.log(var5); // ReferenceError: var5 is not defined
```

- 모든 식별자(변수 이름, 함수 이름, 클래스 이름 등)는 자신이 선언된 위치에 의해 다른 코드가 식별자 자신을 참조할 수 있는 유효 범위가 결정된다.
- 스코프는 식별자가 유효한 범위를 말한다.

```tsx
var x = 'global';

function foo() {
	var x = 'local';
	console.log(x); // ①
}

foo();

console.log(x); // ②
```

- 위 예제 ①과 ②에서 X 변수를 참조할 때 두 개의 변수 중에서 어떤 변수를 참조해야 할 것인지 결정하는 것을 `식별자 결정(identifier resolution)`이라 한다.
- 스코프란 자바스크립트 엔진이 식별자를 검색할 때 사용하는 규칙이라고도 할수 있다.
- 코드의 문맥과 환경
    - `코드의 문맥(context)`은 `렉시컬 환경(lexical environment)`으로 이뤄진다.
    - 이를 구현한 것이 `실행 컨텍스트(execution context)`다.
    - 모든 코드는 실행 컨텍스트에서 평가되고 실행된다.
    - 스코프는 실행 컨텍스트와 깊은 관련이 있다.
- 스코프라는 개념이 없다면 같은 이름을 갖는 변수는 충돌을 일으키므로 프로그램 전체에서 하나밖에 사용할 수 없다.
- 식별자는 어떤 값을 구별할 수 있어야 하므로 `유일(unique)`해야 한다.
- 하나의 값은 유일한 `식별자에 연결(name binding)`되어야 한다.
- 스코프 내에서 식별자는 유일해야 하지만 다른 스코프에는 같은 이름의 식별자를 사용할 수 있다. 즉, 스코프는 네임스페이스다.
- var 키워드로 선언한 변수의 중복 선언
    - var 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언이 허용된다.
    - 이는 의도치 않게 변수값이 재할당되어 변경되는 부작용을 발생시킨다.
    - let이나 const 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언을 허용하지 않는다.

## 13.2 스코프의 종류

- 코드는 `전역(global)`과 `지역(local)`으로 구분할 수 있다.

| 구분 | 설명 | 스코프 | 변수 |
| --- | --- | --- | --- |
| 전역 | 코드의 가장 바깥 영역 | 전역 스코프 | 전역 변수 |
| 지역 | 함수 몸체 내부 | 지역 스코프 | 지역 변수 |

### 13.2.1 전역과 전역 스코프

```tsx
var x = "global x";
var y = "global y";

function outer() {
	var z = "outer's local z";

	console.log(x); // ① global x
	console.log(y); // ② global y
	console.log(z); // ③ outer's local z

	function inner() {
		var x = "inner's local x";

		console.log(x); // ④ inner's local x
		console.log(y); // ⑤ global y
		console.log(z); // ⑥ outer's local z
	}

	inner();
}

outer();

console.log(x); // ⑦ global x
console.log(z); // ⑧ ReferenceError: z is not defined
```

- 전역이란 코드의 가장 바깥 영역을 말한다.
- 전역은 `전역 스코프(global scope)`를 만든다.
- 전역에 변수를 선언하면 전역 스코프를 갖는 `전역 변수(global variable)`가 된다.
- 전역 변수는 어디서든지 참조할 수 있다.

### 13.2.2 지역과 지역 스코프

- 지역이란 함수 몸체 내부를 말한다.
- 지역은 `지역 스코프(local scope)`를 만든다.
- 지역에 변수를 선언하면 지역 스코프를 갖는 `지역 변수(local variable)`가 된다.
- 지역 변수는 자신의 지역 스코프와 하위 지역 스코프에서 유효하다.
- 전역 변수 x가 선언된 상태에서 지역 변수 x를 선언 후 x 변수를 참조하면 지역 변수 x를 참조하는데, 자바스크립트 엔진이 스코프 체인을 통해 참조할 `변수를 검색(identifier resolution)` 했기 때문이다.

## 13.3 스코프 체인

- 함수 몸추 네배우세 함수가 정의되는 것을 ‘함수의 중첩’이라 한다.
- 함수 몸체 내부에서 정의한 함수를 `중첩 함수(nested function)`, 중첩 함수를 포함하는 함수를 `외부 함수(outer function)`라고 한다.
- 스코프가 함수의 중첩에 의해 계층적 구조를 갖으며, 스코프가 계층적으로 연결된 것을 `스코프 체인(scope chain)`이라 한다.
- 변수를 참조할 때 자바스크립트 엔진은 스코프 체인을 통해 변수를 참조하는 코드의 스코프에서 시작하여 상위 스코프 방향으로 이동하며 선언된 `변수를 검색(identifier resolution)`한다.
- `렉시컬 환경(Lexical Environment)`
    - 스코프 체인은 실행 컨텍스트의 렉시컬 환경을 단방향으로 `연결(chaining)`한 것이다.
    - 전역 렉시컬 환경은 코드가 로드되면 곧바로 생성되고 함수의 렉시컬 환경은 함수가 호출되면 곧바로 생성된다.

### 13.3.1 스코프 체인에 의한 변수 검색

- 상위 스코프에서 유효한 변수는 하위 스코프에서 자유롭게 참조할 수 있지만 하위 스코프에서 유효한 변수를 상위 스코프에서 참조할 수 없다.
- 스코프의 계층적 구조는 `상속(inheritance)`과 유사하다.

### 13.3.2 스코프 체인에 의한 함수 검색

```tsx
// 전역 함수
function foo() {
	console.log('global function foo');
}

function bar() {
	// 중첩 함수
	function foo() {
		console.log('local function foo');
	}
	foo(); // ①
}

bar();
```

- 스코프는 식별자를 검색하는 규칙이다.

## 13.4 함수 레벨 스코프

- 코드 블록이 아닌 함수에 의해서만 지역 스코프가 생성된다.
- 모든 코드 블록이 지역 스코프를 만드는 특성을 `블록 레벨 스코프(block level scope)`라 한다.
- var 키워드로 선언된 변수는 오로지 함수의 코드 블록(함수 몸체)만을 지역 스코프로 인정하며, 이러한 특성을 `함수 레벨 스코프(function level scope)`라 한다.

```tsx
var x = 1;

if (true) {
	// var 키워드로 선언된 변수는 함수의 코드 블록(함수 몸체)만을 지역 스코프로 인정한다.
	// 함수 밖에서 var 키워드로 선언된 변수는 코드 블록 내에서 선언되었다 할지라도 모두 전역 변수다.
	// 따라서 x는 전역 변수다. 이미 선언된 전역 변수 x가 있으므로 x 변수는 중복 선언된다.
	// 이는 의도치 않게 변수 값이 변경되는 부작용을 발생시킨다.
	var x = 10;
}

console.log(x); // 10

var i = 10;

// for 문에서 선언한 i는 전역 변수다. 이미 선언된 전역 변수 i가 있으므로 중복 선언된다.
for (var i = 0; i < 5; i++) {
	console.log(i); // 0 1 2 3 4
}

// 의도치 않게 변수의 값이 변경되었다.
console.log(i); // 5
```

## 13.5 렉시컬 스코프

```tsx
var x = 1;

function foo() {
	var x = 10;
	bar();
}

function bar() {
	console.log(x);
}

foo(); // ?
bar(); // ?
```

- `동적 스코프(dynamic scope)`
    - 함수를 어디서 호출했는지에 따라 함수의 상위 스코프를 결정한다.
- `렉시컬 스코프(lexical scope)` 또는 `정적 스코프(static scope)`
    - 함수를 어디서 정의했는지에 따라 함수의 상위 스코프를 결정한다.
- 자바스크립트는 렉시컬 스코프를 따르므로 함수를 어디서 호출했는지가 아니라 함수를 어디서 정의했는지에 따라 상위 스코프를 결정한다.
- 함수가 호출된 위치는 상위 스코프 결정에 어떠한 영향도 주지 않는다.
- 함수의 상위 스코프는 언제나 자신이 정의된 스코프다.
- 함수의 상위 스코프는 함수 정의가 실행될 때 정적으로 결졍된다.
- 함수 정의(함수 선언문 또는 함수 표현식)가 실행되어 생성된 함수 객체는 이렇게 결정된 상위 스코프를 기억한다.
- 함수가 호출될 때마다 함수의 상위 스코프를 참조할 필요가 있기 때문이다.
