# **RxAndroid (Reactive Extensions for Android)**

- Android applications에서 추가적인 수고로움 없이 RxJava를 사용할 수 있도록 최소한의 class만 추가한 라이브러리
- 기존 안드로이드 개발에서 가장 어려움을 겪는 문제 중 하나는 복잡한 스레드 사용이고
- 복잡한 스레드 사용으로 발생하는 문제
    - 안드로이드 비동치 처리 및 핸들링
    - 수많은 핸들러와 콜백 때문에 발생하는 디버깅 문제
    - 2개의 비동기 처리 후 결과를 하나로 합성하는 작업
    - 이벤트 중복 실행
- Main thread나 다른 주어진 Looper에서 로직이 수행될 수 있도록 Scheduler를 제공함

<br>

### **기존 안드로이드 개발과 비교했을 때 장점**

- 간단한 코드로 복잡한 병행(concurrency) 프로그래밍 가능
- 비동기 구조에서 에러를 다루기 쉽다
- 함수형 프로그래밍 기법도 부분적으로 적용할 수 있다
<br>

### **문제점**

- 높은 진입 장벽. Rx라는 라이브러리에 대해서 구조와 동작 방식에 대해 이해하고 있어야 한다.
- Rx에서 제공해주는 함수들로 기능들을 적절하게 구현할 수 있지만 보일러플레이트 코드들이 비교적 많이 존재하게 된다.
<br><br>

# • RxAndroid의 기본

- RxAndroid의 기본 개념은 RxJava와 동일
- RxJava의 구조에 안드로이드의 각 컴포넌트를 사용할 수 있게 변경해 놓은 것. 따라서 RxAndroid의 구성 요소는 다음처럼 RxJava의 구성요소와 같음
    - Observable : 비즈니스 로직을 이용해 데이터를 발행합니다.
    - 구독자 : Observable에서 발행한 데이터를 구독합니다.
    - 스케줄러 : 스케줄러를 통해서 Observable, 구독자가 어느 스레드에서 실행될지 결정할 수 있습니다.
    
    ```java
    // 1. Observable 생성
    Observable.create()
    // 2. 구독자 이용
        .subscribe();
     
    // 3. 스케줄러 이용
        .subscribeOn(Scheduler.io())
        .observeOn(AndroidSchedulers.mainThread())
    ```
    
    - Observable과 구독자가 연결되면 스케줄러에서 각 요소가 사용할 스레드를 결정하는 기본적인 구조.
    - Observable이 실행되는 스레드는 subscribeOn() 함수에서 설정하고 처리된 결과를 onServeOn() 함수에 설정된 스레드로 보내 최종 처리.
        - AndroidScheduler.mainThread() - 안드로이드의 UI 스레드에서 동작하는 스케줄러
        - HandlerScheduler.from(handler) - 특정 핸들러에 의존하여 동작하는 스케줄러.
        
        <br>
        
        좋아요 기능
        
        Rx 함수 중, throttleFirst`는 **일정 시간 구간(Timeslot) 동안 발생한 이벤트 중 첫 번째로 발생한 이벤트만 통과시키고, 나머지 이벤트를 무시합니다.**
         뷰의 클릭 액션이 발생할 때 마다 Rx 스트림으로 데이터를 보낸다고 생각하시면 됩니다
        
        [https://ju-hyang.tistory.com/40](https://ju-hyang.tistory.com/40)
        
        [https://dundun-dev.tistory.com/9](https://dundun-dev.tistory.com/9)
        
        [https://mashup-android.vercel.app/mashup-11th/minuk/androidClick/](https://mashup-android.vercel.app/mashup-11th/minuk/androidClick/)
        
        [https://sinwho.tistory.com/entry/안드로이드-RxAndroid-사용법-및-정리asynctask-deprecated](https://sinwho.tistory.com/entry/%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-RxAndroid-%EC%82%AC%EC%9A%A9%EB%B2%95-%EB%B0%8F-%EC%A0%95%EB%A6%ACasynctask-deprecated)
