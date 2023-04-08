# RxJava

Reactive X (Reactive Extensions)를 자바로 구현한 라이브러리

Reactive X란 Microsoft사 주도 아래 옵저버 패턴, 이터레이터 패턴, 함수형 프로그래밍의 장점과 개념을 접목한 반응형 프로그래밍 기법

## 반응형 프로그래밍

주변 환경과 끊임없이 상호 작용을 하는 프로그래밍

**환경이 변하면 이벤트를 받아 동작**하도록 만드는 기법 → 외부 요구에 끊임없이 반응하고 처리가능

- 시간순으로 들어오는 모든 데이터의 흐름을 스트림으로 처리
- 하나의 데이터 흐름은 다른 데이터 흐름으로 변형 가능
- 여러 데이터 흐름이 하나의 데이터 흐름으로 변경 가능

이 반응형 프로그래밍을 쉽게할 수 있또록 도와주는게 reactiveX라이브러리

명령형 프로그래밍

- 작성된 코드가 정해진 순서대로 실행되는 방식의 프로그래밍
- 이해하기 쉬움

## **RxJava, RxAndroid, RxKotlin 차이**

RxKotlin은 Rxjava를 기반으로 하여 코틀린만의 함수형 프로그래밍을 지원하고, RxAndroid는 Rxjava 기반으로 해서 몇가지 클래스를 더 추가하여 안드로이드 앱에서 리액티브 구성요소를 쉽고 편리하게 만들 수 있는 라이브러리

공통점

- **비동기 처리**를 쉽게할 수 있도록 도와주는 라이브러리
- **Observer Pattern**을 사용함
- REST API 통신 라이브러리인 Retrofit과의 뛰어난 호환성
- **콜백 지옥에서 벗어날 수 있음**

## 구성요소

### **[Observable](https://gogigood.tistory.com/33#Observable)**

- 데이터 스트림
- 하나의 스레드에서 다른 스레드로 전달할 데이터를 압축
- 주기적으로 또는 설정에 따라 생애주기 동안 한 번만 데이터를 방출
- 데이터를 처리하고 다른 구성요소에 전달하는 역할을 함

### **[Observers](https://gogigood.tistory.com/33#Observers)**

- Observable에 의해 방출된 데이터 스트림을 소비
- Observable을 구독(subscribe)하여 방출하는 데이터를 수신할 수 있음

### **[Schedulers](https://gogigood.tistory.com/33#Schedulers)**

- Observable과 Observers이 실행되어야 할 스레드를 알려줌

[https://velog.io/@hyejiseo-dev/Android-RxJava에-대하여](https://velog.io/@hyejiseo-dev/Android-RxJava%EC%97%90-%EB%8C%80%ED%95%98%EC%97%AC)

[https://devyul.tistory.com/entry/Android-Reactive-Programming-RxjavakotlinAndroid란](https://devyul.tistory.com/entry/Android-Reactive-Programming-RxjavakotlinAndroid%EB%9E%80)

[https://gogigood.tistory.com/33](https://gogigood.tistory.com/33)
