# 48. 모듈

## 1. 모듈 module 이란

### 애플리케이션을 구성하는 개별적 요소로서 재사용 가능한 코드 조각을 말한다.

### 자신만의 파일 스코프를 갖는 모듈의 모든 자산은 캡슐화되어 다른 모듈에서 접근할 수없다.
- 자신만의 파일 스코프를 갖는 모듈의 변수, 함수, 객체 등은 기본적으로 비공개 상태다.

### export : 공개가 필요한 자산에 한정하여 명시적으로 선택적 공개

### import : 모듈이 export 한 자산 중 일부 또는 전체를 선택해 자신의 스코프 내로 불러들여 재사용할 수 있다.

### 코드의 단위를 명확히 분리하여 애플리케이션을 구성할 수 있고, 재사용성이 좋아서 개발 효율성과 유지보수성을 높일 수 있다. 

## 2. 자바스크립트 모듈

### 한계
- 자바스크립트 파일을 여러 개의 파일로 분리하여 script 태그로 로드해도 분리된 자바스크립트 파일들은 결국 하나의 자바스크립트 파일 내에 있는 것처럼 동작한다.
- 즉, 모든 자바스크립트 파일은 하나의 전역을 공유한다.
- 따라서 분리된 자바스크립트 파일들의 전역 변수가 중복되는 등의 문제가 발생할 수 있다.

### node.js
- 모듈 시스템의 표준인 CommonJS를 채택하여 현재는 CommonJS 사양과 100% 동일하지는 않지만 기본적으로 CommonJS 사양을 따르고 있다.
- 즉, Node.js는 ECMAScript 표준 사양은 아니지만 모듈 시스템을 지원한다.
- 따라서 Node.js 환경에서는 파일별로 독립적인 파일 스코프(모듈 스코프)를 갖는다.

## 3. ESM (ES6 모듈)

### 클라이언트 사이드 자바스크립트에서도 동작하는 모듈 기능

### 동작
- script 태그에 type="module" 어트리뷰트를 추가 하면 로드된 자바스크립트 파일은 모듈로서 동작한다.

### 확장자
- 일반적인 자바스크립트 파일이 아닌 ESM임을 명확히 하기 위해 mjs 를 사용할 것을 권장한다.

### 클래스와 마찬가지로 기본적으로 strict mode가 적용된다. 

### ESM은 파일 자체의 독자적인 모듈 스코프를 제공한다.
- 따라서 모듈 내에서 var 키워드로 선언한 변수는 더는 전역 변수가 아니며 window 객체의 프로퍼티도 아니다.
- 【 예제 48-05 】  
  // foo.mjs // x 변수는 전역 변수가 아니며 window 객체의 프로퍼티도 아니다.  
  var x = 'foo';  
  console . log(x); // foo console . log(window . x); // undefined
- 【 예제 48-06 】  
  // bar.mjs // x 변수는 전역 변수가 아니며 window 객체의 프로퍼티도 아니다.  
  // foo.mjs에서 선언한 x 변수와 스코프가 다른 변수다.  
  var x = 'bar';  
  console . log(x); // bar console . log(window . x); // undefined

### 모듈 내에서 선언한 식별자는 모듈 외부에서 참조할 수 없다. 모듈 스코프가 다르기 때문이다.
- 【 예제 48-08 】  
  // foo.mjs const x = 'foo';  
  console . log(x); // foo
- 【 예제 48-09 】  
  // bar.mjs console . log(x); // ReferenceError: x is not defined
- 

### export
- 모듈 내부에서 선언한 식별자를 외부에 공개하여 다른 모듈들이 재사용할 수 있게 한다. 
- 사용법
	- 선언문 앞에 사용하여 하나씩 export한다. 
		- export const pi = Math . PI;
	- 하나의 객체로 구성하여 한번에 export한다. 
		- export { pi , square , Person };
- 대상
	- 변수, 함수, 클래스 등 모든 식별자

### import
- 다른 모듈에서 export한 식별자를 자신의 모듈 스코프 내부로 로드한다.
- 사용법
	- 다른 모듈이 export한 식별자 이름으로 import한다.
		- import { pi , square , Person } from ' . /lib . mjs';
		- ESM의 경우 파일 확장자를 생략할 수 없다. 
		- as를 이용하여 다른 이름으로 변경할 수 있다. 
		- import { pi as PI , square as sq , Person as P } from ' . /lib . mjs';
	- 모듈이 export한 식별자 이름을 일일이 지정하지 않고 하나의 이름으로 한 번에 import할 수도 있다.
		- import * as lib from ' . /lib . mjs';
		- 이때 import되는 식별자는 as 뒤에 지정한 이름의 객체에 프로퍼티로 할당된다.

### default
- 모듈에서 하나의 값만 export한다면 default 키워드를 사용할 수 있다.
- var , let , const 키워드는 사용할 수 없다.
- default 키워드와 함께 export한 모듈은 {} 없이 임의의 이름으로 import한다.
