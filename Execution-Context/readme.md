# Execute Context

## Introduction

이 문서는 JavaScript 의 Execute Context (실행 문맥) 에 대한 내용을 다룬 포스트입니다.

## 실행 컨텍스트란?

* 실행 컨텍스트는 Javascript 코드가 평가되고 실행되는 환경이라고 할 수 있습니다.
* 실행 컨텍스트는 함수나 메소드가 호출되었을 때 생성됩니다.
* 사용자가 작성한 코드를 실행 할 수 있는, JavaScript 엔진에 의해서 만들어지는 익명의 공간입니다.
* 실행 컨텍스트는 사용자가 작성하지 않은 코드들 (this, 변수들 및 객체와 함수 정의 등) 도 포함합니다.
* JavaScript 의 코드들은 실행될 때 각 Scope 에 해당되는 실행 컨텍스트 내에서 동작합니다.

정리하면 **실행 컨텍스트**란 함수나 메소드가 호출 될 때 JavaScript 엔진에 의해 만들어지는 익명의 공간으로서
JavaScript 엔진이 사용자 코드를 실행하기 전 사용자에게 제공할 환경 (this, 모든 변수 및 변수의 Scope, 함수 정의) 을 구성하고
사용자의 코드를 한줄 한줄씩 실행 할 수 있도록 하는 등 JavaScript 가 도움을 주는 모듈입니다.

## 실행 컨텍스트가 포함하고 있는것

* Global 객체 (전역 공간일 경우 - window / 그렇지 않을 경우 - Arguments)

* this (전역 공간일 경우 - window / 그렇지 않을 경우에는 문맥에 따라서 변함.)

* VariableEnvironment / LexicalEnvironment 이 각각 포함하는 것  
 (VariableEnvironment 는 Execution Context 가 만들어 질 때의 스냅샷 /  
  LexicalEnvironment 는 VariableEnvironment 의 클로닝으로, 이후 변경사항에 대한 내용을 갖고 있다.)
 
  * Environment Record (environmentRecord) - 변수나 참조 값을 기록.
  * Outer Environment (outerEnvironmentReference) - 외부의 Lexical Environment 를 참조.

## JavaScript 엔진이 코드를 실행하는 단계

JavaScript 엔진은 실행컨텍스트를 생성 단계 할 때 두 단계로 수행합니다.

* 생성 단계
* 실행 단계

### 생성 단계

* Global 객체를 생성합니다.

* 해당 실행 컨텍스트 내부에 제공할 this 를 바인딩 합니다.

* 함수가 호출 됐을 때 그 함수 내부의 모든 변수 및 함수에 대한 메모리 공간을 설정합니다.  
  여기서 **Hoisting (호이스팅)** 이란 개념이 적용되는데, 호이스팅에 대한 내용은 [호이스팅] 포스트에서 참고 부탁 드립니다.

### 실행 단계

* JavaScript 엔진에 의해 사용자가 작성 한 코드가 한줄한줄 실행됩니다.

* 이때 실행 컨텍스트 내부에 정의 된 변수들에 접근 할 수 있습니다.

* 코드 내에서 또 다른 함수가 호출되지 않는다면 실행 컨텍스트는 역할은 거기서 끝이지만  
  또 다른 함수가 호출 된다면 그 함수에 대해 


## 실행 컨텍스트의 타입

JavaScript 에는 세가지 타입의 실행 컨텍스트가 존재합니다.

* Global Execution Context
* Functional Execution Context
* Eval Function Execution Context

### Global Execution Context

* Global Execution Context 는 JavaScript 엔진이 JS 파일을 실행하게 될 때 필수적으로 생성되는 기본 컨텍스트 입니다.

* JavaScript 엔진은 스크립트를 처음 발견하면 전역 실행 컨텍스트를 생성하여 call-stack 으로 푸시합니다.

* JS 파일 안에서 특정 함수나 메소드 안에서 정의되지 않는 코드들은 Global Execution Context 에 존재하게 됩니다.

* 전역 실행 컨텍스트의 경우 global 객체가 브라우져인 경우 window / node.js 의 경우 global 이 되는데 (전역의 this 객체는 window 객체와 동일합니다.) 이과 같은 객체는 JavaScript 엔진에 의해 만들어진 것이 아니므로 호스트 객체 (host object) 라고 불립니다.

* 프로그램에는 하나의 전역 실행 컨텍스트 만있을 수 있습니다.  
  ※ 실행 컨텍스트가 생성되는 과정은 "실행 컨텍스트가 생성되는 과정" 에서 살펴보도록 하겠습니다.

### Functional Execution Context

* 함수가 호출 될 때 그때마다 호출 된 함수에 대한 새로운 실행 컨텍스트가 생성됩니다.

* 각 함수에는 자체 실행 컨텍스트가 있지만 함수를 호출하거나 호출 할 때 생성됩니다.

* 실행 컨텍스트는 갯수 제한이 존재하지 않습니다.

* 새로운 실행 컨텍스트가 생성될 때마다 정의된 순서로 단계를 거칩니다.

* 함수가 호출 될 때의 global 변수는 arguments 가 됩니다.

### Eval Function Execution Context

* eval 함수 내에서 실행 된 코드도 자체 실행 컨텍스트를 가져 오지만 일반적으로 JavaScript 개발자는 eval을 사용하지 않으므로 여기서는 설명하지 않겠습니다.

## 예제로 보는 Execution Context

```
//test.js

const x = 10;
const y = 10;

var add = function(num1, num2) {
  return num1 + num2;
}

var result = add(x, y);
```

JavaScript 엔진은 스크립트를 처음 발견하면 전역 실행 컨텍스트 (Global execution context) 를 생성하여 현재 실행 스택으로 푸시합니다.

![](https://user-images.githubusercontent.com/58318174/75947521-005ef900-5ee4-11ea-878c-e0154ff0e8fc.png)

test.js 파일을 발견 했을 때 생성되는 전역 실행 컨텍스트의 안은 아래 이미지와 같습니다.

![](https://user-images.githubusercontent.com/58318174/75947525-01902600-5ee4-11ea-8853-a4bc0c9d5b8d.png)

※ y 값이 before initialize 인 이유는 hoisting 과 관계가 있는 내용입니다. [Hoisting]() 을 참조 부탁 드립니다.

이후 코드를 한줄 한줄 수행해 나가며 add function 이 호출 되었을 때에는 또 다른 샐행 컨텍스트를 만들게 됩니다.

![](https://user-images.githubusercontent.com/58318174/75947523-00f78f80-5ee4-11ea-9b37-a7ee88ca0c33.png)

![](https://user-images.githubusercontent.com/58318174/75947526-01902600-5ee4-11ea-9018-4396ea980fa1.png)

이후 연산을 통해 20 이란 결과를 반환하고 add 함수 내부에서는 더 이상 호출 할 함수가 없으므로 life cycle 이 종료됩니다.

![](https://user-images.githubusercontent.com/58318174/75947527-0228bc80-5ee4-11ea-9776-e882e3254173.png)

![](https://user-images.githubusercontent.com/58318174/75947521-005ef900-5ee4-11ea-878c-e0154ff0e8fc.png)

그 후 test.js 코드에서 전역 실행 컨텍스트의 마지막 모습은 아래와 같습니다.

![](https://user-images.githubusercontent.com/58318174/75947528-0228bc80-5ee4-11ea-8e0b-a666e76fd399.png)

여러 개의 중첩 함수 호출 또는 조건이있는 시나리오에서 이러한 모든 실행 컨텍스트를 어떠한 방법으로 추적하고  
어떠한 것이 완전히 실행되었는지 알 수 있는 방법에 대해서는 Call Stack 에서 소개하고자 합니다.  
-> [Call Stack](https://github.com/dev-angelo/DevTips-FrontEnd/tree/master/Call-Stack)

<hr>

> 참조:
* [Understanding Execution Context and Execution Stack in Javascript](https://blog.bitsrc.io/understanding-execution-context-and-execution-stack-in-javascript-1c9ea8642dd0)
* [The JavaScript Execution Context, Call-stack & Event Loop](https://dev.to/thebabscraig/the-javascript-execution-context-call-stack-event-loop-1if1)
* [What is the execution context in javascript exactly](https://stackoverflow.com/questions/9384758/what-is-the-execution-context-in-javascript-exactly)
