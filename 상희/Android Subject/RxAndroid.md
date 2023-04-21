# 💡 RxAndroid

# ✅ RxAndroid란?
## RxAndroid
Android를 위한 ReactiveX Extensions이다.  
RxJava에 최소한의 클래스를 추가하여 안드로이드 앱에서 리액티브 구성 요소를 쉽고 간편하게 사용하게 만드는 라이브러리이다.

<br/>

기존 안드로이드 개발에서 가장 어려움을 겪는 문제는 복잡한 스레드 사용이다.  
복잡한 스레드 사용으로 발생하는 문제는 다음과 같다.  
- 안드로이드의 비동기 처리 및 에러 핸들링
- 수많은 핸들러와 콜백 때문에 발생하는 디버깅 문제
- 2개의 비동기 처리 후 결과를 하나로 합성하는 작업
- 이벤트 중복 실행

<br/>

숙련도 높은 개발자도 멀티 스레드 환경에서 발생하는 이러한 문제를 디버깅하는 데 많은 시간을 투자한다.  
RxAndroid는 습득하기 어려운 부분도 있지만 기존 안드로이드 개발과 비교했을 때 장점이 많다.  
다음과 같은 특징을 통해 앞 문제를 해결하는 데 도움을 준다.  
- 간단한 코드로 복잡한 병행(concurrency) 프로그래밍을 할 수 있다.
- 비동기 구조에서 에러를 다루기 쉽다.
- 함수형 프로그래밍 기법도 부분적으로 적용할 수 있다.

<br/>

## 리액티브 라이브러리와 API
RxAndroid는 기본적으로 RxJava의 리액티브 라이브러리를 이용한다. 안드로이드에서 이용하는 리액티브 API와 라이브러리는 상당히 많다.  
* 안드로드에서 사용할 수 있는 리액티브 API와 라이브러리 : RxLifecycle, RxBinding, RxLocation, RxFit, RxWear, RxImagePicker, ReactiveNetwork, RxDataBinding 등  
- RxLifecycle : RxJava를 사용하는 안드로이드 앱용 라이프 사이클 처리 API
- RxBinding : 안드로이드 UI 위젯용 RxJava 바인딩 API
- RxPermissions : RxJava에서 제공하는 안드로이드 런타임 권한 라이브러리

<br/>

## Android Studio Setting
gradle의 dependencies 부분에 RxAndroid 라이브러리를 추가한다.

> RxAndroid는 RxJava에 대한 의존성이 있어 RxJava를 추가하지 않아도 되지만, 최신 버전의 RxJava를 사용하려면 명시해 주는 것이 좋다.
> 

```groovy
dependencies{
	// RxJava & RxAndroid
	implementation 'io.reactivex.rxjava2:rxjava:2.2.2'
	implementation 'io.reactivex.rxjava2:rxandroid:2.1.0'
	
	// RxLifecycle
	implementation 'com.trello.rxlifecycle2:rxlifecycle-android:2.2.2'
	implementation 'com.trello.rxlifecycle2:rxlifecycle:2.2.2'
	implementation 'com.trello.rxlifecycle2:rxlifecycle-components:2.2.2'
}
```

<br/>
<br/>

# ✅ RxAndroid 개념 및 구성 요소
## RxAndroid 구성 요소
RxAndroid의 기본 개념은 RxJava와 동일하다. RxJava의 구조에 안드로이드의 각 컴포넌트를 사용할 수 있도록 변경해 놓은 것이다. 따라서 RxAndroid의 구성 요소는 다음처럼 RxJava의 구성 요소와 같다.  
- `Observable`  : 비즈니스 로직을 이용해 데이터를 발행한다.
- `구독자`  : Observable에서 발행한 데이터를 구독한다.
- `스케줄러`  : 스케줄러를 통해서 Observable, 구독자가 어느 스레드에서 실행될지 결정할 수 있다.

<br/>

이러한 과정을 간단한 코드로 나타내면 다음과 같다.  
Observable과 구독자가 연결되면 스케줄러에서 각 요소가 사용할 스레드를 결정하는 기본적인 구조이다. Observable이 실행되는 스레드는 subscribeOn() 함수에서 설정하고 처리된 결과를 onserveOn() 함수에 설정된 스레드로 보내 최종 처리한다.

```java
// 1. Observable 생성
Observable.create()
    .subscribe();  // 2. 구독자 이용

    // 3. 스케줄러 이용
    .subscribeOn(Schedulers.io())
    .observeOn(AndroidSchedulers.mainThread())
```

<br/>

## RxAndroid에서 제공하는 스케줄러
| 스케줄러 이름 | 설명 |
| --- | --- |
| AndroidSchedulers.mainThread() | 안드로이드의 UI 스레드에서 동작하는 스케줄러 |
| HandlerScheduler.from(handler) | 특정 핸들러에 의존하여 동작하는 스케줄러 |

안드로이드의 UI 스레드는 메인 스레드를 뜻한다.

<br/>

## RxAndroid 예제 : TextView에 텍스트 출력해 보기
### create() 사용

```java
Observer<String> observer = new DisposableObserver<String>() {
  @Override
  public void onNext(String s){
    textView.setText(s);
  }
  @Override
  public void onError(Throwable e) { }
  @Override
  public void onComplete() { }  
}

Observable.create(new ObservableOnSubscribe<String>(){
  @Override
  public void subscribe(ObservableEmitter<String> e) throws Exception{
    e.onNext("I'm student.");
    e.onComplete();
  }
}).subscribe(observer);
```

Observable.create()로 Observable 을 생성해 'I'm student.'(출력할 텍스트)를 입력 받고 subscribe() 함수 안 onNext() 함수에 전달한다.  
onNext() 함수는 전달된 문자를 TextView에 업데이트 하도록 정의되어 있으므로 실제 구독자를 subscribe(observer) 함수를 통해 등록하고 호출하면 'I'm student.'를 TextView에 표시한다.

<br/>

### create() 사용 - 람다 표현식으로 변형

```java
Observable.<String> create(s->{
  s.onNext("I'm smart!");
  s.onComplete();
}).subscribe(o -> textView.setText(o));
```

위와 비교하면 콜백 함수를 람다 표현식으로 바꾸며 데이터의 흐름이 명확해져 가독성이 좋아졌다.  
전달자는 명확한 단어로 변경할 수도 있지만 기본적으로 이니셜을 많이 사용한다.

<br/>

### just() 사용

```java
Observable.just("I'm hungry.")
  .subscribe(textView::setText);
```

메서드 레퍼런스 를 이용하여 Observable의 생성 코드를 단순하게 했다.

> Observable의 생성 방법은 워낙 다양하고 개발자의 성향에 따라 선택의 기준이 달라질 수 있다.
> 

<br/>

## RxLifecycle 라이브러리
RxAndroid에는 RxLifecycle 라이브러리를 제공한다.  
안드로이드의 Activity 와 Fragment 의 라이프 사이클을 RxJava에서 사용할 수 있게 한다.  
안드로이드와 UI 라이프 사이클을 대체한다기보다 구독할 때 발생할 수 있는 메모리 누수를 방지하기 위해 사용한다. 완료하지 못한 구독을 자동으로 해제(dispose)한다.

<br/>

### RxLifecycle 사용 이유
Observable은 안드로이드의 Context를 복사하여 유지한다. onComplete(), onError() 함수가 호출되면 내부에서 자동으로 unsubscribe() 함수를 호출한다.  
그런데 액티비티가 비정상적으로 종료되면 뷰가 참조하는 액티비티는 종료해도 가비지 컬렉션의 대상이 되지 못한다. 따라서 메모리 누수가 발생하게 된다.  
이때 이런 문제를 해결하기 위한 방법 중 하나가 RxLifecycle을 이용하는 것이다.

<br/>

### RxLifecycle 라이프 사이클 컴포넌트
RxLifecycle 라이브러리는 안드로이드의 라이프 사이클에 맞게 Observable을 관리할 수 있는 컴포넌트를 제공한다.

| 컴포넌트 | 설명 |
| --- | --- |
| RxActivity | 액티비티에 대응 |
| RxDialogFragment | Native/Support 라이브러리인 DialogFragment 에 대응 |
| RxFragment | Native/Support 라이브러리인 Fragment 에 대응 |
| RxPreferenceFragment | PreferenceFragment에 대응 |
| RxAppCompatActivity | Support 라이브러리인 DialogFragment에 대응 |
| RxAppCompatDialogFragment | Support 라이브러리인 AppCompatDialogFragment에 대응 |
| RxFragmentActivity | Support 라이브러리인 FragmentActivity에 대응 |

<br/>

### RxLifecycle 예제
build.gradle 파일의 depencies에 추가

```groovy
dependencies{
	// RxLifecycle
	implementation 'com.trello.rxlifecycle2:rxlifecycle-android:2.2.2'
	implementation 'com.trello.rxlifecycle2:rxlifecycle:2.2.2'
	implementation 'com.trello.rxlifecycle2:rxlifecycle-components:2.2.2'
}
```

<br/>

Observable.interval()을 이용해 1초에 한번 로그를 찍다가 화면이 뒤로 가 액티비티가 종료되어도 unsubscribe(구독 해제)를 하지 않는다면, 스트림은 계속 유지되어 로그가 계속 찍히는 것을 확인할 수 있다.

```java
Observable.interval(0,1,TimeUnit.SECONDS)
    .map(String::valueOf)
    .subscribe(s -> Lob.i("###",s));
```

<br/>

compose() 함수로 라이프 사이클을 관리하도록 추가했다. Observable은 해당 클래스가 종료되면 자동으로 해제(dispose)가 된다.

```java
Observable.interval(0,1,TimeUnit.SECONDS)
    .map(String::valueOf)
    .compose(bindToLifecycle())
    .subscribe(s -> Lob.i("Lifecycle 적용한 Observable",s));
```

<br/>

### RxLifecycle 마무리
RxJava2에서는 RxLifecycle의 컴포넌트 이외에도 메모리 관리를 위한 방법을 제공한다.  
예를 들어 RxJava에 익숙한 개발자들은 안드로이드의 전통적인 라이프 사이클 관리 기법보다는 직접 관리하기 편한 dispose() 함수를 사용한 것 등이 있다.  
어떤 것이 좋다고 이야기하기는 어렵고 각각 장단점이 있다. 상황에 맞게 개발자가 잘 선택하여 사용하면 된다.

<br/>
<br/>

# 🗂 참고
- [RxJava, RxKotlin - RxAndroid 란? (tistory.com)](https://jeongupark-study-house.tistory.com/133)
- [Android-Study/RxAndroid.md at master · taeiim/Android-Study (github.com)](https://github.com/taeiim/Android-Study/blob/master/study/week14/RxAndroid/RxAndroid.md)
- https://github.com/ReactiveX/RxAndroid
- [rxAndroid, rxJava, rxKotlin (tistory.com)](https://philosopher-chan.tistory.com/1320)
