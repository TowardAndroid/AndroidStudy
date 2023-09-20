# thread

한 개의 Process내에서 동시에 실행되는 작업의 단위를 나타냄

Thread는 Process의 자원을 공유 하지만 독립적으로 실행 될 수 있음
안드로이드 Main Thread는 UI를 실행 시키고 사용자와의 인터액션을 위한
용도로 사용
Thread내에서 생성한 자원은 해당 Thread에 종속적 임

장점

실행 속도, 빠른 반응 시간, 동시성을 갖는 프로그램을 쉽게 작성

함수

start() : 해당 Thread 객체를 실행시키는 메소드
 run() : start() 시 Thread 객체의 run 메소드가 시작된다

Multi-Thread
 한 개의 Process내에서 동시에 2개 이상의 Thread가 실행되는 상태를 나타냄
 JVM은 기본적으로 Multi-Thread를 지원 함
 동시성 문제가 발생 할 수 있음

### Thread.State

현재 쓰레드의 상태를 나타내는 Enum( getState() )

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7f47bfd4-e35e-4707-9520-32146c12f886/c559bf3e-f675-45d5-8057-f57841b7803e/Untitled.png)

### 쓰레드의 특징

1.Thread는 가상머신이 설치된 OS를 기반으로 동작

Thread는 플랫폼(OS) 쓰레드 기반 동작방식
– Thread를 만들면 OS Thread 가 위임 받아 동작하는 방식(Wrapping)
– OS 커널을 사용하면 Thread 숫자도 제한적이고 만들고 유지하는데 소요되는 비용이 비싼편
– OS Thread를 효율적으로 사용하기 위해 보통 Thread Pool을 만들어 사용

 2.Throughput(처리량)의 한계
- Spring등의 웹 애플리케이션은 요청당 하나의 Thread가 필요

- 애플리케이션에서 많은 요청을 처리하려면 Thread의 증가는 필수이나 OS Thread를 무한정
늘릴 수는 없음

3.Thread Blocking
- Request는 기본적으로 I/O 작업이므로 블럭킹 발생으로 낭비

### Not-Blocking 방식의 프로그래밍의 필요성(Reactive Programming)

1. 기존 Thread로는 Reactive Programming에 대한 대처 부족
-처리량을 향상하기 위해 Blocking 방식이 아닌 Non-Blocking방식의 Reactive 방식은 지금
도 계속 발전하고 있다(Webflux 등)
– Kotlin 은 Flow로 코루틴 방식의 향상된 Reactive Programming을 제공
- 기본 Thread 방식은reactive library를 만들거나 사용하려면 대대적인 작업이 필요

2.  플랫폼의 변화 필요
-예외처리, 디버깅, 프로파일링 등도 모두 쓰레드 기반이며 Thread Stack을 이루어 동작하므
로 컨텍스트 스위칭이 발생하여 개발 플랫폼 전체에 비용(디버깅의 어려움 등)발생
– 위의 부분을 Reactive 로 변환하려면 기존 쓰레드로는 한계가 존재
