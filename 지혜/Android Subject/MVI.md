## MVI
mvc에서 파생된, 능동적인 controller 대신 Intent 라고 불리는 Reactive 요소를 이용한 아키텍처 패턴

- 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0d05c95e-0b05-4e50-ad1f-3aeaddb9af48/Untitled.png)

- Model

 Model은 상태를 나타낼 수 있다. MVI에서 Model은 데이터의 플로우가 단방향으로 이루어지기 위해 무조건 불변성을 보장해야 한다.

- View

View는 Activity나 Fragment를 나타내며, 앱의 상태를 전달 받아 화면에 랜더링하는 역할이다.

- Intent
- Intent는 앱이나, 사용자가 취하는 행위를 나타내기 위한 의도이다. View는 Intent를 받고, ViewModel은 Intent를 옵저빙하며 Model은 그에따라 새로운 상태로 변환한다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/be3a0646-2c80-43dc-9be5-7dd41d545577/Untitled.png)

1.Intent로 User로 부터 입력을 가져온다.

1. Intent는 model에서 처리해야 할 동작을 제공한다
2. model은 intent로부터 동작은 가져온다. (model은 데이터,애플리케이션상태,비즈니스로직관리(
3. model은 view에 표시할 새로운 모델을 생성한다.
4. view는 model로부터 새로운 모델을 가져와 표시한다.

장점

단방향성 데이터 프흐름, 불변성 데이터를 이용해 예측 가능한 상태가 만들어지기 떄문에 유지보수 용이

서로 간 의존성이 없다.

단점

RxJava와 같은 Observable한 외부 라이브러리를 이용해야 한다.

[https://brunch.co.kr/@oemilk/113](https://brunch.co.kr/@oemilk/113)
