# 💡 Android Jetpack

# ✅ Android Jetpack이란?
Jetpack은 2018년 5월 8일에 구글이 발표한 라이브러리와 도구 모음집이다.  
개발자들이 쉽고, 빠르고, 퀄리티 좋은 앱을 만들 수 있도록 도와주는 라이브러리와 도구를 모아 두었다.

<br/>

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/IRsdO/btq1OMAIouc/vjkeYKEVXu3K3exdD9t2QK/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/IRsdO/btq1OMAIouc/vjkeYKEVXu3K3exdD9t2QK/img.png)

<br/>

이 구성 요소를 통해 권장 사항을 따르고, 상용구 코드 작성 작업에서 벗어나며, 복잡한 작업을 간소화하여 중요한 코드에만 집중할 수 있다.  
Jetpack은 플랫폼 API와는 별도로 제공되는 androidx.* 패키지 라이브러리로 구성된다. 즉, 이전 버전과 호환되며 Android 플랫폼보다 더 자주 업데이트되므로 개발자는 항상 가장 뛰어난 최신 버전의 Jetpack 구성 요소에 액세스할 수 있다.

<br/>

## Android Jetpack을 사용해야 하는 이유
![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/255cd4fa-e564-44c3-98ef-c88dba1bef9e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230311T001102Z&X-Amz-Expires=86400&X-Amz-Signature=325f1978377e88538393c5c4779749c495b49c5537a4dd6696f81533ef3a868d&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

<br/>

## Jetpack이 나오게 된 배경
![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/7m06i/btq1WJCvpXu/mQsHyLxSOqDTILgVP0PRy1/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/7m06i/btq1WJCvpXu/mQsHyLxSOqDTILgVP0PRy1/img.png)

<br/>

사실 Jetpack이 나오기 전 Support library라고 하는 라이브러리 모음집이 이미 존재했었다.  
그러나 Support library에는 여러 가지 문제점이 있었고 이를 개선하면서 새로운 이름을 붙여 다시 나온 것이 Jetpack인 것이다. Support library는 현재도 사용 가능하지만 위 사진(공식 문서)에 쓰여있듯이 AndroidX를 사용할 것을 권장하고 있다. (AndroidX는 Jetpack의 라이브러리들을 묶은 패키지 명이다.)

<br/>

### Support Library의 문제점
- Support Library는 패키지명과 버전 규칙이 모호했다.
    
    com.android.support:support-v4    
    com.android.support:support-v13
    
    <br/>
    
    서포트 라이브러리는 위와 같은 패키지명을 사용했는데 v13이 v4의 기능을 포함한 상위 버전인 것 같은 느낌을 주지만, 사실 API레벨 13 이상에서 사용 가능이라는 뜻을 가지고 있다. 충분히 착각할 수 있는 여지를 주는 버전 규칙이었다.    
    또 스마트폰의 스펙이 상향 표준화된 요즘에는 minSdkVersion이 19 이상만 되어도 95% 이상의 기기를 지원하기 때문에 사실상 버전명에 큰 의미가 없어지게 되었다. (마지막 버전이 28인데 사실상 숫자를 증가시키는 게 더 이상 무의미…)    
    더군다나 24.2.0 버전을 릴리즈하면서 v4를 사용하려면 API 레벨 14 이상이 되어야 하게 바뀌었으며 이는 v4 = API 4 레벨 이상이라는 규칙성을 상실하게 되었다.
    
<br/>

- 단일 라이브러리로 제공된다.    
    서포트 라이브러리는 3만 여개의 함수를 제공하는 단일 라이브러리였다.    
    이게 무슨 말이냐면 ViewPager 기능을 사용하고 싶어서 라이브러리를 추가했는데, 원치 않는 다른 라이브러리도 함께 추가된다는 뜻이다.
    
    <br/>
    
    앱의 규모가 커지거나 라이브러리 내의 메서드가 많으면 '64K reference limit'이라는 에러를 만나게 된다.    
    이 에러는 dex파일이 64K를 넘어가면서 뜨는 에러이다.    
    안드로이드는 MainActivity.java → MainActivity.class → MainActivity.dex 이렇게 변환해서 사용한다.    
    즉, 클래스 파일이 많아질수록 dex파일의 용량도 커진다.    
    기본적으로 APK당 하나의 DEX파일을 사용하기 때문에 64K 이내의 용량을 사용해야 하는데, 서포트 라이브러리는 이 에러가 뜨게 만드는 주원인이 되었다.    
    이 문제를 해결할 수 있는 Multidex라는 기술이 나왔지만 여전히 단일 라이브러리는 좋은 방법이 아니라는 게 분명하다.
    
    <br/>
    
    ※ Multidex : Multidex는 메서드가 64k(65536)개를 초과하지 않도록 dex파일을 여러개로 쪼개주고, 쪼개진 dex를 읽을 수 있게 해 준다.
    
<br/>

- 바이너리 호환성 제약    
    
    |  | 기능 A | 기능 B |
    | --- | --- | --- |
    | 1.1.0 버전 | 정식 버전 | 베타 버전 |
    | 1.1.1 버전 | 새로운 버전(문제 발생) | 정식 버전 |
    
    <br/>
    
    1.1.0 버전을 이용해 개발한 앱이 있다고 친다. 기능 B가 베타 버전이었지만 문제 없이 잘 돌아갔다.    
    1.1.1 버전이 나오고 기능 B가 정식 버전으로 나왔다고 해서 헐레벌떡 업데이트를 했다.    
    근데 1.1.1 버전 기능 A에 문제가 생겨서 눈물을 머금고 다시 1.1.0 버전으로 다운그레이드를 했다.    
    이게 단일 라이브러리의 단점이었다. 한꺼번에 업데이트하고 다운그레이드 해야 한다는 것.    
    이를 해결하고자 AndroidX는 위젯 단위의 세분화된 형태로 모듈화 해서 라이브러리를 제공하게 되었다.

<br/>

정리해서 말하자면 서포트 라이브러리는 위와 같은 문제점들이 있었다.  
이를 해결하면서 새로운 기능의 라이브러리들을 추가하면서 이름을 바꾸어 내놓은 것이 Jetpack인 것이다.

<br/>

## Android Jetpack의 특징
JetPack의 구성 요소는 다양하다. 기존의 Support library를 비롯하여 아키텍처 컴포넌트를 포함하는데 이를 크게 4 가지로 나누어 볼 수 있다.

<br/>

![https://miro.medium.com/v2/resize:fit:720/format:webp/0*yGfvV-RR_8QcioE1.png](https://miro.medium.com/v2/resize:fit:720/format:webp/0*yGfvV-RR_8QcioE1.png)

<br/>

또한 JetPack의 컴포넌트는 안드로이드 플랫폼의 일부가 아니므로 개발자는 원하는 androidx.* 패키지 라이브러리를 이용하여 원하는 컴포넌트만 취사선택하여 이용할 수 있다.

<br/>

Android Jetpack은 기본 Android 플랫폼에 속하지 않은 "별도의" 라이브러리로서 제공된다.  
또한 Android Jetpack은 특정 버전에 관계 없이 기능을 제공하도록 빌드되고 이전 버전과의 호환성을 제공하기 때문에, 다양한 버전의 플랫폼에서 앱을 실행할 수 있다.

<br/>

### 새롭게 추가된 것
- WorkManager
- Navigation
- Paging
- Slices
- Android KTX

<br/>

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/195c4ff7-2b29-4728-9c8d-c81e569621d9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230311T001141Z&X-Amz-Expires=86400&X-Amz-Signature=d65b6af71b360852636c568bd73635b6b78037a0b3ed29b7b08a1d84ce2a4407&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

> [유형별 Jetpack 라이브러리 살펴보기  |  Android 개발자  |  Android Developers](https://developer.android.com/jetpack/androidx/explorer?hl=ko)
> 

<br/>

Jetpack을 구성하는 라이브러리는 굉장히 많다. 자세한 설명과 목록은 위 링크에 들어가서 확인하면 된다.

<br/>
<br/>

# ✅ 앱에서 Jetpack 라이브러리 사용
모든 Jetpack 구성 요소는 Google Maven 저장소에서 사용할 수 있다.  
`settings.gradle`  파일을 열고 아래와 같이 `dependencyResolutionManagement { repositories {...}}`  블록에 `google()`  저장소를 추가한다.

```groovy
dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        google()
        jcenter()
    }
}
```

<br/>

그런 다음 아래와 같이 Jetpack 구성 요소(예: LiveData, ViewModel과 같은 아키텍처 구성요소)를 모듈의 `build.gradle`  파일에 추가할 수 있다.

```groovy
dependencies {
    def lifecycle_version = "2.2.0"

    implementation "androidx.lifecycle:lifecycle-livedata-ktx:$lifecycle_version"
    implementation "androidx.lifecycle:lifecycle-viewmodel-ktx:$lifecycle_version"
    ...
}
```

<br/>

많은 Jetpack 라이브러리에서 `lifecycle-livedata-ktx`와 `lifecycle-viewmodel-ktx`를 통해 위에 나타난 것과 같이 Android KTX 확장 프로그램을 제공한다. KTX 확장 프로그램은 자바 기반 API를 토대로 빌드되어 Kotlin 관련 언어 기능을 활용한다.

<br/>

## Jetpack 활용
Jetpack 라이브러리는 앱의 다양한 요구를 해결하기 위해 단독으로 또는 조합하여 사용할 수 있다.  
- WorkManager : 백그라운드 일정 예약 요구 해결
- Room : 데이터 저장소 지속성 해결
- Navigation : 애플리케이션 탐색 흐름 관리
- CameraX : 카메라 앱 요구 해결
- 모든 Jetpack 라이브러리의 개요를 참고

<br/>

Jetpack 라이브러리는 `androidx`  네임스페이스에 게시된다.  
프로젝트에서 현재 Android 지원 라이브러리를 사용하는 경우, androidx 네임스페이스로 이전하는 방법을 참조.

<br/>
<br/>

# ✅ Compose

구글에서는 개발자들이 쉽게 모범적인 코드를 작성하고 보일러 플레이트 코드는 줄일 수 있도록 라이브러리 모음을 제공하는데 이것을 Jetpack이라고 한다. 그리고 Compose는 선언형 UI 개발을 가능하게 하는 안드로이드 프레임워크이다. 안드로이드 개발자 문서에는 [Compose를 왜 사용해야 하는가](https://developer.android.com/jetpack/compose/why-adopt?hl=ko)에 대해 이유를 설명한 페이지가 있다.

<br/>

- 코드 감소
- 직관적
- 빠른 개발 과정
- 강력한 성능

<br/>

한 마디로 Compose는 개발자들이 편하게 UI 개발하라고 만든 툴킷이다

<br/>

![https://dealicious-inc.github.io/assets/image/posts/2022-03-14-android-compose-apply/01.png](https://dealicious-inc.github.io/assets/image/posts/2022-03-14-android-compose-apply/01.png)

<br/>

이전까지는 Kotlin과 xml을 오가며 작업했지만, Compose를 사용하면서 Kotlin으로만 개발할 수 있게 되었다.  
코드가 줄어드는 것은 당연하고, 기존에 뷰를 직접 조작했던 데에서 왔던 번거로움과 버그 위험성을 줄일 수 있다.  
그리고 기존 코드와의 호환이 되어 모든 코드를 바꾸지 않고 조금씩 점진적으로 적용할 수 있다는 점도 Compose를 시도해 보는 계기가 되었다.

<br/>
<br/>

# 🗂 참고
- [안드로이드 Jetpack이란? (tistory.com)](https://todaycode.tistory.com/40)
- [Android: Jetpack이란?. 이번에는 안드로이드의 Jetpack에 대해 포스팅해보고자 한다… | by LUNA Y0UNG | Medium](https://medium.com/@lunay0ung/android-jetpack%EC%9D%B4%EB%9E%80-bfb360ab05ec)
- [[안드로이드] Multidex 란 (colinch4.github.io)](https://colinch4.github.io/2020-11-25/Multidex/)
- [Android-Study/android jetpack.md at master · taeiim/Android-Study (github.com)](https://github.com/taeiim/Android-Study/blob/master/study/week06/jetpack/android%20jetpack.md)
- [Android Jetpack 시작하기  |  Android 개발자  |  Android Developers](https://developer.android.com/jetpack/getting-started?hl=ko)
- [Android Jetpack Compose 한 번 써봤습니다 | dealicious-inc.github.io](https://dealicious-inc.github.io/2022/03/14/android-compose-apply.html)
