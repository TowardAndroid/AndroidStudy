AAC는 Android Architecture Components의 약자로,

테스트와 유지보수가 쉬운 앱을 디자인할 수 있도록 돕는 라이브러리의 모음

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9eb8e2f5-3ee3-4800-a152-718ddfef5b1f/Untitled.png)

### **[ViewModel]**

AAC의 ViewModel과 MVVM의 ViewModel은 서로 다르다.

하지만 MVVM의 ViewModel을 만들 때, AAC의 ViewModel을 사용하여 만들면 더 편리하다.



### **[LiveData]**

관찰 가능한 데이터 홀더 클래스

LifeCycle을 인식 (Activity, Fragment 등 다른 앱 구성요소의 LifeCycle 고려)

LifeCycle 인식을 통해 LiveData는 LifeCycle이 활동 상태인 앱 구성요소 Observer만 업데이트

### **[Repository]**

Model을 Repository -> DataSource로 좀 더 세분화하여 Model에서 직접 DataSource를 다루기보다 연동하는 부분을 따로 떼어 놓은 것 (**[출처](https://dunchi.tistory.com/96)**)

ViewModel은 DB나 서버에 직접 접근하지 않고, Repository에 접근하는 것으로 앱의 데이터를 관리한다.

## viewmodel 비교

**MVVM 패턴에서의 ViewModel**

MVP 패턴에서 파생된 패턴으로, 비즈니스 로직과 프레젠테이션 로직을 UI로부터 분리하는 것을 목표로 사용된다. View와 Model 사이의 의존성을 없애 테스트, 유지 보수, 재사용성을 높인다.

ViewModel은 쉽게 말해서, **뷰와 모델 사이에서 데이터를 관리하고, 바인딩해주는 역할**을 하게 된다.

**AAC에서의 ViewModel**

**[안드로이드 공식 문서]**에 따르면 수명 주기를 고려하여 UI 관련 데이터를 저장하고 관리하도록 설계되어 있다. 화면 회전과 같이 구성을 변경할 때도 데이터를 유지할 수 있다.라고 나와있다.

화면 회전이 발생했을 때 액티비티가 종료되고 다시 생성되는 과정을 거치는데, 이때 **생명 주기를 관리하여 데이터를 유실하지 않고 그대로 보존해두고 사용할 수 있게** 해 준다.

[https://ku-hug.tistory.com/193](https://ku-hug.tistory.com/193)

[https://hanyeop.tistory.com/167](https://hanyeop.tistory.com/167)
