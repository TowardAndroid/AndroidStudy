# handling lifecycles

****LifeCycle****

LifeCycle은 Activity나 Fragment와 같은 구성요소의 수명 주기 상태 관련 정보를 포함하며 다른 객체가 이 상태를 관찰할 수 있게 하는 클래스입니다.

이벤트

프레임워크 및 클래스에서 전달되는 수명 주기 이벤트입니다. 이러한 이벤트는 활동과 프래그먼트의 콜백 이벤트에 매핑됩니다.

상태 객체가 추적한 구성요소의 현재 상태입니다.

![image](https://github.com/overthename/AndroidStudy/assets/80188940/82809294-4238-4ce3-bea7-efd13a79d21e)


애플리케이션은 수명 주기를 고려해야 하며, 그렇게 하지 않으면 메모리 누수 또는 애플리케이션 비정상 종료가 발생할 수 있습니다.

# **LifeCycle은 언제 쓰는가?**

- 대략적인 위치/세분화된 위치 업데이트 간 전환.
    - 수명 주기 인식 구성요소를 사용하면 위치 앱이 공개 상태이면 세분화된 위치 업데이트를 사용하고, 앱이 백그라운드에 있으면 대략적인 위치 업데이트로 전환할 수 있습니다. 수명 주기 인식 구성요소인 [LiveData](https://developer.android.com/reference/androidx/lifecycle/LiveData)를 사용하면 사용자가 위치를 변경할 때 앱에서 자동으로 UI를 업데이트할 수 있습니다.
- 동영상 버퍼링 중지와 시작.
    - 수명 주기 인식 구성요소를 사용하면 동영상 버퍼링을 최대한 빨리 시작하지만, 앱이 완전히 시작될 때까지 재생을 연기합니다. 또한 수명 주기 인식 구성요소를 사용하여 앱이 제거될 때 버퍼링을 종료할 수 있습니다.
- 네트워크 연결 시작과 중지.
    - 수명 주기 인식 구성요소를 사용하면 앱이 포그라운드에 있는 동안 네트워크 데이터를 실시간으로 업데이트(스트리밍)할 수 있으며, 앱이 백그라운드로 이동하면 실시간 업데이트를 자동으로 일시중지할 수도 있습니다.
- 애니메이션 드로어블 일시중지와 재개.
    - 수명 주기 인식 구성요소를 사용하면 앱이 백그라운드에 있는 동안 애니메이션 드로어블 일시중지를 처리하고, 앱이 포그라운드로 이동한 후 드로어블을 재개할 수 있습니다.
    

구성요소

****(1) Lifecycle Owner****

Activity, Fragment에서 생명주기를 분리하여 Lifecycle 객체에 담습니다. Lifecycle 객체를 통해 다른 곳에서 해당 화면의 생명주기를 모니터링 할 수 있습니다. 자신의 생명주기를 담은 Lifecycle 객체가 Lifecycle Owner 입니다.

![image](https://github.com/overthename/AndroidStudy/assets/80188940/67a254da-5dd3-42c7-9276-f8ca7ca59c84)


## **(2) Lifecycle Observer**

화면 밖에서도 생명주기에 따른 동작을 정의하기 위해서는 원하는 클래스에 LifecycleObserver 인터페이스를 구현하고, 넘겨받은 Lifecycle Owner 객체에 구현한 LifecycleObserver를 등록해야 합니다. LifecycleObserver를 구현한 클래스는 onResume() 등의 생명주기 메소드를 정의할 수 있습니다. 이 메소드들은 등록한 Lifecycle Owner가 해당 생명주기 상태가 되면 자동으로 수행되면서, 객체가 화면과 동일한 생명주기를 가진 것처럼 행동하도록 합니다.

![image](https://github.com/overthename/AndroidStudy/assets/80188940/8acaa2ef-6413-4b26-b1e0-e5d954bc45a1)


Lifecycles를 통해 우리는 화면 밖에서 화면의 생명주기를 모니터링 하고, 동작을 정의할 수 있습니다. 이는 더 직관적인 생명주기 프로그래밍을 가능하게 합니다.
