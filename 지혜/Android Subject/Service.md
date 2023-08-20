# service

안드로이드 4대 컴포넌트 중 하나

사용자에게 인터페이스를 제공하지 않고 백그라운드에서 오래 실행되는 작업을 수행할 수 있는 애플리케이션 구성 요소

화면 출력 능력은 가지지 않은 컴포넌트(액티비티와 다르게 UI가 존재하지 않는다.)

서비스의 시작과 종료는 다른서비스, Activity, BroadCast Receiver를 포함한 다른 Application에서 가능

### 필요할 때

- 예를 들어 Activity가 Pause되거나, 화면에 없어지는 경우(Stop) 음악이 계속흘러나와야 하는 할 때 / 파일 다운로드 해야할 때
- 화면 뒷단 즉--> 백그라운드 영역에서 작업을 해야하는 경우
- 어플리케이션이 실행 중이지 않을 때도 작업해야하는 경우

### 종류

### 포그라운드

알림창을 통해 서비스가 실행중인 것을 나타내줍니다. 대신, 시스템에 의해서 강제종료 당하지 않습니다.

앱이 꺼져도 여전히 동작하는 서비스

하지만 유저에게 서비스가 작동하고 있음을 알려줘야함

### 백그라운드

사용자에게 보이지 않고 작업을 수행합니다. 대신, 시스템에서 리소스가 부족할 경우 강제종료 당할 수 있습니다.

앱이 켜져 있을때만 동작하는 서비스

앱이 꺼지면 함께 꺼짐

### **Bound**

바인딩된 구성요소가 아직 살아있는 경우에만 실행되는 서비스

<br>

### 서비스 구현 방법

### **startService**

startService() 함수를 호출해서 서비스를 시작하면, 시작타입의 서비스가 실행

 시작타입의 서비스는 한 번 시작되면, 백그라운드에서 무한정 실행되지만, 보통의 경우는 일처리를 다 완료하면 서비스가 종료된다. 

시작타입의 서비스는 호출한 곳에 결과값을 반환하지 않고 계속해서 서비스한다. (음악재생,파일다운로드 등)

하나의 프로세스안에서 동작하며, 패키지내 컴포넌트들과 유기적으로 통신하는 역할

### **boundService**

bindService() 함수를 통해서 서비스하면, 연결타입의 서비스가 실행된다. 

연결타입의 서비스는 서버-클라이언트 형식의 구조를 취하기 때문에 호출자(액티비티)에서 서비스에게 어떤것을 요청하고 서비스는 그 요청을 처리한 후 결과값을 반환한다.

 이러한 구조때문에 액티비티가 사라지면, 서비스도 자동적으로 destroy되면서 없어진다. 또 하나의 서비스에 여러개의 액티비티가 붙을 수 있다.

다른 프로세스들 간에서도 통신이 유기적으로 가능.

### **intentService**

일반 Service와 다르게 요청이 끝나면, 자동으로 서비스가 종료, 또 다른 서비스들과 다르게 onHandleIntent()함수 하나만을 통해 작업을 처리할 수 있다.

<br>

### 생명주기

**startService**

startService() 함수에 의해 실행된 서비스는 특정 객체를 리턴하지 않는다. 즉, 컴포넌트 간의 상호 데이터를 서비스에 직접 전달할 수 있는 방법이 없다

![image](https://github.com/overthename/AndroidStudy/assets/80188940/cd842437-0158-42f8-b5fe-f5dd7d3cea30)

- startService() → onCreate(), onStartCommand()
- stopService() → onDestroy()
- onCreate() 함수는 서비스 객체 생성 시 최초에 한번만 실행된다.
- 서비스가 중단되었다가 다시 실행될 때는 onStartCommand() 함수가 호출된다.
- onStartCommand() 함수는 자신을 실행시킨 인텐트의 요청 사항을 처리한다.

**bindService**

- bindService()는 서비스가 실행되면서 자신을 실행시킨 곳에 객체를 바인딩한다는 의미
- 아래 그림처럼 서비스의 객체를 액티비티에 바인딩시키면, 액티비티는 해당 객체의 메서드를 사용할 수 있게 된다. (메서드의 매개변수나 리턴값으로 컴포넌트 간의 상호 데이터 전달이 가능해짐

![image](https://github.com/overthename/AndroidStudy/assets/80188940/e2081ffd-2eaa-469a-9aa1-00f6ea5a4035)


- bindService() → onCreate(), onBind()
- unbindService() → onUnbind(), onDestroy()
- onCreate()는 서비스 객체 생성 시 최초에 한번만 실행되지만, onBind()는 여러 번 호출될 수 있다.

[https://seosh817.tistory.com/115#2. Service 종류-1](https://seosh817.tistory.com/115#2.%20Service%20%EC%A2%85%EB%A5%98-1)

https://velog.io/@jxlhe46/Android-Service

https://stickode.tistory.com/736

https://limkydev.tistory.com/43
