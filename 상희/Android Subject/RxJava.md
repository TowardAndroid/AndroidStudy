# 💡 RxJava

# ✅ RxJava란?
## Rx 관련 용어
- RxAndroid는 RxJava에 안드로이드용 스케쥴러 등 몇 가지 클래스를 추가해 안드로이드 개발을 쉽게 해 주는 라이브러리
- RxJava는 ReactiveX(Reactive Extensions)를 Java로 구현한 라이브러리
- ReactiveX는 관찰 가능한(Observable) 스트림을 사용하는 비동기 프로그래밍을 위한 API이다.  
  ([공홈](https://reactivex.io/) 헤드 문구이다. - An API for asynchronous programming with observable streams.)
- Reactive Programming은 데이터 흐름과 변화의 전파와 관련있는 선언적 프로그래밍 패러다임이다.  
  ([위키백과](https://en.wikipedia.org/wiki/Reactive_programming) 출처 - Reactive programming is a declarative programming paradigm concerned with data streams and the propagation of change.)

<br/>

RxJava도, 상위 개념들도 모두 한 문장으로 정의 내리기엔 개념이 어렵다. 반응형 프로그래밍이란 대체 무엇이길래 ReactiveX와 RxJava, RxAndroid 등을 만드는 배경이 되었을까?

<br/>

## 반응형 프로그래밍(Reactive Programming)
반응형 프로그래밍(Reactive Programming)은 주변 환경과 끊임없이 상호 작용을 하는 프로그래밍 을 의미한다. 환경이 변화하면 이벤트를 받아 동작하도록 만드는 프로그래밍 기법이다.  
그럼 기존에는 주변 환경과 상호 작용을 하지 않았을까? 여기 간단한 예시가 있다.

```
기존의 명령형 프로그래밍에서는 a = b + c 에서 a는 b + c의 연산이 끝난 이후에 그 결과를 통해 값이 할당될 것이다. 
만약 이후에 b나 c의 값이 변하더라도 a에는 영향을 주지 않기 때문에 문제가 생길 수 있다. 
반면 리액티브 프로그래밍에서는 b나 c의 값이 변동되더라도 b + c 연산을 다시 할 필요 없이 자동으로 업데이트된다.
```

<br/>

반응형 프로그래밍에서는 데이터가 변하면 알아서 캐치해서 반영한다.  
구체적으로 어떻게 돌아가는 것인지는 명령형 프로그래밍과의 차이를 통해 알아본다.

<br/>

## 명령형 프로그래밍과 반응형 프로그래밍의 차이
### 명령형 프로그래밍(Imperative Programming)
명령형 프로그래밍은 작성된 코드가 정해진 순서대로 실행되는 방식의 프로그래밍이다. 코드가 순서대로 진행되므로 이해하기 쉽다.  
즉, 개발자가 작성한 조건문, 반복문, 함수를 따라 컴파일러가 다른 코드로 이동하게 된다.

<br/>

예제는 다음과 같다. 짝수만 출력하도록 만들어졌다.

```java
public void imperativeProgramming() {
    ArrayList<Integer> items = new ArrayList<>();
    items.add(1);
    items.add(2);
    items.add(3);
    items.add(4);

    for (Integer item : items) {
        if (item % 2 == 0) {
            System.out.println(item);
        }
    }

    items.add(5);
    items.add(6);
    items.add(7);
    items.add(8);
}
```

```java
// Result
2
4
```

<br/>

위의 코드는 다음과 같이 작동한다.  
1. 리스트를 만든다.
2. 리스트에 1~4 아이템을 추가한다.
3. for문으로 items 리스트를 순회하며 짝수를 출력한다.
4. 리스트에 5~8 아이템을 추가한다.

<br/>

`println()`  이후에 리스트에 아이템을 추가해도 결과에는 영향을 미치지 않는다.

<br/>

### 반응형 프로그래밍(Reactive Programming)
반응형 프로그래밍은 시간 순으로 들어오는 모든 데이터의 흐름을 스트림(Stream)으로 처리한다.  
하나의 데이터 흐름은 다른 데이터 흐름으로 변형되기도 하고, 여러 데이터 흐름이 하나의 데이터 흐름으로 변경될 수도 있다.

<br/>

예제는 다음과 같다. 짝수만 출력하도록 만들어졌다.

```java
public void reactiveProgramming() {
    PublishSubject<Integer> items = PublishSubject.create();
    items.onNext(1);
    items.onNext(2);
    items.onNext(3);
    items.onNext(4);

    items.filter(item -> item % 2 == 0)
            .subscribe(System.out::println);

    items.onNext(5);
    items.onNext(6);
    items.onNext(7);
    items.onNext(8);
}
```

```java
// Result
6
8
```

<br/>

위의 코드는 다음과 같이 작동한다.  
1. 데이터 스트림을 만든다. (PublishSubject)
2. 데이터 스트림에 1~4 아이템을 추가한다.
3. 데이터 스트림에서 짝수만 출력하는 데이터 스트림으로 변형한 뒤 구독한다.
4. 데이터 스트림에 5~8 아이템을 추가한다.

<br/>

`PublishSubject`는 구독 시점 이후의 데이터만 옵저버에 전달하기 때문에 6, 8만 출력된다. (구독 시점 이전의 데이터까지 출력하려면 `ReplaySubject`로 대체할 수 있다.)

<br/>

## RxJava
### RxJava
**RxJava는 데이터를 관찰할 수 있고 데이터를 스트림으로 처리한다**는 것을 알 수 있다.  
RxJava는 개발자들이 직면하는 문제들인 **동시성 문제, 다중 이벤트 처리, 백그라운드 처리 등의 문제를 좀 더 쉽게 해결**할 수 있도록 해 준다.  
안드로이드 개발의 경우 화면(UI)을 변경할 수 있는 것은 메인 스레드뿐이기 때문에 비동기 처리를 해야 하는 일이 생긴다. Rx를 이용하면 이런 작업들을 쉽게 할 수 있고 새로운 프로세스가 추가되어야 하거나 삭제되어야 한다면 로직의 큰 변경 없이 간단히 수정할 수 있다.

<br/>

### Rx 구성 요소
Rx는 세 가지 주요 컴포넌트로 구성되어 있다.  
- Observable    
    : Observable은 데이터 스트림이다.     
    Observable은 하나의 스레드에서 다른 스레드로 전달할 데이터를 압축한다.     
    주기적으로 또는 설정에 따라 생애 주기 동안 한번만 데이터를 방출한다.     
    Observable은 데이터를 처리하고 다른 구성 요소에 전달하는 역할을 한다고 생각하면 된다.    
- Observers    
    : Observers는 Observable에 의해 방출된 데이터 스트림을 소비한다.     
    Observers는 subscribeOn() 메서드를 사용해서 Observable을 구독하고 Observable이 방출하는 데이터를 수신할 수 있다.    
- Schedulers    
    : Schedulers 는 Observable과 Observers에게 그들이 실행되어야 할 스레드를 알려 준다.    
    observeOn() 메서드로 observers에게 관찰해야 할 스레드를 알려 줄 수 있다.     
    또한 scheduleOn() 메서드로 observable이 실행해야 할 스레드를 알려 줄 수 있다.
    
<br/>
<br/>

# ✅ Android Project에 RxJava 적용하기
## build.gradle
안드로이드에 RxJava를 적용하려면 `build.gradle`에 추가해야 한다.

```groovy
dependencies {
    implementation 'io.reactivex.rxjava3:rxandroid:3.0.0'
    implementation 'io.reactivex.rxjava3:rxjava:3.0.7'
}
```

> RxJava 최신 버전 확인 : [ReactiveX/RxJava: RxJava – Reactive Extensions for the JVM – a library for composing asynchronous and event-based programs using observable sequences for the Java VM. (github.com)](https://github.com/ReactiveX/RxJava)
> 

<br/>

## Observer
Observable은 다음의 3가지 이벤트를 사용하여 동작한다.  
- onNext()    
    : 하나의 소스 Observable에서 Observer까지 한 번에 하나씩 순차적으로 데이터를 발행한다.    
- onComplete()    
    : 데이터 발행이 끝났음을 알리는 완료 이벤트를 Observer에 전달하여 onNext()를 더 호출하지 않음을 나타낸다.    
- onError()    
    : 오류가 발생했음을 Observer에 전달함
    
<br/>

```java
Observer<Integer> observer = new Observer<Integer>() {

    @Override
    public void onCompleted() {
        System.out.println("All data emitted.");
    }
    
    @Override
    public void onError(Throwable e) {
        System.out.println("Error received: " + e.getMessage());
    }
    
    @Override
    public void onNext(Integer integer) {
        System.out.println("New data received: " + integer);
    }
};
```

<br/>

## Schedular
반응형 프로그래밍에서 Scheduler는 동시성을 관리한다.  
Scheduler에는 스레드 관리를 제어하는 두개의 메서드가 있다.  
- subscribeOn()    
    : observable이 어느 스레드에서 동작할 것인지 정의할 수 있다.    
- observeOn()    
    : observer가 어느 스레드에서 동작할 것인지 정의할 수 있다.
    
<br/>

Schedulers.newThread()와 같이 RxJava에서 제공된 메인 기본 스레드는 새로운 백그라운드를 생성한다.  
Schedulers.io() 는 IO 스레드에서 코드를 실행한다.

<br/>

다음과 같이 Scheduler를 사용할 수 있고, **Observer에서 발행하는 데이터를 수신하기 위해서는 꼭 구독을 해야 한다.**

```java
Subscription subscription = observable 
    .subscribeOn(Schedulers.io()) // observable을 IO 스레드에서 실행
    .observeOn(AndroidSchedulers.mainThread()) // Observer 메인 스레드에서 실행
    .subscribe(observer); // observer 구독

subscription.unsubscribe(); // 구독 취소
```

<br/>
<br/>

# 🗂 참고
- [[Android] RxJava란? (tistory.com)](https://soohyun6879.tistory.com/123)
- [[Android] RxJava 시작하기 (yena.io)](https://blog.yena.io/studynote/2020/10/11/Android-RxJava(1).html)
- [리액티브 프로그래밍이란? (tistory.com)](https://dev-daddy.tistory.com/25)
- [아키텍처 구성요소 관련 추가 리소스  |  Android 개발자  |  Android Developers](https://developer.android.com/training/camerax/additional-resources?hl=ko)
- [Rxjava를 안드로이드에 적용시켜보기! (tistory.com)](https://hyeals.tistory.com/79)
- [Android : RxJava에 대하여 (velog.io)](https://velog.io/@hyejiseo-dev/Android-RxJava%EC%97%90-%EB%8C%80%ED%95%98%EC%97%AC)
