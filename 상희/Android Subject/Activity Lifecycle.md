# 💡 Activity Lifecycle

# ✅ Lifecycle
Activity, Fragment, Service, View 등의 Lifecycle이 있다.

<br/>
<br/>

# ✅ Activity Lifecycle
Activity Lifecycle은 앱을 사용하는 사용자의 행동에 따라서 변경되는 Activity의 상태를 의미한다.  
이렇게 상태가 변경될 때 마다 시스템은 Lifecycle 콜백 함수들을 호출하고, 개발자는 아래의 문제 상황을 막기 위해 콜백 함수들이 실행이 될 때 적절한 처리를 해 주어 올바르게 앱을 개발해야 한다.  
- 사용자가 앱을 사용하는 도중에 전화가 걸려오거나 다른 앱으로 전환할 때 비정상 종료되는 문제
- 사용자가 앱을 활발하게 사용하지 않는 경우 귀중한 시스템 리소스가 소비되는 문제
- 사용자가 앱에서 나갔다가 나중에 돌아왔을 때 사용자의 진행 상태가 저장되지 않는 문제
- 화면이 가로 방향과 세로 방향 간에 회전할 경우, 비정상 종료되거나 사용자의 진행 상태가 저장되지 않는 문제

<br/>

Activity 생명 주기는 다음 그림과 같다.  
![https://mashup-android.vercel.app/static/693ff3c37db64daedc460ced7793670f/267f6/Lifecycle.png](https://mashup-android.vercel.app/static/693ff3c37db64daedc460ced7793670f/267f6/Lifecycle.png)

<br/>

Activity는 위 그림과 같이 상태에 따른 콜백 메소드를 가지고 있다.

<br/>

## Callback Method
### onCreate
Activity가 생성됨을 의미하는 Created 상태일 때 호출되는 콜백 함수이다.  
onCreate 함수는 반드시 override해야 하는 함수이고, Activity 전체 생명 주기에서 한 번만 호출되는 함수로 레이아웃을 inflate하고 필요한 변수들을 초기화하는 작업이 이 함수 내에서 이루어진다.

<br/>

추가적으로 onCreate 함수 매개변수로 Bundle이 있다. 이 변수는 액티비티가 시스템에 의해 강제 종료 되거나 가로 모드 등 config change가 발생될 때, UI에 필요한 Data를 유지시키기 위해 사용할 수 있다. 하지만 만약 Bitmap 등 커다란 Data를 유지하려고 한다면 AAC ViewModel을 이용해야 한다.

```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
		
		setContentView(R.layout.activity_main)

		if (savedInstanceState != null) {
			...
    }

    textView = findViewById(R.id.text_view)	      
}
```

<br/>

### onStart
Activity가 Started 상태일 때 호출되는 콜백 함수이다. (Activity가 사용자에게 보이기 직전 호출된다.)  
이 상태일 때는 뷰가 로드가 되어 화면 내에 UI가 표시되고 아직 사용자와 상호작용은 할 수 없는 상태이다. 따라서 시스템은 이 상태를 빠르게 완료하고 넘어가길 원하기 때문에 이 함수에서 복잡한 연산을 하는 것은 안 좋다고 한다.

<br/>

### onResume
Activity가 Resumed 상태일 때 호출되는 콜백 함수입니다. (Activity가 사용자와 상호 작용을 하기 직전 호출된다.)  
이 상태일 때 비로소 앱이 사용자와 상호 작용을 할 수 있다.  
그리고 앞서 언급된 상태와 다르게 다른 이벤트가 없다면 Activity는 Resumed 상태에서 머물게 된다.  
다른 Activity로 전환되었다가 다시 돌아와 Activity가 활성화될 때도 최종적으로 Resumed 상태가 되므로 이 콜백 함수 내에서 최신 정보를 갱신하는 작업이 이루어진다고 생각한다.

<br/>

### onPause
Activity가 Paused 상태일 때 호출되는 콜백 함수이다. (다른 액티비티의 호출로 해당 액티비티가 백그라운드로 진입할 때 호출된다.)  
사용자가 포그라운드의 Activity를 벗어날 때 처음 호출되는 함수로 아직 Activity가 소멸된 것은 아니지만 화면이 아직 일부분 보이는 상태이며 사용자와 상호작용을 할 수 없는 상태이다.  
시스템 리소스, 카메라처럼 배터리를 많이 소모하는 리소스를 해제하는 작업이 이 함수 내에서 이루어질 수 있지만, onPause는 화면이 일부분 보이는 상태이며 곧 Activity가 포그라운드로 돌아올 가능성이 있고 멀티 윈도우 환경에서 Paused 상태는 아직 UI가 보이는 상태일 수도 있기 때문에 UI 리소스를 해제하는 작업은 하면 안 된다고 한다.  
이 메소드가 리턴 되기전까지는 다음 액티비티의 실행이 이루어지지 않으므로 되도록 빨리 끝내야 한다.

<br/>

### onStop
Activity가 Stopped 상태일 때 호출되는 콜백 함수이다. (액티비티가 더 이상 화면에 나오지 않는다.)  
화면이 모두 다른 Activity에 의해 가려진 상태를 의미하고 onPause에서 해제하지 못했던 UI 관련 리소스들을 해제하는 작업이 이 함수 내에서 이루어지면 좋다고 한다.

<br/>

### onDestroy
Activity가 Destroyed 상태일 때 호출되는 콜백 함수이다. (액티비티가 소멸되기 전에 호출된다.)  
Activity가 소멸되는 상태이며 다음과 같은 2가지 상황으로 인해 변경되었다고 한다.  
- finish 함수를 호출하여 Activity가 명시적으로 종료
- config changed가 발생, 예를 들어 가로 모드 전환 등으로 인해 Activity를 재생성할 때

onDestroy 콜백 함수 내에서는 onStop에서 하지 못한 리소스 해제를 진행해야 한다. 위의 2 가지 상황 중 config changed로 인한 Destroyed 상태는 다시 뷰가 생성되는 작업으로 AAC ViewModel 내에서 저장하고 있던 데이터를 해제하면 안 된다. 그래서 이를 구분하기 위해 isFinish 함수를 제공해 준다고 한다.

<br/>

### onRestart
- 액티비티가 중단되었다가 다시 시작되기 직전에 호출
- 이 뒤에는 항상 onStart()가 호출

<br/>

## 액티비티 재시작된 경우
- onPause() 상태까지 호출 뒤 재시작된 경우
    - onPause() → onResume()
- onStop() 상태까지 호출 뒤 재시작된 경우
    - onStop() → onRestart() → onStart() → onResume()

<br/>
<br/>

# 🗂 참고
- [[안드로이드] Activity Lifecycle (velog.io)](https://velog.io/@its-mingyu/%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-Activity-Lifecycle)
- [[Android] 액티비티 생명 주기 (Activity Lifecycle) (tistory.com)](https://bbaktaeho-95.tistory.com/62)
- [안드로이드 면접 질문 #3 액티비티 (tistory.com)](https://leesincee94.tistory.com/18)
- [[Android] 액티비티 생명 주기 (Activity Lifecycle) (tistory.com)](https://bbaktaeho-95.tistory.com/62)
- [Activity LifeCycle (액티비티 생명주기) (velog.io)](https://velog.io/@sh1mj1/Activity-LifeCycle-%EC%95%A1%ED%8B%B0%EB%B9%84%ED%8B%B0-%EC%83%9D%EB%AA%85%EC%A3%BC%EA%B8%B0)
