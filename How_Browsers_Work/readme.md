# 웹사이트 동작 분석
## 1. Introduction
* 해당 readme.md 문서에서는 웹 페이지가 어떻게 동작하는지 설명한다.
* 타겟 웹사이트는 https://www.kakaocorp.com 로 선정.
* 웹사이트 동작 분석을 위한 도구로는 Chrome 개발자 도구를 사용한다.

## 2. js, css 는 어디에 위치했는가? 왜 그곳에 위치되었을까?

### 2-1. js 의 위치
* 상단에 있는 js(라이브러리):
<img src="https://user-images.githubusercontent.com/58318174/73628294-31ed6600-4693-11ea-9a87-81f5897c02a5.png">

* 상단에 있는 js의 내용 (라이브러리):
<img src="https://user-images.githubusercontent.com/58318174/73628293-31ed6600-4693-11ea-9dc0-96854eff34be.png">

* 하단에 있는 js(site event처리[hover, click, scroll, 셀렉트 박스]):
<img src="https://user-images.githubusercontent.com/58318174/73628292-3154cf80-4693-11ea-9e4e-43302b4126a0.png">

* 하단에 있는 js의 내용:
<img src="https://user-images.githubusercontent.com/58318174/73628295-31ed6600-4693-11ea-9489-3edd77a2733a.png">

#### 최상단에 js 가 위치 한 이유
JQuery CDN 등의 라이브러리를 사용하기 위해서.
#### 최하단에 js 가 위치 한 이유
렌더링이 완료 된 후 사용자의 Interaction 을 처리하기 위하여.

자바스크립트는 싱글스레드로 동작합니다.
파서가 내부 태그이든 외부 태그이든 script 태그에 도달하면 (외부 태그 인 경우) fetch를 중단하고 실행한다.  그 뜻은 한가지 일을 하고 있을때 모든 작업이 block 된다는 것, 따라서 문서 내의 요소를 참조하는 JavaScript 파일이 있는 경우 해당 문서가 표시된 후에 배치 해야 한다.

많은 코드가 들어있고 코드중 일부의 속도가 느리다면 최초 화면 로딩이 느려 사용자에게 답답함을 유발할 것 따라서 스크립트는 고정된 위치가 아니라 상황에 맞춰 적절히 분배해야 한다

### 2-2. css 의 위치
css 가 위치한 곳 (상단):
<img src="https://user-images.githubusercontent.com/58318174/73628610-0cad2780-4694-11ea-8287-9f261534e038.png">

css 가 위치한 곳 (가운데) -> 반응형 사이트 css 적용 :
<img src="https://user-images.githubusercontent.com/58318174/73628820-aaa0f200-4694-11ea-92e6-1475fe1af830.png">
<img src="https://user-images.githubusercontent.com/58318174/73629106-77ab2e00-4695-11ea-98bc-6c735318fefe.png">

#### 2-3. css가 최상단에 위치한 이유
HTML DOM 요소가 화면에 보일때 원하는 디자인이 적용된 형태로 나타나야 되기 때문에

#### 2-4. css가 가운데에 embed 형태로 위치한 이유


## 3. 화면을 표시하기 위해 어떤 파일들이 다운로드 되는가?
<img src="https://user-images.githubusercontent.com/58318174/73629486-a4137a00-4696-11ea-8bcd-b4af1a4bce88.png">
1. Image Files (*.png, *.gif etc..) </br>
2. JS Files (라이브러리 포함) </br>
3. Font Files (woff) </br>
4. 스타일 시트 </br>
5. text/html </br>
</br>
* 다운로드 된 파일 타입을 Network 탭에서 Content-Type 으로 확인 가능.
<img src="https://user-images.githubusercontent.com/58318174/73630052-55ff7600-4698-11ea-9abd-b63f57b38818.png">

## 4. 특정 자원의 Request Headers 와 Response Headers의 내용을 분석.(네트워크 탭 활용)
### 4-1. Request
<img src="https://user-images.githubusercontent.com/58318174/73630309-07061080-4699-11ea-97d1-dcdab1b99bb0.png"></br>
request headers : 페치될 리소스나 클라이언트 자체에 대한 자세한 정보를 포함하는 헤더.

### 4-2. Response
<img src="https://user-images.githubusercontent.com/58318174/73630213-cc03dd00-4698-11ea-958d-0fe8a4155e84.png">
response headers : 위치 또는 서버 자체에 대한 정보(이름, 버전 등)와 같이 응답에 대한 부가적인 정보를 갖는 헤더

## 5. 화면에 보여지기 시작하는 시간은 언제인가?
* First Paint: 첫 번째 페인트는 사용자가 웹 페이지를 탐색 한 후 첫 번째 픽셀이 화면에서 렌더링되는 지점.
<img src="https://user-images.githubusercontent.com/58318174/73636902-4ee16380-46aa-11ea-99d8-1f1d12644558.png">
* First Contentful Paint: 텍스트, 이미지, 흰색이 아닌 캔버스 또는 SVG (Scalable Vector Graphics)를 포함하여 DOM (Document Object Model)의 컨텐츠를 페이지에 처음 렌더링 하는 지점.
<img src="https://user-images.githubusercontent.com/58318174/73703011-ea69e700-4731-11ea-8b3d-247923f4b1d5.png">

### Flow
* DOM 트리 구축(Constructing the DOM Tree)</br>
* CSSOM 트리 구축(Constructing the CSSOM Tree)</br>
* JavaScript 실행(Running JavaScript)</br>
* 랜더링 트리 구축(Creating the Render Tree)</br>
* 레이아웃 생성(Generating the Layout)</br>
* 페인팅(Painting)</br>

## 6. DOMContentLoaded라는 이벤트는 언제 발생하는가? load랑은 어떤 차이점이 있는가?

### 6-1. DOMContentLoaded 이벤트
DOMContentLoaded 이벤트는 초기 HTML 도큐먼트가 로드되고 파스되면 스타일시트, 이미지 및 다른 프레임이 로딩되기전에 실행됩니다. 이벤트의 진짜 타겟은 로드가 완료된 이벤트 입니다. 이벤트는 Window 인터페이스에서 이벤트를 수신하여 캡쳐하고 버블링할 수 있습니다.

### 6-2. load 이벤트
load 이벤트는 스타일시트 이미지와 같이 의존성이 있는 리소스가 준비되면 실행됩니다. 이것은 DOMContentLoaded와 정반대입니다.

참조> 
Page: DOMContentLoaded, load, beforeunload, unload (https://javascript.info/onload-ondomcontentloaded)
DOMContentLoaded, load (https://yngmanie.space/posts/dom-event)


## HTML 파일 응답 받은 이후부터, 모니터화면에 보이기까지의 과정.
* Send Request - index.html에 대한 GET 요청 전송
* Parse HTML and Send Request - HTML 및 DOM 구문 분석을 시작. style.css 및 main.js에 대한 GET 요청
* Parse Stylesheet - CSSOM이 style.css 용으로 생성
* Evaluate Script - main.js 평가
* Layout - HTML의 메타 뷰포트 태그를 기반으로 레이아웃 생성
* Paint - 문서의 픽셀을 페인트

참조> 
HTML Critical rendering path의 이해 ("https://blog.asamaru.net/2017/05/04/understanding-the-critical-rendering-path/")
