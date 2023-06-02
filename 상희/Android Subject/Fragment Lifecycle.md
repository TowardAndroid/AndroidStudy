# 💡 Fragment Lifecycle

# ✅ Fragment
프래그먼트를 사용하면 화면 하나를 독립적으로 작동하는 부분 화면 여러 개로 구현할 수 있다.  
프래그먼트는 액티비티처럼 정의된 레이아웃을 표시하고, 자체 생명 주기를 가지며 입력 이벤트를 받을 수 있다.  
하지만 독립적으로 존재할 수 없고, 해당 프래그먼트를 관리하는 호스트 액티비티나 프래그먼트 하위에서만 존재할 수 있다.

<br/>

## Advantages
### Lightweight
액티비티는 안드로이드 4대 컴포넌트 중 하나로 안드로이드 시스템에서 관리한다. 반면 프래그먼트는 안드로이드 시스템이 직접 관리하지 않고 프래그먼트 매니저가 관리하기 때문에 메모리 리소스가 상대적으로 덜 소모되어 액티비티보다 가볍다.

<br/>

### Reusability
한 번 작성된 프래그먼트는 여러 액티비티에서 재사용이 가능하며, 따라서 UI 구현에 필요한 작업량을 상당히 감소시킬 수 있다.

<br/>
<br/>

# ✅ Fragment Lifecycle
프래그먼트의 생명 주기는 아래 그림과 같다.  
![https://developer.android.com/static/images/guide/fragments/fragment-view-lifecycle.png](https://developer.android.com/static/images/guide/fragments/fragment-view-lifecycle.png)

<br/>

위의 그림은 안드로이드 공식 문서에서 제공하는 것으로 프래그먼트 자체와 프래그먼트 뷰의 생명주기를 구분해서 표현하고 있다.  
실제로 프래그먼트 자체와 프래그먼트 뷰는 생성되고 소멸되는 시기가 다르기 때문에 이를 잘 인지해서 프로그램을 작성해주지 않으면 메모리 릭에 빠지거나 앱이 터질 수가 있다.
  - ex : 뷰가 생성되지 않았을 때 뷰를 참조하는 실수를 할 수도 있다.

<br/>
<br/>

# 🗂 참고
- [책] 깡샘의 안드로이드 프로그래밍
- [프래그먼트 라이프사이클 | Android 개발자](https://developer.android.com/guide/fragments/lifecycle)
- [[Android] Fragment Lifecycle (velog.io)](https://velog.io/@jeongminji4490/Android-Fragment-Lifecycle)
- [[Android] 의외로 잘 모르는 Fragment 의 Lifecycle :: 준비된 개발자 (tistory.com)](https://readystory.tistory.com/199)
