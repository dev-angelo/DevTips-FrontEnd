# Call Stack
## Introduction

## 콜 스택이란?
* 콜 스택은 JS 코드에서의 함수 실행을 추적하고 관리하는 데 사용되는 데이터 구조입니다.
* 코드 실행 중에 생성된 모든 실행 컨텍스트를 저장하고하고, 실제로 어떤 실행 컨텍스트와 여전히 스택에 남아있는 실행 컨텍스트를 기록하는 것 입니다.
* 함수를 호출하면 엔진은 해당 함수를 스택 맨 위로 푸시 한 다음 실행 컨텍스트를 만듭니다.
* 실행 컨텍스트를 살펴보면이 컨텍스트가 전역 컨텍스트이거나 함수 실행 컨텍스트 일 것입니다.
* 각 함수가 실행될 때 콜 스택은이를 비우고 비어 있고 모든 함수가 실행될 때까지 다음 함수로 넘어갑니다.
* 해당 시퀀스를 LIFO-Last In First Out (후입선출) 이라고합니다.

## 콜 스택의 동작 흐름
* JavaScript 엔진이 스크립트를 처음 발견하면 전역 실행 컨텍스트를 생성하여 현재 실행 스택으로 푸시합니다. 
* 엔진이 함수 호출을 발견 할 때마다 해당 함수에 대한 새로운 실행 컨텍스트를 생성하고 이를 스택의 맨 위로 푸시합니다.
* 엔진은 스택의 맨 위에 있는 함수에 해당하는 실행 컨텍스트를 실행합니다.
* 이 함수가 완료되면 해당 실행 컨텍스트가 스택에서 pop 되어 현재 스택에서 컨트롤이 그 아래 컨텍스트에 도달합니다.

## 콜 스택 동작 흐름 예제
```

function thirdFunction() {
    console.log("thirdFunction()");
}

function secondFunction() {
    thirdFunction();
    console.log("secondFunction()");
}

function firstFunction() {
    secondFunction();
    console.log("firstFunction()");
}

firstFunction();
```
![Stack-Flow](https://github.com/dev-angelo/DevTips-FrontEnd/blob/master/Call-Stack/images/stack_flow.png)
1\. 엔진이 firstFunction() 을 만나면 firstFunction() 에 대한 실행 컨텍스트<br>
(컨텍스트에 변수, 매개 변수 및 함수 선언을 저장하기 위해 로컬 실행 컨텍스트 및 로컬 메모리 할당을 작성합니다. -> 범위의 개념은 이것과 관련이 있습니다) 를 만들고 엔진은 컨텍스트를 실행시킵니다.

2\. firstFunction() 의 첫번째 줄에서 secondFunction() 호출 구문을 만나서 secondFunction() 에 대한 실행 컨텍스트를 Call Stack 에 push 후 엔진은 실행 컨텍스트를 실행시킵니다.

3\. secondFunction() 의 첫번째 줄에서 thirdFunction() 호출 구문을 만나서 thirdFunction() 에 대한 실행 컨텍스트를 Call Stack 에 push 후 엔진은 실행 컨텍스트를 실행시킵니다.

4\. thirdFunction() 에서는 "thirdFunction()" 로그를 찍고 Call Stack 에서 pop 됩니다.

5\. 그 후 엔진은 Call Stack 의 최상위로 올라온 secondFunction() 에 대한 실행 컨텍스트를 다시 실행합니다. -> "secondFunction()" 로그를 찍고 Call Stack 에서 pop 됩니다.

6\. 그 후 엔진은 Call Stack 의 최상위로 올라온 firstFunction() 에 대한 실행 컨텍스트를 다시 실행합니다. -> "secondFunction()" 로그를 찍고 Call Stack 에서 pop 됩니다.

7\. 스택이 비면 프로그램 실행이 중지됩니다.

## 콜 스택의 특성
* 콜 스택의 특성은 JavaScript가 단일 스레드이며 한 번에 하나의 실행 컨텍스트 만 실행할 수 있다는 사실을 반영합니다.
* 함수를 실행하는 동안 엔진이 동시에 다른 컨텍스트를 실행할 수 없음을 의미합니다. 
* 함수를 호출 스택에 밀어넣을 때마다 능동 실행 컨텍스트가 되고 (반환 문구와 함께) 명시적으로 또는 암묵적으로 (모든 명령이 실행되었을 때) 돌아올 때까지 그 기능을 호출한 함수에서 제어 흐름을 빼앗아 간다는 것을 의미합니다.
