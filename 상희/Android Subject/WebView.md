# 💡 WebView

# ✅ WebView란?
WebView : 안드로이드 앱 내에서 사용할 수 있는 인터넷 브라우저이다.

<br/>

안드로이드 컴포넌트 뷰(View)를 개발할 경우 유연성이 떨어지게 된다. 안드로이드 컴포넌트로도 유연성 있게 개발할 수 있지만, 이미 작성된 코드 내에서 유연성이 생길 뿐이다.  
이에 따라 유연성이 필요한 곳에는 WebView를 쓰는 곳이 많다. WebView를 사용하기 위해서는 Android와 WebView 간 통신 방법을 알아야 한다.

<br/>
<br/>

# ✅ WebView에서 웹 앱 빌드
웹 애플리케이션 또는 웹 페이지만 클라이언트 애플리케이션의 일부로 제공하려는 경우 WebView를 사용하면 된다.  
WebView 클래스는 Android의 View 클래스의 확장으로, 웹 페이지를 활동 레이아웃의 일부로 표시할 수 있게 해 준다. 탐색 컨트롤이나 주소 표시줄 등 완전히 개발된 웹 브라우저의 기능은 전혀 포함되어 있지 않다. WebView의 모든 작업은 기본적으로 웹 페이지를 표시하는 것이다.

<br/>

## WebView를 사용하는 것이 도움이 되는 상황
- 최종 사용자 계약이나 사용자 가이드 같은 업데이트해야 할 정보를 앱에서 제공하려는 경우
    - Android 앱 내에서는 WebView를 포함하는 Activity를 만들어 온라인으로 호스팅된 문서를 표시하는 데 사용할 수 있다.
- 이메일과 같은 데이터를 가져오기 위해 항상 인터넷이 연결되어 있어야 하는 사용자에게 앱에서 데이터를 제공하는 경우
    - 이 경우 네트워크 요청을 수행한 다음 데이터를 파싱하고 Android 레이아웃에서 렌더링하는 것보다 모든 사용자 데이터가 포함된 웹 페이지를 표시하는 WebView를 Android 앱에 빌드하는 것이 더 쉽다. 대신에 Android 기기에 맞춤화된 웹 페이지를 설계한 다음 웹페이지를 로드하는 WebView를 Android 앱에 구현할 수 있다.

<br/>

## WebView 사용
### 앱에 WebView 추가
WebView를 앱에 추가하려면 활동 레이아웃에서 \<WebView> 요소를 포함하거나 onCreate()에서 전체 활동 창을 WebView로 설정하면 된다.

<br/>  
  
- 활동 레이아웃에서 WebView 추가

```xml
    <WebView
        android:id="@+id/webview"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
    />
```

<br/>  
  
WebView에서 웹 페이지를 로드하려면 loadUrl()을 사용한다.

```kotlin
    val myWebView: WebView = findViewById(R.id.webview)
    myWebView.loadUrl("http://www.example.com")
```

<br/>  
  
- onCreate()에서 WebView 추가

```kotlin
    val myWebView = WebView(activityContext)
    setContentView(myWebView)
```

<br/>  
  
그런 다음 아래와 같이 페이지를 로드한다.

```kotlin
    myWebView.loadUrl("http://www.example.com")
```

<br/>
  
또는 HTML 문자열에서 URL을 로드한다.

```kotlin
    // Create an unencoded HTML string
    // then convert the unencoded HTML string into bytes, encode
    // it with Base64, and load the data.
    val unencodedHtml =
            "&lt;html&gt;&lt;body&gt;'%23' is the percent code for ‘#‘ &lt;/body&gt;&lt;/html&gt;"
    val encodedHtml = Base64.encodeToString(unencodedHtml.toByteArray(), Base64.NO_PADDING)
    myWebView.loadData(encodedHtml, "text/html", "base64")
```

<br/>  
  
이 작업을 수행하려면 앱이 인터넷에 액세스할 수 있어야 한다. 인터넷 액세스 권한을 받으려면 manifest 파일에서 INTERNET 권한을 요청해야 한다.

```xml
    <manifest ... >
        <uses-permission android:name="android.permission.INTERNET" />
        ...
    </manifest>
```

<br/>  
  
이러한 작업이 웹 페이지를 표시하는 기본 `WebView`에 필요한 모든 사항이다. 이 외에도 다음을 수정하여 `WebView`를 맞춤 설정할 수 있다.  
- `WebChromeClient`로 전체 화면 지원 사용 설정. 이 클래스는 `WebView`가 창을 만들거나 닫고 자바스크립트 대화 상자를 사용자에게 전송하는 등 호스트 앱의 UI를 변경하기 위한 권한을 필요로 할 때도 호출된다.
- `WebViewClient`를 사용한 탐색 오류 또는 양식 제출 오류 등 콘텐츠 렌더링에 영향을 미치는 이벤트 처리. 이 서브 클래스를 사용하여 URL 로드를 가로챌 수도 있다.
- `WebSettings`를 수정하여 자바스크립트 사용 설정.
- `WebView`에 삽입된 Android 프레임워크 객체에 자바스크립트를 사용하여 액세스.

<br/>
<br/>  
  
# 🗂 참고
- [[안드로이드] 웹뷰(WebView) - 초간단 웹브라우저 예제 (with 로딩바(ProgressBar)) (tistory.com)](https://jhshjs.tistory.com/57)
- [[Android] WebView와 브릿지를 사용해 통신하는 방법 한 번에 정리하기 — Dev World (kotlinworld.com)](https://kotlinworld.com/364)
- [WebView에서 웹 앱 빌드  |  Android 개발자  |  Android Developers](https://developer.android.com/guide/webapps/webview?hl=ko)
