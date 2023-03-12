# 💡 AAC

# ✅ AAC란?
AAC(Android Architecture Components)는 테스트와 유지 보수가 쉬운 앱을 디자인할 수 있도록 돕는 라이브러리의 모음이다.

<br/>

Google I/O 2017에서 새로운 라이브러리를 AAC로 묶어서 발표를 하여 AAC라는 것이 사용되게 되었고,  
Google I/O 2018에서 Android Jetpack을 발표할 때는 Jetpack의 구성 요소 중 하나로 AAC가 들어가 있다.

<br/>

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/bMk7kC/btrDxpmTmlo/daWm7VbPDJEXU6CBnCLeqK/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/bMk7kC/btrDxpmTmlo/daWm7VbPDJEXU6CBnCLeqK/img.png)

<br/>

Google I/O 2018의 발표 자료를 보면 다음과 같은 이미지를 확인할 수 있는데, 여기서 Architecture 부분이 AAC라고 볼 수 있다.  
New로 붙어있는 것들이 Jetpack에서 추가된 AAC이고, 그렇지 않은 부분이 2017년도 Google I/O에서 발표된 AAC라고 생각하면 된다.

<br/>

![https://velog.velcdn.com/images/hwi_chance/post/f8773023-1064-4259-b0e6-65eced0e2210/final-architecture.png](https://velog.velcdn.com/images/hwi_chance/post/f8773023-1064-4259-b0e6-65eced0e2210/final-architecture.png)

<br/>

AAC는 2017년도에 발표한 5개의 라이브러리로  
- Lifecycles(Easy handling lifecycles)    
    : 앱의 수명 주기를 관리    
- LiveData(Lifecycle aware observable)    
    : 기본 데이터베이스가 변경되면 뷰에 알리는 데이터 객체 빌드    
- ViewModel(Managing data in a lifecycle)    
    : 앱 회전 시 제거되지 않는 UI 관련 데이터 저장    
- Room(object Mapping for SQLite)    
    : SQLite 개체 매핑 라이브러리    
- Paging(Gradually loading information)    
    : 페이징 기법을 쉽게 적용    
- Databinding    
    : 프로그래매틱 방식이 아닌 선언적 형식으로 UI 구성 요소를 앱의 데이터 소스와 매핑    
- Navigation    
    : 프래그먼트의 진행을 보기 쉽게 정리해 준다.    
- WorkManager    
    : 지연 가능한 비동기 작업을 쉽게 예약할 수 있는 API    

다음과 같이 구성되어 있다.

<br/>
<br/>

# ✅ AAC ViewModel
## MVVM 패턴의 ViewModel과 AAC의 ViewModel

> AAC에서 말하는 ViewModel과 MVVM 패턴에서의 ViewModel은 ViewModel이라는 이름만 같을 뿐, 전혀 다른 것이다.
> 

<br/>

### MVVM 패턴의 ViewModel
- MVP 패턴에서 파생된 패턴으로, 비즈니스 로직과 프레젠테이션 로직을 UI로부터 분리하는 것을 목표로 사용된다. View와 Model 사이의 의존성을 없애 테스트, 유지 보수, 재사용성을 높인다.
- ViewModel은 쉽게 말해서, 뷰와 모델 사이에서 데이터를 관리하고, 바인딩해 주는 역할을 하게 된다.
- MVVM에서의 ViewModel은 View가 ViewModel에서의 값을 Observe하여 Update하고, ViewModel은 Model을 Update하는 역할을 담당한다.

<br/>

### AAC의 ViewModel
- [안드로이드 공식 문서](https://developer.android.com/topic/libraries/architecture/viewmodel)에 따르면 수명 주기를 고려하여 UI 관련 데이터를 저장하고 관리하도록 설계되어 있다, 화면 회전과 같이 구성을 변경할 때도 데이터를 유지할 수 있다, 라고 나와있다.
- 화면 회전이 발생했을 때 액티비티가 종료되고 다시 생성되는 과정을 거치는데, 이때 생명 주기를 관리하여 데이터를 유실하지 않고 그대로 보존해 두고 사용할 수 있게 해 준다.
- Activity/Fragment당 하나의 ViewModel만 생성 가능하다.
- 메모리 누수, 화면 회전과 같은 상황에서도 Data를 저장할 수 있다.

<br/>

AAC에서의 ViewModel은 간단하게 생각해서 LifeCycle을 관리하여 화면을 회전했을 때 데이터를 유실하지 않고 사용할 수 있게 해주는 역할, MVVM에서의 ViewModel은 뷰와 모델 사이에서 데이터를 관리하고 바인딩해 주는 역할로 둘은 완전히 다르다.

<br/>

### MVVM 패턴에서의 AAC의 ViewModel
MVVM 패턴의 예제를 확인해보면, AAC의 ViewModel을 사용하여 구현하고 있는 모습을 볼 수 있다.  
MVVM에서의 ViewModel은 그러한 역할을 하는 Class를 만들어서 구현할 수 있다.  
여기서 중요한 것은, MVVM에서의 ViewModel이라고 하는 것은 그러한 역할을 하는 클래스라는 점이다.  
즉, AAC의 ViewModel에 MVVM의 ViewModel이 해야 하는 역할을 준다면 AAC ViewModel이면서 MVVM의 ViewModel이 될 수 있다.  
AAC의 ViewModel은 화면 회전과 같은 이벤트에서도 데이터가 유실되지 않고 그대로 사용할 수 있으니 오히려 더 좋은 환경에서 MVVM의 ViewModel을 만들 수 있게 되는 셈이다.

<br/>

**MVVM 패턴에서의 ViewModel과 AAC에서의 ViewModel의 차이점**  
- AAC의 ViewModel은 해당 액티비티에서 싱글톤으로 하나만 존재한다.
    - 따라서 여러 번 ViewModel을 생성하여 사용한다고 해도, 싱글톤이기 때문에 최초에 생성한 하나의 객체만 사용하게 된다.
- MVVM에서 View와 ViewModel은 1:N 관계이기 때문에 하나의 액티비티에 여러 개의 ViewModel을 사용할 수 있다.
    - 따라서 A라는 액티비티에 AViewModel, BViewModel, CViewModel과 같이 여러 개의 ViewModel을 사용할 수 있으며, AAC ViewModel의 특성상 각 ViewModel은 싱글톤으로 생성되어 사용하게 되는 것이다.
    - 하지만 구글에서 권장하는 ViewModel은 하나의 액티비티에 하나의 ViewModel을 사용하고, LiveData와 여러 개의 Model을 사용하여 구현하는 것을 권장하고 있다. 개발자가 판단하여 프로젝트에 알맞게 ViewModel을 선언해서 사용하면 될 것이다.

<br/>

## AAC ViewModel
- 안드로이드 생명 주기를 고려해서 만들어진 ViewModel이다.
    - Activity/Fragment당 하나의 ViewModel만 생성 가능하다.
    - 메모리 누수, 화면 회전과 같은 상황에서도 Data를 저장할 수 있다.

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/KfCgk/btrnHS7ds66/Ieo5zkpaGBGzV022H7eVv1/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/KfCgk/btrnHS7ds66/Ieo5zkpaGBGzV022H7eVv1/img.png)

> 화면 회전 상황에서 AAC ViewModel과 Activity의 생명 주기
> 

Activity Scope ViewModel의 경우에는 화면 회전에서도 살아있는 것을 알 수 있다. (Fragment Scope의 경우에는 화면 회전에서 자유롭지 못한 것 같다. 물론 Manifest에서 ConfigureChange 속성을 사용하면 될 것 같다.)

<br/>

- UI 관련 요소를 저장하고 관리한다.
    - 따라서 Activity Scope의 ViewModel을 하나 만들어 놓으면 해당 Activity 위에 존재하는 Fragment들은 데이터를 쉽게 공유할 수 있게 된다.

<br/>

- ViewModel이 로더 역할을 대체할 수 있다.

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/A7edd/btrnJAZsBJz/9Enzz7JgTLfAXSTmlljQSk/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/A7edd/btrnJAZsBJz/9Enzz7JgTLfAXSTmlljQSk/img.png)

> 로더를 사용한 데이터 로드 & UI 업데이트 로직
> 

<br/>

원래는 로더를 사용해서 데이터를 로드하고, 로더 매니저가 콜백을 통해서 UI Controller에게 알려 주면 UI Controller가 그 때 반응해서 UI를 업데이트 시켰다.

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/btkt8e/btrnClvzsWO/UredyrsnGDzHpkjT9ReAik/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/btkt8e/btrnClvzsWO/UredyrsnGDzHpkjT9ReAik/img.png)

> ViewModel을 사용한 데이터 로드 & UI 업데이트 로직
> 

<br/>

ViewModel을 사용하면 UI Controller는 ViewModel(LiveData)을 Observe하다가 값이 업데이트되면 그 때 UI를 업데이트하면 된다. 즉, UI 컨트롤러는 데이터 로드 작업에서 분리되므로 클래스 간 의존성이 사라지게 된다.

<br/>

- 코루틴을 공식적으로 지원한다.
    - 자세한 정보는 아래를 참조하면 된다.
        - [수명 주기 인식 구성요소와 함께 Kotlin 코루틴 사용  |  Android 개발자  |  Android Developers](https://developer.android.com/topic/libraries/architecture/coroutines?hl=ko)

<br/>

> AAC ViewModel을 사용한다 해서 MVVM 패턴이 되는 것은 아니다.  
> 그러나 AAC ViewModel을 MVVM 패턴으로 구현할 수 있기 때문에(LiveData, Flow 등 사용) AAC ViewModel로 MVVM 패턴을 구현하면, 생명 주기를 고려한 MVVM 패턴을 만들 수 있게 된다.
> 

<br/>
<br/>

# 🗂 참고
- [[Android] 안드로이드 AAC (velog.io)](https://velog.io/@hwi_chance/Android-%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-AAC)
- [안드로이드 AAC(Android Architecture Components)란? (velog.io)](https://velog.io/@heetaeheo/%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-AAC)
- [[Android] 안드로이드 AAC & MVVM (tistory.com)](https://hanyeop.tistory.com/167)
- [[Android] AAC (Android Architecture Components) 란 ? (Feat. ViewModel) (tistory.com)](https://heegs.tistory.com/m/119)
- [[Kotlin] 안드로이드 AAC ViewModel과 앱 아키텍처 가이드 (feat. SharedPreferences) - 여러 Fragment에서 AAC ViewModel 공유해서 사용하기. — For Better Code Tomorrow (tistory.com)](https://kimyunseok.tistory.com/152)
