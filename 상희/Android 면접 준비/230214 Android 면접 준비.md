# 230214 Android 면접 준비

## Q1. Android 4대 컴포넌트
Android 앱은 컴포넌트로 구성되어 있다. Activity, Service, Broadcast Receiver, Content Provider, 이를 4대 컴포넌트라고 부른다.  
각 컴포넌트들은 하나의 독립된 형태로 존재하며 정해진 역할을 수행한다.  
컴포넌트는 앱의 구성 단위로 컴포넌트를 조합하여 하나의 앱을 만드는 것을 의미한다.  
Activity는 UI 화면을 담당하는 컴포넌트다.  
Service는 화면에 존재하지 않고 백그라운드에서 실행되는 컴포넌트다. 크게 3 가지로 나뉘는데, Foreground Service, Background Service, Bound Service다.  
Foreground Service는 알림을 표시해 놓고 사용자와 상호 작용하지 않아도 계속 실행되는 걸 말한다.  
Background Service는 사용자가 직접 알지 못하는 작업을 수행할 때 사용한다.  
Bound Service는 앱 내에서 서비스를 사용하여 간단한 클라이언트/서버 환경을 구성하는 것을 말한다.  
Broadcast Receiver는 단말기에서 발생하는 다양한 이벤트, 정보를 받고 반응하는 컴포넌트다. 정적 리시버, 동적 리시버로 나뉜다.  
정적 리시버는 매니페스트에 등록하여 리시버를 구현하는 형태인데 한 번 등록하면 해제할 수 없는 방식이다.  
동적 리시버는 클래스 파일에서 리시버를 등록, 해제할 수 있는 형태이기 때문에 앱에 부하를 줄 일 수 있다. 하지만 해제를 적절히 해 주지 않는다면 메모리 릭이 발생할 수 있다.  
Content Provider는 앱 간 데이터 공유를 위한 클래스를 제공하는 컴포넌트다.

<br/>

## Q2. Activity와 Fragment의 차이점
1. 액티비티는 독립적으로 활용할 수 있다.
2. 프래그먼트는 액티비티에 종속되어 있다.
3. 액티비티는 전체 화면을 차지하지만, 프래그먼트는 전체 화면이 아니어도 되며 디자인에 많은 유연성을 가지고 있다.
4. 액티비티는 자동적으로 스택에 넣어지고 프래그먼트는 트랜잭션을 통해서 요청해야 한다.

<br/>

## Q3. Activity LifeCycle
Activity LifeCycle은 Activity가 시작되고 종료되는 시점까지의 상태를 Activity LifeCycle이라 한다.  
Activity LifeCycle에는 onCreate(), onStart(), onResume(), onPause(), onStop(), onDestroy(), onRestart()가 있다.  
onCreate()는 액티비티가 시작될 때 레이아웃을 구성하면서 한 번 실행된다.  
onStart()는 액티비티가 사용자에게 보이기 직전에 실행된다. BroadcastReceiver를 실행한다.  
onResume()는 사용자가 액티비티와 상호 작용하는 기능을 넣는 곳으로, 무조건 실행되어야 하는 기능이 들어간다.  
onPause()는 포커스를 잃어 화면이 부분적으로는 보이지만 곧 사라질 때 실행된다.  
onStop()는 사용자에게서 화면이 완전히 사라지고, 다른 액티비티가 보여질 때 호출된다.  
onDestroy()는 화면 회전 혹은 화면이 완전히 종료되기 직전에 호출된다.  

<br/>

## Q4. Fragment LifeCycle
Fragment LifeCycle은 Fragment가 시작되고 종료될 때 까지 상태를 Fragment LifeCycle라고 한다.  
Fragment LifeCycle에는 onAttach(), onCreate(), onCreateView(), onActivityCreated(), onStart(), onResume(), onPause(), onStop(), onDestroyView(), onDestroy(), onDetach()가 있다.  
onAttach(Activity)는 액티비티에서 프래그먼트가 호출될 때 최초 한 번 호출되는 함수다.  
onCreate(Bundle)은 프래그먼트가 생성될 때 호출되는 함수다.  
onCreateView(LayoutInflater, ViewGroup, Bundle)은 프래그먼트의 뷰를 생성하는 함수다.  
onActivityCreated(Bundle)은 액티비티에서 onCreate()가 호출된 프래그먼트에서 호출되는 함수다.  
onStart()는 프래그먼트가 사용자한테 보여지기 직전 호출되는 함수다.  
onResume()은 프래그먼트가 사용자와 상호 작용할 수 있는 상태다.  
onPasue()는 화면이 일부 가려졌을 때 호출된다.  
onStop()은 프래그먼트가 화면에 사라졌을 때 호출된다.  
onDestroyView()는 프래그먼트의 View가 사라질 때 호출되는 함수다.  
onDestroy()는 프래그먼트가 제거될 때 호출되는 함수다.  
onDetach()는 프래그먼트가 액티비티와 연결이 종료될 때 호출되는 함수다.  

<br/>

## Q5. ListView와 RecyclerView의 차이
ListView와 RecyclerView는 모두 스크롤 가능한 리스트 형식의 레이아웃을 구현할 때 사용된다. ListView는 스크롤할 때 나오는 아이템을 끊임없이 새로 만들어 메모리 성능에 부담이 갈 수 있다. 반면, RecyclerView는 처음 만들어지는 아이템의 개수는 정해져 있고, ViewHolder를 통해 들어가는 View의 재사용을 가능하게 한다.

<br/>
<br/>

# 🗂 참고
- [Android Interview (notion.so)](https://www.notion.so/3ce7ddf12ddb413a9d2213173654d52c)
- [안드로이드 앱개발자 기술면접 준비하기 (velog.io)](https://velog.io/@gina5757/%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-%EC%95%B1%EA%B0%9C%EB%B0%9C%EC%9E%90-%EA%B8%B0%EC%88%A0%EB%A9%B4%EC%A0%91%EC%A4%80%EB%B9%84%ED%95%98%EA%B8%B0)
