# Event Loop
## Introduce 
JavaScript 에 대한 가장 중요한 부분 중 하나인 이벤트 루프에 대한 내용 정리.

## 이벤트 루프의 역할.
* 이벤트 루프는 콜 스택이 비어 있는지 확인하는 지속적으로 실행되는 프로세스입니다.<br>
* 주기적으로 콜 스택을 보고 비어있으면 콜백 큐를 찾습니다.<br>
* 콜백 큐에 대기중인 것이 있으면 콜 스택으로 이동시킵니다.<br>
* 콜 스택이 비어있지 않거나 콜백 큐에 대기중인 컨텍스트가 존재하지 않으면 아무동작도 수행하지 않습니다.

> 참조:
* JavaScript Call Stack - (https://www.javascripttutorial.net/javascript-call-stack/)
* Understanding Asynchronous JavaScript - (https://blog.bitsrc.io/understanding-asynchronous-javascript-the-event-loop-74cd408419ff)
