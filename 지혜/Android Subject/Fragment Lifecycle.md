### 1. onAttach()

- 프래그먼트가 액티비티에 붙을 때 호출
- 인자로 Context가 주어진다.

### 2. onCreate()

- 프래그먼트가 액티비티의 호출을 받아 생성
- Bunddle로 액티비티로부터 데이터가 넘어옴
- 프래그먼트가 일시정지 혹은 중단 후 재개되었을 때 유지하고 있어야 하는 것을 여기서 초기화
- **UI 초기화는 불가능**

### 3. onCreateView()

- **레이아웃 inflate 담당**
- 프래그먼트가 자신의 인터페이스를 처음 그리기 위해 호출
- View를 반환
- savedInstanceState로 이전 상태에 대한 데이터 제공

### 4. onViewCreated()

- onCreagteView()를 통해 반환된 **View 객체는 onViewCreated()의 파라미터로 전달** 된다.
- 이 때 Lifecycle이 **INITIALIZED 상태로 업데이트**가 됨
- 때문에 **View의 초기값 설정, LiveData 옵저빙, RecyclerView, ViewPager2에 사용될 Adapter 세팅은 이 메소드에서 해주는 것이 적절함**

### 5. onViewStateRestored()

- 저장해둔 모든 state 값이 Fragment의 View의 계층 구조에 복원되었을 때 호출 ex) 체크박스 위젯이 현재 체크되어있는가
- View lifecycle owner : **INITIALIZED → CREATED** 변경

### 6. onStart()

- 사용자에게 보여질 수 있을 때 호출
- Activity의 onStart() 시점과 유사
- 액티비티가 시작됨 상태에 들어가면 이 메서드를 호출
- 사용자에게 프래그먼트가 보이게 되고, 이 메서드에서 UI를 관리하는 코드를 초기화 합니다. 이 메서드는 매우 빠르게 완료되고, 완료되면 Resumed(재개)상태로 들어가 onResume() 메서드를 호출합니다.

### 7. onResume()

- **사용자와 프래그먼트가 상호작용 할 수 있는 상태일 때 호출**
- 어떤 이벤트가 발생하여 포커스가 떠날 때 까지 이 상태에 머무름
- 프로그램이 일시정지되어 onPause()를 호출하고 다시 재개되면 onResume() 메서드를 다시 호출

### 8. onPause()

- **Fragment가 visible 일 때 onPause()가 호출**
- 이 때 **Faragment와 View의 Lifecycle이 PAUSED가 아닌 STARTED가 됨**
- 사용자가 프래그먼트를 떠나면 첫번 째로 이 메서드를 호출합니다. 사용자가 돌아오지 않을 수도 있으므로 여기에 현재 사용자 세션을 넘어 지속되어야 하는 변경사항을 저장

### 9. onStop()

- Fragment가 더 이상 화면에 보여지지 않게 되면 onStop() 콜백 호출
- 부모 액티비티, 프래그먼트가 중단될 때, 상태가 저장될 때 호출
- View와 Lifecycle : **STARTED** → **CREATED**
- API 28버전을 기점으로 onSaveInstanceState() 함수와 onStop() 함수 호출 순서가 달라짐, 따라서 **onStop()이 FragmentTransaction을 안전하게 수행하는 마지막 지점**이 됨

### 10. onDestoryView()

- **모든 exit animation, transaction이 완료되고 Fragment가 화면으로부터 벗어났을 경우 호출**
- view와 lifecycle : **CREATED → DESTROYED**
- 가비지 컬렉터에 의해 수거될 수 있도록 **Fragment View에 대한 모든 참조가 제거되어야 함**
- getViewLifecycleOwnerLiveData()

### 11. onDestroy()

- **Fragment가 제거되거나, FragmentManager가 destroy 됐을 경우, onDestroy() 콜백 함수가 호출**
- Fragment Lifecycle의 끝을 알림

### 12. onDetach()

- **프래그먼트가 액티비티로부터 해제되어질 때 호출된다.**

**액티비티와 프래그먼트의 수명 주기에서 가장 중요한 차이점은** **백스택에 저장되는 방법에 있습니다.** 액티비티는 정지되면 시스템에서 관리하는 액티비티의 백 스택에 들어갑니다. 하지만 프래그먼트는 이를 제거하는 트랜잭션에서 **addToBackStack()**을 호출하여 인스턴스를 저장하라고 명시적으로 요청할 경우에만 액티비티에서 관리하는 백 스택으로 들어갑니다.
