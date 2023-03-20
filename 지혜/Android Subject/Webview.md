# Webview

### ***WebView***

- 웹 탐색과 웹 브라우저는 Android, iOS, PC 모두 가진 기능
- **WebView**는 웹 브라우저를 구성하는 **HTML**과 같은 요소들을 받아들여 이를 브라우저와 **동일한 형식**으로 해석해서 표현해주는 뷰
- 그래서 **WebView**는 PC의 서버에서 response 한 웹 파일을 받아서 Android에서도 똑같이 보여주고 다룰 수 있고, 디바이스 상관없이 정보 공유가 가능한 **하이브리드 앱**을 쉽게 구현할 수 있도록 도와줍니다.

### ***java script 연동 (앱 -> 웹뷰 JavaScript 호출)***

- 웹 브라우저는 java script를 사용
- 단순히 받아온 코드를 해석하는 것은 문제가 없을지 몰라도, 화면에 표시되는 웹 페이지와 안드로이드 코드가 유기적으로 동작하기 어려울 수 있습니다.
- 하지만, 이를 지원해주는 api가 존재합니다.
- **loadUr**l 메소드에 **java script**의 함수명을 적어주어, 정의된 함수를 실행시킬 수 있습니다.
- 앱의 동작에 연동하여 java script의 어떠한 동작을 하도록 이벤트를 걸 때 사용하면 좋습니다.

```kotlin
webView.loadUrl("javascript:alerthello()")
```

[https://yoon-dailylife.tistory.com/109](https://yoon-dailylife.tistory.com/109)

[https://developer.android.com/guide/webapps/webview?hl=ko](https://developer.android.com/guide/webapps/webview?hl=ko)
