# 💡 Service

# ✅ Service

## Started Service(Unbound Service) 생성
Started Service란 다른 구성 요소가 startService()를 호출하여 시작하고, 그 결과로 서비스의 onStartCommand() 메서드가 호출되는 경우를 말한다.  
서비스가 시작되면 이를 시작한 구성 요소와 독립적인 수명 주기를 가지게 된다.  
서비스는 백그라운드에서 무한히 실행될 수 있으며, 이는 해당 서비스를 시작한 구성 요소가 소멸되었더라도 무관하다.  
따라서 서비스는 작업이 완료되면 stopSelf()를 호출하여 스스로 중단하거나 다른 구성 요소가 stopService()를 호출하여 중단시킬 수도 있다.  
애플리케이션 구성 요소(예: 액티비티)가 서비스를 시작하려면 startService()를 호출하고, Intent를 전달하면 됩니다. 인텐트에서 서비스를 지정하고 이 서비스가 사용할 모든 데이터를 포함한다.  
서비스는 onStartCommand() 메서드에서 이 Intent를 받는다.  
예를 들어 어느 액티비티가 온라인 데이터베이스에 어떤 데이터를 저장해야 한다고 가정한다.  
액티비티가 Companion Service를 시작하고, 인텐트를 startService()에 전달하여 서비스에 저장할 데이터를 전달할 수 있다.  
서비스는 이 인텐트를 onStartCommand()에서 수신하고, 인터넷에 연결한 다음, 데이터베이스 트랜잭션을 수행한다.  
트랜잭션이 완료되면 서비스가 스스로 중단되어 소멸된다.

> 주의 : 서비스는 기본적으로 자신이 선언된 애플리케이션의 같은 프로세스에서 실행되기도 하고, 해당 애플리케이션의 기본 스레드에서 실행되기도 한다. 
따라서 사용자가 같은 애플리케이션의 액티비티와 상호 작용하는 동안 서비스가 집약적이거나 차단 작업을 수행하는 경우, 해당 서비스 때문에 액티비티 성능이 느려지게 된다. 
애플리케이션 성능에 영향을 미치는 것을 방지하려면, 서비스 내에서 새 스레드를 시작해야 한다.
> 

<br/>

Started Service를 생성하기 위해 확장할 수 있는 클래스가 2 개 있다.  
- Service
    - 모든 서비스의 기본 클래스이다.
    - 이 클래스를 확장할 때는 서비스가 모든 작업을 완료할 수 있는 새 스레드를 생성하는 것이 중요하다.
    - 서비스는 기본적으로 애플리케이션의 기본 스레드를 사용하기 때문에 애플리케이션이 실행 중인 액티비티의 성능을 저하시킬 수 있다.
- IntentService
    - Service의 하위 클래스로, 작업자 스레드를 사용하여 모든 시작 요청을 처리하되 한 번에 하나씩 처리한다.
    - 서비스가 여러 개의 요청을 동시에 처리하지 않아도 되는 경우에는 최선의 옵션이다.
    - onHandleIntent()를 구현한다. 이는 각 시작 요청에 대해 인텐트를 수신해서 백그라운드 작업을 완료하도록 합니다.

<br/>

### IntentService 클래스 확장
대부분의 시작된 서비스는 여러 개의 요청을 동시에 처리하지 않아도 되기 때문에(이는 사실 위험한 다중 스레딩 시나리오일 수 있다.), 서비스를 구현할 때에는 IntentService 클래스를 사용하는 것이 최선일 것이다.

<br/>

IntentService 클래스는 다음과 같이 작동한다.  
- 애플리케이션의 기본 스레드와는 별도로, onStartCommand()에 전달된 모든 인텐트를 실행하는 기본 작업자 스레드를 생성한다.
- 인텐트를 한 번에 하나씩 onHandleIntent() 구현에 전달하는 작업 큐를 생성하므로, 다중 스레딩에 대해 염려할 필요가 전혀 없다.
- 시작 요청이 모두 처리된 후 서비스를 중단하므로 개발자가 stopSelf()를 호출할 필요가 전혀 없다.
- onBind()의 기본 구현을 제공하여 null을 반환하도록 한다.
- onStartCommand()의 기본 구현을 제공하여, 인텐트를 작업 큐로 보내고 그다음은 onHandleIntent() 구현으로 보낸다.

<br/>

클라이언트가 제공한 작업을 완료하기 위해 onHandleIntent()를 구현한다.  
다만, 서비스에 대해 작은 생성자를 제공해야 하기도 한다.

<br/>

다음 코드는 IntentService 구현의 예이다.

```kotlin
/**
 * A constructor is required, and must call the super [android.app.IntentService.IntentService]
 * constructor with a name for the worker thread.
 */
class HelloIntentService : IntentService("HelloIntentService") {

    /**
     * The IntentService calls this method from the default worker thread with
     * the intent that started the service. When this method returns, IntentService
     * stops the service, as appropriate.
     */
    override fun onHandleIntent(intent: Intent?) {
        // Normally we would do some work here, like download a file.
        // For our sample, we just sleep for 5 seconds.
        try {
            Thread.sleep(5000)
        } catch (e: InterruptedException) {
            // Restore interrupt status.
            Thread.currentThread().interrupt()
        }

    }
}
```

<br/>

필요한 것은 이게 전부이다. 생성자 하나와 onHandleIntent()만 구현하면 된다.  
다른 콜백 메서드도 재정의하려면(예: onCreate(), onStartCommand() 또는 onDestroy()) 슈퍼 구현을 꼭 호출해야 한다. 그래야만 IntentService가 작업자 스레드의 수명을 적절하게 처리할 수 있다.  
예를 들어 onStartCommand()는 반드시 기본 구현을 반환해야 한다. (그래야 인텐트가 onHandleIntent()로 전달된다.)

<br/>

```kotlin
override fun onStartCommand(intent: Intent?, flags: Int, startId: Int): Int {
    Toast.makeText(this, "service starting", Toast.LENGTH_SHORT).show()
    return super.onStartCommand(intent, flags, startId)
}
```

<br/>

onHandleIntent() 외에 슈퍼 클래스를 호출하지 않아도 되는 메서드는 onBind() 뿐이다. 이것은 서비스가 바인드를 허용하는 경우에만 구현해야 한다.  
다음 섹션에서는 기본 Service 클래스를 확장할 때 같은 종류의 서비스를 구현하는 방법을 배우게 된다. 이때에는 코드가 더 많이 필요하지만, 동시 시작 요청을 처리해야 하는 경우에 적합할 수 있다.

<br/>

### 서비스 클래스 확장
IntentService를 사용하면 시작된 서비스 구현이 매우 단순해진다.  
하지만 서비스가 멀티스레딩을 수행해야 하는 경우(작업 큐를 통해 시작 요청을 처리하는 대신), 그때는 Service 클래스를 확장하여 각 인텐트를 처리하게 할 수 있다.  
비교를 위해 다음 예시 코드에서는 이전 예시에서 IntentService를 사용해서 수행한 작업과 같은 작업을 수행하는 Service 클래스 구현을 나타내었다.  
바꿔 말하면 각 시작 요청에 대해 작업자 스레드를 사용하여 작업을 수행하고 한 번에 요청을 하나씩만 처리한다는 뜻이다.

<br/>

```kotlin
class HelloService : Service() {

    private var serviceLooper: Looper? = null
    private var serviceHandler: ServiceHandler? = null

    // Handler that receives messages from the thread
    private inner class ServiceHandler(looper: Looper) : Handler(looper) {

        override fun handleMessage(msg: Message) {
            // Normally we would do some work here, like download a file.
            // For our sample, we just sleep for 5 seconds.
            try {
                Thread.sleep(5000)
            } catch (e: InterruptedException) {
                // Restore interrupt status.
                Thread.currentThread().interrupt()
            }

            // Stop the service using the startId, so that we don't stop
            // the service in the middle of handling another job
            stopSelf(msg.arg1)
        }
    }

    override fun onCreate() {
        // Start up the thread running the service.  Note that we create a
        // separate thread because the service normally runs in the process's
        // main thread, which we don't want to block.  We also make it
        // background priority so CPU-intensive work will not disrupt our UI.
        HandlerThread("ServiceStartArguments", Process.THREAD_PRIORITY_BACKGROUND).apply {
            start()

            // Get the HandlerThread's Looper and use it for our Handler
            serviceLooper = looper
            serviceHandler = ServiceHandler(looper)
        }
    }

    override fun onStartCommand(intent: Intent, flags: Int, startId: Int): Int {
        Toast.makeText(this, "service starting", Toast.LENGTH_SHORT).show()

        // For each start request, send a message to start a job and deliver the
        // start ID so we know which request we're stopping when we finish the job
        serviceHandler?.obtainMessage()?.also { msg ->
            msg.arg1 = startId
            serviceHandler?.sendMessage(msg)
        }

        // If we get killed, after returning from here, restart
        return START_STICKY
    }

    override fun onBind(intent: Intent): IBinder? {
        // We don't provide binding, so return null
        return null
    }

    override fun onDestroy() {
        Toast.makeText(this, "service done", Toast.LENGTH_SHORT).show()
    }
}
```

<br/>

IntentService를 사용할 때보다 훨씬 손이 많이 간다.  
그러나 각 호출을 onStartCommand()로 직접 처리할 수 있기 때문에 여러 개의 요청을 동시에 수행할 수 있다.  
이 예시는 그 작업을 보여주는 것은 아니지만, 그런 작업을 원하는 경우 각 요청에 대해 새 스레드를 하나씩 생성한 다음 곧바로 실행하면 된다. (이전 요청이 끝날 때까지 기다리는 대신)

<br/>

onStartCommand() 메서드가 반드시 정수를 반환해야 한다는 사실을 유의해야 한다.  
이 정수는 시스템이 서비스를 종료할 경우 서비스를 유지하는 방법을 설명하는 값이다.  
IntentService에 대한 기본 구현이 이 작업을 자동으로 처리해주지만, 수정할 수는 있어야 한다.  
onStartCommand()로부터의 반환 값은 반드시 다음 상수 중 하나여야 한다.

<br/>

- START_NOT_STICKY  
  : 시스템이 서비스를 onStartCommand() 반환 후에 중단시키면 서비스를 재생성하면 안 된다. 다만 전달할 보류 인텐트가 있는 경우는 예외이다. 이는 서비스가 불필요하게 실행되는 일을 피할 수 있는 가장 안전한 옵션이며, 애플리케이션이 완료되지 않은 모든 작업을 단순히 다시 시작할 수 있을 때 유용하다.
- START_STICKY  
  : 시스템이 onStartCommand() 반환 후에 서비스를 중단하면 서비스를 다시 생성하고 onStartCommand()를 호출하되 마지막 인텐트는 전달하지 않는다. 그 대신 시스템이 null 인텐트로 onStartCommand()를 호출한다. 단, 서비스를 시작하기 위한 보류 인텐트가 있는 경우는 예외이다. 이 경우에는 그러한 인텐트가 전달된다. 이것은 명령을 실행하지는 않지만, 무한히 실행 중이며 작업을 기다리고 있는 미디어 플레이어(또는 그와 비슷한 서비스)에 적합하다.
- START_REDELIVER_INTENT  
  : 시스템이 onStartCommand() 반환 후에 서비스를 중단하는 경우, 서비스를 다시 생성하고 이 서비스에 전달된 마지막 인텐트로 onStartCommand()를 호출하면 된다. 모든 보류 인텐트가 차례로 전달된다. 이것은 즉시 재개되어야 하는 작업을 능동적으로 수행 중인 서비스(예: 파일 다운로드 등)에 적합하다.

<br/>

### 서비스 시작
액티비티 또는 다른 구성 요소에서 서비스를 시작하려면 Intent(시작할 서비스를 지정)를 startService() 또는 startForegroundService()에 전달하면 된다.  
Android 시스템이 서비스의 onStartCommand() 메서드를 호출하고 여기에 시작할 서비스를 지정하는 Intent를 전달한다.

<br/>

> 참고 : 앱이 API 레벨 26 이상을 대상으로 한다면 앱이 포그라운드에 있지 않을 때 시스템에서 백그라운드 서비스 사용하거나 생성하는 것에 제한을 적용한다. 
앱이 포그라운드 서비스를 생성해야 하는 경우, 해당 앱은 startForegroundService()를 호출해야 한다. 
이 메서드는 백그라운드 서비스를 생성하지만, 메서드가 시스템에 신호를 보내 서비스가 자체적으로 포그라운드로 승격될 것이라고 알린다. 
서비스가 생성되면 5초 이내에 startForeground() 메서드를 호출해야 한다.
> 

<br/>

예를 들어, 아래에서 볼 수 있듯이 이전 섹션의 예시 서비스(HelloService)를 액티비티가 시작하려면 startService()로 명시적 인텐트를 사용하면 된다.

```kotlin
Intent(this, HelloService::class.java).also { intent ->
    startService(intent)
}
```

<br/>

startService() 메서드가 즉시 반환되며 Android 시스템이 서비스의 onStartCommand() 메서드를 호출한다.  
서비스가 아직 실행되지 않고 있다면 먼저 onCreate()를 호출한 다음, onStartCommand()를 호출해야 한다.

<br/>

서비스가 바인딩도 제공하지 않는 경우, startService()와 함께 전달된 인텐트가 애플리케이션 구성 요소와 서비스 사이의 유일한 통신 수단이다.  
그러나 서비스가 결과를 돌려보내기를 원하는 경우, 서비스를 시작한 클라이언트가 브로드캐스트를 위해 PendingIntent를 만들고(getBroadcast() 사용) 이를 서비스를 시작한 Intent의 서비스에 전달할 수 있다. 

<br/>

그러면 서비스가 이 브로드캐스트를 사용하여 결과를 전달할 수 있게 된다.  
서비스를 시작하기 위한 요청을 여러 개 보내면 그에 대응하여 서비스의 onStartCommand()에 대해 여러 번 호출이 발생한다.  
하지만 서비스를 중단하려면 한 번만 중단을 요청하면 된다. (stopSelf() 또는 stopService())

<br/>

### 서비스 중단
시작된 서비스는 자신의 수명 주기를 직접 관리해야 한다.  
다시 말해, 시스템이 서비스를 중단하거나 소멸시키지 않는다는 뜻이다.  
다만 시스템 메모리를 회복해야 하고 서비스가 onStartCommand() 반환 후에도 계속 실행되는 경우는 예외이다.  
서비스는 stopSelf()를 호출하여 스스로 중지하고 하고, 아니면 다른 구성 요소가 stopService()를 호출하여 이를 중지시킬 수 있다.

<br/>

일단 stopSelf() 또는 stopService()로 중단 요청을 보내면 시스템은 가능한 한 빨리 서비스를 소멸시킨다.  

<br/>

서비스가 onStartCommand()에 대한 여러 요청을 동시에 처리하는 경우에는, 시작 요청의 처리를 끝낸 뒤에도 서비스를 중단하면 안 된다.  
그 이후 새 시작 요청을 받았을 수 있기 때문이다. (첫 요청이 끝날 때 중단하면 두 번째 요청이 종료될 수 있다.)  
이 문제를 피하려면, stopSelf(int)를 사용하여 서비스 중단 요청이 항상 가장 최근 시작 요청을 기준으로 하도록 해야 한다.  
다시 말해, stopSelf(int)를 호출할 경우 시작 요청의 ID(onStartCommand()에 전달된 startId)를 전달하며, 여기에 중단 요청이 대응된다.  
그런 다음 stopSelf(int)를 호출할 수 있게 되기 전에 서비스가 새 시작 요청을 수신하면 ID가 일치하지 않으므로 서비스는 중단되지 않는다.

<br/>

> 주의 : 시스템 리소스 낭비를 피하고 배터리 전력 소모를 줄이기 위해 서비스의 작업이 완료되면 애플리케이션에서 서비스를 중단해야 한다. 
필요한 경우 stopService()를 호출하여 다른 구성 요소가 서비스를 중단할 수 있다. 
서비스에 대해 바인딩을 활성화하더라도 서비스가 onStartCommand()에 대한 호출을 한 번이라도 받았으면 항상 직접 서비스를 중단해야 한다.
> 

<br/>

## Bound Service 생성
바인딩된 서비스는 bindService()를 호출하여 애플리케이션 구성 요소를 서비스에 바인딩하고 오래 유지되는 연결을 설정하는 것이다.  
일반적으로는 startService()를 호출하더라도 구성 요소가 서비스를 시작하도록 허용하지 않는다.

<br/>

액티비티와 애플리케이션의 다른 구성 요소에서 서비스와 상호 작용하기를 원하는 경우 바인딩된 서비스를 생성해야 한다.  
아니면 애플리케이션의 기능 몇 가지를 프로세스 간 통신(IPC)을 통해 다른 애플리케이션에 노출하고자 하는 경우에도 좋다.

<br/>

바인딩된 서비스를 생성하려면 onBind() 콜백 메서드를 구현하여 서비스와의 통신을 위한 인터페이스를 정의하는 IBinder를 반환하도록 해야 한다.  
그러면 다른 애플리케이션 구성 요소가 bindService()를 호출하여 해당 인터페이스를 검색하고, 서비스에 있는 메서드를 호출하기 시작할 수 있다.  
서비스는 자신에게 바인딩된 애플리케이션 구성 요소에 도움이 되기 위해서만 존재하는 것이므로 서비스에 바인딩된 구성 요소가 없으면 시스템이 이를 소멸시킨다.  
바인딩된 서비스는 서비스를 onStartCommand()를 통해 시작했을 때와 같은 방식으로 중단하지 않아도 된다.

<br/>

바인딩된 서비스를 생성하려면 클라이언트가 서비스와 통신할 수 있는 방법을 나타내는 인터페이스를 정의해야 한다.  
서비스와 클라이언트 사이에서 쓰이는 이 인터페이스는 반드시 IBinder의 구현이어야 하며 이를 서비스가 onBind() 콜백 메서드에서 반환해야 한다.  
클라이언트가 IBinder를 수신하면 해당 인터페이스를 통해 서비스와 상호작용을 시작할 수 있다.  

<br/>

여러 클라이언트가 서비스에 한꺼번에 바인딩될 수 있다.  
클라이언트가 서비스와의 상호작용을 완료하면 이는 unbindService()를 호출하여 바인딩을 해제한다.  
서비스에 바인딩된 클라이언트가 하나도 없으면 시스템이 해당 서비스를 소멸시킨다.

<br/>

바인딩된 서비스를 구현하는 데에는 여러 가지 방법이 있으며 그러한 구현은 시작된 서비스보다 훨씬 복잡하다. 

<br/>

## 사용자에게 알림 전송
- 서비스가 실행되고 있을 때 사용자에게 토스트 알림 또는 상태 표시줄 알림 등을 사용해 이벤트를 알릴 수 있다.
    - 토스트 알림은 현재 창의 표면에 잠깐 나타났다가 사라지는 메시지이다.
- 상태 표시줄 알림은 상태 표시줄에 메시지가 담긴 아이콘을 제공하여 사용자가 이를 선택하여 조치를 취할 수 있게 하는 것이다.
    - 예 : 액티비티 시작
- 일반적으로 상태 표시줄 알림은 파일 다운로드와 같은 백그라운드 작업이 완료되고 사용자가 작업을 수행할 수 있는 경우 사용하는 가장 좋은 기술이다.
- 사용자가 확장된 뷰의 알림을 선택하면, 해당 알림이 액티비티를 시작할 수 있다.
    - 예 : 다운로드한 파일 보기

<br/>

자세한 내용은 [알림 메시지](https://developer.android.com/guide/topics/ui/notifiers/toasts?hl=ko) 또는 [상태 표시줄 알림](https://developer.android.com/guide/topics/ui/notifiers/notifications?hl=ko) 개발자 가이드를 참조하면 된다.

<br/>

## 사용자 수명 주기 관리
서비스의 수명 주기는 액티비티의 수명 주기보다 훨씬 간단하다.  
하지만 서비스를 생성하고 소멸하는 방법에 특히 주의를 기울여야 한다는 면에서 중요도는 이쪽이 더 높다.  
서비스는 사용자가 모르는 채로 백그라운드에서 실행될 수 있기 때문이다.

<br/>

서비스 생명 주기(생성된 시점부터 소멸되는 시점까지)는 두 가지 서로 다른 경로를 따를 수 있다.  
- Started Service(시작된 서비스)
    - 다른 구성 요소가 `startService()`를 호출하면 서비스가 생성된다.
    - 그러면 서비스가 무기한으로 실행될 수 있으며, `stopSelf()`를 호출하여 자체적으로 중단해야 한다.
    - 다른 구성 요소도 `stopService()`를 호출하면 서비스를 중단시킬 수 있다. 서비스가 중단되면 시스템이 이를 소멸시킨다.
- Bound Service(바인딩된 서비스)
    - 다른 구성 요소(클라이언트)가 `bindService()`를 호출하면 서비스가 생성된다.
    - 그러면 클라이언트가 `IBinder`  인터페이스를 통해 서비스와 통신을 주고받을 수 있다.
    - 클라이언트가 연결을 종료하려면 `unbindService()`를 호출하면 된다.
    - 여러 클라이언트가 같은 서비스에 바인딩될 수 있으며, 모든 클라이언트가 바인딩을 해제하면 시스템이 해당 서비스를 소멸시킨다. 서비스가 스스로 중단하지 않아도 된다.

<br/>

이 두 가지는 완전히 별개는 아니다.  
이미 `startService()`로 시작된 서비스에 바인딩할 수도 있다.  
예를 들어 재생할 음악을 식별하는 `Intent`를 포함해 `startService()`를 호출하면 백그라운드 음악 서비스를 시작할 수 있다.  
나중에 아마도 사용자가 플레이어에 좀 더 많은 통제력을 발휘하려고 하거나 현재 노래에 대한 정보를 얻고자 할 때, 액티비티가 `bindService()`를 호출하여 서비스에 바인딩할 수 있다.  
이와 같은 경우에는 모든 클라이언트가 바인딩을 해제할 때까지 `stopService()`  또는 `stopSelf()`가 서비스를 중단하지 않는다.

<br/>

### Lifecycle callbacks 구현
액티비티와 마찬가지로 서비스에도 수명 주기 콜백 메서드가 있어, 이를 구현하면 서비스의 상태 변경 내용을 모니터할 수 있고 적절한 시기에 작업을 수행할 수 있다.  
다음의 기본 서비스는 각 수명 주기 메서드를 보여 준다.

```kotlin
class ExampleService : Service() {
    private var startMode: Int = 0             // indicates how to behave if the service is killed
    private var binder: IBinder? = null        // interface for clients that bind
    private var allowRebind: Boolean = false   // indicates whether onRebind should be used

    override fun onCreate() {
        // The service is being created
    }

    override fun onStartCommand(intent: Intent?, flags: Int, startId: Int): Int {
        // The service is starting, due to a call to startService()
        return mStartMode
    }

    override fun onBind(intent: Intent): IBinder? {
        // A client is binding to the service with bindService()
        return mBinder
    }

    override fun onUnbind(intent: Intent): Boolean {
        // All clients have unbound with unbindService()
        return mAllowRebind
    }

    override fun onRebind(intent: Intent) {
        // A client is binding to the service with bindService(),
        // after onUnbind() has already been called
    }

    override fun onDestroy() {
        // The service is no longer used and is being destroyed
    }
}
```

> 참고 : 액티비티 생명 주기 콜백 메서드와는 달리 이와 같은 콜백 메서드를 구현하는 데 superclass 구현을 호출하지 않아도 된다.
> 

<br/>

- 아래 그림은 서비스의 생명 주기이다.
    - 왼쪽의 다이어그램은 서비스가 startService()로 생성된 경우의 생명 주기를 나타낸다.
    - 오른쪽의 다이어그램은 서비스가 bindService()로 생성된 경우의 생명 주기를 나타낸다.

<br/>

![Untitled](https://developer.android.com/static/images/service_lifecycle.png?hl=ko)

<br/>

위의 그림은 서비스에 대한 일반적인 콜백 메서드를 나타낸 것이다.  
이 그림에서는 startService()로 생성된 서비스와 bindService()로 생성된 서비스를 구분하고 있지만, 어떤 식으로 시작되었든 모든 서비스는 클라이언트와 바인딩되도록 허용할 수 있다는 점을 명심해야 한다.  
onStartCommand()로 처음 시작된 서비스(클라이언트가 startService()호출하는 경우)라고 해도 여전히 onBind()에 대한 호출을 받을 수 있다. (클라이언트가 bindService()를 호출하는 경우)  
이와 같은 메서드를 구현함으로써, 서비스 생명 주기의 두 가지 중첩된 루프를 모니터링할 수 있다.

- 서비스의 전체 수명은 onCreate()가 호출된 시점부터 onDestroy() 반환 시점까지이다. 
액티비티와 마찬가지로 서비스는 자신의 초기 설정을 onCreate()에서 수행하며, 남은 리소스를 모두 onDestroy()에서 릴리스한다. 
예를 들어 음악 재생 서비스는 스레드를 생성하고, 이 스레드의 onCreate()에서 음악이 재생된다. 그런 다음, onDestroy()에서 스레드를 중단할 수 있다.

> 참고 : onCreate() 및 onDestroy() 메서드는 모든 서비스에 대해 호출된다. 이는 서비스가 startService()로 생성되었든 bindService()로 생성되었든 상관없이 적용된다.
> 
- 서비스의 활성 수명은 onStartCommand() 또는 onBind()에 대한 호출에서부터 시작된다. 
각 메서드는 Intent를 받아서 startService() 또는 bindService()에 전달한다.
서비스가 시작되면 수명 주기 전체가 종료되는 것과 동시에 활성 수명 주기도 종료됩니다(서비스는 onStartCommand()가 반환된 뒤에도 여전히 활성 상태이다). 
서비스가 바인딩된 경우, onUnbind()가 반환되면 활성 수명 주기가 종료됩니다.

> 참고 : 시작된 서비스를 중단하려면 `stopSelf()`  또는 `stopService()`를 호출하면 되지만, 서비스에 대한 개별 콜백은 없다. (즉, `onStop()`  콜백이 없다.) 
그러므로 서비스가 클라이언트에 바인딩되어 있지 않은 한, 시스템은 서비스가 중단되면 이를 소멸시킨다. 수신되는 콜백은 `onDestroy()`가 유일하다.
> 

<br/>
<br/>

# 🗂 참고

- [서비스 개요  |  Android 개발자  |  Android Developers](https://developer.android.com/guide/components/services?hl=ko)
- [Services overview  |  Android Developers](https://developer.android.com/guide/components/services)
