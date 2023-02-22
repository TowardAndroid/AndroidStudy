# 230222 Android 면접 준비

## Q1. ANR이 무엇인가요?
ANR은 Application Not Responding의 약자로, Android 앱의 UI 스레드가 너무 오랫동안 차단되면 'ANR(애플리케이션 응답 없음)' 오류가 나타나게 된다.  
앱이 포그라운드에 있으면 아래와 같이 시스템에서 사용자에게 다이얼로그를 표시한다.

<br/>

![https://developer.android.com/topic/performance/images/anr-example-framed.png?hl=ko](https://developer.android.com/topic/performance/images/anr-example-framed.png?hl=ko)

<br/>

안드로이드 프레임워크에서 ANR 관련한 내용은 com.android.server.am.ActivityManagerService에서 확인 할 수 있다.(ActivityManagerService는 system_server 프로세스에서 실행된다.)

```java
static final int BROADCAST_FG_TIMEOUT = 10 * 1000;
static final int BROADCAST_BG_TIMEOUT = 60 * 1000;
static final int KEY_DISPATCHING_TIMEOUT = 5 * 1000;
```

<br/>

### ANR이 발생하는 경우
- 화면 터치와 키 입력에서 ANR
    - 메인 스레드를 어디선가 이미 점유하고 있다면 키 이벤트를 전달하지 못하는데, 이벤트를 전달할 수 없는 시간이 타임아웃을 넘는다면 이때 ANR이 발생한다. **키 이벤트인 볼륨, 메뉴, 백 키의 경우는 눌리고서 5초 이상 지연 시 바로 ANR을 발생**시킨다. 참고로 홈 키와 전원 키는 앱과 별개로 동작하고 ANR 발생과는 무관하다.
    - 터치 이벤트는 경우가 다르다. 터치 이벤트도 메인 스레드가 사용 중이라면 대기하는 것은 동일하지만 타임아웃 된다고 해서 바로 ANR이 발생하지 않는다. 그 다음으로 이어서 터치 이벤트가 왔을 떄는 **두 번째 터치 이벤트가 전달되지 않는 시간이 타임아웃되면 ANR이 발생**한다. 예를 들어, 어디선가 메인 스레드를 블로킹하고 있는데 이 때 첫 번째 터치 이벤트만으로는 ANR이 발생하지 않는다. 두 번째 터치 이벤트가 있고서 5초가 지나면 그때서야 ANR이 발생한다.

<br/>

- Message 처리 각각이 5초 이내라도 총합 처리 시간 영향
    - 가끔 혼동하는 경우가 있는데 특정 Message 처리가 5초가 넘더라도 그 사이에 터치가 없을 때는 문제가 발생하지 않는다. 예를 들어, for문을 0부터 4까지 돌리는데 2초씩 메인 스레드를 블로킹하고 있다고 가정한다. 5개의 Message를 처리하는 시간은 총 10초다. 가만히 두면 문제가 없다. **하지만 Message를 처리하는 중에 화면을 두 번 이상 터치하면 ANR이 발생**한다. (앞에 쌓여있는 Message를 먼저 처리하느라 터치 이벤트에 대한 처리가 지연되는 것이다.)

<br/>

- 서비스나 브로드캐스트 리시버에서도 5초 이내로 Message 처리 필요
    - 예를 들어 50초 동안 BroadcastReceiver의 onReceive()가 실행되고 있을 때 액티비티 화면을 터치하면 역시 ANR 발생 가능성이 높다. 브로드캐스트 리시버나 서비스도 액티비티가 떠있는 상태를 고려해서, 타임아웃을 5초라고 생각하는 편이 낫다. **결론적으로 브로드캐스트 리시버의 경우에 오래 걸리는 작업이 있다면 서비스로 넘겨서 실행해야 하고, 서비스에서는 다시 백그라운드 스레드를 이용**해야 한다.

<br/>
<br/>

## Q2. Thread와 Process의 차이점을 설명해 주세요.
모두 프로그램의 실행과 관련된 단어들이다.  
차이점은 Process는 실행의 단위, Thread는 Process 내에서 실행되는 흐름의 단위이다.  
Process는 독립적으로 실행되지만, Thread는 Process 내의 Thread들끼리는 Heap, Data 등(Stack은 개별 할당)을 공유한다.

<br/>
<br/>

## Q3. 안드로이드 스튜디오의 Thread 에 대해 설명해 주세요. Main Thread와 Worker Thread 등을 구분하는 이유와 Main Thread에서 반드시 동작해야 하는 함수가 있는지도 설명해 주세요.
안드로이드 스튜디오는 크게 2가지 Thread로 분류된다. Main Thread(UI Thread ) 와 Worker Thread.

<br/>

Main Thread는 액티비티와 컴포넌트들의 사용을 담당하고 연동하는 역할을 한다. UI 컴포넌트들과 밀접한 연관이 있는 Thread이다 보니 UI Thread라고도 부른다. 즉, System Call-Back Method, LifeCycle에 관련된 Method 등은 반드시 Main Thead에서 관리되어야 한다.

<br/>

그런데 다른 작업들에 의해 Main Thread가 UI와 동기화되지 못하고 지연되는 경우에는 문제가 발생한다. 이러한 오류를 ANR(Application Not Responding, UI 관련 작업이 일정 기간 이상 반응되지 못하면 발생)이라 부른다.

<br/>

이러한 문제점을 막기 위해 불안정한 UI 관련 작업이나 비동기 작업(애니메이션 등), High Cost의 연산 작업(Database 처리 등) 등은 Worker Thread를 따로 만들어 처리하도록 한다.

<br/>

하지만 View 등의 UI 관련 컴포넌트를 업데이트 하는 작업은 UI Thread에서 진행되어야 하는데 애니메이션 등의 비동기 작업을 진행하며 UI를 수정해야 한다면, Async Task 등을 이용하는 것이 바람직하다.

<br/>
<br/>

## Q4. onStart()와 onResume() 함수가 구분되어 있는데, 둘의 차이점은 무엇인가요?
onStart()는 액티비티가 사용자에게 보여지기 직전에 호출되고, onResume()은 사용자에게 보이지만 사용자와 상호 작용하기 직전 상태일 때 실행된다.

<br/>
<br/>

## Q5. Kotlin 언어의 by lazy와 lateinit에 대해서 설명해 주세요.
- var에서만 사용 가능한 lateinit
- val에서만 사용 가능한 by lazy

<br/>

> lateinit은 언제는 값을 변경할 수 있고(null 제외), by lazy는 값을 바꾸지 못한다.
> 

<br/>

### lateinit 조건
lateinit은 꼭 변수를 부르기 전에 초기화 시켜야 하는데 아래와 같은 조건을 가지고 있다.
- var(mutable)에서만 사용이 가능
- var이기 때문에 언제든 초기화를 변경할 수 있다.
- null을 통한 초기화를 할 수 없다.
- 초기화를 하기 전에는 변수에 접근 불가(접근 시 lateinit property subject has not been initialized 에러를 만나게 된다.)
- 변수에 대한 setter/getter properties 정의가 불가능
- lateinit은 모든 변수가 가능한 건 아니고, primitive type에서는 활용이 불가능

<br/>

### lateinit 초기화 확인
::을 통해서만 접근이 가능한 .isInitialized을 사용하여 체크할 수 있다.

```kotlin
if (::변수.isInitialized) {
    // something
}

```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/bc293567-e229-4c76-85dd-332d317bbf2e/_2021-04-08__3.24.42.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230222%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230222T092304Z&X-Amz-Expires=86400&X-Amz-Signature=e472dccc9b1e78e203fe83e417544d61924c5e94f0816c8a23660889ebde0243&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22_2021-04-08__3.24.42.png%22&x-id=GetObject)

초기화를 하지 않으면 접근하는 것은 불가능하니, 꼭 초기화해야 한다.

<br/>

### lazy
lazy 초기화는 기존 val 변수 선언에 by lazy를 추가함으로 lazy {}에 생성과 동시에 값을 초기화하는 방법을 사용한다.

```kotlin
private val multiAdapter: MultiViewTypeAdapter by lazy {
        MultiViewTypeAdapter()
}

```

<br/>

### lazy 조건
- 호출 시점에 by lazy 정의에 의해서 초기화를 진행
- val(immutable)에서만 사용이 가능
- 값 교체 불가능
- lazy 를 사용하는 경우 기본 Synchronized로 동작한다

<br/>

⇒ 호출 시점 한번 초기화를 진행하고, 그 이후에는 가져다가 쓰기만 한다.

<br/>
<br/>

## 🗂 참고
- [안드로이드 앱 개발자 면접 후기 - 1차면접 (질문 & 답변 중심) : 네이버 블로그 (naver.com)](https://blog.naver.com/PostView.nhn?blogId=csi468_&logNo=221465784013)
- [<안드로이드/Android> 안드로이드에서 스레드란? :: 앱해피의 프로그래밍 이야기 (tistory.com)](https://apphappy.tistory.com/63)
- [Android Interview (notion.so)](https://www.notion.so/Android-Interview-3ce7ddf12ddb413a9d2213173654d52c)
