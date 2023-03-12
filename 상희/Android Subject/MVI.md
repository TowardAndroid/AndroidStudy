# 💡 MVI

# ✅ 기존 패턴의 문제
Android 개발자로서 일반적으로 사용되는 패턴으로 MVC, MVP, MVVM이 있다. 이 패턴들은 명령형 프로그래밍 접근 방식을 사용한다. 이 접근 방식을 사용하면 안드로이드에서 발생하는 대부분의 문제가 해결되지만, thread safety 또는 state 관리에 관련해서 여전히 몇 가지 문제에 직면할 수 있다.

<br/>
<br/>

# ✅ MVI 도입 배경
기존 안드로이드에서 흔히 쓰던 패턴은 MVVM이었을 것이다. 하지만 이 MVVM 패턴에서는 크게 상태와 부수 효과라는 문제가 있었다.  
- Multiple Inputs : ViewModel은 많은 input, output을 관리해야 하는 경우가 있다. 이때 백그라운드 스레드를 사용하게 되면 thread safety하지 못한 문제가 발생할 수 있다.
- Multiple States : 복잡하게 분산된 상태와 복잡한 비즈니스 로직을 가질 수 있다. 이를 Observer Pattern을 이용해 상태를 동기화 하는 방법을 사용하는데, 이 또한 행위의 충돌을 일으킬 수 있다. 상태 정보가 뷰와 모델 두 곳에 존재하기 때문에 다중 스레드 및 다양한 입력에 의해 모델에 대한 업데이트가 동시에 발생할 수도 있는 멀티 스레드나 동적 환경에서는 이들 상태를 관리 및 보장하기 힘들다.

<br/>

## 상태 문제
앱은 상태 제어와 큰 연관성이 있다. 상태를 관리하기 힘들어지고 의도하지 않은 방향으로 갈 때 이것을 상태 문제라고 한다.  
예를 들어 아래와 같이 API의 응답을 성공적으로 리스트에 출력했지만, 상태 문제가 발생해 계속해서 프로그래스 바가 화면에 보이는 상황이 있다.

![https://miro.medium.com/v2/resize:fit:640/0*e6y9sVMGT882KU7_.gif](https://miro.medium.com/v2/resize:fit:640/0*e6y9sVMGT882KU7_.gif)

<br/>

앱의 상태는 시간의 흐름에 따라 다음과 같이 다양하게 변경될 수 있다.  
- 네트워크 연결이 끊어졌을 때 표현되는 Snackbar
- 사용자의 입력에 의해 작성되는 텍스트
- 특정 시간에 울리는 알람 소리

<br/>

일반적으로 이 분야에서 상태(state)라 함은 클래스 오브젝트의 어떠한 값 또는 데이터다.  
ex : ViewModel 객체에 선언되어 있는 State  
Compose의 업데이트는 상태의 변경에 의해서 이루어지며 이를 재구성(Recomposition)이라고 한다.  
Compose를 도입한 이후, 개발자는 더 이상 View에 접근해서 업데이트 하는 수고를 덜었으며 그저 ‘상태 관리’에만 집중하면 된다.

<br/>

## 부수 효과
- 부수 효과(Side Effect)는 원래의 목적과 다르게 다른 효과 또는 부작용이 나는 상태를 지칭한다.
- 안드로이드에서 서버 호출, 데이터베이스 접근 등에서 부수 효과가 발생해 그에 따른 상태 변경에 어려움을 겪을 수 있습니다.
- 부수 효과로 인해 함수가 어떤 결과를 반환할지 예측하기 힘들게 되고, 이에 따라 상태 변경에 있어 어려움을 겪는다.

<br/>
<br/>

# ✅ MVI란?
Hannes Dorfman에 의해 JavaScript용 Redux 라이브러리를 기반으로 한 MVI가 만들어졌다.

<br/>

### Key Concepts
- Unidirectional cycle of data
- Non-blocking
- Immutable state
    - MVI는 Single source of truth로써 비즈니스 로직을 유지하기 위해 모델은 불변성(Immutable)을 지니고 있어야 한다. 이 방식은 여러 클래스에서 모델이 수정되지 않음을 보장하기 위해서인데, 앱의 전체 라이프 사이클 동안 단일 상태를 유지할 수 있게 된다. (불변성을 가지고 있다는 의미는 모델을 수정할 수 없기 때문에, 내부의 Property는 바꿀 수는 없고 모델 자체를 copy()해서 새로 생성하는 방법이 필요하다.)

<br/>

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/bMb3jo/btrfZrnTocO/G9Sokkjs52fIk2T68sCMhK/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/bMb3jo/btrfZrnTocO/G9Sokkjs52fIk2T68sCMhK/img.png)

<br/>

- MVI는 MVP, MVVM 같은 다른 패턴과 유사하지만 의도(Intent)와 상태(State)라는 두 가지 새로운 개념이 도입되었다.
- MVI는 사용자 또는 시스템의 상호 작용을 기반으로 Model이 업데이트 되고 Model에서 방출된 상태를 기반으로 View가 업데이트되는 반응형 아키텍처 패턴이다.
- MVI는 Cycle.js 자바스크립트 프레임워크에서 영감을 받았다.
- 단방향(Unidirectional) 및 순환(Circular Data Flow)의 원칙을 기반으로 작동한다.
- MVI 아키텍처를 적용한 라이브러리는 대표적으로 Airbnb의 Mavericks가 있다.
- 사용자가 객체를 발행하는 행위가 기본적으로 앱의 상태를 변화시키고자 하는 의도를 나타낸다고 규정하고 이를 Intent라고 부른다.

<br/>

### State
- State는 Immutable한 데이터 구조
- 어느 시점이건 앱에는 현재의 시점을 표현하는 하나의 상태만 존재하고 그걸 바꿀 수 있는 유일한 트리거는 새로운 State를 만드는 Intent이다.
- 즉 UI의 변화는 곧 Intent 실행의 결과가 된다.
- 만약 Configuratin Change(화면 전환, 언어 변경 등)이 발생하면 어떻게 처리할까?
    - 가장 최근의 State를 표시하면 된다.

<br/>

### Redux
- React 기반 프론트엔드에서 주로 사용되는 상태 관리 패턴
- 복잡한 상태를 쉽게 관리하기 위해 사용
- 한 곳에서 모든 상태를 관리
- 상태는 불변 타입
- 상태 변화는 순수 함수로 작성

<br/>

### UDA(Uni-Directional-Architecture)
- UDA는 하나의 아키텍처로 이해하는 것보단, 앱을 디자인하는 방법 또는 아키텍처의 특성이라고 생각이 된다.
- 데이터의 흐름이 한 방향으로 진행되고, 상태는 모델에서만 관리된다면 UDA라고 할 수 있다.
- 대표적으로 MVC(Mode-View-Controller) 패턴이 가장 단순한 형태의 UDA입니다.

<br/>

## MVI(Model - View - Intent) 패턴
MVC, MVP 또는 MVVM처럼 MVI도 관심사를 나누고 해당 관심사의 앞 글자를 따서 만든 패턴이다.

<br/>

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/d5w9Bg/btrfV92Fmxk/Gsp1nzKvUzRjM2BmaV3bP1/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/d5w9Bg/btrfV92Fmxk/Gsp1nzKvUzRjM2BmaV3bP1/img.png)

<br/>

### Model
- UI에 반영될 상태를 의미한다. 그러므로 MVP 또는 MVVM 모델의 정의와는 다르다.
    - MVC, MVP, MVVM 패턴에서 지칭되는 Model은 일반적으로 비지니스 로직 표현과 데이터를 저장하기 위한 공간, 데이터베이스나 API 같은 서버와의 통신에서 비즈니스 로직의 응답을 처리하기 위한 연결 고리 역할을 한다. 즉, View가 화면에 그려줘야 할 것들을 알려주는 Entity로 정의되었다.
    - 반면에 MVI 패턴에서 Model은 데이터를 가지고 있으며 또한, UI의 상태를 나타낸다. 예를 들어 UI는 Data Loading, Loaded, Change in UI with User Action, Error 등 다양한 상태를 가질 수 있다.
    - 즉, Model은 상태에 대해 뷰가 어떤 것을 화면에 렌더링 해야 하는지를 말해주는 응답이다.
- 아래의 코드처럼 Model을 데이터가 아닌 상태를 나타내도록 한다. 이런 식으로 Model을 정의해 준다면 View, ViewModel 등 여러 곳에서 상태를 관리해 줄 필요가 없어진다.

```kotlin
sealed class MainState {
    object Idle : MainState()
    object Loading : MainState()
    data class Users(val user: List<User>) : MainState()
    data class Error(val error: String?) : MainState()
}
```

<br/>

### View
- UI 그 자체다. View, Activity, Fragment, Compose 등이 될 수 있다.
- 새로운 State를 받아 화면에 표시하는 로직이 정의된 곳이다.
- 사용자 상호 작용에 대한 결과로 이벤트를 발생시켜 Intent에 전달한다.

<br/>

### Intent
- 사용자 액션 및 시스템 이벤트에 따른 결과
- Intent는 앱의 상태를 바꾸려는 의도를 의미한다.
- 사용자의 버튼 클릭 등을 통한 모든 UI의 변화는 Intent 함수의 결과로 동작한다.
- 이를 통해 앱에서 진행 중인 작업에 대해 더 명확하게 이해할 수 있다.
- 사용자 또는 앱 내 발생하는 Action을 나타낸다.
- 모든 Action에 대해 View는 Intent를 수신한다. Presenter는 Intent를 관찰하고 Model은 새로운 상태로 변환한다.

> MVI의 Intent는 android.content.Intent를 의미하지 않는다. MVI의 Intents는 앱의 상태를 변화시킬 액션을 의미한다.
> 

<br/>

아래 그림은 MVVM 계층 관점에서 MVI가 어느 계층에 속하는지 보여 준다.

![https://www.charlezz.com/wordpress/wp-content/uploads/2022/12/www.charlezz.com-android-mvi--2022-12-28--11.14.22-1024x578.png](https://www.charlezz.com/wordpress/wp-content/uploads/2022/12/www.charlezz.com-android-mvi--2022-12-28--11.14.22-1024x578.png)

<br/>
<br/>

# ✅ MVI 패턴의 기존 패턴의 문제 해결 방법
- MVI에서 상태는 불변한다. 이 말은 View를 업데이트 하기 위해서는 Intent()를 사용해 이벤트를 발생시켜 그에 따라 새로운 상태를 생성해 적용하는 것이 상태를 변경하기 위한 유일한 방법이다.
- 또한 Model은 현재 뷰 상태에 대한 변경 불가능한 단일 소스(Single Source Of Truth)이므로 상태가 겹치지 않는다.
- Single Source Of Truth로 비즈니스 로직을 유지하기 위해 Model은 불변성을 지니고 있어야 한다. 이 방식은 앱의 전체 생명 주기 동안 단일 상태를 유지할 수 있게 된다.
- 불변성을 가지고 있다는 의미는 Model을 수정할 수 없기 때문에, 내부의 property는 바꾸지 못하고 Model 자체를 copy() 메소드를 사용해서 새로 생성하는 방법을 사용한다.

<br/>

Model이 Mutable하다면 아래의 메서드를 호출해 앱의 상태를 쉽게 바꿀 수 있다.

```kotlin
viewModel.insert(items)
```

<br/>

Immutable하다면 앱의 상태를 바꾸기 위해서 매번 새로운 Model을 만들어야 하는데, 만약 이전 상태에 대한 정보가 필요하다면?

<br/>

## State Reducer
- State Reducer는 이전 상태를 입력으로 받아 다음과 같이 이전 상태에서 새 상태를 계산하는 Reactive Programming의 개념이다.
- 이 아이디어는 reduce() 메소드가 이전 상태를 foo와 결합하여 새 상태를 계산한다는 것이다.
- State Reducer의 컨셉은 반응형 프로그래밍의 Reducer 함수로부터 유래되었다. Reducer 함수는 우리에게 데이터를 합치고, 누적해 주는 기능을 제공하기 때문에 편리하게 쓸 수 있고, 대부분의 표준 라이브러리들은 불변 객체 구조를 위해 reducer와 비슷한 메소드가 구현되어 있다.

```java
public State reduce( State previous, Foo foo ){
  State newState;
  // ... compute the new State by taking previous state and foo into account ...
  return newState;
}
```

<br/>

Kotlin의 List는 reduce()라는 메소드를 포함하고 있는데, 리스트의 처음 요소부터 시작하여 값을 누적하는 기능을 가지고 있다.

```kotlin
val myList = listOf(1, 2, 3, 4, 5)

// accumulator : 누적된 총 값, 
// currentValue : iterator 를 통해 들어온 현재 위치의 value
var result = myList.reduce { accumulator, currentValue ->
  println("accumulator = $accumulator, currentValue = $currentValue")
  accumulator + currentValue }
println(result)

// result
accumulator = 1, currentValue = 2
accumulator = 3, currentValue = 3
accumulator = 6, currentValue = 4
accumulator = 10, currentValue = 5
```

<br/>

- State Reducer와 MVI 패턴이 가지고 있는 관계    
    **Tying It All Together.** 값들을 함께 묶을 수 있다는 점이다. State Reducer는 reducer 함수와 동작이 매우 비슷하다. 주요 차이점은 State Reducer는 과거 상태에 기반하여, 새로운 상태를 만들며 변경 사항을 유지하면서 현재 상태를 만들지만, reduce 함수는 일반적으로 collection 함수 내부에서 모든 행위가 이루어진다는 점이다.     
    이 과정은 Rxjava를 사용하여 아래와 같이 만들 수도 있을 것이다.
    
<br/>

- State Reducer를 RxJava를 사용하여 리팩터링 한다면
    1. 앱의 새로운 상태를 나태내는 PartialState라는 새로운 상태가 필요하다.
    2. 이전 상태 정보가 필요한 새로운 Intent가 있을 때, 완료된 상태로부터 새로운 PartialState를 만든다.
    3. reduce() 메서드에서 이전 상태와 PartialState를 사용하여 화면에 표시할 새로운 상태로 merge한다.
    4. RxJava의 scan() 메서드를 사용하여 앱의 초기 상태에 reduce() 메서드를 적용하고, 새 상태를 반환한다.

<br/>
<br/>

# ✅ MVI의 흐름
![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/HwymB/btrfU2QlhrQ/yqYU8VzkB3PEJWl6NZ0bL0/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/HwymB/btrfU2QlhrQ/yqYU8VzkB3PEJWl6NZ0bL0/img.png)

<br/>

1. 사용자가 의도(Intent)가 될 행동(Action)을 수행.
2. Intent는 Model에 대한 입력인 상태.
3. Model은 상태를 저장하고 요청된 상태를 View에 보낸다.
4. View는 Model로부터 상태(State)를 로드.
5. 사용자에게 표시한다. 만약 관찰하고 있다면 데이터의 흐름은 항상 사용자로부터 오고 Intent를 통해 사용자와 함께 끝난다.
6. 다른 방식으로는 불가능하기 때문에 단방향(Unidirectional) 아키텍처. 여기서 사용자가 한 번 더 작업을 수행하면 동일한 주기가 반복되므로 순환(Cyclic).

<br/>

### 예시

![https://miro.medium.com/max/1400/1*v8KIUJ1lssii9HhWXBdLFg.png](https://miro.medium.com/max/1400/1*v8KIUJ1lssii9HhWXBdLFg.png)

<br/>

- 위의 예시를 보면 Intent(Increase) 이벤트를 발생시키면 기존 count 값에 + 1을 해 새로운 상태를 생성한다.
- 그리고 새로운 상태를 화면에 render()한다.
- 사용자가 또 다른 이벤트를 발생시킨다면 같은 순환(Circular)을 거친다.
- MVI에서 상태는 불변성을 가지기 때문에 예상 가능한 값을 얻을 수 있다. 부수 효과가 발생하지 않는 함수형 프로그래밍의 장점이 반영된다.

<br/>

### 순수 함수로 이루어진 Cycle 예시

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/mKaiG/btrfXH5pRBM/DiG9gaCxRm5FAqx3U1oKH1/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/mKaiG/btrfXH5pRBM/DiG9gaCxRm5FAqx3U1oKH1/img.png)

<br/>

- 위의 순수 함수로 이루어진 Cycle을 통해서는 API 콜, 데이터 베이스 작업 등에서 발생하는 부수 효과를 피하기는 힘들다.
- 그래서 기존 Cycle에 Side Effect가 추가되었다. Intent()를 사용해 새로운 상태를 생성함과 동시에 부수 효과를 실행(Dispatch)한다. 실행이 끝났다면 결과를 바로 render()하는 것이 아니라 Event로써 결과를 전달한다.
- 부수 효과의 결과를 Event로 전달한다. 이는 부수 효과의 결과를 성공적으로 전달받았다면, 그 데이터를 특정한 이벤트를 통해 상태에 적용할 수 있다.

<br/>

## 이런 흐름을 유지한다면?
모델의 불변성과 레이어 간의 순환 구조 덕분에 다음과 같은 이점을 얻을 수 있다.

<br/>

### Single State
Immutable한 데이터 구조는 한 곳에서만 데이터를 관리할 수 있다는 이점을 가져 관리하기 유용하고, 앱의 모든 레이어에서 단일 상태를 보장한다.

<br/>

### Thread Safety
비동기 처리를 위한 라이브러리(RxJava, Coroutines)를 사용할 때, 어떤 함수도 모델을 수정할 수 없기 때문에 모델은 항상 한 곳에서 다시 만들어지고 유지된다. 이런 점이 다른 스레드에서 모델을 수정하여 일어나는 충돌을 방지한다.

<br/>
<br/>

# ✅ MVI의 장단점
## MVI의 장점
- 상태에 초점을 맞추기 때문에 상태를 유지하는 더 이상 문제 되지 않고 상태의 충돌이 없다.
- 단방향 데이터 흐름을 통해 앱의 로직을 명확하게 이해하고 쉽게 추적 및 예측할 수 있다.
- 상태 개체는 변경할 수 없으므로 스레드 안정성을 보장.
- 디버그하기 쉽고 오류가 발생했을 때 개체의 상태를 알고 있다.
- 각 구성 요소가 자체 책임을 수행함에 따라 결합도가 낮아진다.

<br/>

## MVI의 단점
- 각 사용자 작업에 대한 상태를 유지하고, 모든 상태에 대한 많은 객체를 생성해야 하므로 많은 상용구 코드로 이어진다.
- 단일 이벤트 문제가 발생. 예를 들어 Toast, SnackBar 메시지 등. 이 또한 상태로 접근하게 되는데, 메시지를 출력하고 다시 상태를 변경하지 않는다면 다른 이벤트가 발생할 때마다 메시지가 출력되는 문제가 발생한다. 이를 위해 SingeLiveEvent 등의 방법이 필요.
- 러닝 커브가 높을 수 있다.

<br/>
<br/>

# 🗂 참고
- [Android) MVI 아키텍처 살펴보기 :: 알면 쓸모있는 개발 지식 (tistory.com)](https://yoon-dailylife.tistory.com/117)
- [아직도 MVVM? 이젠 MVI 시대!. Orbit을 이용한 MVI 디자인패턴 알아보기 | by jisungbin | 성빈랜드](https://sungbin.land/%EC%95%84%EC%A7%81%EB%8F%84-mvvm-%EC%9D%B4%EC%A0%A0-mvi-%EC%8B%9C%EB%8C%80-319990c7d60)
- [Android 프로젝트에 MVI 도입하기 | 찰스의 안드로이드 (charlezz.com)](https://www.charlezz.com/?p=46365)
- [Android 에서 등장한 MVI Architecture (velog.io)](https://velog.io/@jshme/MVI-Architecture-for-Android)
- [[번역] 안드로이드를 위한 MVI (Model-View-Intent) 아키텍쳐 튜토리얼: 시작하기 | by Jaeho Choe | Medium](https://jaehochoe.medium.com/%EB%B2%88%EC%97%AD-%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C%EB%A5%BC-%EC%9C%84%ED%95%9C-mvi-model-view-intent-%EC%95%84%ED%82%A4%ED%85%8D%EC%B3%90-%ED%8A%9C%ED%86%A0%EB%A6%AC%EC%96%BC-%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-165bda9dfbe7)
