Chrome Devtools 를 활용한 웹 페이지 디버깅에 대한 블로그입니다.

# Introduction
Chrome Devtools 를 활용한 웹 페이지 디버깅은 Visual Studio Code 와 같은 IDE 를 사용하여 코드 수정을 한 후 확인하는것보다 빠르게 Layout 구조 및 디자인 수정 및 확인이 가능합니다.

# Elements 탭
![Elements](https://github.com/dev-angelo/DevTips-FrontEnd/blob/master/Debugging-Webpage-With-Chrome-Devtools/images/elements.png)
* html 구조, Styles (css), Computed (box model) 등을 확인 가능합니다.

# HTML 구조
![Elements_HTML](https://github.com/dev-angelo/DevTips-FrontEnd/blob/master/Debugging-Webpage-With-Chrome-Devtools/images/elements_html.png)
* HTML 의 전체적인 구조 확인이 가능합니다.
* HTML 수정을 통한 Layout 구조 변경을 즉각적으로 확인 가능합니다.

# Styles
![Elements_Styles](https://github.com/dev-angelo/DevTips-FrontEnd/blob/master/Debugging-Webpage-With-Chrome-Devtools/images/elements_styles.png)
* 스타일링을 위한 css 에 대해 확인 가능합니다.
* HTML 과 마찬가지로 내용 수정 혹은 추가/삭제를 통하여 실시간으로 디버깅이 가능합니다.

# Computed
* Box Model 을 통해 margin, border, padding, width 및 height 를 수정하는 등의 Layout 디버깅이 가능합니다.
* Styles 에서는 tag 추가/삭제가 되었던 것에 반하여 여기에서는 tag 추가/삭제는 불가능합니다.

# Performance 탭
![Performance](https://github.com/dev-angelo/DevTips-FrontEnd/blob/master/Debugging-Webpage-With-Chrome-Devtools/images/performance.png)
* 각 스레드에서 특정 작업을 하는데에 걸리는 시간을 체크 할 수 있습니다.
