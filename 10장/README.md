# 10장 - 객체 리터럴
## 10.1 객체란?

> `객체 타입(object/reference type)`은 다양한 타입의 값(원시 값 또는 다른 객체)을 하나의 단위로 구성한 복합적인 `자료구조(data structure)`다. 원시 값은 `변경 불가능한 값(immutable value)`이지만 객체는 `변경 가능한 값(mutable value)`이다.
> 
- 객체는 0개 이상의 프로퍼티로 구성된 집합이며, 프로퍼티는 `키(key)`와 `값(value)`로 구성된다.

- 객체는 프로퍼티와 메서드(method)로 구성된 집합체다.
    - 프로퍼티 - 객체의 상태를 나타내는 값(data)
    - 메서드 - 프로퍼티(상태 데이터)를 참조하고 조작할 수 있는 동작(behavior)

## 10.2 객체 리터럴에 의한 객체 생성

- 인스턴스(instance)
    - 클래스에 의해 생성되어 메모리에 저장된 실체
    - 객체지향 프로그래밍에서 객체는 클래스와 인스턴스를 포함한 개념
    - 클래스는 인스턴스를 생성하기 위한 템플릿 역할
- 객체 생성 방법
    - 객체 리터럴
    - Object 생성자 함수
    - 생성자 함수
    - Object.create 메서드
    - 클래스(ES6)
- 리터럴(literal) - 문자 또는 기호를 사용하여 값을 생성하는 표기법
- 객체 리터럴 - 중괄호 { … } 내에 0개 이상의 프로퍼티를 정의

```jsx
var person = {
	name: 'Lee',
	sayHello: function () {
		console.log(`Hello! My name is ${this.name}.`);
	}
};

console.log(typeof person); // object
console.log(person); // {name:'Lee', sayHello: ƒ}

var empty = {}; // 빈 객체
console.log(typeof empty); // object
```

- 객체 리터럴의 중괄호는 코드 블록을 의미하지 않기 때문에 중괄호 뒤에 세미콜론을 붙인다.

## 10.3 프로퍼티

> 객체는 프로퍼티의 집합이며, 프로퍼티는 키와 값으로 구성된다.
> 

```jsx
var person = {
	// 프로퍼티 키는 name, 프로퍼티 값은 'Lee'
	name: 'Lee',
	// 프로퍼티 키는
	age: 20
};
```

- 프로퍼티를 나열할 때 쉼표(,)로 구분하고, 마지막 프로퍼티는 쉼표 생략 가능
- 프로퍼티 키와 프로퍼티 값으로 사용가능한 값
    - 프로퍼티 키 - 빈 문자열을 포함하는 모든 문자열 또는 심벌 값
    - 프로퍼티 값 - 자바스크립트에서 사용할 수 있는 모든 값
- 식별자 네이밍 규칙을 따르지 않는 프로퍼티 키는 반드시 따옴표를 사용해야 한다.

```jsx
var person = {
	firstName: 'Ung-mo', // 식별자 네이밍 규칙을 준수하는 프로퍼티 키
	'last-name': 'Lee'
};

console.log(person); // {firstName: "Ung-mo", last-name: "Lee"}
```

- firstName은 식별자 네이밍 규칙을 준수하여 따옴표 생략 가능하지만, last-name은 네이밍 규칙을 준수하지 않기 때문에 따옴표를 생략할 수 없다.

```jsx
var person = {
	firstName: 'Ung-Mo',
	last-name: 'Lee' // SyntaxError: Unexpected toekn -
};
```

- 문자열 또는 문자열로 평가할 수 있는 표현식을 사용해 프로퍼티 키를 동적으로 생성할 수도 있으며, 프로퍼티 키로 사용할 표현식을 대괄호 [ … ] 로 묶어야 한다.

```jsx
var obj = {};
var key = 'hello';

// ES5: 프로퍼티 키 동적 생성
obj[key] = 'world';
// ES6: 계산된 프로퍼티 이름
// var obj = { [key]: 'world' };

console.log(obj); // {hello: "world"}
```

- 빈 문자열을 프로퍼티 키로 사용해도 에러가 발생하지는 않으나, 키로서의 의미를 갖지 못함

```jsx
var foo = {
	'': '' // 빈 문자열도 프로퍼티 키로 사용할 수 있다.
}

console.log(foo); // {"": ""}
```

- 프로퍼티 키에 문자열이나 심벌 값 외의 값을 사용하면 암묵적 타입 변환을 통해 문자열이 된다.

```jsx
var foo = {
	0: 1,
	1: 2,
	2: 3
};

console.log(foo); // {0: 1, 1: 2, 2: 3}
```

- var, function과 같은 예약어도 프로퍼티 키로 사용 가능하지만, 에러 발생할 여지가 있어 권장하지 않음

```jsx
var foo = {
	var: '',
	function: ''
};

console.log(foo); // {var: "", function: ""}
```

- 이미 존재하는 프로퍼티 키를 중복 선언하면 나중에 선언한 프로퍼티가 먼저 선언한 프로퍼티를 덮어쓴다.

```jsx
var foo = {
	name: 'Lee',
	name: 'Kim'
};

console.log(foo); // {name: "Kim"}
```

## 10.4 메서드

> 프로퍼티 값이 함수일 경우 일반 함수와 구분하기 위해 `메서드(method)`라 부른다. 즉, 메서드는 객체에 묶여 있는 함수를 의미한다.
> 

```jsx
var circle = {
	radius: 5, // ← 프로퍼티

	// 원의 지름
	getDiameter: function () { // ← 메서드
		return 2 * this.radius; // this는 circle을 가르킨다.
	}
};

console.log(circle.getDiameter()); // 10
```

- 메서드 내부에서 사용한 this 키워드는 객체 자신을 가르키는 참조변수다.

## 10.5 프로퍼티 접근

- 프로퍼티 접근 방법
    - 마침표 프로퍼티 접근 연산자(.)를 사용하는 `마침표 표기법(dot notation)`
    - 대괄호 프로퍼티 접근 연산자([ … ])를 사용하는 `대괄호 표기법(bracket notation)`
- 프로퍼티 키가 식별자 네이밍 규칙을 준수하면 마침표 표기법과 대괄호 표기법을 모두 사용 가능하다.

```jsx
var person = {
	name: 'Lee'
};

// 마침표 표기법에 의한 프로퍼티 접근
console.log(person.name); // Lee

// 대괄호 표기법에 의한 프로퍼티 접근
console.log(person['name']); // Lee
```

- 대괄호 표기법을 사용하는 경우 대괄호 프로퍼티 접근 연산자 내부에 지정하는 프로퍼티 키는 반드시 따옴표로 감싼 문자열이야 한다.

```jsx
var person = {
	name: 'Lee'
};

console.log(person[name]); // ReferenceError: name is not defined
```

- 객체에 존재하지 않는 프로퍼티에 접근하면 undefined를 반환한다.

```jsx
var person = {
	name: 'Lee'
};

console.log(person.age); // undefined
```

- 대괄호 내에 들어가는 프로퍼티 키는 숫자를 제외하고 반드시 따옴표로 감싼 문자열이어야 한다.

```jsx
var person = {
	'last-name': 'Lee',
	1: 10
};

person.'last-name'; // → SyntaxError: Unexpected string
person.last-name; // → 브라우저 환경: NaN
								  // → Node.js 환경: ReferenceError: name is not defined
person[last-name]; // → ReferenceError: last is not defined
person['last-name'] // → Lee

// 프로퍼티 키가 숫자로 이뤄진 문자열인 경우 따옴표를 생략할 수 있다.
person.1; // → SyntaxError: Unexpected number
person.'1'; // → SyntaxError: Unexpected string
person[1]; // → 10 : person[1] → person['1']
person['1']; // → 10
```

## 10.6 프로퍼티 값 갱신

> 이미 존재하는 프로퍼티에 값을 할당하면 프로퍼티 값이 갱신된다.
> 

```jsx
var person = {
	name: 'Lee'
};

// person 객체에 name 프로퍼티가 존재하므로 name 프로퍼티의 값이 갱신된다.
person.name = 'Kim';

console.log(person); // {name: "Kim"}
```

## 10.7 프로퍼티 동적 생성

> 존재하지 않는 프로퍼티에 값을 할당하면 프로퍼티가 동적으로 생성되어 추가되고 프로퍼티 값이 할당된다.
> 

```jsx
var person = {
	name: 'Lee'
};

// person 객체에는 age 프로퍼티가 존재하지 않는다.
// 따라서 person 객체에 age 프로퍼티가 동적으로 생성되고 값이 할당된다.
person.age = 20;

console.log(person); // {name: "Lee", age: 20}
```

## 10.8 프로퍼티 삭제

> delete 연산자는 객체의 프로퍼티를 삭제한다. delete 연산자의 피연산자는 프로퍼티 값에 접근할 수 있는 표현식이어야 한다.
> 

```jsx
var person = {
	name: 'Lee'
};

// 프로퍼티 동적 생성
person.age = 20;

// person 객체에 age 프로퍼티가 존재한다.
// 따라서 delete 연산자로 age 프로퍼티를 삭제할 수 있다.
delete person.age;

// person 객체에 address 프로퍼티가 존재하지 않는다.
// 따라서 delete 연산자로 address 프로퍼티를 삭제할 수 없다. 이때 에러가 발생하지 않는다.
delete person.address;

console.log(person); // {name: "Lee"}
```

## 10.9 ES6에서 추가도니 객체 리터럴의 확장 기능

### 10.9.1 프로퍼티 축약 표현

- 객체 리터럴의 프로퍼티는 프로퍼티 키와 프로퍼티 값으로 구성된다.
- 프로퍼티 값은 변수에 할당된 값, 식별자 표현식일 수도 있따.

```jsx
// ES5
var x = 1, y = 2;

var obj = {
	x: x,
	y: y,
};

console.log(obj); // {x: 1, y: 2}
```

- ES6에서는 프로퍼티 값으로 변수를 사용하는 경우 변수 이름과 프로퍼티 키가 동일한 이름일 때 프로퍼티 키를 생략(property shorthand)할 수 있다.

```jsx
// ES6
let x = 1, y = 2;

// 프로퍼티 축약 표현
const obj = { x, y };

console.log(obj); // {x: 1, y: 2}
```

### 10.9.2 계산된 프로퍼티 이름

- 문자열 또는 문자열로 타입 변환할 수 있는 값으로 평가되는 표현식을 사용해 프로퍼티 키를 동적으로 생성할 수도 있다. 프로퍼티 키로 사용할 표현식을 대괄호 [ … ]로 묶어야 하며 이를 `계산된 프로퍼티 이름(computed property name)`이라 한다.

```jsx
// ES5
var prefix = 'prop';
var i = 0;

var obj = {};

// 계산된 프로퍼티 이름으로 프로퍼티 키 동적 생성
obj[prefix + '-' + ++i] = i;
obj[prefix + '-' + ++i] = i;
obj[prefix + '-' + ++i] = i;

console.log(obj);

// ES6
const prefix = 'prop';
let i = 0;

// 객체 리터럴 내부에서 계산된 프로퍼티 이름으로 프로퍼티 키를 동적 생성
const obj = {
	[`${prefix}-${++i}`]: i,
	[`${prefix}-${++i}`]: i,
	[`${prefix}-${++i}`]: i
};

console.log(obj); // {prop-1: 1, prop-2: 2, prop-3: 3}
```

### 10.9.3 메서드 축약 표현

```jsx
// ES5
var obj = {
	name: 'Lee',
	sayHi: function() {
		console.log('Hi! ' + this.name);
	}
};

obj.sayHi(); // Hi! Lee

// ES6
const obj = {
	name: 'Lee',
	// 메서드 축약 표현
	sayHi() {
		console.log('Hi! ' + this.name);
	}
};

obj.sayHi(); // Hi! Lee
```
