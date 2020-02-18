# Event Loop
## Introduce 
JavaScript 에 대한 가장 중요한 부분 중 하나인 이벤트 루프에 대한 내용 정리.
## Single Thread and Synchronous in JavaScript
앞서 [Execute Context](https://github.com/dev-angelo/DevTips-FrontEnd/tree/master/Execute-Context) 및 [Call Stack](https://github.com/dev-angelo/DevTips-FrontEnd/tree/master/Call-Stack) 에서 설명했던것 처럼 JavaScript 는 하나의 Call Stack 을 갖고 있습니다.<br>
<br>
JavaScript 는 단일 스레드 프로그래밍 언어이기 때문에 한번에 하나의 작업만을 수행 할 수 있습니다.<br>
JavaScript 엔진은 코드를 위에서 아래로 순차적으로 실행하는 동기식입니다.<br>
<br>
그 뜻은 콜 스택에 실행되어질 context 가 존재하고 있다면 블록된 상태를 유지하고 있다는것 입니다.<br>
단일 스레드 언어이기 때문에 동시성 문제에 대한 걱정을 하지 않아도 되고 코드 작성도 단순화 됩니다.<br>
<br>
하지만 메인 스레드를 차단하지 않으면서 네트워크 액세스와 같은 긴 작업을 수행 할 수 없게 됩니다.<br>
웹의 경우에서는 블록된 상태에서는 브라우저에 UI 를 렌더링 할 수 없을뿐만 아니라 사용자의마우스 클릭과 같은 이벤트를 처리 할 수 없는 상태가 되어 좋지 않은 사용자 경험을 제공하게 됩니다.<br>
<br>

## 그래서 어떻게? 비동기! (Asynchronous)
특정 로직의 실행이 끝날 때까지 기다려주지 않고 나머지 코드를 먼저 실행하는 것이 비동기 처리입니다.<br>

## JavaScript 에서 비동기 동작을 지원?
* 비동기 동작은 JavaScript 언어 자체의 일부가 아니라 브라우저 (또는 프로그래밍 환경)의 핵심 JavaScript 언어 위에 구축되고 브라우저 API를 통해 액세스됩니다.<br>
* setTimeout() 과 같은 함수는 JavaScript 엔진의 일부가 아니며 웹 API (브라우저) 및 C / C ++ API (node.js)의 일부입니다.<br>

## 이벤트 루프의 역할.
* 이벤트 루프는 콜 스택이 비어 있는지 확인하는 지속적으로 실행되는 프로세스입니다.<br>
* 주기적으로 콜 스택을 보고 비어있으면 이벤트 큐를 찾습니다.<br>
* 콜백 큐에 대기중인 것이 있으면 콜 스택으로 이동시킵니다.<br>
* 콜 스택이 비어있지 않거나 콜백 큐에 대기중인 컨텍스트가 존재하지 않으면 아무동작도 수행하지 않습니다.

> 참조:
* JavaScript Call Stack - (https://www.javascripttutorial.net/javascript-call-stack/)
* Understanding Asynchronous JavaScript - (https://blog.bitsrc.io/understanding-asynchronous-javascript-the-event-loop-74cd408419ff)
