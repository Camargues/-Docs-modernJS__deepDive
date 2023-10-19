# 2장 - 자바스크립트란?

## 2.1 자바스크립트의 탄생

    **넷스케이프 커뮤니케이션즈(Netscape com-munications)**가 **브렌던 아이크(Brendan Eich)**가 개발한 경량 프로그래밍인 자바스크립트를 도입

## 2.2 자바스크립트의 표준화

    자바스크립트의 파편화를 방지하기 위해 넷스케이프 커뮤니케이션즈가 ECMA 인터내셔널에 자바스크립트 표준화를 요청

- 마이크로소프트에서 자바스크립트의 파생 버전인 “JScript”를 인터넷 익스플로러 3.0에 탑재하면서, **크로스 브라우징 이슈**가 발생하여 웹페이지 개발이 어려워짐
- 1997년 7월 **ECMA-262** 표준화 완성, **ECMAScript**로 명명
- **ESCMAScript 6(ECMAScript 2015, ES6)** - let/const 키워드, 화살표 함수, 클래스, 모듈 등 도입

| 버전 | 출시 연도 | 특징 |
| --- | --- | --- |
| ES1 | 1997 | 초판 |
| ES2 | 1998 | ISO/IEC 16262 국제 표준과 동일한 규격을 적용 |
| ES3 | 1999 | 정규 표현식, try … catch |
| ES5 | 2009 | HTML5와 함께 출현한 표준안. JSON, strict mode, 접근자 프로퍼티, 프로퍼티 어트리뷰트 제어, 향상된 배열 조작 기능(forEach, map, filter, reduce, some, every) |
| ES6(ECMAScript 2015) | 2015 | let/const, 클래스, 화살표 함수, 템플릿 리터럴, 디스트럭처링 할당, 스프레드 문법, rest 파라미터, 심벌, 프로미스, Map/Set, 이터러블, for … of, 제너레이터, Proxy, 모듈 import/export |
| ES7(ECMAScript 2016) | 2016 | 지수(**) 연산자, Array.prototype.includes, String.prototype.includes |
| ES8(ECMAScript 2017) | 2017 | async/await, Object 정적 메서드(Object.values, Object.entries, Object.getOwnPropertyDescriptors) |
| ES9(ECMAScript 2018) | 2018 | Object rest/spread 프로퍼티, Promise.prototype.finally, async generator, for await … of |
| ES10(ECMAScript 2019) | 2019 | Object.fromEntries, Array.prototype.flat, Array.prototype.flatMap, optional catch binding |
| ES11(ECMAScript 2020) | 2020 | String.prototype.matchAll, BigInt, globalThis, Promise.allSettled, null 병합 연산자, 옵셔널 체이닝 연산자, for … in enumeration order |

## 2.3 자바스크립트 성장의 역사

### 2.3.1 Ajax

- 서버와 브라우저가 **비동기(asynchronous)** 방식으로 데이터 교환하는 통신 기능
- Ajax의 등장으로 서버로부터 필요한 데이터만 전송받아 일부분만 한정적으로 렌더링 가능해짐

### 2.3.2 jQuery

- **DOM(Document Object Model)**의 제어가 쉬워지고, 크로스 브라우징 이슈 완화

### 2.3.3 V8 자바스크립트 엔진

- V8 자바스크립트 엔진의 등장으로 데스크톱 애플리케이션과 유사한 사용자 경험(UX; user experience)을 제공할 수 있게 됨

### 2.3.4 Node.js

- V8 자바스크립트 엔진으로 빌드된 자바스크립트 **런타임(runtime environment)** 환경
- 브라우저에서 독립된 자바스크립트 실행 환경이며, 주로 서버 사이드 애플리케이션 개발에 사용됨
- 비동기 I/O를 지원하며 **단일 스레드(single thread)** 이벤트 루프 기반으로 동작함으로써 **요청(request)** 처리 서능이 좋음
**SPA(Single Page Application)**에 적합함

### 2.3.5 SPA 프레임워크

- 모던 웹 애플리케이션의 성능과 사용자 경험이 높게 요구되면서 개발 규모와 복잡도가 상승함
- CBD(Component based development) 방법론을 기반으로 하는 SPA(Single Page Applicatioin)가 대중화되면서 Angular, React, Vue.js, Svelte 등 다양한 SPA 프레임워크/라이브러리가 많은 사용층을 확보함

## 2.4 자바스크립트와 ECMAScript

- ECMAScript는 자바스크립트 표준 사양인 ECMA-262를 말하며, 프로그래밍 언어의 핵심 문법을 규정
- 자바스크립트는 ECMAScript와 클라이언트 사이드 Web API를 아우르는 개념

## 2.5 자바스크립트의 특징

    자바스크립트는 HTML, CSS와 함께 웹을 구성하는 요소 중 하나로 **웹 브라우저에서 동작하는 유일한 프로그래밍 언어**

- 자바스크립트는 **인터프리터 언어(interpreter language)**다

| 컴파일러 언어 | 인터프린터 언어 |
| --- | --- |
| 코드가 실행되기 전 단계인 컴파일 타임에 소스코드 전체를 한번에 머신 코드로 변환한 후 실행한다. | 코드가 실행되는 단계인 런타임에 문 단위로 한 줄씩 중간 코드(intermediate code)인 바이트코드로 변환한 후 실행한다. |
| 실행 파일을 생성한다. | 실행 파일을 생성하지 않는다. |
| 컴파일 단계와 실행 단계가 분리되어 있다. 명시적인 컴파일 단계를 거치고, 명시적으로 실행 파일을 실행한다. | 인터프리트 단계와 실행 단계가 분리되어 있지 않다. 인터프리터는 한 줄씩 바이트코드로 변환하고 즉시 실행한다. |
| 실행에 앞서 컴파일은 단 한번 수행된다. | 코드가 실행될 때마다 인터프리트 과정이 반복 수행된다. |
| 컴파일과 실행 단계가 분리되어 있으므로 코드 실행 속도가 빠르다. | 인터프리트 단꼐와 실행 단계가 분리되어 있지 않고 반복 수행되므로 코드 실행 속도가 비교적 느리다. |
- 자바스크립트는 **명령형(imperative), 함수형(functional), 프로토타입 기반(prototype-based) 객체지향 프로그래밍**을 지원하는 **멀티 패러다임 프로그래밍 언어**
- 자바스크립트는 클래스 기반 객체지향 언어보다 효율적이면서 강력한 **프로토타입 기반의 객체지향 언어**다.
