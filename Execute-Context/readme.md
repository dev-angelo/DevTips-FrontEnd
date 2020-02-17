# Execute Context
## Introduction
이 문서는 JavaScript 의 Execute Context (실행 문맥) 에 대한 내용을 다룬 포스트입니다.
## 실행 컨텍스트란?
* 실행 컨텍스트는 Javascript 코드가 평가되고 실행되는 환경의 추상 개념입니다. 
* 코드가 JavaScript로 실행될 때마다 실행 컨텍스트 내에서 실행됩니다.
## 실행 컨텍스트의 타입
JavaScript 에는 세가지 타입의 실행 컨텍스트가 존재합니다.
* Global Execution Context
* Functional Execution Context
* Eval Function Execution Context

### Global Execution Context
* 기본 실행 컨텍스트 입니다.
* 함수 안에 존재하지 않는 코드들은 Global Execution Context 에 존재하게 됩니다.
* JavaScript 엔진은 스크립트를 처음 발견하면 전역 실행 컨텍스트를 생성하여 현재 실행 스택으로 푸시합니다. 
* 브라우저의 경우 window 객체를, node.js 의 경우 global 객체를 생성합니다. (전역의 this 객체는 window 객체와 동일합니다.)
* 프로그램에는 하나의 전역 실행 컨텍스트 만있을 수 있습니다.
※ 실행 컨텍스트가 생성되는 과정은 "실행 컨텍스트가 생성되는 과정" 에서 살펴보도록 하겠습니다.

### Functional Execution Context
* 함수가 호출 될 때 그때마다 호출 된 함수에 대한 새로운 실행 컨텍스트가 생성됩니다.
* 각 함수에는 자체 실행 컨텍스트가 있지만 함수를 호출하거나 호출 할 때 생성됩니다.
* 실행 컨텍스트는 갯수 제한이 존재하지 않습니다.
* 새로운 실행 컨텍스트가 생성될 때마다 정의된 순서로 단계를 거칩니다.

### Eval Function Execution Context
* eval 함수 내에서 실행 된 코드도 자체 실행 컨텍스트를 가져 오지만 일반적으로 JavaScript 개발자는 eval을 사용하지 않으므로 여기서는 설명하지 않겠습니다.


> 참조:
* Understanding Execution Context and Execution Stack in Javascript (https://blog.bitsrc.io/understanding-execution-context-and-execution-stack-in-javascript-1c9ea8642dd0)
* The JavaScript Execution Context, Call-stack & Event Loop (https://dev.to/thebabscraig/the-javascript-execution-context-call-stack-event-loop-1if1)

