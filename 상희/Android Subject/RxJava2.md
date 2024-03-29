# 💡 RxJava

# ✅ Reactive Programming
## Reactive Programming
리액티브 프로그래밍은 데이터 흐름과 전달에 관한 프로그래밍 패러다임이다.  
기존의 명령형(imperative) 프로그래밍은 주로 컴퓨터 하드웨어를 대상으로 프로그래머가 작성한 코드가 정해진 절차에 따라 순서대로 실행된다.  
그러나 리액티브 프로그래밍은 데이터 흐름을 먼저 정의하고 데이터가 변경되었을 때 연관되는 함수나 수식이 업데이트되는 방식이다.

<br/>

명령형 프로그래밍 방식은 변경이 발생했다는 통지를 받아서 연말 매출액을 새로 계산하는 당겨오는(pull) 방식이지만, **리액티브 프로그래밍은 데이터 소스가 변경된 데이터를 밀어주는(push) 방식**이다. 일종의 옵저버 패턴이다.  

<br/>

리액티브 프로그래밍은 새로운 프로그래밍 방식이 아니다. 이미 1990년대에 제시된 개념으로 컴퓨터 프로그래밍에서는 모델의 값에 변화가 생겼을 때 뷰를 자동으로 업데이트해 주는 목적으로 사용했다. 어떤 기능이 직접 실행되는 것이 아니라 시스템에 어떤 이벤트가 발생했을 때 처리하는 것이다.

<br/>

네트워크 프로그래밍할 때 사용하는 콜백(Callback)이나 UI 프로그래밍할 때 버튼 이벤트를 처리하는 클릭 리스너도 개념상으로는 리액티브 프로그래밍에 해당한다. 이 전통적인 개념에 몇 가지 요소를 추가해야 RxJava 기반의 리액티브 프로그래밍이라고 할 수 있다.

<br/>

## Reactive Programming과 Java
자바 언어와 리액티브 프로그래밍은 대략 두 가지 관계가 있다고 정리할 수 있다.

- 기존 pull 방식의 프로그래밍 개념을 push 방식의 프로그래밍 개념으로 바꾼다.
- 함수형 프로그래밍의 지원을 받는다.

<br/>

### 기존 pull 방식의 프로그래밍 개념을 push 방식의 프로그래밍 개념으로 바꾼다.
- ex :
    - 어떤 분석 데이터를 전국에 있는 수많은 매장에 통지해야 한다면 기존의 프로그램으로는 각 매장의 변화 상황을 데이터베이스에서 가져와야(pull 방식) 한다.
    - 혹은 전국에 있는 매장에 분석 데이터를 통지하려면 전체 매장 리스트를 기반으로 순차적으로 변화 상황을 전달해야 한다.
    - 리액티브 프로그래밍에서는 데이터의 변화가 발생했을 때 변경이 발생한 곳에서 새로운 데이터를 보내(push 방식)준다.
- 기존 자바 프로그래밍이 pull 방식이라면 리액티브 프로그래밍은 push 방식이다.

<br/>

### 함수형 프로그래밍의 지원을 받는다.
- 우리가 아는 콜백이나 Observer 패턴을 넘어 RxJava기반의 리액티브 프로그래밍이 되려면 함수형 프로그래밍이 필요하다.
- 콜백이나 Observer 패턴은 Observer가 1 개이거나 단일 스레드 환경에서는 문제가 없지만, 멀티 스레드 환경에서는 많은 주의가 필요하다.
    - 대표적 예로 데드락, 동기화 문제가 있다.
- 함수형 프로그램은 부수 효과가 없다.
    - 부수 효과 : 같은 자원에 여러 스레드가 경쟁 조건에 빠지게 되었을 때 예측할 수 없는 잘못된 결과가 나오는 현상
- 한두 개의 스레드가 있을 때는 정상 동작하다가 수십 수백 개의 스레드가 동시에 단일 자원에 접근하면 계산 결과가 꼬이고 디버깅하다가 매우 어렵다.
- 함수형 프로그래밍은 부수 효과가 없는 순수 함수를 지향한다.
    - 따라서 멀티 스레드 환경에서도 안전하다.

<br/>
<br/>

# ✅ RxJava
## RxJava를 만든 이유
넷플릭스에서 RxJava를 만들게 된 핵심적인 이유 3 가지는 다음과 같다.

<br/>

### 동시성을 적극적으로 끌어안을 필요가 있다. (Embrance Concurrency)
자바가 동시성 처리를 하는 데 번거로움이 있다.  
이를 해결하려고 넷플릭스는 클라이언트의 요청을 처리하는 서비스 계층에서 동시성을 적극적으로 끌어안았다.  
클라이언트의 요청을 처리할 때 다수의 비동기 실행 흐름(스레드 등)을 생성하고 그것의 결과를 취합하여 최종 리턴하는 방식으로 내부 로직을 변경했다.

<br/>

### 자바 Future를 조합하기 어렵다는 점을 해결해야 한다. (Java Futures are Expensive to Compose)
2013년 당시 자바 8에서 제공하는 CompletableFuture 같은 클래스가 제공되지 않았기 때문이다.  
그래서 비동기 흐름을 조합할 방법이 거의 없었다.  
RxJava에서는 이를 해결하려고 비동기 흐름을 조합할 수 있는 방법을 제공한다. RxJava에서는 조합하는 실행 단위를 리액티브 연산자라고 한다.

<br/>

### 콜백 방식의 문제점을 개선해야 한다. (Callbacks Have Their Own Problems)
콜백이 콜백을 부르는 콜백 지옥 상황이 코드의 가독성을 떨어뜨리고 문제 발생 시 디버깅을 어렵게 만든다.  
비동기 방식으로 동작하는 가장 대표적인 프로그래밍 패턴은 콜백이다. 그래서 RxJava는 콜백을 사용하지 않는 방향으로 설계하여 이를 해결했다.  

<br/>

리액티브 프로그래밍은 비동기 연산을 필터링, 변환, 조합하여 위 세가지 핵심 이유를 해결할 수 있다.  
따라서 RxJava는 Observable과 같은 데이터 소스와 map(), filter(), reduce()와 같은 리액티브 연산자를 제공한다.

<br/>

## 마블 다이어그램
마블 다이어그램은 RxJava를 이해하는 핵심 도구이다.  
map(), flatMap() 함수 등의 수많은 리액티브 연산자들을 이해하는데 큰 도움을 준다.

<br/>

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/ekhDwY/btqEcHozeR2/TEzAX8xumL0Asnys7miqf1/img.png)

<br/>

1. 위에 있는 실선은 Observable의 시간 표시 줄(timeline)이다. 시간 순으로 데이터가 발행되는 것을 표현한다.
2. Observable에서 발행하는 데이터이다. 시간 순서대로 별, 삼각형, 오각형, 원 등의 도형을 발행한다. 데이터를 발행할 때는 onNext 알림이 발생한다.
3. 파이프( | )는 Observable에서 데이터 발행을 완료했다는 의미이다. 한 번 완료하면 이후에는 더 이상 데이터를 발행할 수 없다. 완료하면 onComplete 알림이 발생한다.
4. 아래로 내려오는 점선 화살표는 각각 함수의 입력과 출력 데이터이다. 가운데 박스는 함수를 의미한다. flip() 함수는 입력 값을 뒤집는 함수이다. 따라서 입력 값의 색상은 그대로 두고 모양을 위아래 180 도 회전하여 뒤집는다.
5. 함수의 결과가 출력된 표시 시간 줄이다.
6. 엑스(X)는 함수가 입력 값을 처리할 때 발생한 에러를 의미한다. 에러 발생 시에는 onError 알림이 발생한다.

<br/>

조금 더 복잡한 마블 다이어그램은 아래 그림과 같다.  
RxJava의 combineLatest() 함수의 마블 다이어그램으로 2개 이상의 Observable을 처리할 수 있다.  
이전 flip 함수 마블 다이어그램과 다른 점은 Observable의 시간 표시 줄이 1 개가 아니라 2 개로 늘었다는 점이다.

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/AAnA3/btqEcHhNZ2J/J5UL1EKwYCGPbMzB2YNqgk/img.png)

<br/>

1. 첫 번째 Observable은 같은 모양(원)이지만 색깔이 다른 도형을 발행한다.
2. 두 번째 Observable은 모양은 다르지만 번호가 없는 도형을 발행한다.
3. combineLatest() 함수는 첫 번째 Observable의 도형과 두 번째 Observable의 도형이 모두 들어오면 둘을 합성한다.
4. 가장 아래 시간 표시 줄은 combineLatest() 함수의 실행 결과로 자세히 살펴보면 두 Observable의 결과를 조합한 것임을 알 수 있다. 첫 번째 Observable에서는 색상을 취하고 두 번째 Observable에서는 도형의 모을 취하고 있다.

<br/>

RxJava는 리액티브 프로그래밍이라는 새로운 시각을 제공해 주고 비동기 프로그래밍과 함수형 프로그래밍을 모두 활용해 문제를 해결할 수 있다.

<br/>
<br/>

# 🗂 참고
- [[RxJava] RxJava 프로그래밍(1) - 리액티브 프로그래밍 (tistory.com)](https://12bme.tistory.com/570)
- [Android-Study/study/week12/RxJava/RxJava.md at master · taeiim/Android-Study (github.com)](https://github.com/taeiim/Android-Study/blob/master/study/week12/RxJava/RxJava.md)
