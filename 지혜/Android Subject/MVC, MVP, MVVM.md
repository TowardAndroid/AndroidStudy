# MVC

moder-view-controller 측면으로 분리하여 안드로이드 개발에 적용하는 패턴

### model

애플리케이션의 비즈니스 로직과 데이터들을 다루는 부분

### view

사용자에게 보여지는 영역, 모델로부터 얻은 데이터를 뷰에 표현하게 되고 안드로이드에서는 activity/fragment가 뷰의 역할을 하게 됩니다.

### controller

뷰로부터 사용자에게 입력을 받거나 이벤트가 발생하면 로직에 맞게 모델을 변경하게 됩니다. 모델에서 데이터가 변화되는 것에 따라 컨트롤러는 뷰의 상태를 업데이트 시킨다. 

mvc패턴에서는 activity,framgent는 뷰&컨트롤러 동시역할

### 장점

모델에서 데이터를 가져와서 뷰에 구현하고 컨트롤러를 통해 이벤트가 발생하면 모델과 뷰를 갱신이라는 구조로 직관적이고 단순

소스코드만 봐도 패턴 이해가 쉬움

구조가 단순하여 작은 애플리케이션을 개발하는데 크게 신경쓰지 않고 빠르게 개발 진행 가능

### 단점

activity,fragment에 모든 코드가 편중

애플리케이션의 규모가 커지면 한 클래스에 너무 많은 코드

스파게티 코드 양산

컨트롤러는 특정 뷰와 모델에 의존적이며, 뷰도 특정 모델에 의존적이라 결합도가 높아 유닛테스트가 거의 불가능

# mvp 패턴

ui로직과 비즈니스 로직을 분리하는데 집중하여 생겨난 디자인 패턴

### model

mvc의 model과 동일하게 비즈니스 로직을 수행하고 데이터를 다루는 여역

### view

사용자에게 보여지는 화면 영역, activity/fragment

mvc와 다르게 activity, fragment는 view역할만 할 뿐 컨트롤러 역할을 하지 않는다.

### presenter

view와 model을 연결해주는 역할로 presenter를 도입함으로써 ui로직과 비즈니스

로직을 분리할 수 있게 되었습니다. presenter내에는 model과 view의 인스턴스를 가지고 이 둘을 연결해주는 역할이기 때문에 presenter와 view는 1:1관계를 갖는다.

### 장점

mvc에서는 view에서는 모델을 직접 생성하여 변경하기에 의존적이었다. 하지만 mvp에서는 view와 model중간에 presenter라는 연결 부분을 두어 결합도를 약하게 만들었다.

ui로직은 view, 비즈니스 로직은 model로 분리,연결하는 presenter→ 유닛테스트 수월

### 단점

view에서 present를 직접 생성하기에 의존성이 높고 1:1관계를 유지해야 해서 view가 많아질수록 presenter도 많아진다.

애플리케이션 기능이 추가될때마다 presneter코드 증가

# mvvm

별도록 databinding, LiveData또는 RxJava와 같은 Observable타입을 이용하여 Presenter와 view사이의 결합도를 끊는데 집중

### model

애플리케이션의 비즈니스 로직과 데이터를 다루는 부분

### view

사용자에게 보여지는 부분 activity,fragment

### viewmodel

view에서 표현해야할 데이터를 Observalble타입으로 관리하며 view들이 viewModel의 데이터를 구독요청하여 화면을 갱신

databinding라이브러리를 사용하여 viewmodel이 view에 대한 의존성을 갖지 않고 느슨하게 연결되도록 할 수 있다. 

viewmodel은 특정 view에 의존하지 않다보니 다른 view와 연결할 수 있으므로 1:n의 관계가질 수 있다.

### 장점

view와 viewmodel사이의 결합도를 느슨하게 하여 유닛테스트 수행가능

view와 model사이에서의 의존성도 없음

view는 viewmodel을 알지만viewmodel은 view를 알지 못하고 viewmodel은 model을 알지만 model은 viewmodel을 알지 못합니다. 한쪽 방향으로만 의존관계에 있어서 각 모듈별로 분할하여 개발

### 단점

복잡하다

databinding, livedata등 다른 라이브러리를 필수적으로 알아야한다.

[https://velog.io/@ows3090/Android-MVC-MVP-MVVM-장단점을-알고-쓰자](https://velog.io/@ows3090/Android-MVC-MVP-MVVM-%EC%9E%A5%EB%8B%A8%EC%A0%90%EC%9D%84-%EC%95%8C%EA%B3%A0-%EC%93%B0%EC%9E%90)
