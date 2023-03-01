개발자가 관심있는 코드에 집중할 수 있도록 권장사항 준수, 상용구 코드 제거, 모든 Android 버전과 기기에서 일관되게 작동하는 코드 작성을 돕는 라이브러리 모음

= 고품질 앱을 개발하도록 돕는 라이브러리들의 모음집

플랫폼 API와는 별도로 제공되는 androidx.*패키지 라이브러리로 구성 → AndroidX로 마이그레이션 필요

이전 버전과 호환되며 Android플랫폼보다 더 자주 업데이트되므로 개발자는 항상 가장 뛰어난 최신 버전의 Jetpack구성요소에 액세스 가능

**구성요소**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c2279546-a1ab-4b93-9159-e209bfa525b3/Untitled.png)

### Architecture

- Data Binding: xml파일에 Data를 연결해서 사용할 수 있게 도와준다
- Lifecycles: 안드로이드 activity 생명주기 관련 유틸리티
- LiveData: 데이터가 변경될때 실시간으로 view에 알려준다
- Navigation: activity, fragment간 이동을 쉽게 도와준다
- Paging: 대량의 데이트를 관리해주는 유틸리티
- Room: Database 보다 쉽게 사용할 수 있게 도와준다
- WorkManager: 백그라운드 작업을 보다 쉽게 도와준다

### Foundation

- AppCompat: 하위 안드로이드 앱에서 최긴버전 sdk를 사용할 수 있도록 도와준다.
- Android KTX: 코틀린 코드를 더욱 간결하게 만들어준다.
- Multidex: dex 관리 관련 유틸리티
- Test: 안드로이드 테스티관련 유틸리티

### Behavior

- Download manager: 큰 파일 다운로드을 service 차원에서 관리를 도와준다.
- Media & Playback: 미디어 파일 재생 관련 유틸리티
- Permissions: 안드로이드 권한 관련 유틸리티
- Notifications: 안드로이드 notification 관련 유틸리티
- Sharing: Actionbar에서 데이터를 보다 쉽게 공유할 수 있도록 도와준다

### UI

- 앱에서의 다양한 애니메이션, 이모지 또는 다양한 플랫폼 (TV, 워치) 과련 유틸리티를 사용할 수 있는 컴포넌트.

[https://velog.io/@eoqkrskfk94/android-Jetpack](https://velog.io/@eoqkrskfk94/android-Jetpack)
