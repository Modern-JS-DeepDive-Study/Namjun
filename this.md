## 📌 실행 컨텍스트

- `실행 컨텍스트`는 자바스크립트의 동작 원리를 담고 있는 **핵심 개념임.**
- 실행 컨텍스트를 바르게 이해하면 자바스크립트가 스코프를 기반으로 식별자와 식별자에 바인딩된 값을 관리하는 방식을 이해할 수 있음.
- 또한 **호이스팅이 발생하는 이유와 클로저의 동작 방식, 태스크 큐와 함께 동작하는 이벤트 루프의 동작 방식을 이해하는 데도 도움이 됨.**

### 📌 소스 코드의 타입

- ECMAScript 사양에서, 실행 컨텍스트를 생성하는 4가지 소스코드는 다음과 같음.
- `전역 코드`는 전역에 존재하는 소스 코드를 말하며, 전역에 정의된 함수, 클래스 등의 내부 코드는 포함하지 않음.
- `함수 코드`는 함수 내부에 존재하는 소스 코드를 말하며, 함수 내부에 중첩된 함수, 클래스 등의 내부 코드는 포함되지 않음.
- `eval 코드`는 빌트인 전역 함수인 `eval` 함수에 인수로 전달되어 실행되는 소스 코드를 말함.
- `모듈 코드`는 모듈 내부에 존재하는 소스 코드를 말함.

### 📌 소스코드의 평가와 실행

- 자바스크립트의 모든 소스코드는 자바스크립트 엔진에 의해 `평가`와 `실행`의 두가지 과정을 거치게 됨.
- 소스코드의 평가 과정에서는 실행 컨텍스트를 생성하고 변수, 함수 등의 선언문만 먼저 실행하여 생성된 변수나 함수 식별자를 키로 실행 컨텍스트가 관리하는 스코프(`렉시컬 환경의 환경 레코드`)에 등록함.
- 소스코드 평가 과정이 끝나면 비로소 선언문을 제외한 소스코드가 순차적으로 실행되기 시작함.(= 런타임 시작) 이과정에서 변수에 값이 할당되고 함수가 호출되는 등의 실행이 이루어짐.
- 소스코드가 순차적으로 실행되면서, 변수나 함수의 참조 등 실행에 필요한 정보들을 평가 과정에서 등록한 실행 컨텍스트가 관리하는 스코프에서 참조하는 것임.

### 📌 실행 컨텍스트 스택

- 생성된 모든 실행 컨텍스트는 `스택` 자료구조로 관리됨.
- 실행 컨텍스트 스택은 코드의 **실행 순서를 관리**함. 실행 컨텍스트 스택은 전역 컨텍스트가 생성되면 호출 스택에 쌓이고, 함수가 호출되면 해당 함수의 실행 컨텍스트가 생성되어 호출 스택에 쌓임.

### 📌 렉시컬 환경

- `렉시컬 환경`은 `식별자`와 `식별자에 바인딩된 값`, `그리고 상위 스코프에 대한 참조`를 기록하는 자료구조임.
- 실행 컨텍스트 스택이 코드의 실행 순서를 관리한다면, 렉시컬 환경은 스코프와 식별자를 관리하는 것임.
- 렉시컬 환경은 `키와 값`을 갖는 객체 형태의 스코프를 생성하고 관리함.
- 렉시컬 환경은 `환경 레코드`와 `외부 렉시컬 환경에 대한 참조`로 구성됨.
- `환경 레코드`는 `식별자`와 `식별자에 바인딩된 값`을 관리하며, `외부 렉시컬 환경에 대한 참조`는 상위 스코프를 가리킴.


### 📌 실행 컨텍스트의 생성과 식별자 검색 과정

- 소스코드가 런타임에 실행될때, `전역 객체 생성-전역 코드 평가-전역 코드 실행-지역 코드 평가-지역 코드 실행`의 순서로 실행됨.
- 소스코드의 평가 과정의 세부 순서를 살펴보면, `실행 컨텍스트 생성 - 렉시컬 환경 생성 - 변수, 함수 등의 선언문만 평가 - this 바인딩-외부 렉시컬 환경 참조`의 순서로 진행됨.
- 소스코드가 실행되면서 식별자를 검색할 때는 평가 과정의 `렉시컬 환경`을 활용함.
- 실행 컨텍스트 스택의 최상위에 존재하는 실행 컨텍스트의 렉시컬 환경을 `실행 중인 코드의 렉시컬 환경`이라고 함.