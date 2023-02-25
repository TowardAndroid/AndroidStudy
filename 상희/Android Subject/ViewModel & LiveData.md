# 💡 ViewModel & LiveData

# ✅ ViewModel이란?
- ViewModel 클래스는 UI 관련 데이터를 저장하고 관리하기 위해 설계되었다. 안드로이드 프레임워크는 특정 사용자 동작 또는 사용자 제어에서 완전히 벗어난 장치 이벤트에 대한 응답으로 UI 컨트롤러를 파괴하거나 re-create 하도록 한다.
- 사용하기 위해서는 ViewModel이 Abstract class라 별도의 클래스를 하나 만들고 ViewModel을 상속받는다.
- MVVM 패턴에서 수명 주기를 고려하여 데이터를 저장하고 관리한다.
- 회전 등의 화면 변화가 있을 때에도 데이터를 유지한다.
- ViewModel 객체는 자동 보관되어 다른 Activity나 Fragment에서도 사용할 수 있다.

<br/>

ViewModel을 사용하면 화면이 변경될 때 onSaveInstanceState() 등의 활용 없이 데이터를 보관하여 유지할 수 있다.

<br/>

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/cY7ZWE/btq2TcZvug2/gLFh33xBcVckbOYDkHd5pK/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/cY7ZWE/btq2TcZvug2/gLFh33xBcVckbOYDkHd5pK/img.png)

<br/>

ViewModel은 액티비티가 종료될 때 까지 유지된다.  
하지만 Lifecycle 또는 view, activity context를 참조하면 메모리 누수가 발생하므로, 이러한 객체를 참조해서는 안된다.

<br/>

또한 LiveData와 같은 LifecycleObserver들을 포함할 수 있지만, LiveData와 같이 수명 주기를 인식하는 Observable의 변경 사항을 관찰하면 안 된다.

<br/>

context가 필요하다면 AndroidViewModel을 상속하여 application 생성자를 사용하면 된다.

<br/>

즉, ViewModel은 생명 주기의 영향을 받지 않고 데이터를 유지, 보관하기 위해 사용한다고 볼 수 있다.  
또한 UI와 컨트롤러가 분리되고, 다른 액티비티와 프래그먼트 간의 데이터 공유가 쉬워지는 장점도 있다.

<br/>

## ViewModel 사용 시 이점
ViewModel을 이용하면, UI와 내부 로직을 분리할 수 있고, 리소스 관리가 용이해져 메모리를 관리하는데 간편하다는 장점이 있다. UI 컨트롤러 로직에서 뷰 데이터 소유권을 분리하는 것이다. Activity/Fragment Lifecycle을 따라 동작하는데 생성된 시점에서 Activity/Fragment가 finish() 되기 전까지 데이터를 유지하는 기능을 가지고 있다.

<br/>
<br/>

# ✅ LiveData이란?
- Android JetPack 라이브러리의 하나의 기능
- LiveData는 Data의 변경을 관찰할 수 있는 Data Holder 클래스이다.
- 관찰자(액티비티, 프래그먼트)의 생명 주기를 알고 있는 간단한 Observable
    - 일반적인 Observable과는 다르게 LiveData는 안드로이드 생명 주기(Lifecycle)을 알고 있다. (Lifecycler-Aware)
    - 즉, 액티비티나 프레그먼트, 서비스 등과 같은 안드로이드 컴포넌트의 생명 주기(Lifecycle)를 인식하며 그에 따라 LiveData는 활성 상태(Active)일 때만 데이터를 업데이트(Update)한다.
    - 활성 상태란 STARTED 또는 RESUMED를 의미한다.
- LiveData 객체는 Observer 객체와 함께 사용된다.
    - LiveData가 가지고 있는 데이터에 어떠한 변화가 일어날 경우, LiveData는 등록된 Observer 객체에 변화를 알려주고, Observer의 onChanged() 메서드가 실행되게 된다.
- Observer 패턴을 구현하기 위하여 사용된다.
- 보통 ViewModel과 함께 사용된다.
- 수명 주기를 수동으로 처리하지 않아도 되고, 메모리 누수가 사라진다.

<br/>

## LiveData가 어떻게 생명 주기를 아는가?
LifeCycleOwner가 안드로이드 생명 주기(Android LifeCycle)를 알고 있는 클래스라 보면 된다.  
메서드가 오직 getLifeCycle()밖에 없는 단일 메서드 인터페이스 클래스이며, Activity나 Fragment에서 이를 상속하고 있다.  
한 마디로 LiveData의 Observer 메서드의 LifeCycleOwner를 Activity나 Fragment를 변수로써 사용한다면 각 화면별 생명 주기에 따라 LiveData는 자신의 임무를 수행한다.

<br/>

> LifecycleOwner의 getLifeCycle() 메서드를 통해 현재의 Lifecycle을 가져올 수 있어 상태 체크가 가능하다.
> 

<br/>

## LiveData 장점
- Data와 UI 간 동기화    
    : LiveData는 Observer 패턴을 따른다. 그에 따라 LiveData는 안드로이드 생명 주기에 데이터 변경이 일어날 때마다 Observer 객체에 알려 준다.
    그리고 이 Observer 객체를 사용하면 데이터의 변화가 일어나는 곳마다 매번 UI를 업데이트하는 코드를 작성할 필요 없이 통합적이고 확실하게 데이터의 상태와 UI를 일치시킬 수 있다.    
- 메모리 누수(Memory Leak)가 없다.    
    : Observer 객체는 안드로이드 생명 주기 객체와 결합되어 있기 때문에 컴포넌트가 Destroy될 경우 메모리상에서 스스로 해제한다.    
- Stop 상태의 액티비티와 Crash가 발생하지 않는다.    
    : 액티비티가 Back Stack에 있는 것처럼 Observer의 생명 주기가 inactive(비활성화)일 경우, Observer는 LiveData의 어떤 이벤트도 수신하지 않는다.    
- 생명 주기에 대한 추가적인 handling을 하지 않아도 된다.    
    : LiveData가 안드로이드 생명 주기에 따른 Observing을 자동으로 관리를 해 주기 때문에 UI 컴포넌트는 그저 관련있는 데이터를 "관찰"하기만 하면 된다.    
- 항상 최신 데이터를 유지한다.    
    : 화면 구성이 변경되어도 데이터를 유지한다.
    예를 들어, 디바이스를 회전하여 세로에서 가로로 화면이 변경될 경우에도 LiveData는 회전하기 전의 최신 상태를 즉시 받아온다.    
- 자원(Resource)을 공유할 수 있다.    
    : LiveData를 상속하여 자신만의 LiveData 클래스를 구현할 수 있고 싱글톤 패턴을 이용하여 시스템 서비스를 둘러싸면(Wrap) 앱 어디에서나 자원을 공유 할 수 있다.
    
<br/>

## LiveData 사용 시 주의할 점
LiveData 객체를 사용하기 위해서는 다음 내용을 알고 있으면 된다.

<br/>

- Generic을 사용해 관찰하고자 하는 데이터의 타입(Type)을 갖는 LiveData 인스턴스를 생성한다. (보통 LiveData 객체는 안드로이드 아키텍처 패턴의 ViewModel 클래스 내에서 함께 사용된다.)
- LiveData 클래스의 observe() 메소드를 사용해 Observer 객체를 LiveData 객체에 "결합"한다. 이 때 observe() 메소드는 LifecycleOwner 객체를 필요로 하며 보통은 Activity를 전달한다.  
  LiveData에 저장된 데이터에 어떠한 변화가 일어난 경우, 결합된 LifecycleOwner에 의해서 상태가 active(활성)인 한 모든 데이터에 대해 Trigger가 발생한다.
- Observer 객체를 생성한다.  
  생성 시 LiveData가 들고 있는 데이터가 변화가 일어났을 때 수행해야 할 로직이 들어있는 onChanged() 메서드를 정의해야 한다.  
  보통은 액티비티나 프래그먼트 같은 UI Controller 내에서 해당 메서드를 생성한다.
- observeForever(Observer)를 통해 LifeCycleOwner 없이 Observer를 생성하여 등록할 순 있지만, 이 경우에는 Observer는 항상 active(활성) 상태이므로 데이터 변화를 항상 전달받는다. 단, removeObserver(Observer) 메소드를 통해 Observer를 제거할 수 있다.

<br/>
<br/>

# 🗂 참고
- [Android-Study/livedata-viewmodel.md at master · taeiim/Android-Study (github.com)](https://github.com/taeiim/Android-Study/blob/master/study/week09/livedata-viewmodel.md)
- [[Android] LiveData + ViewModel 사용해보기 - Junghoon's Blog (junghun0.github.io)](https://junghun0.github.io/2019/05/22/android-viewmodel/)
- [[Android] 안드로이드 ViewModel, LiveData (+DataBinding) (tistory.com)](https://hanyeop.tistory.com/168)
- [[Android] LiveData...넌 누구냐? (velog.io)](https://velog.io/@jojo_devstory/Android-LiveData...%EB%84%8C-%EB%88%84%EA%B5%AC%EB%83%90)
