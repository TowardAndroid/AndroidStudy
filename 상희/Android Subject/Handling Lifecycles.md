# 💡 Handling Lifecycles

# ✅ Handling Lifecycles
## Handling Lifecycles란?
생명 주기 인식 구성 요소는 Acitivity와 Fragment 같은 구성 요소의 생명 주기 상태 변경에 따라 작업을 실행한다. 이러한 구성 요소를 사용하면 잘 구성된 경량의 코드를 만들고 더욱 쉽게 유지할 수 있다.  
즉, Handling Lifecycles는 Activity와 Fragment에 생명 주기의 상태 변경의 응답을 통해 작업을 수행하는 것을 말한다.  

<br/>

일반적인 패턴은 Activity와 Fragment의 생명 주기 메서드에 종속 구성 요소의 작업을 구현한다. 하지만 이 패턴으로 인해 코드 구성이 나빠지고 오류가 증가하게 된다. 생명 주기 인식 구성 요소를 사용하면 생명 주기 메서드에서 구성 요소 자체로 종속 구성 요소의 코드를 옮길 수 있다.  
`androidx.lifecycle`  패키지는 생명 주기 인식 구성 요소(Activity나 Fragment의 현재 생명 주기 상태를 기반으로 동작을 자동 조정할 수 있는 구성 요소)를 빌드할 수 있는 클래스 및 인터페이스를 제공한다.  

<br/>

Android 프레임워크에 정의된 대부분의 앱 구성 요소에는 생명 주기가 연결되어 있다. 생명 주기는 운영체제 또는 프로세스에서 실행 중인 프레임워크 코드에서 관리한다. 또한 Android 작동 방식의 핵심으로, 애플리케이션은 생명 주기를 고려해야 하며 그렇게 하지 않으면 메모리 누수 또는 애플리케이션 비정상 종료가 발생할 수 있다.

<br/>

`androidx.lifecycle`  패키지는 생명 주기의 현재 상태에 따라 UI와 다른 구성 요소를 관리하는 호출이 너무 많이 발생하게 되어 생긴 문제들을 탄력적이고 단독적인 방법으로 처리하는 데 도움이 되는 클래스와 인터페이스를 제공한다.

<br/>

### Lifecycle
Lifecycle은 Activity나 Fragment와 같은 구성 요소의 생명 주기 상태 관련 정보를 포함하며 다른 객체가 이 상태를 관찰할 수 있게 하는 클래스이다.

<br/>

Lifecycle은 두 가지 기본 열거를 사용하여 연결된 구성 요소의 생명 주기 상태를 추적한다.  
다시 말해 Handling Lifecycles는 다음과 같은 생명 주기 구조의 States나 Events의 응답에 따라 작업할 수 있다.

![Untitled](https://developer.android.com/static/images/topic/libraries/architecture/lifecycle-states.svg?hl=ko)

> Android Activity 생명 주기를 구성하는 상태 및 이벤트
> 

<br/>

- Events(이벤트)
    - 프레임워크 및 Lifecycle 클래스에서 전달되는 생명 주기 이벤트이다.
    - 이러한 이벤트는 Activity와 Fragment의 콜백 이벤트에 매핑된다.
- States(상태)
    - Lifecycle 객체가 추적한 구성 요소의 현재 상태이다.

<br/>

위 그림의 그래프에서 상태를 노드(node)로, 이벤트를 노드 사이의 간선(edge)으로 생각하면 된다.

<br/>

클래스는 DefaultLifecycleObserver를 구현하고 onCreate, onStart 등의 상응하는 메서드를 재정의하여 구성 요소의 생명 주기 상태를 모니터링할 수 있다.  
그러면 다음 예에 나와 있는 것처럼 Lifecycle 클래스의 addObserver() 메서드를 호출하고 관찰자의 인스턴스를 전달하여 관찰자를 추가할 수 있다.

```kotlin
class MyObserver : DefaultLifecycleObserver {
    override fun onResume(owner: LifecycleOwner) {
        connect()
    }

    override fun onPause(owner: LifecycleOwner) {
        disconnect()
    }
}

myLifecycleOwner.getLifecycle().addObserver(MyObserver())
```

<br/>

위 예에서 myLifecycleOwner 객체는 LifecycleOwner 인터페이스를 구현한다.

<br/>

### LifecycleOwner
LifecycleOwner는 클래스에 Lifecycle이 있음을 나타내는 단일 메서드 인터페이스이다.  
이 인터페이스에는 클래스에서 구현해야 하는 getLifecycle() 메서드가 하나 있다. 대신 전체 애플리케이션 프로세스의 생명 주기를 관리하려는 경우 [ProcessLifecycleOwner](https://developer.android.com/reference/androidx/lifecycle/ProcessLifecycleOwner?hl=ko)를 참고해야 한다.  
이 인터페이스는 Fragment 및 AppCompatActivity와 같은 개별 클래스에서 Lifecycle의 소유권을 추출하고, 함께 작동하는 구성 요소를 작성할 수 있게 한다. 모든 맞춤 애플리케이션 클래스는 LifecycleOwner 인터페이스를 구현할 수 있다.  
관찰자가 관찰을 위해 등록할 수 있는 생명 주기를 소유자가 제공할 수 있으므로 DefaultLifecycleObserver를 구현하는 구성 요소는 LifecycleOwner를 구현하는 구성 요소와 원활하게 작동한다.  
다음의 위치 추적 예에서는 MyLocationListener 클래스에서 DefaultLifecycleObserver를 구현하도록 한 후 onCreate() 메서드에서 Activity의 Lifecycle로 클래스를 초기화할 수 있다. 이렇게 하면 MyLocationListener 클래스가 자립할 수 있다. 즉, 생명 주기 상태의 변경에 반응하는 로직이 Activity 대신 MyLocationListener에서 선언된다. 개별 구성 요소가 자체 로직를 저장하도록 설정하면 Activity와 Fragment 로직을 더 쉽게 관리할 수 있다.

```kotlin
class MyActivity : AppCompatActivity() {
    private lateinit var myLocationListener: MyLocationListener

    override fun onCreate(...) {
        myLocationListener = MyLocationListener(this, lifecycle) { location ->
            // update UI
        }
        Util.checkUserStatus { result ->
            if (result) {
                myLocationListener.enable()
            }
        }
    }
}
```

<br/>

일반적인 사용 사례에서는 Lifecycle이 현재 정상 상태가 아닌 경우 특정 콜백 호출을 피한다. 예를 들어 Activity 상태가 저장된 후 콜백이 Fragment 트랜잭션을 실행하면 비정상 종료를 트리거할 수 있으므로 콜백을 호출하지 않는 것이 좋다.  
이러한 사용 사례를 쉽게 만들 수 있도록 Lifecycle 클래스는 다른 객체가 현재 상태를 쿼리할 수 있도록 한다.

```kotlin
internal class MyLocationListener(
        private val context: Context,
        private val lifecycle: Lifecycle,
        private val callback: (Location) -> Unit
): DefaultLifecycleObserver {

    private var enabled = false

    override fun onStart(owner: LifecycleOwner) {
        if (enabled) {
            // connect
        }
    }

    fun enable() {
        enabled = true
        if (lifecycle.currentState.isAtLeast(Lifecycle.State.STARTED)) {
            // connect if not connected
        }
    }

    override fun onStop(owner: LifecycleOwner) {
        // disconnect if connected
    }
}
```

<br/>

이 구현으로 LocationListener 클래스는 생명 주기를 완전히 인식한다. 다른 Activity나 Fragment의 LocationListener를 사용해야 한다면 클래스를 초기화하기만 하면 된다. 모든 설정과 해제 작업은 클래스 자체에서 관리한다.  
라이브러리에서 Android 생명 주기와 작동하는 데 필요한 클래스를 제공한다면 생명 주기 인식 구성 요소를 사용하는 것이 좋다. 클라이언트 측에서 직접 생명 주기를 관리하지 않아도 라이브러리 클라이언트는 이러한 구성 요소를 쉽게 통합할 수 있다.

<br/>

- 맞춤 LifecycleOwner 구현  

지원 라이브러리 26.1.0 이상의 Fragment 및 Activity에서는 이미 LifecycleOwner 인터페이스가 구현되어 있다.  
LifecycleOwner를 만들려는 맞춤 클래스가 있다면 LifecycleRegistry 클래스를 사용할 수 있지만, 다음 코드 예와 같이 이 클래스에 이벤트를 전달해야 한다.

```kotlin
class MyActivity : Activity(), LifecycleOwner {

    private lateinit var lifecycleRegistry: LifecycleRegistry

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        lifecycleRegistry = LifecycleRegistry(this)
        lifecycleRegistry.markState(Lifecycle.State.CREATED)
    }

    public override fun onStart() {
        super.onStart()
        lifecycleRegistry.markState(Lifecycle.State.STARTED)
    }

    override fun getLifecycle(): Lifecycle {
        return lifecycleRegistry
    }
}
```

<br/>
<br/>

## 🗂 참고
- [taeiim/Android-Study: 📚안드로이드 관련 지식을 공부하고 발표하는 스터디 📚 (github.com)](https://github.com/taeiim/Android-Study)
- [수명 주기 인식 구성요소로 수명 주기 처리  |  Android 개발자  |  Android Developers](https://developer.android.com/topic/libraries/architecture/lifecycle?hl=ko)
