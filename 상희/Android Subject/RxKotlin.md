# 💡 RxKotlin

# ✅ RxKotlin이란?
RxKotlin은 ReactiveX의 RxJava 라이브러리를 기반으로 포팅하여 코틀린을 위한 리액티브 프로그래밍의 특정 부분을 함수형 프로그래밍으로써 구현한 라이브러리이다.  
RxKotlin는 함수 컴포지션을 선호하며 전역 상태와 함수를 호출함으로써 발생하는 사이드 이펙트를 방지하는 역할도 제공한다.  
Rx라이브러리에서는 값을 발행하는 Producers(프로듀서)와 값을 구독하여 소비하는 Consumers(컨슈머) 구조로 옵저버 패턴으로 이루어져 있다. 해당 구조에 스케줄링, 스로틀링, 변형, 병합, 에러 처리, 라이프 사이클 등을 관리하는 오퍼레이터를 제공한다.

<br/>
<br/>

# ✅ RxKotlin 사용
Gradle 빌드 환경을 기준으로 세팅

```groovy
compile 'io.reactivex.rxjava2.rxkotlin:2.x.y'
```

<br/>

## RxJava의 푸시 메커니즘과 풀 메커니즘 비교
RxKotlin은 과거 패러다임에서 사용하던 프로그래밍 방식인 Iterator 반복자 패턴의 풀 매커니즘을 사용하지 않고, 푸시 매커니즘의 옵저버블 패턴을 중심으로 작용한다.  
그렇기 때문에 지연이 일어날 수 있으며 동기식과 비동기식 방식 모두 이용될 수 있다.

```kotlin
fun main(args: Array<String>) {
    val list = listOf("One", 2, "Three", "Four", 4.5, "Five", 6.0f) // 1
    val iterator = list.iterator() // 2
    while (iterator.hasNext()) { // 3
        println(iterator.next()) // 4 각 엘리먼트를 출력한다
    }
}
```

<br/>

결과는 다음과 같다.

```
One
2
Three
Four
4.5
Five
6.0
```

<br/>

Observable 패턴으로 구성된 동일한 예제

```kotlin
fun main(args: Array<String>) {
    val list:List<Any> = listOf("One", 2, "Three", "Four", 4.5, "Five", 6.0f)
    val observable: Observable<Any> = list.toObservable(); //1

    observable.subscribeBy(  // 2 named arguments for lambda Subscribers
            onNext = { println(it) },
            onError =  { it.printStackTrace() },
            onComplete = { println("Done!") }
    )

}
```

<br/>

결과는 다음과 같다.

```
One
2
Three
Four
4.5
Five
6.0
Done!
```

<br/>

마찬가지로 리스트의 모든 값을 출력하는 것을 볼 수 있다.  
차이점으로 Done을 출력하는 것을 볼 수 있다. 

<br/>

내부적으로 어떤 차이가 있을까?
1. 리스트를 생성한다. (이전 코드와 동일)
2. 1 번에서 생성한 리스트로 Observable 인스턴스를 생성한다.
3. Observable 인스턴스를 구독한다.

<br/>

옵저버블 객체를 구독했기 때문에 내부 리스트의 값을 하나 하나씩 푸시하고, 그렇게 방출된 값에 대해 변경 사항을 추적합니다. 따라서,
  - `onNext: (T) -> Unit`    
    : 변경 사항을 추적하고 방출한다.    
  - `onError: (Throwable) -> Unit`    
    : 에러가 발생 시 Throwable 인스턴스를 넘겨 준다.    
  - `onComplete: () -> Unit`    
    : 모든 데이터가 푸시가 완료되면 호출되는 함수이다.
    
<br/>

## Reactive하게 코드 변경
아래의 코드는 짝수와 홀수를 구분하기 위한 간단한 프로그램을 구현한 코드이다.

```kotlin
fun main(args: Array<String>) {
    var number = 4
    var isEven = isEven(number)
    println("The number is" + (if (isEven) "Even" else "Odd"))
    number = 9
    println("The number is" + (if (isEven) "Even" else "Odd"))
}

fun isEven(n: Int): Boolean = (n % 2 == 0)
```

<br/>

위의 코드를 리액티브하게 바꿔 보면 다음과 같다.

```kotlin
fun main(args: Array<String>) {
    val subject: Subject<Int> = PublishSubject.create()

    subject.map { isEven(it) }
            .subscribe {
                println("The number is ${(if (it) "Even" else "Odd")}" )
            }

    subject.onNext(4)
    subject.onNext(9)
}
fun isEven(n: Int): Boolean = (n % 2 == 0)
```

<br/>

결과는 다음과 같다.

```
The number is Even
The number is Odd
```

<br/>

변환한 코드를 보면 `map(Function<? super T, ? extends R>):Observable<R>`  함수를 사용하였는데, 해당 함수를 통해 `isEven(Int):Boolean`에 인자로 푸시된 값을 차례로 받아 가공하는 과정을 거친다.  
`subject.onNext(@NonNull T)`  메서드는 새로운 값을 받아 subject로 전달해 처리할 수 있다.

<br/>
<br/>

# 🗂 참고
- [1-02.RxKotlin 시작하기 | 소다의 개발 블로그 (soda1127.github.io)](https://soda1127.github.io/start-rx-kotlin/)
- [RxKotlin과 RxAndroid 알아보기 :: 서랍 속 작은 공간 (tistory.com)](https://dundun-dev.tistory.com/9)
- [투덜이의 리얼 블로그 :: [RxKotlin] Reactive 코틀린 #1 - 개념 및 설치 (tistory.com)](https://tourspace.tistory.com/278)
