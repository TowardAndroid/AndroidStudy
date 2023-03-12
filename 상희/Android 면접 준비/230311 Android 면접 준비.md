# 230311 Android 면접 준비

## Q1. MVI 패턴이 등장하게 된 배경을 설명해 주세요.
- Multiple Inputs    
    : MVP의 Presenter, MVVM의 ViewModel은 종종 많은 입력과 출력을 관리한다. 이는 백그라운드 작업이 많은 큰 앱에서 문제가 된다.    
- Multiple States    
    : MVP와 MVVM에서 business logic과 View는 어떤 시점에 다른 상태를 가질지도 모른다. 이를 위해 Observable과 Observer callaback으로 상태에 대한 동기를 맞춰 줘야 하는데 충돌이 있을 수 있다.    
- View → Presenter →Business Logic → View
    - View : user action을 observing / Model을 표현
    - Presenter : data 관리
    - Business Logic : 다른 상태를 가지는 새로운 Model 생성

<br/>
<br/>

## Q2. MVI 패턴 사용 시 얻을 수 있는 이점을 설명해 주세요.
- Single State    
    : Immutable data는 다루기 쉽고 한 곳에서만 관리된다.    
- Thread Safety    
    : 어떤 메서드도 Model을 변경할 수 없기 때문에 항상 새로 생성되고 유지된다. 이는 다른 스레드에서 Model 객체를 수정하는 Side Effect를 방지할 수 있다.
    
<br/>
<br/>

## Q3. MVVM ViewModel과 AAC ViewModel 차이점을 설명해 주세요.
MVVM ViewModel은 View와 Model을 바인딩해 주는 역할을 하고 AAC ViewMdoel은 수명 주기를 고려해 UI 관련 데이터를 저장하고 관리한다.

<br/>
<br/>

## Q4. 화면 전환 시에 대한 생명 주기는 어떻게 되나요?
화면 전환 시에는 소멸 후에 다시 액티비티가 생성된다. 즉, onStop, onDestroy 후에 onCreate, onStart, onResume을 호출하게 된다.

<br/>
<br/>

## Q5. 화면 전환 시 데이터는 어떻게 될까요?
별도의 데이터베이스에 저장하지 않았다면 리셋될 것이다.  
따라서 데이터를 유지하기 위해서는 별도로 데이터를 저장해 주어야 하는데, onPause 직전에 호출되는 onSaveInstanceState 메소드를 통해 저장하고자 하는 데이터를 번들에 담을 수 있다. 그리고 onCreate에서 savedInstanceState에서 해당하는 데이터를 받아올 수 있다.  
혹은 AAC의 ViewModel을 사용하면 데이터를 유지할 수 있다.

<br/>
<br/>

## 🗂 참고
- [[Android] MVC, MVP, MVVM, MVI, Android App Architecture | by kimji1 | Medium](https://dev-kimji1.medium.com/mvc-mvp-mvvm-mvi-android-app-architecture-e0087bc0e5a7)
- [안드로이드 면접 질문 대비 — 안솝우화 (tistory.com)](https://asuhdevstory.tistory.com/71)
- [[Android] 안드로이드 면접 질문 정리 :: Hello, Maejing! (tistory.com)](https://maejing.tistory.com/entry/Android-%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-%EC%A7%81%EB%AC%B4-%EB%A9%B4%EC%A0%91-%EC%A7%88%EB%AC%B8-%EC%A0%95%EB%A6%AC)
