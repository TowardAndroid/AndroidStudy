# 230506 Android 면접 준비

## Q1. Activity에 대해 설명해 주세요.
액티비티는 일종의 어플리케이션 구성 요소로, 사용자와 상호 작용 할 수 있는 화면을 제공한다.  
액티비티마다 layout.xml 파일을 구현함으로써 사용자에게 인터페이스를 제공해 줄 수 있다.  
액티비티를 사용하기 위해서는 아래와 같은 내용들을 알아야 한다.  
- setContentView()를 이용하여 액티비티의 View를 Draw
- AndroidManifest 파일에 Activity를 등록
- 라이프 사이클 콜백 처리
    - onCreate, onStart, onResume, onPause, onDestroy
- 액티비티 시작 시에 정보를 전달하거나 액티비티가 종료될 때 결과를 리턴할 수 있다.

<br/>
<br/>

## Q2. Activity의 3 가지 상태에 대해 말씀해 주세요.
- 활성화(Active) 또는 실행 중(Running) 상태
    - Activity가 전면에 나와서 실행되고 있을 때
    - 현재 Task에 대한 Activity Stack의 최상위에 존재하고 있을 때
    - 이 상태의 Activity는 사용자와 상호작용 할 수 있다.
- 멈춤(Pause) 상태
    - 사용자의 포커스를 가지고 있지 않지만 여전히 화면이 보여지고 있을 때
    - 다른 액티비티가 위에 위치 하지만 그 액티비티가 투명 상태 혹은 전체 화면을 채우지 못해 아직은 이전 액티비티가 보이는 상태이다. 이 때, 이전 액티비티의 상태는 멈춤 상태이다.
    - 극도로 메모리가 부족한 상태에서는 시스템에 의해 강제로 종료될 수 있다.
- 정지(Stopped) 상태
    - 다른 Activity에 의해서 완전히 가려져 더 이상 사용자에게 보여지지 않을 때

<br/>
<br/>

## Q3. A Activity 에서 버튼을 눌러 B Activity 로 이동한다고 했을때 두 Activity의 생명 주기 함수 호출을 순서대로 말씀해 주세요.(A Activity 생명 주기 함수 호출이 다 끝나고 B Activity의 생명 주기 함수가 호출된다고 생각하시나요?)
활성 상태인 A 화면의 onPause 함수까지만 호출되고 활성화될 B 화면의 작업이 모두 완료 된 후 다시 A의 onStop이 호출된다.  
- [A Activity] onPause()
- [B Activity] onCreate()
- [B Activity] onStart()
- [B Activity] onResume()
- [A Activity] onStop()

<br/>
<br/>

## Q4. 그럼 이제 B Activity에서 백 버튼을 눌러 A Activity로 돌아간다고 했을 때 어떤 순서로 생명 주기 함수들이 호출되나요?
활성 상태인 B 화면의 onPause 함수까지만 호출되고 활성화 될 A 화면의 작업이 모두 완료된 후 다시 B의 onStop과 onDestroy가 호출된다.  
- [B Activity] onPause()
- [A Activity] onRestart()
- [A Activity] onStart()
- [A Activity] onResume()
- [B Activity] onStop()
- [B Activity] onDestroy()

<br/>
<br/>

## Q5. Launch Mode에 대해 설명해 주세요.
Launch Mode의 종류는 총 4 가지가 있다.  
- standard(Default)
    - 인텐트를 할 때마다 Activity를 새로 생성한다.
- singleTop
    - 인텐트를 할 때마다 Activity를 새로 생성하나, 동일한 Activity가 해당 태스크의 top에 있을 경우 새로 생성하지 않고 기존에 있던 Activity를 호출한다.
    - 생명 주기는 onPause() → onNewIntent() → onResume
- singleTask
    - 하나의 Activity만 생성이 되나 다른 Activity가 해당 태스크의 일부가 되는 것을 허용한다.
- singleInstance
    - 이 옵션도 singleTask와 비슷하나 그 어떤 Activity와도 섞이지 않고 유일한 Activity로 동작
    - Task안에 Activity가 하나만 존재

<br/>
<br/>

## 🗂 참고
- [생각지도 못했던 안드로이드 생명주기 면접질문. 모 회사 면접에서 안드로이드 개발자라면 누구나 한번씩 숙지하고 있을… | by DevSoupe | Medium](https://devsoupe.medium.com/%EC%83%9D%EA%B0%81%EC%A7%80%EB%8F%84-%EB%AA%BB%ED%96%88%EB%8D%98-%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-%EC%83%9D%EB%AA%85%EC%A3%BC%EA%B8%B0-%EB%A9%B4%EC%A0%91%EC%A7%88%EB%AC%B8-a34b19895d83)
- [안드로이드 면접 질문 #3 액티비티 (tistory.com)](https://leesincee94.tistory.com/18)
