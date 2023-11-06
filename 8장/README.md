# 8장 - 제어문
> `제어문(control flow statement)`은 조건에 따라 `코드 블록을 실행(조건문)`하거나 `반복 실행(반복문)`할 때 사용한다. 일반적으로 코드는 위에서 아래 방향으로 순차적으로 실행되지만, 제어문을 사용하면 코드의 실행 흐름을 인위적으로 제어할 수 있다.
> 

## 8.1 블록문

> `블록문(block statement/compound statement)`은 0개 이상의 문을 중괄호로 묶은 것으로, 코드 블록 또는 블록이라고 부르기도 한다. 자바스크립트는 블록문을 하나의 실행 단위로 취급한다. 블록문은 단독으로 사용할 수도 있으나 일반적으로 제어문이나 함수를 정의할 때 사용하는 것이 일반적이다.
> 

```jsx
// 블록문
{
	var foo = 10;
}

// 제어문
var x = 1;
if (x < 10) {
	x++;
}

// 함수 선언문
function sum(a, b) {
	return a + b;
}
```

## 8.2 조건문

> `조건문(conditional statement)`은 주어진 `조건식(conditional expression)`의 평가 결과에 따라 코드 블록(블록문)의 실행을 결정한다. 조건식은 불리언 값으로 평가될 수 있는 표현식이다.
> 

### 8.2.1 if … else 문

> if … else 문은 주어진 `조건식(불리언 값으로 평가될 수 있는 표현식)`의 평가 결과, 즉 논리적 참 또는 거짓에 따라 실행할 코드 블록을 결정한다.
> 

```jsx
if (조건식) {
	// 조건식이 참이면 이 코드 블록이 실행된다.
} else {
	// 조건식이 거짓이면 이 코드 블록이 실행된다.
}
```

- if 문의 조건식은 불리언 값이 아닌 값으로 평가되면 자바스크립트 엔진에 의해 암죽억으로 불리언 값으로 강제 변환되어 실행할 코드 블록을 결정한다.
- 조건식을 추가하여 조건에 따라 실행될 코드 블록을 늘리고 싶으면 else if 문을 사용한다.

```jsx
if (조건식1) {
	// 조건식1이 참이면 이 코드 블록이 실행된다.
} else if (조건식2) {
	// 조건식2가 참이면 이 코드 블록이 실행된다.
} else {
	// 조건식1과 조건식2가 모두 거짓이면 이 코드 블록이 실행된다.
}
```

- else if 문과 else 문은 옵션이다.
- else if 문은 여러번 사용 할 수 있다.

```jsx
var num = 2;
var kind;

// if 문
if (num > 0) {
  kind = '양수'; // 음수를 구별할 수 없다
}
console.log(kind); // 양수

// if...else 문
if (num > 0) {
  kind = '양수';
} else {
  kind = '음수'; // 0은 음수가 아니다.
}
console.log(kind); // 양수

// if...else if 문
if (num > 0) {
  kind = '양수';
} else if (num < 0) {
  kind = '음수';
} else {
  kind = '영';
}
console.log(kind); // 양수
```

- 코드 블록 내의 문이 하나뿐이라면 중괄호 생략 가능

```jsx
var num = 2;
var kind;

if (num > 0)      kind = '양수';
else if (num < 0) kind = '음수';
else              kind = '영';

console.log(kind); // 양수
```

- if … else 문은 삼항 조건 연산자로 바꿔 사용 가능

```jsx
// if ... else 문
// x가 짝수이면 result 변수에 문자열 '짝수'를 할당하고, 홀수이면 문자열 '홀수'를 할당한다.
var x = 2;
var result;

if (x % 2) { // 2 % 2는 0이다. 이때 0은 false로 암묵적 강제 변환된다.
  result = '홀수';
} else {
  result = '짝수';
}

console.log(result); // 짝수

// 삼항 조건 연산자
var x = 2;

// 0은 false로 취급된다.
var result = x % 2 ? '홀수' : '짝수';
console.log(result); // 짝수

// 경우의 수가 세 가지인 경우의 삼항 조건 연산자
var num = 2;

// 0은 false로 취급된다.
var kind = num ? (num > 0 ? '양수' : '음수') : '영';

console.log(kind); // 양수
```

### 8.2.2 switch 문

> `switch 문`은 주어진 표현식을 평가하여 그 값과 일치하는 표현식을 갖는 `case 문`으로 실행 흐름을 옮긴다. case 문은 상황(case)을 의미하는 표현식을 지정하고 콜론으로 마친 뒤 실행할 문들을 위치시킨다. 일치하는 case 문이 없다면 실행 순서는 `default 문`으로 이동한다. default 문은 선택사항이다.
> 

```jsx
switch (표현식) {
	case 표현식1:
		switch 문의 표현식과 표현식1이 일치하면 실행될 문;
		break;
	case 표현식2:
		switch 문의 표현식과 표현식2가 일치하면 실행될 문;
		break;
	default:
		switch 문의 표현식과 일치하는 case 문이 없을 때 실행될 문;
}
```

- if … else 문은 논리적 참, 거짓으로 실행할 코드 블록을 결정한다.
- switch 문은 다양한 상황(case)에 따라 실행할 코드 블록을 결정할 때 사용한다.

```jsx
// 월을 영어로 변환한다. (11 → 'November')
var month = 11;
var monthName;

switch (month) {
  case 1: monthName = 'January';
  case 2: monthName = 'February';
  case 3: monthName = 'March';
  case 4: monthName = 'April';
  case 5: monthName = 'May';
  case 6: monthName = 'June';
  case 7: monthName = 'July';
  case 8: monthName = 'August';
  case 9: monthName = 'September';
  case 10: monthName = 'October';
  case 11: monthName = 'November';
  case 12: monthName = 'December';
  default: monthName = 'Invalid month';
}

console.log(monthName); // Invalid month
```

- 위 예제 실행결과로 ‘Invalid month’가 출력되는 이유는 switch 문의 일치하는 case 문으로 이동하여 실행 후 탈출하지 않고 모든 case 문과 default 문을 실행했기 때문이다. 이를 `폴스루(fall through)`라 한다.
- 위 예제의 올바른 switch 문은 `break 문`을 사용하여 코드블록에서 탈출 시켜야한다.

```jsx
// 월을 영어로 변환한다. (11 → 'November')
var month = 11;
var monthName;

switch (month) {
  case 1: monthName = 'January';
    break;
  case 2: monthName = 'February';
    break;
  case 3: monthName = 'March';
    break;
  case 4: monthName = 'April';
    break;
  case 5: monthName = 'May';
    break;
  case 6: monthName = 'June';
    break;
  case 7: monthName = 'July';
    break;
  case 8: monthName = 'August';
    break;
  case 9: monthName = 'September';
    break;
  case 10: monthName = 'October';
    break;
  case 11: monthName = 'November';
    break;
  case 12: monthName = 'December';
    break;
  default: monthName = 'Invalid month';
}

console.log(monthName); // November
```

- default 문의 실행이 종료되면 switch 문을 빠져나오기 때문에 break 문이 필요없다.
- 폴스루가 유용한 경우도 존재한다.

```jsx
var year = 2000; // 2000년은 윤년으로 2월이 29일이다.
var month = 2;
var days = 0;

switch (month) {
  case 1: case 3: case 5: case 7: case 8: case 10: case 12:
    days = 31;
    break;
  case 4: case 6: case 9: case 11:
    days = 30;
    break;
  case 2:
    // 윤년 계산 알고리즘
    // 1. 연도가 4로 나누어떨어지는 해(2000, 2004, 2008, 2012, 2016, 2020...)는 윤년이다.
    // 2. 연도가 4로 나누어떨어지더라도 연도가 100으로 나누어떨어지는 해(2000, 2100, 2200...)는 평년이다.
    // 3. 연도가 400으로 나누어떨어지는 해(2000, 2400, 2800...)는 윤년이다.
    days = ((year % 4 === 0 && year % 100 !== 0) || (year % 400 === 0)) ? 29 : 28;
    break;
  default:
    console.log('Invalid month');
}

console.log(days); // 29
```

## 8.3 반복문

> `반복문(loop statement)`은 조건식의 평가 결과가 참인 경우 코드 블록을 실행한다. 그 후 조건식을 다시 평가하여 여전히 참인 경우 코드 블록을 다시 실행한다. 이는 조건식이 거짓일 때까지 반복한다.
> 

### 8.3.1 for 문

> for 문은 조건식이 거짓으로 평가될 때까지 코드 블록을 반복 실행한다.
> 

```jsx
for (변수 선언문 또는 할당문; 조건식; 증감식) {
	조건식이 참인 경우 반복 실행될 문;
}

for (var i = 0; i < 2; i++) {
	console.log(i)
}
// 실행결과
// 0
// 1
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/9f69fc70-40b2-485c-b26d-6bdfa6b5e397/78f79b69-54a7-4b3d-8300-750e3484f6cb/Untitled.png)

1. for 문을 실행하면 맨 먼저 변수 선언문 var i = 0이 실행된다. 변수 선언문은 단 한번만 실행된다.
2. 변수 선언문의 실행이 종료되면 조건식이 실행된다. 현재 i 변수의 값은 0이므로 조건식의 평가 결과는 true다.
3. 조건식의 평가 결과가 true이므로 코드 블록이 실행된다. 증감문으로 실행 흐름이 이동하는 것이 아니라 코드 블록으로 실행 흐름이 이동하는 것에 주의.
4. 코드 블록의 실행이 종료되면 증감식 i++가 실행되어 i 변수의 값은 1이 된다.
5. 증감식 실행이 종료되면 다시 조건식이 실행된다. 변수 선언문이 실행되는 것이 아니라 조건식이 실행된다는 점에 주의. 현재 i 변수의 값은 1이므로 조건식의 평과 결과는 true다.
6. 조건식의 평가 결과가 true이므로 코드 블록이 다시 실행된다.
7. 코드 블록의 실행이 종료되면 증감식 i++가 실행되어 i 변수의 값은 2가 된다.
8. 증감식 실행이 종료되면 다시 조건식이 실행된다. 현재 i 변수의 값은 2이므로 조건식의 평가 결과는 false다. 조건식의 평가 결과가 false이므로 for 문의 실행이 종료된다.
- for 문의 변수 선언문, 조건식, 증감식은 모두 옵션이므로 반드시 사용할 필요는 없다.
- 어떤 식도 선언하지 않으면 무한루프가 된다.

```jsx
// 무한루프
for (;;) { ... }
```

- for 문 내에 for 문을 중첩해 사용할 수 있다. (중첩 for문)

```jsx
// 이중 중첩 for문
for (var i = 1; i <= 6; i++) {
  for (var j = 1; j <= 6; j++) {
    if (i + j === 6) console.log(`[${i}, ${j}]`);
  }
}
// 실행 결과
// [1, 5]
// [2, 4]
// [3, 3]
// [4, 2]
// [5, 1]
```

### 8.3.2 while 문

> while 문은 주어진 조건식의 평가 결과가 참이면 코드 블록을 계속해서 반복 실행한다. while 문은 반복 횟수가 불명확할 때 주로 사용하며, 조건문의 평가 결과가 거짓이 되면 코드 블록을 실행하지 않고 종료한다.
> 

```jsx
var count = 0;

// count가 3보다 작을 때까지 코드 블록을 계속 반복 실행한다.
while (count < 3) {
  console.log(count); // 0 1 2
  count++;
}
```

- 조건식의 평가 결과가 언제나 참이면 무한루프가 된다.

```jsx
// 무한루프
while (true) { ... }
```

- 무한루프에서 탈출하기 위해서는 코드 블록 내에 if 문으로 탈출 조건을 만들고 break 문으로 코드 블록을 탈출한다.

```jsx
var count = 0;

// 무한루프
while (true) {
  console.log(count);
  count++;
  // count가 3이면 코드 블록을 탈출한다.
  if (count === 3) break;
} // 0 1 2
```

### 8.3.3 do … while 문

> do … while 문은 코드 블록을 먼저 실행하고 조건식을 평가한다. 코드 블록은 무조건 한 번 이상 실행된다.
> 

```jsx
var count = 0;

// count가 3보다 작을 때까지 코드 블록을 계속 반복 실행한다.
do {
  console.log(count);
  count++;
} while (count < 3); // 0 1 2
```

## 8.4 break 문

> break 문은 레이블 문, 반복문(for, for … in, for … of, while, do … while) 또는 switch 문의 코드 블록을 탈출한다. 위 경우 외에 break 문을 사용하면 SyntaxError(문법 에러)가 발생한다.
> 

```jsx
if (true) {
  break; // Uncaught SyntaxError: Illegal break statement
}
```

- `레이블 문(label statement)`이란 식별자가 붙은 문을 말한다.

```jsx
// foo라는 레이블 식별자가 붙은 레이블 문
foo: console.log('foo');
```

- 레이블 문은 프로그램의 실행 순서를 제어하는 데 사용한다.
- 레이블 문을 탈출하려면 break 문에 레이블 식별자를 지정한다.

```jsx
// foo라는 식별자가 붙은 레이블 블록문
foo: {
  console.log(1);
  break foo; // foo 레이블 블록문을 탈출한다.
  console.log(2);
}

console.log('Done!');
```

- 중첩된 for 문의 내부 for 문에서 break 문을 실행하면 내부 for 문을 탈출하여 외부 for 문으로 진입한다.
- 내부 for 문이 아닌 외부 for 문을 탈출하려면 레이블 문을 사용한다.

```jsx
// outer라는 식별자가 붙은 레이블 for 문
outer: for (var i = 0; i < 3; i++) {
  for (var j = 0; j < 3; j++) {
    // i + j === 3이면 outer라는 식별자가 붙은 레이블 for 문을 탈출한다.
    if (i + j === 3) break outer;
    console.log(`inner [${i}, ${j}]`);
  }
}

console.log('Done!');
```

- break 문은 반복문, switch 문에서도 사용 가능하며, 이 경우는 break 문에 레이블 식별자를 지정하지 않는다.
- break 문은 박복문을 더 이상 진행하지 않아도 될 때 불필요한 반복을 회피할 수 있어 유용함.

```jsx
var string = 'Hello World.';
var search = 'l';
var index;

// 문자열은 유사배열이므로 for 문으로 순회할 수 있다.
for (var i = 0; i < string.length; i++) {
  // 문자열의 개별 문자가 'l'이면
  if (string[i] === search) {
    index = i;
    break; // 반복문을 탈출한다.
  }
}

console.log(index); // 2

// 참고로 String.prototype.indexOf 메서드를 사용해도 같은 동작을 한다.
console.log(string.indexOf(search)); // 2
```

## 8.5 continue 문

> continue 문은 반복문의 코드 블록 실행을 현 지점에서 중단하고 반복문의 증감식으로 실행 흐름을 이동시킨다.
> 

```jsx
var string = 'Hello World.';
var search = 'l';
var count = 0;

// 문자열은 유사배열이므로 for 문으로 순회할 수 있다.
for (var i = 0; i < string.length; i++) {
  // 'l'이 아니면 현 지점에서 실행을 중단하고 반복문의 증감식으로 이동한다.
  if (string[i] !== search) continue;
  count++; // continue 문이 실행되면 이 문은 실행되지 않는다.
}

console.log(count); // 3

// 참고로 String.prototype.match 메서드를 사용해도 같은 동작을 한다.
const regexp = new RegExp(search, 'g');
console.log(string.match(regexp).length); // 3

// 위와 동일하게 작동한다
for (var i = 0; i < string.length; i++) {
  // 'l'이면 카운트를 증가시킨다.
  if (string[i] === search) count++;
}
```

- if 문 내에서 실행해야 할 코드가 한 줄이라면 continue 문을 사용했을 때보다 간편하고 가독성이 좋다
- if 문 내에서 실행해야 할 코드가 길다면 continue 문을 사용하는 편이 가독성이 더 좋다

```jsx
// continue 문을 사용하지 않으면 if 문 내에 코드를 작성해야 한다.
for (var i = 0; i < string.length; i++) {
  // 'l'이면 카운트를 증가시킨다.
  if (string[i] === search) {
    count++;
    // code
    // code
    // code
  }
}

// continue 문을 사용하면 if 문 밖에 코드를 작성할 수 있다.
for (var i = 0; i < string.length; i++) {
  // 'l'이 아니면 카운트를 증가시키지 않는다.
  if (string[i] !== search) continue;

  count++;
  // code
  // code
  // code
}
```
