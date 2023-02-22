# Thread

안드로이드 애플리케이션을 실행하면 메모리에 올라와 프로세스가 실행되고 자동으로 메인 스레드가 생성하고 실행하게 된다. main thread에서는 ui관련된 작업들을 처리하는데 main thread ㅣ외의 일반thread에서는 ui작업을 처리할 수 없도록 하였다

**Main Thread**

주로 ui작업, ui 스레드라고 불림 메인 스레드에서 ui작업이 아닌 시간이 오래 걸리는 작업을 하게 되면 ANR이 발생할 수도 있음 

안드로이드 컴포넌트의 생명주기 메소드와 그 내부 호출은 모두 main thread에서 처리

activity, bradcastreceiver,service,application이 처리

**일반 thread**

애플리케이션의 성능을 향상시키기 위한 thread생성, network작업, db쿼리 등 오래 걸리는 작업 처리

백그라운드에서 처리하는 작업들이 많아 백그라운드 thread라고 불림

***ANR(Application Not Response)**

애플리케이션이 더이상 반응하지 않는 상태 , main thread에서 너무 오래 걸리는 작업을 수행할 경우 발생 

# Looper

Message Queue를 관리하는 역할

message나 Runnable 객체를 하나씩 꺼내서 Handler에 전달한다

Looper클래스와 Message Queue로 인해 ui의 경쟁상태를 방지할 수 있다.

# Handler

Looper로 부터 처리되어야 할 Message들을 받아서 처리하는 역할과 다시 Message Queue에 Message를 전달하는 역할을 한다. handler를 통해 다른 thread에서 요청하는 메세지를 처리하고 다시 해당 thread에 메세지를 전달할 수도 있기 때문에 thread간의 통신을 담당

주요용도

1. 일반 스레드에서 ui업데이트 

일반스레드에서 네트워크 통신이나 db작업 시 ui업데이트가 필요한 경우 main thread의 handler를

1. 메인 스레드에서 다음 작업 예약
2. 반복 갱신
3. 시간 제한

1. 메시지는 다른 스레드에 속한 Message Queue에서 전달됩니다.
2. MessageQueue에 메시지를 넣을 땐 Handlerdㅢ sendMessage( )를 이용합니다.
3. Looper는 MessageQueue에서 Loop( )을 통해 반복적으로 처리할 메시지를 Handler에 전달합니다.
4. Handler는 handleMessage를 통해 메시지를 처리합니다.

[https://math-coding.tistory.com/240](https://math-coding.tistory.com/240)

[https://itmining.tistory.com/5](https://itmining.tistory.com/5)
