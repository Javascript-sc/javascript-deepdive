## 40장 이벤트

####40.1 이벤트 드리븐 프로그래밍

- 브라우저는 처리해야 할 특정 사건이 발생하면 이를 감지하여 이벤트를 발생시킨다.
- 예_) 클릭, 키보드 입력, 마우스 이동 등

**이벤트 드리븐 프로그래밍**
이벤트 드리븐 프로그래밍(Event-Driven Programming)은 프로그램이 외부 이벤트 또는 사용자 입력에 응답하여 동작하는 프로그래밍 패러다임이다.
이벤트 드리븐 프로그래밍은 주로 그래픽 사용자 인터페이스(GUI) 및 웹 애플리케이션, 네트워크 통신 등 다양한 응용 프로그램에서 사용된다.
이 패러다임의 핵심 아이디어는 프로그램이 외부에서 발생하는 이벤트에 대응하고, 해당 이벤트가 발생할 때 특정 동작을 수행하는 방식이다.

* * *

- 애플리케이션이 특정 타입의 이벤트에 대해 반응하여 어떤 일을 하고 싶다면 해당 타입 이벤트가 발생했을 때 호출될 함수를 브라우저에 알려 호출을 위임한다.
- 이때 이벤트가 발생했을 때 호출될 함수를 `이벤트 핸들러(event handler)`라 하고, 이벤트 핸들러 호출을 위임하는 것을 `이벤트 핸들러 등록`이라 한다.
- 이벤트와 그에 대응하는 함수(이벤트 핸들러)를 통해 사용자와 애플리케이션은 상호작용을 하고 프로그램의 흐름을 이벤트 중심으로 제어하는 프로그래밍 방식을 `이벤트 드리븐 프로그래밍`이라 한다.

#### 40.2 이벤트 타입
- 이벤트 종류를 나타내는 문자열이다.
- 이벤트 타입은 약 *200*여개가 있으며, 상세 목록은 MDN의 Event reference에서 확인할 수 있다.

###### 40.2.1 마우스 이벤트
이벤트 타입	| 이벤트 발생 시점
---|---
click	| 마우스 버튼을 클릭했을 때
dblclick  |	마우스 버튼을 더블 클릭했을 때
mousedown |	마우스 버튼을 눌렀을 때
mouseup	 | 누르고 있던 마우스 버튼을 놓았을 때
mousemove | 마우스 커서를 움직였을 때
mouseenter | 마우스 커서를 HTML 요소 안으로 이동했을 때(버블링되지 않는다)
mouseover | 마우스 커서를 HTML 요소 안으로 이동했을 때 (버블링된다)
mouseleave | 마우스 커서를 HTML 요소 밖으로 이동했을 때(버블링되지 않는다)
mouseout | 마우스 커서를 HTML 요소 밖으로 이동했을 때(버블링된다)

* * *

###### 40.2.2 키보드 이벤트
이벤트 타입	| 이벤트 발생 시점
---|---
keydown | 모든 키를 눌렀을 때 발생한다. ※ control, option, shift, tab, delete, enter, 방향키, 문자, 숫자, 특수 문자 키를 눌렀을 때 발생한다. 단, 문자, 숫자, 특수 문자, enter 키를 눌렀을 때는 연속적으로 발생하지만 그 외의 키는 한 번만 발생한다.	
keypress | 문자 키를 눌렀을 때 연속적으로 발생한다. ※ 폐지되었음	
keyup |	누르고 있던 키를 놓았을 때 한 번만 발생한다. ※ keydown 이벤트와 마찬가지
	
###### 40.2.3 포커스 이벤트
이벤트 타입 | 이벤트 발생 시점
---|---
focus | HTML 요소가 포커스를 받았을 때(버블링되지 않는다)
blur | HTML 요소가 포커스를 잃었을 때(버블링되지 않는다)
focusin | HTML 요소가 포커스를 받았을 때(버블링된다)
focusout | HTML 요소가 포커스를 잃었을 때(버블링된다)

###### 40.2.4 폼 이벤트
이벤트 타입 | 이벤트 발생 시점
---|---
submit | form 요소 내의 submit 버튼을 클릭했을 때
reset | form 요소 내의 reset 버튼을 클릭했을 때(최근에는 사용 안함) 

###### 40.2.5 값 변경 이벤트
이벤트 타입 | 이벤트 발생 시점
---|---
input | input(text, checkbox, radio), select, textarea 요소의 값이 입력되었을 때
change | input(text, checkbox, radio), select, textarea 요소의 값이 변경되었을 때 ※ change 이벤트는 input 이벤트와는 달리 HTML 요소가 포커스를 잃었을 때 사용자 입력이 종료되었다고 인식하여 발생한다. 즉, 사용자가 입력을 하고 있을 때는 input 이벤트가 발생하고 사용자 입력이 종료되어 값이 변경되면 change 이벤트가 발생한다.	
readystatechange | HTML 문서의 로드와 파싱 상태를 나타내는 document.readyState 프로퍼티 값(‘loading’, ‘interactive’, ‘complete’)이 변경될 때
40.2.6 DOM 뮤테이션 이벤트
이벤트 타입 | 이벤트 발생 시점
---|---
DOMContentLoaded | HTML 문서의 로드와 파싱이 완료되어 DOM 생성이 완료되었을 때

###### 40.2.7 뷰 이벤트
이벤트 타입 | 이벤트 발생 시점
---|---
resize | 브라우저 윈도우(window)의 크기를 리사이즈할 때 연속적으로 발생한다. ※ 오직 window 객체에서만 발생한다.	
scroll | 웹페이지(document) 또는 HTML 요소를 스크롤할 때 연속적으로 발생한다.

###### 40.2.8 리소스 이벤트
이벤트 타입 | 이벤트 발생 시점
---|---
load | DOMContentLoaded 이벤트가 발생한 이후, 모든 리소스(이미지, 폰트 등)의 로딩이 완료되었을 때(주로 window 객체에서 발생)
unload | 리소스가 언로드될 때(주로 새로운 웹페이지를 요청한 경우)
abort | 리소스 로딩이 중단되었을 때
error | 리소스 로딩이 실패했을 때

#### 40.3 이벤트 핸들러 등록
- 이벤트 핸들러(event handler, event listener)는 이벤트가 발생했을 때 브라우저에 호출을 위임한 함수다.
- 이벤트가 발생했을 때 브라우저에게 이벤트 핸들러의 호출을 위임하는 것을 이벤트 핸들러 등록이라 한다.

###### 40.3.1 이벤트 핸들러 어트리뷰트 방식
- HTML 요소의 어트리뷰트 중에는 이벤트에 대응하는 이벤트 핸들러 어트리뷰트가 있다.
- 어트리뷰트 이름은 on 접두사와 이벤트 타입으로 이루어져 있다.
- 이벤트 핸들러 어트리뷰트 값으로 함수 호출문 등의 문을 할당하면 이벤트 핸들러가 등록된다.
``` html
<!DOCTYPE html>
<html>
  <body>
    <button onclick="sayHi('Seo')">Click me!</button>
    <script>
      function sayHi(name) {
        console.log(`Hi! ${name}.`);
      }
    </script>
  </body>
</html>
```

- 주의할 점은 이벤트 핸들러 어트리뷰트 값으로 함수 참조가 아닌 함수 호출문 등의 문을 할당한다는 것이다.
- 이벤트 핸들러 등록이란 함수 호출을 브라우저에게 위임하는 것이므로, 이벤트 핸들러를 등록할 때 콜백 함수와 마찬가지로 함수 참조를 등록해야 브라우저가 이벤트 핸들러를 호출할 수 있다.
- 만약 함수 참조가 아니라 함수 호출문을 등록하면 함수 호출문의 평과 결과가 이벤트 핸들러로 등록된다.
- 함수를 반환하는 고차 함수 호출문을 이벤트 핸들러로 등록한다면 문제가 없겠지만 함수가 아닌 값을 반환하는 함수 호출문을 이벤트 핸들러로 등록하면 브라우저가 이벤트 핸들러를 호출할 수 없다.
- 이벤트 핸들러 어트리뷰트 값은 사실 암묵적으로 생성될 이벤트 핸들러의 함수 몸체를 의미한다.
- 즉, 어트리뷰트는 파싱되어 함수를 암묵적으로 생성하고, 핸들러 어트리뷰트 이름과 동일한 키 onclick 이벤트 핸들러 프로퍼티에 할당한다.
- *이벤트 핸들러 어트리뷰트 방식은 오래된 코드에서 이 방식을 사용한 경우가 있어 알아둘 필요는 있지만 더는 사용하지 않는 것이 좋다.*
이유: HTML과 자바스크립트는 분리하는 것이 좋기 때문
- 단, 모던 자바스크립트에서는 이벤트 핸들러 어트리뷰트 방식을 사용하는 경우가 있다.
- CBD방식의 React, Angular, Vue 같은 프레임워크/라이브러리에서는 이벤트 핸들러 어트리뷰트 방식으로 이벤트를 처리한다.
- CBD에서는 HTML, CSS, 자바스크립트를 다른 개별적인 요소가 아닌 뷰를 구성하기 위한 구성 요소로 보기 때문에 관심사가 다르다고 생각하지 않는다.


###### 40.3.2 이벤트 핸들러 프로퍼티 방식
- window 객체와 Document, HTMLElement 타입의 DOM 노드 객체는 이벤트에 대응하는 이벤트 핸들러 프로퍼티를 가지고 있다.
- 이벤트 핸들러 프로퍼티의 키는 이벤트 핸들러 어트리뷰트와 마찬가지로 onclick과 같이 on 접두사와 이벤트의 종류를 나타내는 이벤트 타입으로 이루어져 있다.

``` html
<!DOCTYPE html>
<html>
  <body>
    <button>Click me!</button>
    <script>
			const $button = document.querySelector('button');
			
			// 이벤트 핸들러 프로퍼티에 이벤트 핸들러를 바인딩
			$button.onclick = function () {
				console.log('button click');
			};
    </script>
  </body>
</html>
```

- 이벤트 핸들러를 등록하기 위해서는 이벤트를 발생시킬 객체인 **이벤트 타깃(event target)**과 이벤트의 종류를 나타내는 문자열인 이벤트 타입 그리고 이벤트 핸들러를 지정할 필요가 있다.
- 이벤트 핸들러는 대부분 이벤트를 발생시킬 이벤트 타깃에 바인딩한다.
- 이벤트 핸들러는 이벤트 타깃 또는 전파된 이벤트를 캐치할 DOM 노드 객체에 바인딩한다.
- 이벤트 핸들러 어트리뷰트 방식도 결과적으로는 이벤트 핸들러 프로퍼티 방식과 동일하다고 할 수 있다.
- 단, 이벤트 핸들러 프로퍼티 방식은 HTML과 자바스크립트가 뒤섞이는 문제를 해결할 수 있다.
- 그러나 이벤트 핸들러 프로퍼티에 하나의 이벤트 핸들러만 바인딩할 수 있다는 단점이 있다.

###### 40.3.3 addEventListener 메서드 방식
- DOM Level 2에서 도입된 EventTarget.prototype.addEventListener 메서드를 사용해 이벤트 핸들러를 등록할 수 있다.
- addEventListener 메서드의 구성
- 이벤트 타깃.addEventListener

첫 번째 매개변수 : 이벤트 타입
두 번째 매개변수 : 이벤트 핸들러
세 번째 매개변수 : captuer 사용 여부
첫 번째 매개변수에 이벤트 타입을 전달하는데, 프로퍼티 방식과는 달리 on접두사를 붙이지 않는다.


- addEventListener 메서드 방식과 이벤트 핸들러 프로퍼티 방식 둘 다 사용하면, 이벤트가 발생했을 시 각각에 바인딩 된 이벤트 핸들러가 모두 호출된다.
- addEventListener 메서드는 하나 이상의 이벤트 핸들러를 등록할 수 있다. (호출은 등록된 순서대로)

- 참조가 동일한 이벤트 핸들러를 중복 등록하면 하나의 이벤트 핸들러만 등록된다.

#### 40.4 이벤트 핸들러 제거
- 이벤트 핸들러를 제거하는 것은 웹 애플리케이션에서 이벤트 관리의 중요한 부분이다.
- removeEventListener 메서드를 사용하여 이벤트 핸들러를 제거할 수 있다. 
- addEventListener 메서드로 등록한 이벤트 핸들러를 제거하려면 `EventTarget.prototype.removeEventListener` 메서드를 사용한다.

(정확한 매칭)
- removeEventListener에 전달한 인수는 addEventListener 메서드와 동일하다. 
- 단, addEventListener 메서드에 전달한 인수와 removeEventListener 메서드에 전달한 인수가 동일하지 않으면 이벤트 핸들러가 제거되지 않는다.
- 즉, 무명 함수를 이벤트 핸들러로 등록한 경우 제거할 수 없다.

(기명 함수를 사용한 경우)
- 기명 이벤트 핸들러 내부에서 removeEventListener 메서드를 호출해 이벤트 핸들러를 제거하는 것은 가능하다.
``` html 
// 이벤트 핸들러 등록
function myEventHandler() {
    // 이벤트 처리 로직
}
element.addEventListener('click', myEventHandler);
// 이벤트 핸들러 제거
element.removeEventListener('click', myEventHandler);
```
- 이때 이벤트 핸들러는 단 한번만 호출된다.
- 기명 함수를 이벤트 핸들러로 등록할 수 없다면 호출된 함수인 함수 자신을 가리키는 `arguments.callee`를 사용할 수도 있다.
- 그러나 이 방법은 ES5의 strict mode에서는 금지되었다.

(이벤트 핸들러 프로퍼티 방식)
- 객체의 프로퍼티로 이벤트 핸들러를 등록한 경우, 해당 프로퍼티에 null을 할당하여 제거할 수 있습니다.



#### 40.5 이벤트 객체
- 이벤트가 발생하면 이벤트 객체가 동적으로 생성된다. 생성된 이벤트 객체는 이벤트 핸들러의 첫 번째 인수로 전달된다.
- 브라우저가 이벤트 핸들러를 호출할 때 이벤트 객체를 인수로 전달한다.
- 이벤트 객체를 전달받으려면 이벤트 핸들러를 정의할 때 이벤트 객체를 전달받을 매개변수를 명시적으로 선언해야 한다.
- 이벤트 핸들러 어트리뷰트 방식으로 이벤트 핸들러를 등록했다면 event 이름으로 인수를 전달해야 event 객체가 전달된다.
- 그 이유는 이벤트 핸들러 어트리뷰트 값은 암묵적으로 생성되는 이벤트 핸들러의 함수 몸체를 의미하며, 함수를 생성할 때 첫 번째 매개변수의 이름이 event로 암묵적으로 명명되기 때문에 event가 아닌 다른 이름으로는 이벤트 객체를 전달받지 못한다.

###### 40.5.1 이벤트 객체의 상속 구조
- 이벤트 객체는 JavaScript에서 생성자 함수와 프로토타입 체인의 일부로 구성된다. 이러한 객체들은 DOM 이벤트 모델에서 사용한다.
1) 이벤트 객체 생성자 함수: 이벤트 객체들은 생성자 함수를 통해 생성. 
예를 들어, Event, UIEvent, MouseEvent 등은 모두 생성자 함수이고, 이 생성자 함수를 사용하여 특정 이벤트 객체를 생성할 수 있다.
2) 프로토타입 체인: 이벤트 객체는 생성자 함수와 관련된 프로토타입 객체로 구성된 프로토타입 체인의 일부.
 이를 통해 이벤트 객체는 해당 객체의 생성자 함수와 프로토타입 체인 내에 정의된 메서드와 속성을 상속받는다.
3) Event 인터페이스: Event 인터페이스는 DOM 내에서 발생한 모든 이벤트에 의해 생성되는 이벤트 객체를 나타낸다. 
이 인터페이스에는 모든 이벤트 객체에서 공통으로 사용되는 프로퍼티와 메서드가 정의되어 있다.
4) 하위 인터페이스: Event 인터페이스를 상속하여, 특정 이벤트 유형에 따라 고유한 프로퍼티와 메서드가 추가된 하위 인터페이스들이 있다. 
예를 들어, FocusEvent, MouseEvent, KeyboardEvent 등은 이러한 하위 인터페이스에 속한다. 각각의 하위 인터페이스는 특정 유형의 이벤트와 관련된 정보를 제공한다.
5) 이벤트 객체의 프로퍼티: 이벤트 객체의 프로퍼티는 발생한 이벤트의 유형에 따라 다양하다. 예를 들어, load 이벤트의 경우 Event 타입의 이벤트 객체를 생성하며, change 이벤트는 또 다른 Event 객체를 생성한다. 각각의 이벤트 객체는 해당 이벤트 유형에 필요한 정보를 포함하고 있다.
6) 이벤트 타입별 차이: 이벤트 객체의 프로퍼티는 발생한 이벤트의 타입에 따라 다르게 정의된다. 예를 들어, 마우스 클릭(click) 이벤트의 경우 MouseEvent 객체를 생성하며, 해당 객체에는 마우스 클릭과 관련된 정보가 포함된다.

* * *
load 이벤트 → Event 타입 이벤트 객체
change 이벤트 → Event
focus 이벤트 → FocusEvent
input 이벤트 → InputEvent
keyup 이벤트 → KeyboardEvent
click 이벤트 → MouseEvent

###### 40.5.2 이벤트 객체의 공통 프로퍼티
- UIEvent, CustomEvent, MouseEvent 등 모든 파생 이벤트 객체에 상속된다.
- 즉, Event 인터페이스의 이벤트 관련 프로퍼티는 모든 이벤트 객체가 상속받은 공통 프로퍼티다.
공통 프로퍼티 | 설명 | 타입
---|---|---
type | 이벤트 타입 | string
target | 이벤트를 발생시킨 DOM 요소 | DOM 요소 노드
currentTarget | 이벤트 핸들러가 바인딩된 DOM 요소 | DOM 요소 노드
eventPhase | 이벤트 전파 단계	0: 이벤트 없음, 1: 캡처링 단계, 2: 타깃 단계, 3: 버블링 단계	number
bubbles	이벤트를 버블링으로 전파하는지 여부. 다음 이벤트는 bubbles: false로 버블링하지 않는다.	

- 일반적으로 이벤트 객체의 target 프로퍼티와 currentTarget 프로퍼티는 동일한 DOM 요소를 가리키지만 이멘트 위임에 의해 다른 DOM 요소를 가리킬 수도 있다.

###### 40.5.3 마우스 정보 취득
- click, dblclick, mousedown, mouseup, mousemove, mouseenter, mouseleave 이벤트가 발생하면 생성되는 MouseEvent 타입의 이벤트 객체는 다음과 같은 고유 프로퍼티를 갖는다.
- 마우스 포인터 좌표 정보를 나타내는 프로퍼티 : screenX/screenY, clientX/clientY, pageX/pageY, offsetX/offsetY
- 버튼 정보를 나타내는 프로퍼티 : altKey, ctrlKey, shiftKey, button

`DOM 요소를 드래그하여 이동시키는 예제`
* * *
- 드래그는 마우스 버튼을 누른 상태에서 마우스를 이동하는 것으로 시작하고 마우스 버튼을 떼면 종료한다.
- mousedown 이벤트 && mousemove 이벤트 (시작) ⇒ mouseup 이벤트 (종료)
- mousedown 이벤트의 마우스 포인터 좌표와 드래그 하고있는 시점의 마우스 포인터 좌표를 비교하여 드래그 대상의 이동 거리 계산.
- mouseup 이벤트가 발생하면 드래그가 종료한 것이므로 이벤트 핸들러를 제거
- 마우스 포인터 좌표를 MouseEvent 타입의 이벤트 객체에서 제공한다.
- MouseEvent 타입 이벤트 객체는 screenX/screenY, clientX/clientY, pageX/pageY, offsetX/offsetY 프로퍼티를 제공한다.
- clientX/clientY는 뷰포트(viewport), 즉 웹페이지의 가시 영역을 기준으로 마우스 포인터 좌표를 나타낸다.

``` html
<!DOCTYPE html>
<html>
  <head>
    <style>
      .box {
        width: 100px;
        height: 100px;
        background-color: #fff700;
        border: 5px solid orange;
        cursor: pointer;
      }
    </style>
  </head>
  <body>
    <div class="box"></div>
    <script>
      // 드래그 대상 요소
      const $box = document.querySelector('.box');
	  //HTML에서 .box 클래스를 가진 요소를 선택하여 $box 변수에 할당합니다. 이 요소가 드래그 대상이다.

      // 드래그 시작 시점의 마우스 포인터 위치
      const initialMousePos = { x: 0, y: 0 };
	  //변수는 드래그를 시작한 시점의 마우스 포인터 좌표를 저장합니다. 초기값은 { x: 0, y: 0 }로 설정
	  
      // 오프셋: 이동할 거리
      const offset = { x: 0, y: 0 };
	  //변수는 드래그 동안 이동한 거리를 저장합니다. 초기값은 { x: 0, y: 0 }로 설정된다.

      // mousemove 이벤트 핸들러
	  ///move 함수는 mousemove 이벤트 핸들러로, 마우스 포인터가 이동할 때 호출된다. 
	  // 이 함수는 현재 마우스 포인터 위치와 드래그 시작 시점의 위치를 비교하여 offset 변수에 이동 거리를 계산하고, translate3d 스타일을 사용하여 $box 요소를 이동시킨다.
      const move = e => {
        // 오프셋 = 현재(드래그하고 있는 시점) 마우스 포인터 좌표 - 드래그 시작 시점의 마우스 좌표
        offset.x = e.clientX - initialMousePos.y;
        offset.y = e.clientY - initialMousePos.y;

        // translate3D는 GPU를 사용하므로 absolute의 top, left를 사용하는 것보다 빠르다.
        // top, left는 레이아웃에 영향을 준다.
        $box.style.transform = `translate3d(${offset.x}px, ${offset.y}px, 0)`;
      };

      // mousedown 이벤트가 발생하면 드래그 시작 시점의 마우스 포인터 좌표를 저장한다.
	  // mousedown 이벤트 핸들러는 마우스 버튼을 누를 때 호출되며, mousemove 이벤트 핸들러를 등록하여 드래그를 시작합니다. 
	  // 또한, 드래그 시작 시점의 마우스 포인터 좌표를 initialMousePos에 저장합니다.
      $box.addEventListener('mousedown', e => {
        // 이동 거리를 계산하기 위해 mousedown 이벤트가 발생(드래그를 시작)하면 드래그 시작 시점의
        // 마우스 포인터 좌표(e.clientX/e.clientY: 뷰포트 상에서 현재 마우스의 포인터 좌표)를 저장해 둔다.
        // 한 번 이상 드래그로 이동한 경우 move에서 translate3d${ooset.x}px, ${offset.y}px, 0)으로
        // 이동한 상태이므로 offset.x와 offset.y를 빼주어야한다.
        initialMousePos.x = e.clientX - offset.x;
        initialMousePos.y = e.clientX - offset.y;

        // mousedown 이벤트가 발생한 상태에서 mousemove 이벤트가 발생하면 box 요소를 이동시킨다.
        document.addEventListener('mousemove', move);
      });

      // mouseup 이벤트가 발생하면 mousemove 이벤트를 제거해 이동을 멈춘다.
	  // mouseup 이벤트 핸들러는 마우스 버튼을 뗄 때 호출되며, mousemove 이벤트 핸들러를 제거하여 드래그를 종료한다
      document.addEventListener('mouseup', () => {
        document.removeEventListener('mousemove', move);
      });
	  
	  console.log("offsetX/offsetY = ", offset.x + offset.y);
    </script>
  </body>
</html>
```

###### 40.5.4 키보드 정보 취득
- 웹 브라우저에서 발생하는 키보드 관련 이벤트
- 해당 이벤트 객체는 키보드 관련 이벤트 중 하나인 keydown, keyup, keypress 이벤트가 발생할 때 생성
- keydown, keyup, keypress 이벤트가 발생하면 생성되는 `, shKeyboardEvent` 타입의 이벤트 객체는 altKey, ctrlKeyiftKey, metaKey, key, keyCode 같은 고유의 프로퍼티를 갖는다.
* * *
- altKey: Alt 키가 눌렸는지 여부를 나타내는 부울 값. 눌렀으면 true, 아니면 false.
- ctrlKey: Ctrl 키가 눌렸는지 여부를 나타내는 부울 값. 눌렀으면 true, 아니면 false.
- shiftKey: Shift 키가 눌렸는지 여부를 나타내는 부울 값. 눌렀으면 true, 아니면 fal`se.
- metaKey: 메타 키 (예: Command 키 또는 Windows 키)가 눌렸는지 여부를 나타내는 부울 값. 눌렀으면 true, 아니면 false.
- key: 눌린 키의 이름을 나타내는 문자열. 예를 들어, 'A', 'Enter', 'ArrowUp' 등이 될 수 있다.
- keyCode: 눌린 키의 유니코드 값 또는 키 코드 값. 이 값은 키보드의 물리적 키에 대한 고유한 식별자로 사용된다. 주의: keyCode는 더 이상 권장되지 않으며, 대신 key 프로퍼티를 사용하는 것이 좋다.