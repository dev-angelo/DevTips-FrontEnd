# Event Table, Event Queue

## Introduction

[Call Stack](https://github.com/dev-angelo/DevTips-FrontEnd/blob/master/Call-Stack/readme.md) 에서 설명 하였던 JavaScript 의 특징인 single thread 환경에서, 어떻게 비동기 프로그래밍을 할 수 있는가에 대해 정리하는 포스트입니다.

## Single Thread and Synchronous in JavaScript

앞서 [Execute Context](https://github.com/dev-angelo/DevTips-FrontEnd/tree/master/Execute-Context) 및 [Call Stack](https://github.com/dev-angelo/DevTips-FrontEnd/tree/master/Call-Stack) 에서 설명했던것 처럼 JavaScript 는 하나의 Call Stack 을 갖고 있습니다.

JavaScript 는 단일 스레드 프로그래밍 언어이기 때문에 한번에 하나의 작업만을 수행 할 수 있습니다.
JavaScript 엔진은 코드를 위에서 아래로 순차적으로 실행하는 동기식입니다.

그 뜻은 콜 스택에 실행되어질 context 가 존재하고 있다면 블록된 상태를 유지하고 있다는것 입니다.
단일 스레드 언어이기 때문에 동시성 문제에 대한 걱정을 하지 않아도 되고 코드 작성도 단순화 됩니다.

하지만 메인 스레드를 차단하지 않으면서 네트워크 액세스와 같은 긴 작업을 수행 할 수 없게 됩니다.
웹의 경우에서는 블록된 상태에서는 브라우저에 UI 를 렌더링 할 수 없을뿐만 아니라 사용자의마우스 클릭과 같은 이벤트를 처리 할 수 없는 상태가 되어 좋지 않은 사용자 경험을 제공하게 됩니다.

특정 로직의 실행이 끝날 때까지 기다려주지 않고 나머지 코드를 먼저 실행하는 것이 비동기 처리입니다.

## JavaScript 에서 비동기 동작을 지원?

* **`비동기 동작은 JavaScript 언어 자체의 일부가 아닙니다.`** 브라우저 (또는 프로그래밍 환경)의 핵심 JavaScript 언어 위에 구축되고 브라우저 API를 통해 액세스됩니다.
* setTimeout() 과 같은 비동기 동작 함수들은 JavaScript 엔진의 일부가 아니며 웹 API (브라우저) 및 C / C ++ API (node.js)의 일부입니다.

비동기 호출을 위해서 보통 callback function 을 비동기 API 의 인자로 넘겨주게 되는데, 이 때 등록 한 callback function 을 최종적으로 JavaScript 엔진의 콜 스택 쌓이게 하는 매커니즘을 브라우저 및 node.js 에서 제공 해 줌으로서 비동기 프로그래밍이 가능해지는것 입니다.

## Browser/Node.js 에서의 JavaScript 비동기 프로그래밍을 위한  매커니즘.

Browser/Node.js 에서는 JavaScript 에서 비동기 프로그래밍을 가능하게 하기 위한 **Event Table**, **Event Queue**, **[Event Loop](https://github.com/dev-angelo/DevTips-FrontEnd/tree/master/Event-Loop)** 가 있습니다.
이어서 **Event Table** 및 **Event Queue** 에 대해서 설명 해 보도록 하겠습니다.

## Event Table

### What is the Event Table?

* 이벤트 테이블은 일부 지연된 이벤트 목록을 저장하는 데이터 구조입니다.
* 이벤트 테이블은 함수를 실행하지 않으며 자체 호출 스택에 추가하지 않습니다.
* 이벤트 테이블의 유일한 목적은 이벤트를 추적하여 이벤트 큐로 보내는 것입니다.

### 예제로 보는 Event Table 의 역할

setTimeout 함수를 호출하거나 비동기 작업을 수행 할 때마다 이벤트 테이블에 추가됩니다.
이벤트 테이블은 특정 이벤트 후에 특정 기능이 트리거되어야한다는 것을 알고있는 데이터 구조입니다.

```
//Example1
setTimeout(function() {
    console.log('This will be displayed after 1 second');
}, 1000);
```

* 1\. 예제 1이 실행되면 익명의 콜백 함수 및 1000ms 의 딜레이라는 정보가 이벤트 테이블에 등록됩니다.
* 2\. 1초가 지난 후 이벤트 테이블은 실행 될 익명의 콜백 함수를 이벤트 큐에 전달합니다.

## Event Queue

### What is the Event Queue?
* 이벤트 큐는 FIFO (First In First Out) 정책을 사용하여 이벤트 목록을 저장하는 데이터 구조입니다.

이벤트 큐로 보내진 함수는 다른 포스트에서 설명 할 [Event Loop](https://github.com/dev-angelo/DevTips-FrontEnd/tree/master/Event-Loop) 에 의해 Call Stack 으로 전달됩니다.

> 참조:
* Javascript and Asynchronous Magic — Explaining the JS Engine and Event Loop - (https://levelup.gitconnected.com/javascript-and-asynchronous-magic-bee537edc2da)
* What is the JavaScript event loop? - (http://altitudelabs.com/blog/what-is-the-javascript-event-loop/)
* Event Loops, Event Tables & Event Queues in JavaScript - (https://www.knowledgescoops.com/2019/07/event-loops-event-tables-event-queues.html)
* Understanding JS: The Event Loop - (https://hackernoon.com/understanding-js-the-event-loop-959beae3ac40)
