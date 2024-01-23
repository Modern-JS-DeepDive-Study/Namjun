- **DOM**은( Document Object Model)은 HTML 문서의 계층적 구조와 정보를 표현하며 이를 제어할 수 있는 API, 즉 프로퍼티와 메서드를 제공하는 트리 자료구조임. 
​
### **📌 노드**
​
- HTML요소는 (HTML element)는 HTML 문서를 구성하는 개별적인 요소를 의미함.
​
​![image](https://github.com/Modern-JS-DeepDive-Study/Namjun/assets/69416561/d12be51f-4cdb-4b28-bef3-d0f791eb8c83)

- 다음의 HTML 요소는 렌더링 엔진에 의해 파싱되어, DOM을 구성하는 요소 노드 객체로 변환됨. 
​
- 먼저 위의 예시의 `<p></p>` 태그는 요소 노드, `class='para'`는 어트리뷰트 노드, 'TCPschool.com'은 텍스트 노드로 변환됨.
​
- 이후 중첩 관계에 의한 계층적 부자 관계가 형성되며, 이러한 HTML 요소 간의 부자 관계를 반영해 모든 객체를 트리 자료구조로 구성함.
​
- 이런 노드 객체들로 구성된 트리 자료구조를 **DOM**이라고 부르늣 것임.
​
#### **참고 : 트리 자료구조**
​![image](https://github.com/Modern-JS-DeepDive-Study/Namjun/assets/69416561/7025d777-a0e3-42b1-b1e9-3625fe5413ae)

​
1. 트리 자료구조는 부모 노드와 자식 노드로 구성되어 **노드 간의 계층적 구조를 표현하는 비선형 자료구조**임. 
​
2. 트리는 부모가 없는 단일 최상위 노드(Root Node) 로 부터 시작하고, 루트노드는 0개 이상의 자식 노드를 가짐.
​
3. 자식 노드가 없는 노드를 리프 노드(Leaf Node)라고 함.
​
### **📌 노드 객체의 타입**
​
- 문서 노드 : DOM 트리 최상위에 존재하는 루트 노드로, document 객체를 가리킴.
​
- 요소 노드 : HTML 요소를 가리키는 객체(h1, p, div, section, main tag등) 

- 어트리뷰트 노드 : HTML 요소의 어트리뷰트를 가리키는 객체로, **지정된 요소의 요소노드와 연결됨.**
​
- 텍스트 노드 : HTML 요소의 텍스트를 가리키는 객체로, **지정된 요소의 요소노드와 연결되며, 자식노드가 없는 리프 노드임.**
​
### **📌 노드 객체의 상속 구조**
​
![image](https://github.com/Modern-JS-DeepDive-Study/Namjun/assets/69416561/2d381a6e-c6eb-4bf6-aa51-325bddd0197e)

​
- DOM을 구성하는 노드 객체는 자신의 구조와 정보를 제어할 수 있는 DOM API를 사용할 수 있음. 이를 통해 자신의 부모, 형제, 자식을 탐색할 수 있고, 자신의 어트리뷰트와 텍스트를 조작할 수 있는 것임.
​
- 이를 위해 DOM API의 인터페이스와 객체의 상속 구조를 알아둘 필요가 있음.
​
- 먼저 모든 노드 객체들은 **Object, EventTarget, Node 인터페이스**를 상속받음.
​
- EventTarget 인터페이스의 경우 이벤트에 관련된 기능(ex EventTarget.addEventListener)을 제공하고, Node 인터페이스는 노드 정보를 제공하는 역할을 함.(ex. Node.previousSibling, Node.nextSibling)
​
- HTML 요소의 종류에 따라 공통적으로 갖는 기능은 HTMLElement 인터페이스가 제공함.(ex. style, id 등)
​
- input에는 value 프로퍼티가 필요하지만 div에는 아닌 것처럼, HTML 요소의 종류에 따라 고유한 기능들은 각 별도의 인터페이스(HTMLInputElement, HTMLDivElement 등)가 존재함.
​
- 웹 개발자로서 이런 상속 구조를 자세히 아는 것보다는, DOM API가 제공하는 메서드를 사용해 **노드에 접근하고 HTML의 구조나 내용 또는 스타일 등을 동적으로 변경하는 방법을 익히는 것이 중요함.** 
​
### **📌 요소 노드의 취득과 탐색, 텍스트 조작**
​
- document.getElementById(selector)
​
- document.getElementByClassName(class)
​
- document.getElementByTagName(TagName)
​
- document.querySelector(selector)
​
- document.querySelectorAll(selectors) - NodeList 반환
​
- Element.matches(selector)
​
- Element.previous/nextElementSibling
​
- Node.parentNode/childNodes

- Node.first/lastChild
​
- Element.first/lastElementChild
​
### **📌 HTMLCollection과 NodeList**
​
- DOM 컬렉션 객체인 HTMLCollection 과 NodeList는 DOM API가 여러 개의 결과값을 반환하기 위한 DOM 컬렉션 객체임.
​
- 두 객체 모두 유사 배열 객체이면서 이터러블이므로, 스프레드 문법이나 배열 변환이 간편함.
​
- getElementsByTageName, getElementByClassName 메서드가 반환하는 HTMLCollection 객체는 노드 객체의 **상태 변화를 실시간으로 반영하는 살아있는 DOM 객체임.**
​
- HTMLCollection 객체는 상태변경을 실시간으로 반영하다보니, 개발자가 동작을 예상하기 힘든 단점이 있음.
​
- 이런 HTMLCollection 객체의 단점을 해결하기 위해 getElementByTagName, getElementsByClassName 메서드 대신 querySelectorAll 메서드를 사용하는 방법도 있다. 해당 메서드는 DOM 컬렉션 객체인 NodeList 객체를 반환함. 
​
- 해당 객체는 **상태 변경을 실시간으로 반영하지 않는 객체**로, forEach 고차함수를 사용할 수 있음. (단 childNodes가 반환하는 객체는 NodeList 객체이지만 실시간으로 객체의 상태 변경을 반영함.)
​
- 노드 객체의 상태 변경과 관련 없이 안전하게 DOM 컬렉션을 사용하려면, 배열로 변환하여 사용하는 것이 좋음. 
​
### **📌 TextContent와 innerText**
​
- Node.textContent는 한 요소노드 안의 텍스트와 자손 노드의 텍스트를 모두 취득하는 접근자 프로퍼티임. 해당 프로퍼티를 참조시 HTML 마크업을 제외한 순수 텍스트만 반환됨.
​
- 유사한 동작을 하는 프로퍼티로 innerText가 존재하는데, 해당 프로퍼티는 CSS에 의해 비표시된 텍스트를 반환하지 않고, CSS를 고려해야해서 동작속도가 느림.
​
### **📌 DOM 조작**
​
- DOM 조작은 새로운 노드를 생성해 DOM 에 추가하거나 기존 노드를 삭제 또는 교체하는 것을 말함.
​
- DOM에 새로운 노드가 추가되거나 삭제되면 **리플로우와 리페인트가 발생하므로, 최적화를 위해 주의해서 다루어야함.**
​
- innerHTML
​
- insertAdjacentHTML
​
- createElement(node)
​
- appendChild(node)
​
- setAttribute(attr, value)
​
- dataset.속성명
​
- style.css속성
​
- className
​
- classList.add()/remove() 
​
### **📌 innerHTML vs insertAdjacentHTML / XSS**
​
- innerHTML프로퍼티는 요소 삽입시 기존 자식 노드를 모두 제거하고 처음부터 새롭게 자식 노드를 생성함.
​
- 반면에 insertAdjacentHTML 메서드는 기존 요소에는 영향을 주지않고 새롭게 삽입될 요소들만을 파싱하므로, innerHTML 프로퍼티보다 효율적이고 속도가 빠름.
​
- 한편 두 방식 모두 크로스 사이트 스크립팅 공격(XSS)에 취약하다는 단점이 있음.
​
- **XSS란 공격자가 실행 가능한 악성코드를 웹 페이지에 삽입하는 공격을 말함.**
​
- 공격에 성공하면 사이트에 접속한 사용자는 삽입된 코드를 실행하게 되며, 의도치 않은 행동을 수행하거나 쿠키나 세션 토큰 등의 민감한 정보를 탈취하게 됨.
​
- 따라서 이런 문제점을 방지하기 위해, 쿠키의 보안 옵션(httponly)를 설정하거나 방어용 라이브러리를 이용하는 방법이있음.
​
---
​
#### **예상질문**
​
1. HTMLCollection과 NodeList의 차이점에 대해 설명해주세요.
​
2. XSS란 무엇인가요? XSS의 공격 방식, 해결법 등을 간략히 설명해주세요.
​
3. 트리 자료구조에 대해 설명해주세요.
​
4. DOM이란 무엇인가요?
​
#### **레퍼런스**
​
- 모던 자바스크립트 딥다이브(이웅모 저)
