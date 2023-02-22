# 💡 Thread, Handler, Looper
백그라운드 처리라는 공통점이 있다.

<br/>

# ✅ Thread
- Thread란 프로세스 내에서 "순차적으로 실행되는 실행 흐름"의 최소 단위를 말한다.
- 프로그램의 main() 함수로부터 시작되는 최초 실행 흐름 또한 하나의 스레드이며, 이를 메인 스레드라고 부른다.

<br/>

## Android의 UI 동작
안드로이드의 UI 처리는 싱글 스레드 모델로 동작한다. 즉, 메인 스레드가 아닌 다른 스레드에서 UI를 업데이트하는 등의 행위를 하면 안 된다. 따라서 메인 스레드를 UI 스레드라고 부르기도 한다.

<br/>

### 왜 UI는 싱글 스레드 모델로 동작할까?
멀티 스레드 환경이라고 가정했을 때, 여러 스레드에서 TextView의 텍스트를 변경하는 상황이 발생하면 어떤 결과가 나타날지 미지수이기 때문이다.  
따라서 동작의 무결성을 보장하기 위해 타 스레드에서는 UI를 건드릴 수 없고, 오로지 메인 스레드에서만 UI 관련 동작을 할 수 있게끔 하는 것이다.

<br/>

어플리케이션은 성능 향상을 위해 멀티 스레드를 많이 사용하지만, UI를 업데이트 할 때는 단일 스레드 모델이 적용된다. 멀티 스레드로 UI를 업데이트 하면 동일한 UI 자원을 사용할 때 *교착 상태, *경합 상태 등 여러 문제가 발생할 수 있다. 따라서 UI 업데이트는 메인 스레드에서만 허용한다.

<br/>

* 교착상태(dead lock): 두 개 이상의 작업이 서로 상대방의 작업이 끝나기 만을 기다리고 있기 때문에 결과적으로 아무것도 완료되지 못하는 상태  
* 경합상태(race condition) : 두 개 이상의 프로세스가 공통 자원을 병행적으로 읽거나 쓸 때, 공용 데이터에 대한 접근이 어떤 순서에 따라 이루어졌는지에 따라 그 실행 결과가 달라지는 상황

<br/>

### 이러한 싱글 스레드 모델에서 지켜야 할 포인트들
1. 메인 스레드(UI 스레드)를 블로킹해서는 안 된다.    
    : 메인 스레드를 블로킹한다는 뜻은, 사용자에게 보여지는 UI 동작을 멈춘다는 뜻이다. 메인 스레드가 블로킹되어 UI 동작이 멈추게 되면, 이는 표면적으로 앱 퍼포먼스 저하를 유발하게 되며 사용자 경험상 악영향을 끼친다. 따라서 시간이 오래 걸리는 동작을 수행하는 등 메인 스레드를 블로킹해선 안 된다.    
2. UI 관련 동작은 오로지 메인 스레드에서만 접근해야 한다.    
    : 이유는 위에서 설명했다. UI 동작의 무결성을 보장하기 위함이다.
    
<br/>

### 시간이 오래 걸리는 무거운 동작들은 따로 돌린다.
즉, 무거운 동작들은 메인 스레드가 아닌 다른 스레드를 생성하여 수행해야 한다. 그런데 어차피 스레드를 별도로 생성하여 시간이 오래 걸리는 동작들을 한다고 해도 그 동작의 '결과' 는 보통 UI를 업데이트하는 데에 사용된다.

<br/>

> 예 :  
스레드를 새로 생성하여, 고양이 사진을 제공해주는 서버의 API를 호출하여 고양이 사진을 받은 뒤 ImageView에 보여주는 동작을 한다고 한다.  
그런데 아까 별도의 스레드에선 UI 관련 동작을 해서는 안 된다고 했다. 그럼 결과로 받은 고양이 사진을 어떻게 사용자에게 보여줄 수 있을까?  
가장 먼저 떠오르는 방법은, 다른 스레드에서 메인 스레드로 결과를 전송하는 방식이다. 즉, 스레드 간의 통신을 구현하는 것이다.
> 

<br/>

안드로이드에선 스레드간의 통신을 위해, Looper와 Handler라는 장치를 제공해 준다. 이것들을 활용하여 효율적으로 멀티 스레딩 환경을 구축할 수 있다.

<br/>

## Thread를 사용하는 이유?
메인 스레드 만으로 구현하게 된다면, 사용자는 해당 작업이 끝날 때까지 멈춰 있는 화면을 보고만 있어야 한다. 오랜 시간 동안 UI 관련 작업이 처리되지 못하면 결국 *ANR 에러가 발생한다. 그러면 어플리케이션은 정지된다.

<br/>

안드로이드 3.0 버전부터 통신 클래스 내 전송이나 수신과 관련된 메소드는 메인 스레드에서 사용하지 못하도록 의도적으로 막아버렸다.  
ex : 메인 스레드에서 소켓 클래스의 conntect() 메소드를 호출하면 'NetworkOnMainThreadException'이 발생한다.

<br/>

위와 같은 네트워크 통신 기능이나 데이터 검색, 빈번하게 사용하는 파일의 로드과 같이 시간이 걸리는 작업들은 사용자가 기다리지 않도록 하기 위하여 여분의 스레드를 사용해야 한다. (멀티 스레드)

<br/>

안드로이드 앱을 제대로 개발하기 위해서는 멀티 스레드를 이용하는 것은 필수적이라 할 수 있다.

<br/>

* ANR : 안드로이드에서는 어떤 작업을 요청하고 5초간의 응답이 없을 때 강제 종료 여부를 묻는 다이얼로그를 발생시킨다. 이 다이얼로그를 ANR(Application Not Responding) 메시지라고 한다.

<br/>

## Thread 구현
스레드를 구현하는 방법은 2가지가 있다. 하나는 Thread를 이용하는 것이고, 나머지 하나는 Runnable을 이용하는 것이다.

<br/>

### Thread를 상속받아 구현하기

```java
public class SHThread extends Thread {
    @Override
    public void run() {
        super.run();
        // Do something..
    }
}
```

```java
// 스레드 실행
SHThread thread = new SHThread();
thread.start();
```

<br/>

### Runnable 인터페이스 구현
Runnable 인터페이스를 상속받은 후, run() 메소드에 원하는 작업을 하도록 구현하면 된다.  
완성된 클래스를 생성한 후, Thread 클래스의 생성자에 인수로 전달한다.

```java
public class SHRunnable implements Runnable {
    @Override
    public void run() {
        // Do something,, 
    }
}
```

```java
// 사용하기 
SHRunnable myRunnable = new SHRunnable();
Thread thread = new Thread(myRunnable);
thread.start();
```

<br/>

### Thread와 Runnable 차이점
1. Thread는 상속(Extends)을 받는 것이며 Runnable은 인터페이스로서 구현하는 것이 큰 차이점이다.    
    : 자바는 다중 상속이 불가능하기 때문에 Thread를 상속받게 된 클래스는 다른 클래스를 상속받을 수가 없지만, Runnable은 인터페이스이기 때문에 implements만 하면 되고 다른 필요한 클래스를 상속받을 수 있다.    
2. Thread는 재사용 불가능, Runnable 가능    
    : 스레드는 일회용이다. 따라서 한 번 사용한 스레드는 재사용할 수 없다. 재사용시 'IllegalThreadStateException' 이 발생한다. 즉, 하나의 스레드에 대해 start()가 한 번만 호출될 수 있다. 하지만 Runnable로 구현한 경우 재사용 가능하다.
    
<br/>
<br/>

# ✅ Handler
Handler는 Looper로부터 받은 Message를 실행, 처리하거나 다른 스레드로부터 메시지를 받아서 Message Queue에 넣는 역할을 하는 스레드 간의 통신 장치이다.

<br/>

핸들러는 두 종류의 객체를 **메시지 큐(Message Queue)**를 통해 특정 스레드로 전달한다.
- 문자와 필드로 구성된 메시지 객체
- Runnable 객체

<br/>

메시지 큐는 하나의 프로세스 내 서브 스레드가 다른 프로세스 내 존재하는 스레드에 메시지를 전달하는 기능을 한다.  
핸들러는 반드시 메시지 큐가 제공되는 스레드에서 생성해야 한다. 메인 스레드는 기본으로 메시지 큐를 제공한다.

<br/>

## Handler 사용 목적
핸들러는 일반적으로 UI 갱신을 위해 사용된다.

<br/>

1. 메소드가 단일 스레드 모델일 때, Thread-Safe로 만들기 위해    
    : 아래의 코드를 실행시키면 'CalledFromWrongThreadException'이라는 예외가 발생한다. 이것은 뷰 클래스에서 제공하는 메소드(여기서는 setText())를 메인 스레드(UI 스레드)가 아닌 서브 스레드에서 실행 시켰기 때문이다.    
    뷰나 뷰 그룹에서 제공하는 메소드는 단일 스레드 모델(Thread-Unsafe)이기 때문에 메인 스레드에서 호출해야 한다.
    
    ```java
    public class SHThread extends Thread {
        @Override
        public void run() {
            super.run();
            textView.setText("상희");  // Error!!
        }
    }
    ```
    
    이러한 문제를 해결하기 위해 **자바는 동기화(Synchronized)라는 기능을 제공**하지만, 안드로이드는 핸들러를 제공한다.    
    스레드에서 네트워크 등의 작업들을 하는 도중에 UI를 업데이트 할 때 핸들러를 사용한다.
    
<br/>

2. 하나의 프로세스에서 다른 프로세스의 핸들러에 메시지를 전송하여 작업을 요청할 때    
    : 독립적으로 실행되는 스레드 사이에 정보를 주고받는 수단으로 메시지 큐와 핸들러를 채택했다. 만약 일반 스레드 사이에서 필요한 정보를 주고 받으려면 Looper를 사용해야 한다.
    
<br/>

## Handler 구현

```java
package com.example.sh.threadex;

import android.os.Handler;
import android.os.Message;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.widget.Button;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity{
    TextView timeTv;
    Button startBtn;

    Runnable timeRunnable;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        timeTv = (TextView) findViewById(R.id.timeTv);
        startBtn = (Button) findViewById(R.id.startBtn);

        startBtn.setOnClickListener(v -> {
            // Runnable 객체를 매개변수로 Thread 생성
            Thread timeThread = new Thread(timeRunnable);   
            timeThread.start();  // Thread Start
        });

        timeRunnable = new Runnable() {
            @Override
            public void run() {
                int time = 0;
                while(true) {
                    Message msg = new Message();
                    msg.what = 0;
                    msg.arg1 = time;
                    handler.sendMessage(msg);    // Handler에 Message 보냄 

                    try {
                        Thread.sleep(1000);
                        time++;
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
            }
        };
    }

    Handler handler = new Handler(){
        @Override
        public void handleMessage(Message msg) {    
            super.handleMessage(msg);
            if(msg.what == 0){   
                timeTv.setText(String.valueOf(msg.arg1));
            }
        }
    };
}
```

<br/>
<br/>

# ✅ Looper
Looper는 무한히 루프를 돌며 자신히 속한 스레드의 Message Queue에서 Message나 Runnable 객체를 차례로 꺼내 Handler가 처리하도록 전달한다.  
Looper는 스레드당 하나씩밖에 가질 수 없고, Looper는 Message Queue가 비어 있는 동안 아무 행동도 하지 않고, 메시지가 들어오면 해당 메시지를 꺼내 적절한 Handler로 전달한다. 메인 스레드에는 Looper가 기본적으로 생성되어 있지만, 기본적으로 새로 생성한 스레드는 Looper를 가지지 않고 있기 때문에 메시지를 받을 수 없다. 사용할 수 있는 메시지 큐가 없기 때문이다. 서브 스레드에서 메시지를 전달받기 위해서는 Looper를 생성해 줘야 한다. Looper.prepare() 메서드를 호출해야지 Looper가 생성이 된다.

<br/>

> Message는 '하나의 작은 작업 단위'라고 생각하면 편하다. MessageQueue에는 이러한 작은 작업 단위를 하나씩 적재해두고, Looper가 이를 차례대로 처리하는 것이다.
> 

> Message 객체는 내용물이 두 가지 종류로 이루어진다. Runnable 객체로 이루어져 있을 수도 있고, 일반적인 경우 Message 객체로 이루어져 있을 수도 있다. 
Looper 객체가 메시지 큐에서 메시지를 하나 딱 까봤을 때, Runnable 객체가 담겨 있으면 Handler에 메세지를 전달하지 않고 run()을 수행하여 해당 Runnble 작업을 바로 시작한다.
Runnable 객체가 없을 경우, Message 객체 내부에 명시돼있는 Handler의 handleMessage()를 수행하여 처리한다.
> 

<br/>

## Looper 특징
- 루퍼 클래스는 생성자를 사용하여 인스턴스를 만들어 사용하는 것이 아니라 정적 메소드를 사용한다.

```java
public final class Looper {
    ... ...
    // Looper 클래스의 prepare(), loop() 등의 메소드들은 정적 메소드로 되어있다. 
	public static void prepare() {
 	   prepare(true);
	}
	public static void loop() {
	 	......       
	}
  
    ... ... 
}
```

```java
// 그래서 객체를 생성하지 않아도 바로 사용할 수 있다. 
Looper.prepare();
Looper.loop();
```

<br/>

- 루퍼는 핸들러를 사용할 수 있도록 메시지 큐와 연결시켜 준다.
    
    Looper.prepare(); 했을 때 실행되는 순서
    
```java
    public static void prepare() {
        prepare(true);
    }

    private static void prepare(boolean quitAllowed) {
        if (sThreadLocal.get() != null) {
            throw new RuntimeException("Only one Looper may be created per thread");
        }
        sThreadLocal.set(new Looper(quitAllowed));
    }
```

```java
    // prepare(boolean quitAllowed) 메소드에서 new Looper()
    private Looper(boolean quitAllowed) {
        mQueue = new MessageQueue(quitAllowed);   // MessageQueue 여기서 생성
        mThread = Thread.currentThread();   
    }
```

<br/>

## Looper 구현
루퍼는 클래스를 인스턴스화하고 객체 내 메소드를 호출하는 일반적인 자바 프로그램과 다르게  
루퍼 초기화 → 핸들러 생성 → 루퍼 실행 이라는 3단계로 작업을 수행한다.

```java
public class LooperEx extends Thread {
    public Handler handler;

    @Override
    public void run() {
        Looper.prepare();   // Looper 객체를 생성하고 메시지 큐를 초기화
        
        handler = new Handler(){    // 핸들러 객체 생성
            @Override
            public void handleMessage(Message msg) {
                // 메시지 처리 
            }
        };
      
        // 스레드 내 핸들러에 메시지를 전달. 스레드가 종료되지 않도록 내부적으로 메시지를 기다리는 기능.
        Looper.loop();   
    }
}
```

<br/>
<br/>

# 🗂 참고
- [안드로이드 기술 면접에 좋을 자료 (tistory.com)](https://bbul-jit.tistory.com/23)
- [[Android] Looper & Handler 기초 개념 (velog.io)](https://velog.io/@haero_kim/Android-Looper-Handler-%EA%B8%B0%EC%B4%88-%EA%B0%9C%EB%85%90)
- [Android-Study/Thread , Handler , Looper.md at master · taeiim/Android-Study (github.com)](https://github.com/taeiim/Android-Study/blob/master/study/week01/Thread%20%2C%20Handler%20%2C%20Looper.md)
- [핸들러와 루퍼(Handler & Looper) | Jungwoon Blog](https://jungwoon.github.io/android/2019/09/25/Handler-Looper.html)
