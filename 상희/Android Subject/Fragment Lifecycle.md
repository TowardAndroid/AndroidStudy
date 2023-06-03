# 💡 Fragment Lifecycle

# ✅ Fragment
프래그먼트를 사용하면 화면 하나를 독립적으로 작동하는 부분 화면 여러 개로 구현할 수 있다.  
프래그먼트는 액티비티처럼 정의된 레이아웃을 표시하고, 자체 생명 주기를 가지며 입력 이벤트를 받을 수 있다.  
하지만 독립적으로 존재할 수 없고, 해당 프래그먼트를 관리하는 호스트 액티비티나 프래그먼트 하위에서만 존재할 수 있다.

<br/>

## Advantages
### Lightweight
액티비티는 안드로이드 4대 컴포넌트 중 하나로 안드로이드 시스템에서 관리한다. 반면 프래그먼트는 안드로이드 시스템이 직접 관리하지 않고 프래그먼트 매니저가 관리하기 때문에 메모리 리소스가 상대적으로 덜 소모되어 액티비티보다 가볍다.

<br/>

### Reusability
한 번 작성된 프래그먼트는 여러 액티비티에서 재사용이 가능하며, 따라서 UI 구현에 필요한 작업량을 상당히 감소시킬 수 있다.

<br/>
<br/>

# ✅ Fragment Lifecycle
프래그먼트의 생명 주기는 아래 그림과 같다.  
![https://developer.android.com/static/images/guide/fragments/fragment-view-lifecycle.png](https://developer.android.com/static/images/guide/fragments/fragment-view-lifecycle.png)

<br/>

위의 그림은 안드로이드 공식 문서에서 제공하는 것으로 프래그먼트 자체와 프래그먼트 뷰의 생명주기를 구분해서 표현하고 있다.  
실제로 프래그먼트 자체와 프래그먼트 뷰는 생성되고 소멸되는 시기가 다르기 때문에 이를 잘 인지해서 프로그램을 작성해주지 않으면 메모리 릭에 빠지거나 앱이 터질 수가 있다.
  - ex : 뷰가 생성되지 않았을 때 뷰를 참조하는 실수를 할 수도 있다.

<br/>

## onAttach() & onCreate()
### Fragment CREATED
CREATED 상태에 있을 때, 프래그먼트는 FragmentManager에 추가되며 onAttach()와 onCreate()가 차례대로 호출된다.  
onAttach()에서는 프래그먼트가 호스트 액티비티에 attach되고, onAttach()에서 작업이 성공적으로 이루어지면 onCreate()에서 프래그먼트 자체가 생성된다. 이때 프래그먼트 뷰는 아직 생성되지 않은 상태이므로 뷰와 관련된 작업을 onCreate() 내부에 하는 것은 적절하지 않다.

<br/>

#### onAttach()
프래그먼트가 호스트 액티비티에 attach된다.

<br/>

#### onCreate()
프래그먼트 자체가 생성된다.

<br/>

## onCreateView() & onViewCreated()
### Fragment CREATED and View INITIALIZED
onCreateView()에서 프래그먼트 뷰가 초기화된다. 이때 레이아웃을 inflate 하기 때문에 findViewById() 또는 View Binding을 사용해서 다른 뷰들을 참조할 수도 있지만, 종종 레이아웃이 제대로 초기화가 되지 않을 수도 있다.  
onViewCreated()는 onCreateView()에서 정상적인 프래그먼트 뷰 객체가 반환된 직후에 호출되며 뷰가 완전히 생성되었음을 보장한다. 따라서 뷰에 대한 참조 및 작업은 뷰가 완전히 생성된 이후인 onViewCreated()에서 하는 것이 더 안전하다.

<br/>

#### onCreateView()
프래그먼트 뷰가 초기화되며, 정상적으로 초기화가 되었다면 뷰 객체를 반환한다.

<br/>

#### onViewCreated()
onCreateView()에서 뷰 객체가 반환된 직후에 호출되며, 뷰가 완전히 생성되었음을 보장한다.

```kotlin
class MainFragment : Fragment(){ 

    private lateinit var binding : FragmentMainBinding
    private val viewModel : ViewModel by inject()

   	override fun onCreateView(
        inflater: LayoutInflater,
        container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View {
        binding = FragmentMainBinding.inflate(inflater)        
        return binding.root
    }
    
    override fun onViewCreated(view: View, savedInstance: Bundle?){
        super.onViewCreated(view, savedIntanceState)
    
        binding.btn.setOnClickListener {
            ...
        }
        
        viewModel.getAll().observe(viewLifecycleOwner, Observer{
            ...
        })
    }
}
```

<br/>

## onViewStateRestored()
### Fragment and View CREATED
onViewStateRestored()은 저장해 둔 모든 state 값이 프래그먼트 뷰의 계층 구조에 복원되었을 때 호출되며 따라서 각 뷰의 상태 값을 체크할 수 있다.  
- ex : 체크박스가 현재 체크되어 있는지

onStart() ~ onDestroy() (onDestroyView() 제외)까지는 액티비티의 생명 주기와 유사하다.

<br/>

## onStart()
### Fragment and View STARTED
사용자에게 프래그먼트가 보이게 되고, childFragmentManager를 통해 FragmentTransaction을 안전하게 수행할 수 있다.

<br/>

## onResume()
### Fragment and View RESUMED
사용자와 프래그먼트가 상호작용 할 수 있는 상태로 프래그먼트가 보이는 상태에서 모든 Animator와 Transition 효과가 종료된 후 호출된다.

<br/>

## onPause()
### Fragment and View STARTED
사용자가 프래그먼트를 떠났지만 기존 프래그먼트가 조금이라도 보일 때 호출된다. 이 때 프래그먼트와 프래그먼트 뷰의 생명주기는 PAUSED가 아닌 STARTED 상태가 된다.

<br/>

## onStop()
### Fragment and View CREATED
프래그먼트가 더이상 보이지 않을 때 호출된다. onStop()은 호스트 액티비티나 프래그먼트가 중단되었을 뿐만 아니라 이들의 상태가 저장될 때도 호출된다.  
API 레벨 28 이후 onSaveInstanceState()와 onStop() 호출 순서가 달라졌고, 따라서 onStop()이 FragmentTransaction을 안전하게 수행하는 마지막 지점이 되었다.

<br/>

## onDestroyView()
### Fragment CREATED and View DESTROYED
프래그먼트의 뷰가 소멸될 시 호출된다. 이 때 프래그먼트 자체는 아직 메모리에 남아 있으므로 프래그먼트 뷰에 대한 모든 참조를 제거해야 메모리 누수를 방지할 수 있다. 따라서 만약 View Binding을 사용하고 있다면 onDestroyView()에서 binding 변수를 null로 만들어 주는 것이 좋다. (사실 View Binding을 안전하게 해제하기 위해선 이 방법 말고 다른 방법을 사용하는 것이 좋다.)

<br/>

#### onDestroyView()
프래그먼트 뷰가 소멸된다.

```kotlin
override fun onDestroyView() {
    super.onDestroyView()
    binding = null
}
```

<br/>

## onDestroy()
### Fragment DESTROYED
프래그먼트 또는 프래그먼트 매니저가 소멸되었을 경우 호출되며 onDestroy()가 호출되었다는 것은 프래그먼트의 생명 주기도 종료되었다는 것을 의미한다.

<br/>

#### onDestroy()
프래그먼트 자체가 소멸된다.

<br/>
<br/>

# 🗂 참고
- [책] 깡샘의 안드로이드 프로그래밍
- [프래그먼트 라이프사이클 | Android 개발자](https://developer.android.com/guide/fragments/lifecycle)
- [[Android] Fragment Lifecycle (velog.io)](https://velog.io/@jeongminji4490/Android-Fragment-Lifecycle)
- [[Android] 의외로 잘 모르는 Fragment 의 Lifecycle :: 준비된 개발자 (tistory.com)](https://readystory.tistory.com/199)
