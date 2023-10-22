## 4.1 변수란 무엇인가? 왜 필요한가?

- 자바크립트 엔진이 자바스크립트 코드를 `계산(평가 evaluation)`하려면 `기호(리터럴 literal과 연산자 operator)`의 의미를 알고 있어야 하며, `식(표현식 expression)`의 의미도 `해석(파싱 parsing)`할 수 있어야 한다.
- `메모리(memory)`는 데이터를 저장할 수 있는 `메모리 셀(memory cell)`의 집합체다. 메모리 셀 하나의 크기는 `1바이트(8비트)`이며, 컴퓨터는 메모리 셀의 크기, 즉 1바이트 단위로 데이터를 `저장(write)`하거나 `읽어(read)` 들인다.
- 메모리에 저장되는 모든 값은 2진수로 저장된다.
- `변수(variable)`는 하나의 값을 저장하기 위해 확보한 메모리 공간 자체 또는 그 메모리 공간을 식별하기 위해 붙인 이름을 말하며, 값의 위치를 가리키는 상징적인 이름이다.
- 메모리 공간에 저장된 값을 식별할 수 있는 고유한 이름을 `변수 이름(또는 변수명)` 이라 하며, 변수에 저장된 값을 `변수 값`이라고 한다.
- 변수에 값을 저장하는 것을 `할당(assignment 대입,저장)`이라 하고, 변수의 저장된 값을 읽어 들이는 것을 `참조(reference)`라 한다.

## 4.2 식별자

    식별자는 어떤 값을 구별해서 식별할 수 있는 고유한 이름을 말한다.

- 변수 이름을 `식별자(identifier)`라고 한다.
- 식별자는 값이 아니라 `메모리 주소`를 기억하고 있다.
- 변수, 함수, 클래스 등의 이름과 같은 식별자는 네이밍 규칙을 준수해야 하며, `선언(declaration)`에 의해 자바스크립트 엔진에 식별자의 존재를 알린다.

## 4.3 변수 선언

    변수 선언(variable declaration)이란 변수를 생성하기 위해 공간을 확보(allocate)하고 변수 이름과 메모리 공간의 주소를 연결(name binding)해서 값을 저장할 수 있게 준비하는 것이다.

- 변수 선언에 의해 확보된 메모리 공간은 `해제(release)`되기 전까지 보호된다.
- 변수를 사용하려면 반드시 선언이 필요하다. 변수를 선언할 때는 `var, let, const`키워드를 사용한다.
- 변수를 선언 후 값을 할당하지 않으면, `undefined`라는 값이 할당되어 초기화된다.
- var 키워드를 사용한 변수 선언은 선언 단계와 초기화 단계가 동시에 진행된다.

## 4.4 변수 선언의 실행 시점과 변수 호이스팅

    변수 선언은 소스코드가 한 줄씩 순차적으로 실행되는 시점(런타임 runtime)이 아니라 그 이전 단계에서 먼저 실행된다.

- 변수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징을 `변수 호이스팅(variable hoisting)`이라 한다.

## 4.5 값의 할당

    변수에 값을 할당(assignment 대입,저장)할 때는 할당 연산자 =를 사용한다. 할당 연산자는 우변의 값을 좌변에 변수에 할당한다.

- 변수 선언은 소스코드가 순차적으로 실행되는 시점인 런타임 이전에 먼저 실행되지만 값의 할당은 소스코드가 순차적으로 실행되는 시점인 런타임에 실행된다.

## 4.6 값의 재할당

    재할당은 변수에 저장된 값을 다른 값으로 변경한다. 그래서 변수라고 한다.

- 값을 재할당할 수 없어서 변수에 저장된 값을 변경할 수 없다면 변수가 아니라 상수(constant)라 한다.

## 4.7 식별자 네이밍 규칙

    식별자(identifier)는 어떤 값을 구별해서 식별해낼 수 있는 고유한 이름을 말한다.

- 식별자는 특수문자를 제외한 문자, 숫자, 언더스코어(_), 달러 기호($)를 포함할 수 있다.
- 단, 식별자는 특수문자를 제외한 문자, 언더스코어(_), 달러 기호($)로 시작해야 한다. 숫자로 시작하는 것은 허용하지 않는다.
- 예약어는 식별자로 사용할 수 없다.

| 자바스크립트 예약어 | | | | | |
| --- | --- | --- | --- | --- | --- |
| await | break | case | catch | class | const |
| continue | debugger | default | delete | do | else |
| enum | export | extends | false | finally | for |
| function | if | implements | import | in | instanceof |
| interface | let | new | null | package | private |
| protected | public | return | super | static | switch |
| this | throw | true | try | typeof | var |
| void | while | with | yield |  |  |
- 변수는 쉼표(,)로 구분해 하나의 문에서 여러 개를 한번에 선언할 수 있다.

```jsx
var person, $elem, _name, first_name ,val1;
```

- ES5부터 유니코드 문자를 허용하므로 알파벳 외의 한글이나 일본어 식별자도 사용할 수 있다.

```jsx
var 이름, なまえ
```

- 명명 규칙에 위배되는 변수 이름 예시

```jsx
var first-name; // SyntaxError: Unexpected token -
var 1st;        // SyntaxError: Invalid or unexpected token
var this;       // SyntaxError: Unexpected token this
```

- 자바스크립트는 대소문자를 구별하므로 아래 변수는 각각 별개의 변수다.

```jsx
var firstname;
var firstName;
var FIRSTNAME;
```

- 네이밍 컨벤션(naming convention)은 가독성 좋게 구분하기 위해 규정한 명명 규칙이다.

```jsx
// 카멜 케이스(camelCase)
var firstName;

// 스네이크 케이스(snake_case)
var first_name;

// 파스칼 케이스(PascalCase)
var FirstName;

// 헝가리언 케이스(typeHungarianCase)
var strFirstName; // type + identifier
var $elem = document.getElementById('myId'); // DOM 노드
var observable$ = fromEvent(document, 'click'); // RxJS 옵저버블
```
