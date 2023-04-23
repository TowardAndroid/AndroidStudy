# RxKotlin

RxKotlin은 RxJava에 Kotlin의 extension function을 이용하여 좀더 사용하기 편리하도록 만든 경량 library

`RxKotlin`
는 함수 컴포지션을 선호하며, 전역 상태와 함수를 호출함으로써 발생하는 사이드 이펙트를 방지하는 역할도 제공

1. Observable 생성

```kotlin
Observable.fromArray(arrayOf(1, 2, 3, 4, 5))

arrayOf(1, 2, 3, 4, 5).toObservable()
```

바로 자료형 뒤에 toObservable을 하면 알아서 Observable로 바꾸어 준다이외에도 toCompletable, toSingle지원 한다.

2. 매개변수명 지원 subscribe -> subscribeBy 변경

```kotlin
arrayOf(1, 2, 3, 4, 5).toObservable().subscribeBy(
    onNext = {},
    onComplete = {},
    onError = {}
)
```

3. CompositeDisposable PlusAssign과 Disposable의 addTo() 추가

```kotlin
val compositeDisposable = CompositeDisposable()
compositeDisposable += arrayOf(1, 2, 3, 4, 5).toObservable().subscribeBy(
    onNext = {},
    onComplete = {},
    onError = {}
)
```

```kotlin
arrayOf(1, 2, 3, 4, 5).toObservable().subscribeBy(
    onNext = {},
    onComplete = {},
    onError = {}
).addTo(compositeDisposable)
```

[https://ju-hyang.tistory.com/39](https://ju-hyang.tistory.com/39)

[https://gyubgyub.tistory.com/66](https://gyubgyub.tistory.com/66)

[https://soda1127.github.io/start-rx-kotlin/](https://soda1127.github.io/start-rx-kotlin/)
