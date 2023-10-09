# JavaScript_Study

<aside>
  
📖 해당 문서는 자바스크립트가 가지는 타 언어와의 **차이점 위주로 기술**되어 있습니다.
  
</aside>

### 목차
[변수](https://github.com/TTANGGIN/JavaScript_Study#%EB%B3%80%EC%88%98) <br/>
[자료형(Type)](https://github.com/TTANGGIN/JavaScript_Study#%EC%9E%90%EB%A3%8C%ED%98%95type) <br/>
[모듈](https://github.com/TTANGGIN/JavaScript_Study#%EB%AA%A8%EB%93%88) <br/>
[정규표현식](https://github.com/TTANGGIN/JavaScript_Study#%EC%A0%95%EA%B7%9C%ED%91%9C%ED%98%84%EC%8B%9D) <br/>
[참고자료](https://github.com/TTANGGIN/JavaScript_Study#%EC%B0%B8%EA%B3%A0%EC%9E%90%EB%A3%8C) <br/>


**미작성 & 공부 예정**
  - 자바스크립트 동작 원리 (하위문서로 작성)
      - Memory Heap
      - Call Stack
      - 런타임
          - Web API
          - Callback Queue
          - Event Loop
  - 콜백
      - Promise
          - then, catch
          - new Promise()
          - Promise All
      - async & await
  - Execution Context
      - Closure

---

# 변수

## 키워드 (+간단설명)

### const

- 재선언 : X
- 재할당 : X
- 상수와 같은 역할

### let

- 재선언 : X
- 재할당 : O

### var

- 재선언 : O
- 재할당 : O
- **쓰지말 것**

## 상세 설명

자바스크립트에서 `let`, `var`, `const`의 차이점은 주로 스코프와 재할당 가능성, 그리고 호이스팅에 있습니다.

1. **`var`**: 함수 레벨 스코프를 가지며, 호이스팅이 발생합니다. 변수를 재할당할 수 있습니다.
2. **`let`**: 블록 레벨 스코프를 가집니다. 호이스팅은 일어나지만 초기화 전에 변수에 접근할 수 없습니다(Temporal Dead Zone). 변수를 재할당할 수 있습니다.
3. **`const`**: 블록 레벨 스코프를 가지며, 변수에 한 번 값이 할당되면 그 값을 변경할 수 없습니다. 호이스팅은 일어나지만 초기화 전에 변수에 접근할 수 없습니다(Temporal Dead Zone).

### 호이스팅(Hoisting)이란?

호이스팅은 자바스크립트 엔진이 코드를 컴파일 하는 과정에서 변수 및 함수 선언을 스코프의 최상단으로 끌어올리는 (hoist) 특성을 말합니다.

### 작동 방식

변수 선언과 초기화는 두 단계로 이루어집니다.

1. **선언(Declaration)**: 변수가 메모리에 할당됩니다.
2. **초기화(Initialization)**: 변수에 값이 할당됩니다.

호이스팅은 이 선언 단계를 스코프의 최상단으로 끌어올립니다.

### 예시

### `var`와 호이스팅

```jsx
javascriptCopy code
console.log(a); // undefined
var a = 5;
console.log(a); // 5
```

위의 코드는 실제로 아래와 같이 동작합니다.

```jsx
javascriptCopy code
var a;
console.log(a); // undefined
a = 5;
console.log(a); // 5
```

### `let`과 `const`와 호이스팅

`let`과 `const`도 호이스팅이 발생하지만, 선언이 끌어올려지고 초기화가 이루어지기 전까지 해당 변수를 참조하면 오류가 발생합니다. 이를 Temporal Dead Zone (TDZ)이라고 합니다.

```jsx
javascriptCopy code
console.log(b); // ReferenceError: Cannot access 'b' before initialization
let b = 10;
```

이해를 돕기 위해, 실제로는 아래와 같이 동작한다고 생각할 수 있습니다.

```jsx
javascriptCopy code
// TDZ 시작
console.log(b); // ReferenceError
// TDZ 끝, 초기화
let b = 10;
```

**`var`**, **`letconst`** 각각의 호이스팅 특성을 이해하면 코드의 동작을 더 정확히 예측할 수 있습니다.

---

# 자료형(Type)

### number

- 숫자(정수, 실수) 자료형
- 변수에 숫자로 이루어진 값을 넣을 시 자동 할당

### string

- 문자열 자료형
- `‘ ’` 또는 `“ ”`으로 둘러싸인 값을 넣을 시 자동 할당

### booleans

- 참 또는 거짓을 나타내는 자료형
- `true`/`false`로 구분
- null
- undefined

## ⚠️null과 undefined⚠️

### **null**

- 변수에 **값이 없다는 상태**를 **할당**해놓은 상태
- 즉, 값이 없다는 **값**
- 자연적으로 할당될 수 없음

### **undefined**

- 변수에 **값이 할당되지 않음** (초기화 되지 않음)
- 즉, 메모리 공간은 할당되었지만, 해당 공간 내에 값이 할당되지 않음
- 자연적으로 할당 가능

---

# 모듈

<aside>
💡 순수 자바스크립트에서는 모듈 개념이 명확하게 존재하진 않음

</aside>

- 캡슐화와 유사하다고 생각하면 됨

## 인라인 자바스크립트 모듈화

```jsx
<script src="JS파일명.js"></script> // src는 스크립트 파일 경로
```

## Node.js 모듈화

### 로드 대상(모듈)

```jsx
exports.함수명 = function () {};
```

- `exports`를 이용해 다른 파일에서 해당 모듈의 함수 사용 가능

### 로드 주체

```jsx
var 변수명 = require('모듈파일 경로.js'); // ./module.js와 같은 경로
```

- `require()`를 통해 모듈을 불러와서 사용할 수 있음

## 라이브러리

### 라이브러리와 모듈의 차이

<aside>
💡 둘 다 비슷한 개념이지만,
모듈 : 프로그램을 구성하는 작은 부품으로서의 로직
라이브러리 : 자주 사용되는 로직의 편리한 재사용을 위해 정리된 일련의 코드들의 집합

</aside>

- 모듈 예시 : 로그인 유효성 검증 모듈, 쿼리 작성 모듈 등
- 라이브러리 예시 : 수식 계산 라이브러리, 자료구조 라이브러리 등

---

# 정규표현식

## 정규표현식이란?

<aside>
💡 문자열에서 특정한 문자를 찾아내는 도구

</aside>

- 정규표현식 자체를 하나의 언어라 볼 수 있음
- 수십 줄이 필요한 작업을 한 줄로 처리가능!

## 정규표현식 생성

- 정규표현식은 **컴파일**과 **실행** 두가지 단계로 이루어짐

### 컴파일

- 검출하고자 하는 패턴을 만드는 일
- 정규표현식 **객체를 생성**하는 과정

**정규표현식 리터럴**

```jsx
var pattern = /a/;
```

**정규표현식 객체 생성자**

```jsx
var pattern = new RegExp('a');
```

- 두가지 모두 같은 결과를 만들지만 각각의 장단점이 있으므로 상황에 맞게 사용권장

### 실행 1 : 메소드 실행

**RegExp.exec()**

```jsx
console.log(pattern.exec('abcdef')); // ["a"]
console.log(pattern.exec('bcdef')); // null
```

- 정규표현식의 패턴에 해당하는 값을 배열로 리턴
- 해당하는 값이 없으면 `null` 리턴
- 문자열 내 패턴이 중복해서 나타나도 하나만 출력됨

**RegExp.test()**

```jsx
console.log(pattern.test('abcdef')); // true
console.log(pattern.test('bcdef')); // false
```

- 정규표현식의 패턴에 해당하는 값이 존재하면 `true` 리턴
- 해당하는 값이 없으면 `false` 리턴

### 실행 2 : 문자열 메소드 실행

**String.match()**

```jsx
console.log('abcdef'.match(pattern)); // ["a"]
console.log('bcdef'.match(pattern)); // null
```

- RegExp.exec()와 유사함

**String.replace()**

```jsx
console.log('abcdef'.replace(pattern, 'A')); // Abcdef
```

- 문자열에서 패턴을 검색해서 이를 변경한 후 변경된 값 리턴

## 옵션

- 정규표현식 패턴 생성 시 옵션을 설정할 수 있다.

### i : 대소문자 구분 안함

```jsx
var p = /a/;    // 기존
var pi = /a/i;  // i 옵션

console.log(p.exec('Abcdef')); // null
console.log(pi.exec('Abcdef')); // ['A']
```

- 리터럴 뒤에 `i`를 추가하면 패턴은 대소문자를 구분하지 않는다.

### g : 모든 결과 리턴

```jsx
var p = /a/;    // 기존
var pg = /a/g;  // i 옵션

console.log(p.exec('abcdefa')); // ['a']
console.log(pg.exec('abcdefa')); // ['a', 'a']
```

- 리터럴 뒤에 `g`를 추가하면 패턴에 해당하는 **모든** 결과를 리턴한다.
- ---

# 참고자료

[생활코딩](https://opentutorials.org/course/1)

[노마드 코더 Nomad Coders](https://nomadcoders.co/)
