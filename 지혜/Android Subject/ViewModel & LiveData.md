# viewmodel & livedata

### viewModel클래스

비즈니스 로직 또는 화면 수준 상태 홀더 

ui 에 상태를 노출하고 관련 비즈니스 로직을 캡슐화

장점

상태를 캐시하여 구성 변경에도 유지 (화면 회전) 

비즈니스 로직에 대한 액세스 권한 제공

수명 주기

범위와 직접 연결, 범위로 지정된 ViewModelStoreOwner가 사라질 떄까지 메모리에 남아 있음

⇒활동의 경우 완료될 때, 프래그먼트의 경우 분리될 떄, 탐색항목의 경우 백 스택에서 삭제 뙬 때 발생 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4e5aa835-001c-43da-96c3-29f781e2c2c0/Untitled.png)

onCreate()메서드가 처음 호출할 떄 ViewModel요청

viewModel이 처음 요청되었을 때부터 활동이 끝나고 소멸될 때까지viewModel존재

### LiveData

Data의 변경을 관찰 할 수 있는 Data Holder 클래스

LiveData가 가지고 있는 데이터에 어떠한 변화가 일어날 경우 LiveData는 등록된 Observer 객체에 변화를 알려주고 Observer의 onChanged() 메소드가 실행

장점

ui와 데이터 상태의 일치 보장

메모리 누수 없음

중지된 활동으로 인한 비정상 종료 없음

수명 주기를 더 이상 수동으로 처리하지 않음

최신 데이터 유지

적절한 구성 변경

리소스 공유

```
class TestLiveDataViewModel : ViewModel() {
    // String 타입의 MutableLiveData 생성, by lazy로 초기화는 뒤에
    val textValue: MutableLiveData<String> by lazy {
        MutableLiveData<String>()
    }
}
```

```
class MainActivity : AppCompatActivity() {
    // 전역 변수로 ViewModel lateinit 세팅
    private lateinit var model: TestLiveDataViewModel

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        // ViewModel을 가져옵니다.
        model = ViewModelProvider(this).get(TestLiveDataViewModel::class.java)

        // Observer를 생성한 뒤 UI에 업데이트 시켜 줍니다.
        val testObserver = Observer<String> { textValue ->
            // 현재 MainActivity에는 TextView가 하나만 존재합니다.
            // 다른 데이터를 받는 UI 컴포넌트가 있다면 같이 세팅 해줍니다.
            tv_livedata_test.text = textValue
        }

        // LiveData를 Observer를 이용해 관찰하고
        // 현재 Activity 및 Observer를 LifecycleOwner로 전달합니다.
        model.textValue.observe(this, testObserver)
    }
}
```

[https://youngdroidstudy.tistory.com/entry/Kotlin-코틀린의-ViewModel과-LiveData](https://youngdroidstudy.tistory.com/entry/Kotlin-%EC%BD%94%ED%8B%80%EB%A6%B0%EC%9D%98-ViewModel%EA%B3%BC-LiveData)

[https://youngdroidstudy.tistory.com/entry/Kotlin-코틀린의-ViewModel과-LiveData](https://youngdroidstudy.tistory.com/entry/Kotlin-%EC%BD%94%ED%8B%80%EB%A6%B0%EC%9D%98-ViewModel%EA%B3%BC-LiveData)
