# 11장 - 원시 값과 객체의 비교
- 원사 타입과 객체 타입의 차이점

| 원시 타입(primitive type) | 객체 타입(object/reference type) |
| --- | --- |
| 변경 불가능한 값(immutable value) | 변경 가능한 값(mutable value) |
| 변수에 실제 값 저장 | 변수에 참조 값 저장 |
| 원시 값이 복사되어 전달/값에 의한 전달(pass by value) | 참조 값이 복사되어 전달/참조에 의한 전달(pass by reference) |

## 11.1 원시 값

### 11.1.1 변경 불가능한 값

> `원시 값(primitive type)`은 `변경 불가능한 값(immutable value)`/`읽기 전용(read only)` 값이다.
> 
- 변경 불가능하다는 것은 변수가 아니라 값에 대한 의미다.

```jsx
// const 키워드를 사용해 선언한 변수는 재할당이 금지된다. 상수는 재할딩이 금지된 변수일 뿐이다.
const o = {};

// const 키워드를 사용해 선언한 변수에 할당한 원시 값(상수)은 변경할 수 없다.
// 하지만 const 키워드를 사용해 선언한 변수에 할당한 객체는 변경할 수 있다.
o.a = 1;
console.log(o); // {a: 1}
```

- 원시 값은 변경 불가능한 값이기 때문에 원시 값을 재할당하면 새로운 메모리 공간을 확보하고 재할당한 값을 저장한 후, 변수 메모리 공간의 주소를 변경하는데, 이러한 특성을 `불변성(immutability)`이라 한다.
- 불변성을 갖는 원시 값을 할당한 변수는 재할당 이외에 변수 값을 변경할 수 있는 방법이 없다.

### 11.1.2 문자열과 불변성

- 문자열은 0개 이상의 `문자(character)`로 이뤄진 집합을 말하며, 1개의 문자는 2바이트의 메모리 공간에 저장된다.
- 문자열은 몇 개의 문자로 이뤄졌느냐에 따라 필요한 메모리 공간의 크기가 결정된다.

```jsx
// 문자열은 0개 이상의 문자로 이뤄진 집합이다.
var str1 = ''; // 0개의 문자로 이뤄진 문자열(빈 문자열)
var str2 = 'Hello'; // 5개의 문자로 이뤄진 문자열
```

- 유사 배열 객체(array-like object)
    - 유사 배열 객체란 배열처럼 인덱스로 프로퍼티 값에 접근할 수 있고 length 프로퍼티를 갖는 객체다.
    - 문자열은 배열처럼 인덱스를 통해 각 문자에 접근할 수 있으며, length 프로퍼티를 갖기 때문에 유사 배열 객체이다.

```jsx
var str = 'string';

// 문자열은 유사 배열이므로 배열과 유사하게 인덱스를 사용해 각 문자에 접근할 수 있다.
// 하지만 문자열은 원시 값이므로 변경할 수 없다. 이때 에러가 발생하지 않는다
str[0] = 'S';

console.log(str); // string
```

### 11.1.3 값에 의한 전달

```jsx
var score = 80;
var copy = score;

console.log(score); // 80
console.log(copy); // 80

score = 100;

console.log(score); // 100
console.log(copy); // ?
```

- 변수에 원시 값을 갖는 변수를 할당하면 할당받는 변수에는 할당되는 변수의 원시 값이 복사되어 전달되는데 이것을 값에 의한 전달이라 한다.

```jsx
var score = 80;

// copy 변수에는 score 변수의 값 80이 복사되어 할당된다.
var copy = score;

console.log(score, copy); // 80 80
console.log(score === copy); // true
```

- 값에 의한 전달로 할당된 변수와 할당한 변수의 값은 다른 메모리 공간에 저장된 별개의 값이다.

```jsx
var score = 80;

// copy 변수에는 score 변수의 값 80이 복사되어 할당된다.
var copy = score;

console.log(score, copy); // 80 80
console.log(score === copy); // true

// score 변수와 copy 변수의 값은 다른 메모리 공간에 저장된 별개의 값이다.
// 따라서 score 변수의 값을 변경해도 copy 변수의 값에는 어떠한 영향도 주지 않는다.
score = 100;

console.log(score, copy); // 100 80
console.log(score === copy); // false
```

- 변수를 할당할때 변수에 값이 전달되는 것이 아니라 메모리 주소가 전달된다. 변수와 같은 식별자는 값이 아니라 메모리 주소를 기억하고 있기 때문이다.
- 값에 의한 전달도 동일하게 값을 전달하는 것이 아니라 메모리 주소를 전달한다.
- 변수에 원시 값을 갖는 변수를 할당하면 두 변수의 원시 값은 서로 다른 메모리 공간에 저장된 별개의 값이 되어 어느 한쪽에서 재할당을 통해 값을 변경하더라도 서로 간섭할 수 없다.

## 11.2 객체

- 자바스크립트 객체의 관리 방식
    - 자바스크립트 객체는 프로퍼티 키를 인덱스로 사용하는 `해시 테이블(hash table)`과 유사하지만 높은 성능을 위해 일반적인 해시 테이블보다 나은 방법으로 객체를 구현한다.
    - 프로퍼티에 접근하기 위해 `동적 탐색(dynamic lookup)` 대신 `히든 클래스(hidden class)`라는 방식을 사용한다.

### 11.2.1 변경 가능한 값

> 객체(참조) 타입의 값, 즉 객체는 `변경 가능한 값(mutable value)`이다.
> 
- 객체를 할당한 변수가 기억하는 메모리 주소를 통해 메모리 공간에 접근하면 `참조 값(reference value)`에 접근할 수 있다.

```jsx
// 할당이 이뤄지는 시점에 객체 리터럴이 해석되고, 그 결과 객체가 생성된다.
var person = {
	name: 'Lee'
};

// person 변수에 저장되어 있는 참조 값으로 실제 객체에 접근한다.
console.log(person); // {name: "Lee"}
```

- 원시 값은 변경 불가능한 값이므로 원시 값을 갖는 변수의 값을 변경하려면 재할당 외에는 방법이 없다.
- 객체는 변경 가능한 값이므로 객체를 할당한 변수는 재할당 없이 객체를 직접 변경할 수 있다. 재할당 없이 프로퍼티를 동적으로 추가할 수도 있고 프로퍼티 값을 갱신할 수도 있으며 프로퍼티 자체를 삭제할 수도 있다.

```jsx
var person = {
	name: 'Lee',
};

// 프로퍼티 값 갱신
person.name = 'Kim';

// 프로퍼티 동적 생성
person.address = 'Seoul';

console.log(person); // {name: "Kim", address: "Seoul"}
```

- 객체는 메모리를 효율적으로 사용하기 위해 변경 가능한 값으로 설계되어 있다.
- 여러 개의 식별자가 하나의 객체를 공유할 수 있다.
- `얕은 복사(shallow copy)`와 `깊은 복사(deep copy)`
    - 객체를 프로퍼티 값으로 갖는 객체의 경우 얕은 복사는 한 단계까지만 복사하는걸 말한다.
    - 깊은 복사는 객체에 중첩되어 있는 객체까지 모두 복사하는 것을 말한다.
    
    ```jsx
    const o = { x: { y: 1 } };
    
    // 얕은 복사
    const c1 = { ...o }; // 35장 "스프레드 문법" 참고
    console.log(c1 === o); // false
    console.log(c1.x === o.x); // true
    
    // lodash의 cloneDeep을 사용한 깊은 복사
    // "npm install lodash"로 loadsh를 설치한 후, Node.js 환경에서 실행
    const _ = require('lodash');
    // 깊은 복사
    const c2 = _.cloneDeep(o);
    console.log(c2 === o); // false
    console.log(c2.x === o.x); // false
    ```
    
    - 얕은 복사와 깊은 복사로 생성된 객체는 원본과는 다른 객체다.
    
    ```jsx
    const v = 1;
    
    // "깊은 복사"라고 부르기도 한다.
    const c1 = v;
    console.log(c1 === v); // true
    
    const o = { x: 1 };
    
    // "얕은 복사"라고 부르기도 한다.
    const c2 = o;
    console.log(c2 === o); // true
    ```
    

### 11.2.2 참조에 의한 전달

```jsx
var person = {
	name: 'Lee'
};

// 참조 값을 복사(얕은 복사)
var copy = person;
```

- 객체를 가리키는 변수를 다른 변수에 할당하면 원본의 참조 값이 복사되어 전달된다. 이를 참조에 의한 전달이라 한다.
- 참조에 의한 전달 시 두 개의 식별자가 하나의 객체를 공유한다.

```jsx
var person = {
	name: 'Lee'
};

// 참조 값을 복사(얕은 복사). copy와 person은 동일한 참조 값을 갖는다.
var copy = person;

// copy와 person은 동일한 객체를 참조한다.
console.log(copy === person); // true

// copy를 통해 객체를 변경한다.
copy.name = 'Kim';

// person을 통해 객체를 변경한다.
person.address = 'Seoul';

// copy와 person은 동일한 객체를 가리킨다.
// 따라서 어느 한쪽에서 객체를 변경하면 서로 영향을 주고받는다.
console.log(person); // {name: "Kim", addressL "Seoul"}
console.log(copy); // {name: "Kim", address: "Seoul"}
```

- “값에 의한 전달”과 “참조에 의한 전달”은 식별자가 기억하는 메모리 공간에 저장되어 있는 값을 복사해서 전달한다는 면에서 동일하다.
- 자바스크립트에는 “참조에 의한 전달”은 존재하지 않고 “값에 의한 전달”만이 존재한다고 말할 수 있다.
- “공유에 의한 전달” 이라고 표현하는 경우도 있다.
