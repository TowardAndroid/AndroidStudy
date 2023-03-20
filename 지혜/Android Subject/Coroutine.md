# Coroutine

*코루틴*
은 비동기적으로 실행되는 코드를 간소화하기 위해 Android에서 사용할 수 있는 동시 실행 설계 패턴

백그라운드 스레드에서 코드를 처리할 때 사용하는 하나의 방법

Co + routine 2개가 합쳐진 단어

**기능**

- **경량**: 코루틴을 실행 중인 스레드를 차단하지 않는 *[정지](https://kotlinlang.org/docs/reference/coroutines/basics.html)*를 지원하므로 단일 스레드에서 많은 코루틴을 실행할 수 있습니다. 정지는 많은 동시 작업을 지원하면서도 차단보다 메모리를 절약합니다.
- **메모리 누수 감소**: *[구조화된 동시 실행](https://kotlinlang.org/docs/reference/coroutines/basics.html#structured-concurrency)*을 사용하여 범위 내에서 작업을 실행합니다.
- **기본으로 제공되는 취소 지원**: 실행 중인 코루틴 계층 구조를 통해 자동으로 [취소](https://kotlinlang.org/docs/reference/coroutines/cancellation-and-timeouts.html)가 전달됩니다.
- **Jetpack 통합**: 많은 Jetpack 라이브러리에 코루틴을 완전히 지원하는 [확장 프로그램](https://developer.android.com/kotlin/ktx?hl=ko)이 포함되어 있습니다. 일부 라이브러리는 구조화된 동시 실행에 사용할 수 있는 자체 [코루틴 범위](https://developer.android.com/topic/libraries/architecture/coroutines?hl=ko)도 제공합니다.

특징

일시중단 가능한 계산(computation)의 인스턴스다. 코드의 나머지 부분과 동시에 작동하는 코드 블럭을 실행한단 점에서 개념적으로 쓰레드와 유사
이전에 실행이 중된된 지점에서 다시 실행을 재개할 수 있는 기능

코루틴은 메인 쓰레드를 차단하지 않으면서 메인 쓰레드에서 일시중단(suspending) 기능을 호출하는 기능을 제공하는 경량 쓰레드

메모리를 효율적으로 사용하면서 손쉽게 비동기 처리를 할 수 있습니다

코루틴과 쓰레드

**코루틴은 쓰레드와 매우 유사하다. 그러나 코루틴은 협력적으로 멀티태스킹되는 반면 쓰레드는 일반적으로 선점형으로 멀티태스킹된다. 코루틴은 동시성을 제공하지만 병렬성은 제공하지 않는다.**
 쓰레드에 비해 코루틴의 장점은 실시간 컨텍스트에서 사용할 수 있다는 것이다

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a12c1122-9a61-4f48-a980-7778cb1f9a89/Untitled.png)

### Dispatcher

안드로이드 코루틴에서의 dispatcher는 코루틴을 dispatcher에 전송하면 dispatcher가 자신이 관리하는 스레드풀 내의 스레드 부하 상황에 맞춰 코루틴을 배분하는 역할

- Dispatchers.Main : UI와 상호작용하는 작업을 실행하기 위해 메인스레드에서 실행시키는 역할을 한다.
- Dispatchers.IO : 네트워크 I/O 작업을 실행하는데 최적화 되어있다.
- Dispatchers.Default : 는 cpu를 많이 사용하는 작업을 기본 스레드 외부에서 실행하도록 최적화 되어 있다.

[https://onlyfor-me-blog.tistory.com/465](https://onlyfor-me-blog.tistory.com/465)

[https://yozm.wishket.com/magazine/detail/1793/](https://yozm.wishket.com/magazine/detail/1793/)

[https://blog.yena.io/studynote/2020/04/26/Android-Kotlin-Coroutine.html](https://blog.yena.io/studynote/2020/04/26/Android-Kotlin-Coroutine.html)

[https://eunoia3jy.tistory.com/132](https://eunoia3jy.tistory.com/132)
