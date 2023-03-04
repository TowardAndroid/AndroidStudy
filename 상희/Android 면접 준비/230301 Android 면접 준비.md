# 230301 Android 면접 준비

## Q1. Android Jetpack에 대해 설명해 주시고, Jetpack에서 사용해 본 기능을 말씀해 주세요.
안드로이드 앱을 구축하는데 도움이 되는 훌륭한 도구 모음이다.  
즉, Jetpack은 안드로이드 개발자들이 더욱 쉽게 높은 퀄리티의 앱을 개발할 수 있도록 도와주는 라이브러리들의 모음집이다.

<br/>

Jetpack은 크게 4가지로 분류해서 생각할 수 있다.  
- Foundation Components
- Architecture Components
- Behavior Components
- UI Components

<br/>

Android Jetpack에서 CameraX 라이브러리를 사용해 보았습니다.  
Android Jetpack 구성 요소에는 Room, Navigation( - Fragment), ViewModel 등이 있습니다.

<br/>
<br/>

## Q2. Broadcast Receiver를 사용할 때, Broadcast를 수신하는 기능 말고 Broadcast를 송신할 수는 없을까요?
Broadcast Receiver를 이용하여 앱 간의 데이터 전달이나 Broadcast를 송신할 수 있다.  
상호 작용할 앱 모두에 Broadcast Receiver를 등록하고, sendBroadcast()를 이용하여 Intent를 주고받는 방식으로 동작시켜 준다.

<br/>
<br/>

## Q3. Kotlin 언어에서 동일성과 동등성이 어떻게 비교하는지 아시나요?
- 동등성(equality, ==)은 두 개의 객체의 값이 완전히 동일한 것인지 비교한다. (값 비교, 내부적으로 equals를 호출)
- 동일성(idenity, ===)은 같은 주소를 참조하는지 비교한다. (주소 값 비교, 식별자를 기반으로 객체를 판단)

<br/>
<br/>

## Q4. View.GONE과 View.INVISIBLE의 차이점은 무엇인가요?
- INVISIBLE : 뷰를 그려 놓고 보이지는 않지만 레이아웃에 공간을 차지하고 있다.
- GONE : 어댑터에 getView()가 호출되지 않아 뷰를 그리지 않고 레이아웃에 공간을 차지하고 있지 않다.
- View.GONE으로 초기화하면 뷰가 초기화되지 않았을 수 있으므로 임의의 오류가 발생할 수 있다. 따라서 뷰의 처리(이동, 크기 등)를 하기 전에 View.VISIBLE 또는 View.INVISIBLE로 초기화하고 화면에 렌더링 한 다음에 처리해야 한다.

<br/>
<br/>

## Q5. String과 StringBuffer의 차이는 무엇인가요?
- String : 불변, 문자를 수정하려면 지우고 다시 생성(new) → 문자열 연산이 많으면 기능이 떨어진다.
- StringBuffer : 가변, 한 번 만들고 필요할 떄 크기를 변경하여 문자를 변경(append()와 같이)
- StringBuilder : 동기화 지원 X, 멀티 스레드 환경에 부적합 → 싱글 스레드에서 StringBuffer보다 좋다.

<br/>
<br/>

## 🗂 참고
- [Android Jetpack (notion.site)](https://www.notion.so/ba7fc5af7422453e87a1f8354fdba7b2)
- [Android Interview (notion.site)](https://www.notion.so/3ce7ddf12ddb413a9d2213173654d52c)
- [안드로이드 앱 개발자 면접 후기 - 1차면접 .. : 네이버블로그 (naver.com)](https://blog.naver.com/csi468_/221465784013)
- [Android : Difference between View.GONE and View.INVISIBLE? - Stack Overflow](https://stackoverflow.com/questions/11556607/android-difference-between-view-gone-and-view-invisible)
