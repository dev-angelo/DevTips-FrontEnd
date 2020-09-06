# 1. Introduction
* 해당 포스트에서는 웹 페이지가 어떻게 동작하는지 정리하였습니다.
* 타겟 웹사이트는 https://www.kakaocorp.com 로 선정하였습니다.
* 웹사이트 동작 분석을 위한 도구로는 Chrome 개발자 도구를 사용하였습니다.

# 2. js, css 파일들은 어디에 위치했는가? 왜 그곳에 위치되었을까?

## 2-1. js 파일의 의 위치
* 상단에 있는 js(라이브러리):
![image](https://user-images.githubusercontent.com/58318174/92317280-f86e4600-f039-11ea-971c-3910d264e2a0.png)

* 상단에 있는 js의 내용 (라이브러리):
![image](https://user-images.githubusercontent.com/58318174/92317282-fc9a6380-f039-11ea-9189-30ece618f273.png)

* 하단에 있는 js(site event처리[hover, click, scroll, 셀렉트 박스]):
![image](https://user-images.githubusercontent.com/58318174/92317284-ff955400-f039-11ea-96bf-43376468ab08.png)

* 하단에 있는 js의 내용:
![image](https://user-images.githubusercontent.com/58318174/92317285-01f7ae00-f03a-11ea-8578-e7280760ea4a.png)

#### 최상단에 js 가 위치 한 이유
* JQuery CDN 및 자체적으로 개발 한 라이브러리를 사용하기 위해서.
* 여기에서 읽어들이는 js 파일에서는 요청 및 응답을 위한 코드가 포함되어 있지 않음.

#### 최하단에 js 가 위치 한 이유
* 렌더링이 완료 된 후 사용자의 Interaction 을 처리하기 위하여.

* 자바스크립트는 싱글스레드로 동작합니다. 따라서 파서가 내부 태그이든 외부 태그이든 script 태그에 도달하면 (외부 태그 인 경우) fetch를 중단하고 실행합니다. 그 뜻은 한가지 일을 하고 있을때 모든 작업이 block 된다는 것, 따라서 문서 내의 요소를 참조하는 JavaScript 파일이 있는 경우 해당 문서가 표시된 후에 배치 해야 합니다.

* 많은 코드가 들어있고 코드중 일부의 속도가 느리다면 최초 화면 로딩이 느려 사용자에게 답답함을 유발하므로, 스크립트는 고정된 위치가 아니라 상황에 맞춰 적절히 분배해야 합니다.

## 2-2. css 의 위치
* css 가 위치한 곳 (상단):
![image](https://user-images.githubusercontent.com/58318174/92317289-058b3500-f03a-11ea-81b1-43d3d37f5e46.png)

* css 가 위치한 곳 (가운데) -> 반응형 사이트 css 적용 :
![image](https://user-images.githubusercontent.com/58318174/92317292-120f8d80-f03a-11ea-8377-05e698e9af37.png)
![image](https://user-images.githubusercontent.com/58318174/92317295-1471e780-f03a-11ea-87af-a39317b8c0a3.png)

#### 2-3. css가 최상단에 위치한 이유
HTML DOM 요소가 화면에 보일때 원하는 디자인이 적용된 형태로 나타나야 되기 때문입니다.

#### 2-4. css가 가운데에 embed 형태로 위치한 이유


# 3. 화면을 표시하기 위해 어떤 파일들이 다운로드 되는가?
![image](https://user-images.githubusercontent.com/58318174/92317299-176cd800-f03a-11ea-9552-67c913da6e88.png)

1. Image Files (*.png, *.gif etc..) </br>
2. JS Files (라이브러리 포함) </br>
3. Font Files (woff) </br>
4. 스타일 시트 </br>
5. text/html </br>
</br>
* 다운로드 된 파일 타입을 Network 탭에서 Content-Type 으로 확인 가능합니다.
![image](https://user-images.githubusercontent.com/58318174/92317301-19cf3200-f03a-11ea-91fc-b655d0d89b73.png)

# 4. 특정 자원의 Request Headers 와 Response Headers의 내용을 분석.(네트워크 탭 활용)
## 4-1. Request
![image](https://user-images.githubusercontent.com/58318174/92317303-1dfb4f80-f03a-11ea-9a4c-5b9779ce07a2.png)
request headers : 페치될 리소스나 클라이언트 자체에 대한 자세한 정보를 포함하는 헤더입니다.

## 4-2. Response
![image](https://user-images.githubusercontent.com/58318174/92317306-205da980-f03a-11ea-8782-362852d9cf79.png)

response headers : 위치 또는 서버 자체에 대한 정보(이름, 버전 등)와 같이 응답에 대한 부가적인 정보를 갖는 헤더입니다.

# 5. 화면에 보여지기 시작하는 시간은 언제인가?
* First Paint: 첫 번째 페인트는 사용자가 웹 페이지를 탐색 한 후 첫 번째 픽셀이 화면에서 렌더링되는 지점입니다.
![image](https://user-images.githubusercontent.com/58318174/92317307-23f13080-f03a-11ea-8e3a-08a3ad36cb41.png)

* First Contentful Paint: 텍스트, 이미지, 흰색이 아닌 캔버스 또는 SVG (Scalable Vector Graphics)를 포함하여 DOM (Document Object Model)의 컨텐츠를 페이지에 처음 렌더링 하는 지점입니다.
![image](https://user-images.githubusercontent.com/58318174/92317308-26ec2100-f03a-11ea-88c5-9442d463093a.png)

* First Paint, First Contenful paint, First Meaningful Paint 의 예시
![image](https://user-images.githubusercontent.com/58318174/92317311-29e71180-f03a-11ea-80e1-0ff701264824.png)

참조> User-centric Performance Metrics | Web Fundamentals (https://developers.google.com/web/fundamentals/performance/user-centric-performance-metrics)

## Flow
* DOM 트리 구축(Constructing the DOM Tree)</br>
* CSSOM 트리 구축(Constructing the CSSOM Tree)</br>
* JavaScript 실행(Running JavaScript)</br>
* 랜더링 트리 구축(Creating the Render Tree)</br>
* 레이아웃 생성(Generating the Layout)</br>
* 페인팅(Painting)</br>

![image](https://user-images.githubusercontent.com/58318174/92317312-2d7a9880-f03a-11ea-9090-3a11939e41b1.png)

# 6. DOMContentLoaded라는 이벤트는 언제 발생하는가? load랑은 어떤 차이점이 있는가?

## 6-1. DOMContentLoaded 이벤트
DOMContentLoaded 이벤트는 초기 HTML 도큐먼트가 로드되고 파스되면 스타일시트, 이미지 및 다른 프레임이 로딩되기전에 실행됩니다. 이벤트의 진짜 타겟은 로드가 완료된 이벤트 입니다. 이벤트는 Window 인터페이스에서 이벤트를 수신하여 캡쳐하고 버블링할 수 있습니다.

## 6-2. load 이벤트
load 이벤트는 스타일시트 이미지와 같이 의존성이 있는 리소스가 준비되면 실행됩니다. 이것은 DOMContentLoaded와 정반대입니다.

참조> 
Page: DOMContentLoaded, load, beforeunload, unload (https://javascript.info/onload-ondomcontentloaded)
DOMContentLoaded, load (https://yngmanie.space/posts/dom-event)


# 7. HTML 파일 응답 받은 이후부터, 모니터화면에 보이기까지의 과정.
* Send Request - index.html에 대한 GET 요청 전송
* Parse HTML and Send Request - HTML 및 DOM 구문 분석을 시작. style.css 및 main.js에 대한 GET 요청
* Parse Stylesheet - CSSOM이 style.css 용으로 생성
* Evaluate Script - main.js 평가
* Layout - HTML의 메타 뷰포트 태그를 기반으로 레이아웃 생성
* Paint - 문서의 픽셀을 페인트

참조> 
HTML Critical rendering path의 이해 ("https://blog.asamaru.net/2017/05/04/understanding-the-critical-rendering-path/")

# 8. Etc

## 8-1. HTML 이 파싱되기 전 GPU 가 사용되고 있는 이유?
![image](https://user-images.githubusercontent.com/58318174/92317313-30758900-f03a-11ea-828d-28d10d270ec9.png)


## 8-2. Rasterizer Thread 가 하는 일은?
브라우저는 문서의 구조와 각 요소의 스타일, 요소의 기하학적 속성, 페인트 순서를 알고 있습니다. 각 정보들을 화면의 픽셀로 변환하는 작업을 래스터화(rasterizing)라고 합니다.

가장 단순한 래스터화는 아마 뷰포트 안쪽을 래스터하는 것일 겁니다. 사용자가 웹 페이지를 스크롤하면 이미 래스터화한 프레임을 움직이고 나머지 빈 부분을 추가로 래스터화 합니다. 이 방식은 Chrome이 처음 출시되었을 때 래스터화한 방식입니다. 그러나 최신 브라우저는 합성(compositing)이라는 보다 정교한 과정을 거칩니다.

참조> 최신 브라우저의 내부 살펴보기 3 - 렌더러 프로세스의 내부 동작 (https://d2.naver.com/helloworld/5237120) 참조
