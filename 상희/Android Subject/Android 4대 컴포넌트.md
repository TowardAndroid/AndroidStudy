# 💡 Android 4대 컴포넌트

# ✅ Android Component
안드로이드 컴포넌트는 4 가지 종류가 있다.  
- 액티비티(Activity) : UI를 구성하기 위한 컴포넌트
- 서비스(Service) : UI 없이 백그라운드에서 장시간 수행되는 컴포넌트
- 콘텐츠 프로바이더(ContentProvider) : 애플리케이션 간 데이터를 공유하기 위한 컴포넌트
- 브로드캐스트 리시버(BroadcastReceiver) : 이벤트 모델로 수행되는 컴포넌트

<br/>

![Untitled](https://velog.velcdn.com/images/jojo_devstory/post/9138556b-4a4c-4c48-a6dc-c9abc34e9b46/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202020-03-06%20%EC%98%A4%EC%A0%84%2011.51.43.png)

- 각 컴포넌트들은 하나의 독립적인 형태로 존재한다.
- 각 컴포넌트들은 고유의 기능을 수행한다.
- 각 컴포넌트들은 인텐트를 통해 서로 상호 작용한다.

<br/>

## Activity
액티비티(Activity)는 사용자 화면을 제공하는 컴포넌트이다. 안드로이드 앱은 클라이언트 측 애플리케이션이므로 화면 구성이 중요하다. 따라서 가장 많이 작성하는 컴포넌트이다.

<br/>

사용자와 상호작용을 담당하는 인터페이스라고 할 수 있다.  
그래서 안드로이드 애플리케이션은 반드시 하나 이상의 액티비티를 포함하고 있으며 액티비티는 생명 주기(Lifecycle) 관련 메서드들을 재정의하여 원하는 기능들을 구현할 수 있다.

<br/>

- 인텐트(Intent)를 통해 다른 애플리케이션의 액티비티를 호출할 수 있다.
- 2개 이상의 액티비티를 동시에 Display 할 수 없다.
- 1개 이상의 View 또는 ViewGroup을 포함한다.
- 반드시 애플리케이션에는 하나 이상의 액티비티가 있어야 한다.
- 액티비티 내에 프래그먼트(Fragment)를 추가하여 화면을 분할시킬 수 있다.

<br/>

## Service
서비스(Service)는 화면과 전혀 상관없이 사용자 눈에는 보이지 않지만, 백그라운드에서 장시간 무언가를 수행할 수 있는 컴포넌트라고 이해하면 된다.  
채팅을 제공해 주는 애플리케이션을 생각해 보면 사용자가 화면에서 게임을 하고 있더라도 채팅 앱이 서버랑 계속 연결을 유지한 상태에서 데이터를 주고받아야 하는데 이럴 때 이용하는 컴포넌트가 서비스이다.

<br/>

서비스는 사용자와 직접적으로 상호 작용하는 요소는 아니다.  
흔히 백그라운드(Background)에서 어떠한 작업을 처리하기 위해 서비스를 사용한다.  
서비스 같은 경우 사용자의 인터페이스(UI, 화면)를 방해하지 않고 눈에 보이지 않는 곳에서 작업을 처리하기 때문에 별도의 스레드(Thread)에서 동작한다고 오해하는 경우가 많다. 하지만 서비스는 엄연히 메인 스레드에서 동작하기 때문에 서비스 내에서 별도의 스레드를 생성하여 작업을 처리해야 한다.

<br/>

- 네트워크(Network)와 연동이 가능하다.
- 별도의 UI를 가지지 않으며 백그라운드에서 수행된다.
- 액티비티와 서비스는 UI 스레드라고 불리는 동일한 애플리케이션 스레드로 실행된다.
- 애플리케이션이 종료되어도 이미 시작이 된 서비스(Service)는 백그라운드(Background)에서 계속 동작한다.

<br/>

## ContentProvider
콘텐츠 프로바이더(ContentProvider)는 앱 간의 데이터 공유 목적으로 사용하는 컴포넌트이다. 안드로이드 스마트폰에는 여러 앱이 있고, 그 앱들 간의 데이터를 공유하기 위한 목적이다. 예로 들자면 개발자가 작성한 앱에서 주소록 데이터가 필요하다면 주소록 앱의 데이터를 얻어야 한다. 이때 필요한 컴포넌트가 콘텐츠 프로바이더이다.

<br/>

데이터를 관리하고 다른 애플리케이션의 데이터를 제공하는 데 사용되는 컴포넌트로, 특정한 애플리케이션이 사용하고 있는 데이터베이스(DB)를 공유하기 위해 사용하며 애플리케이션 간의 데이터 공유를 위해 표준화된 인터페이스를 제공한다.

<br/>

- SQLite DB / Web / 파일 입출력 등을 통해서 데이터를 관리한다.
- 외부 애플리케이션이 현재 실행 중인 애플리케이션 내에 있는 데이터베이스(DB)에 함부로 접근하지 못하게 할 수 있으면서 나 자신이 공개하고 공유하고 싶은 데이터만 공유할 수 있도록 도와 준다.
- 작은 데이터들은 인텐트(Intent)로 애플리케이션끼리 데이터를 서로 공유가 가능하지만 콘텐츠 프로바이더는 음악 또는 사진 파일 등과 같이 용량이 큰 데이터들을 공유하는 데 적합하다.
- 프로바이더는 데이터의 Read(읽기), Write(쓰기)에 대한 퍼미션이 있어야 애플리케이션에 접근이 가능하다.
- 데이터베이스에서 흔히 사용되는 CRUD(Create, Read, Update, Delete) 원칙을 준수한다.

<br/>

## Broadcast Receiver
브로드캐스트 리시버(Broadcast Receiver)는 흔히 이벤트 모델로 수행되는 컴포넌트라고 이야기한다. 안드로이드 개발 시 자주 이용하지만, 인텐트 원리를 이해하지 못하면 이해가 쉽지 않다.  
시스템에서 배터리가 부족하거나 시스템 부팅이 완료되는 등의 이벤트가 발생하였을 때, 이 이벤트를 받기 위해 작성하는 컴포넌트이다.

<br/>

방송 수신자라고 부르기도 하며 안드로이드 OS로부터 발생하는 각종 이벤트와 정보를 받아와 핸들링하는 컴포넌트이다.  
사용자 안드로이드 디바이스의 시스템 부팅 시 앱 초기화, 네트워크 끊김 등등 특수한 이벤트에 대한 처리나 배터리 부족 알림, 문자 수신과 같은 정보를 받아 처리를 해야 할 필요가 있을 때 동작한다.  
즉, 안드로이드 OS에서 메신저 앱 또는 문자 메시지가 오면 모든 앱에 "메시지가 왔다"라는 하나의 정보를 방송(BroadCast)을 한다.  
이 메시지를 받기 위해 브로드캐스트 리시버를 구현하면 되며 해당 정보가 오면 특정 이벤트를 처리할 수가 있다.

<br/>

- 거의 대부분 UI를 가지지 않는다.
- 안드로이드 디바이스의 특수한 상황에 대응하기 위해 사용된다.
- 특정한 상황을 제외하고는 브로드캐스트는 시스템에서 시작한다.

<br/>
<br/>

# 🗂 참고
- [책] 깡샘의 안드로이드 프로그래밍
- [안드로이드 (Android) 4대 컴포넌트(구성요소) (velog.io)](https://velog.io/@jojo_devstory/%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-Android-4%EB%8C%80-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8)
- [[안드로이드] 4대 컴포넌트 (tistory.com)](https://wookkingkim.tistory.com/entry/%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-4%EB%8C%80-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8)
- [애플리케이션 기본 항목  |  Android 개발자  |  Android Developers](https://developer.android.com/guide/components/fundamentals?hl=ko#Components)
