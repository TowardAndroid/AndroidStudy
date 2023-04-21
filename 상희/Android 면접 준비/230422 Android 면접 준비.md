# 230422 Android 면접 준비

## Q1. 다른 액티비티가 실행되면 생명 주기는 어떻게 되나요?
다른 액티비티가 실행되어 전체 화면을 가리는 상태가 되면 액티비티는 정지 상태가 되며 onPause, onStop을 차례로 호출한다.  
onStop이 호출된 액티비티, 즉 정지 상태의 액티비티는 백스택에 들어가게 된다.  
뒤로 가기를 통해 다시 실행할 경우 onRestart, onStart, onResume을 통해 재실행하게 된다.

<br/>
<br/>

## Q2. onCreate()와 onStart()는 어떤 점이 다른가요?
- onCreate() 메소드는 애플리케이션이 시작되거나 액티비티가 삭제된 후 재생성될 때, 액티비티 사이클에서 한번만 호출된다.    
    ex : 앱의 구성 요소(언어, Orientation 등)가 변경되어 액티비티가 부서지고 다시 생성될 때 등    
- onStart() 메소드는 언제든지 액티비티가 유저에게 보여줄 준비가 되었을 때(가시적일 때) 호출될 수 있다. 전형적으로 onCreate() 이후나 onRestart() 이후에 호출된다.

<br/>
<br/>

## Q3. 액티비티에서 onPause()나 onStop()이 호출되지 않고 onDestroy 가 호출되는 경우는 언제인가요?
onCreate() 함수 안에서 finish()를 호출할 경우, 시스템은 직접 onDestroy()를 호출한다.

<br/>
<br/>

## Q4. Context란 무엇인가요?
어플리케이션에 대한 정보에 접근할 수 있는 인터페이스이다.  
추상 클래스로써 실제 구현은 안드로이드 시스템에 의해 제공된다.  
컨텍스트를 통해 어플리케이션에 특화된 리소스나 클래스에 접근할 수 있고, 액티비티 실행, 인텐트 브로드캐스팅, 인텐트 수신과 같은 응용 프로그래밍 수준의 작업을 수행하기 위한 API를 호출할 수 있다.

<br/>
<br/>

## Q5. HTTP 통신을 메인스레드에서 하면 안되는 이유?
안드로이드는 기본적으로 메인 스레드는 UI스레드로, 처리 시간이 오래 걸리는 작업을 메인 스레드에서 하게 되어 대기할 경우 ANR이 발생한다.

<br/>
<br/>

## 🗂 참고
- [[Android] 안드로이드 면접 질문 정리 :: Hello, Maejing! (tistory.com)](https://maejing.tistory.com/entry/Android-%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-%EC%A7%81%EB%AC%B4-%EB%A9%B4%EC%A0%91-%EC%A7%88%EB%AC%B8-%EC%A0%95%EB%A6%AC)
- [안드로이드 면접 질문 1 (tistory.com)](https://nanamare.tistory.com/99)
