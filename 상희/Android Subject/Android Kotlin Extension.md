# 💡 Android Kotlin Extension

# ✅ Android Kotlin Extension
Android KTX는 Android Jetpack과 기타 Android 라이브러리에 포함된 Kotlin 확장 프로그램 세트이다.  
KTX 확장 프로그램은 간결하고 직관적인 Kotlin을 Jetpack, Android 플랫폼, 기타 API에 제공한다.  
이를 위해 다음을 비롯한 여러 Kotlin 언어 기능을 활용한다.  
- 확장 함수
- 확장 속성
- 람다
- 이름이 지정된 매개변수
- 매개변수 기본값
- 코루틴

<br/>

## 프로젝트에 Android KTX 사용
Android KTX를 사용하려면 프로젝트의 build.gradle 파일에 다음 종속 항목을 추가한다.

```groovy
repositories {
    google()
}
```

<br/>

## AndroidX 모듈
Android KTX는 모듈로 구성되며 각 모듈에는 패키지가 하나 이상 포함된다.  
앱의 build.gradle 파일에 각 모듈 아티팩트의 종속 항목을 포함해야 한다. 아티팩트에 버전 번호를 추가해야 한다.  
Android KTX에는 일반 프레임워크 API 및 여러 도메인별 확장 프로그램에 Kotlin 확장 프로그램을 제공하는 단일 핵심 모듈이 포함되어 있다.  
핵심 모듈을 제외한 모든 KTX 모듈 아티팩트는 build.gradle 파일의 기본 자바 종속 항목을 대체한다.  
예를 들어 androidx.fragment:fragment 종속 항목을 androidx.fragment:fragment-ktx로 대체할 수 있다. 이 구문은 버전 관리를 개선하는 데 도움이 되며 종속 항목 선언 요구 사항을 추가하지 않는다.

<br/>

### AndroidX 모듈 종류
- Core KTX
- Collection KTX
- Fragment KTX
- Lifecycle KTX
- LiveData KTX
- Navigation KTX
- Palette KTX
- Reactive Streams KTX
- Room KTX
- SQLite KTX
- ViewModel KTX
- WorkManager KTX

<br/>

## 기타 KTX 모듈
AndroidX 외부에 있는 추가 KTX 모듈을 포함할 수도 있다.

<br/>

### 기타 KTX 모듈 종류
- Firebase KTX
- Google Maps Platform KTX
- Play Core KTX

<br/>
<br/>

# ✅ Kotlin Android Extensions is deprecated
안드로이드 4.1 버전에서 새로운 프로젝트 생성 시 기본 플러그인으로 제공하던 apply plugin: ‘kotlin-android-extensions’이 제거되고, 기본 ‘com.android.application’과 ‘kotlin-android’ 만 남게 되었다.  
더 이상 ‘kotlin-android-extensions’을 기본으로 제공하지 않는다.  
사용하려면 직접 추가해 사용할 수 있고, 이미 사용하던 것 역시 사용이 가능하다.  
사실 ‘kotlin-android-extensions’은 좋은 플러그인은 아니다.  
findViewById의 반복적인 작업을 제거하려고 만들어졌고, 내부적인 캐시를 통해 재사용성을 높였을 뿐이다.  
하지만 모든 곳에서 재사용성을 지켜주지 않는다. RecyclerView의 ViewHolder에서는 지켜 주지 않는다.

<br/>

## deprecated된 이유
import만 하면 자동으로 view를 찾아 주고, 굳이 변수로 생성할 필요도 없고, 심지어 내부에서 캐싱까지 하는데 이를 지우는 이유는 다음과 같다.  
- 내부적인 캐시를 통해 재사용성을 높인 것이다.
- RecyclerView의 ViewHolder에서는 이 재사용성이 지켜지지 않는다.
    - 디컴파일을 해 보지 않으면 알 수 없기 때문에 상당히 많은 개발자가 놓치고 그대로 활용한다.
    
    ### 기존의 ViewHolder
    
    ```kotlin
    class SampleViewHolder(itemView: View) : RecyclerView.ViewHolder(itemView) {
        fun onBind() {
            itemView.btn.setOnClickListener {
    
            }
        }
    }
    ```
    
    ### 디컴파일한 코드
    
    ```kotlin
    public final void onBind() {
        View var10000 = this.itemView;
        Intrinsics.checkNotNullExpressionValue(var10000, "itemView");
        ((Button) var10000.findViewById(id.btn).setOnClickListener((OnClickListener) null.INSTANCE);
    }
    ```
    
    findCachedViewById를 사용하지 않고 findViewById를 사용하고 있다.    
    이는 onBind()를 호출할 때마다 findViewById를 매번 하는 것이다.    
    ⇒ 재사용성을 높여야 하는 RecyclerView.ViewHolder에서 이를 제공하고 있지 않다.    
- 실수가 생길 여지가 많다.
    - 동일한 id를 가진 서로 다른 widget
        - 해당 레이아웃에서만 사용하는 widget만 추천하는 것이 아니라 모든 레이아웃의 widget이 추천된다.
        - 이런 경우에는 런타임 오류가 발생한다.
    - 동일한 id를 가진 같은 widget
        - 이름만 명확하면 문제를 해결할 수 있고, 사소한 문제이지만 나중에 이슈가 터질 수도 있다.
        - import와 include를 사용하게 되는 경우 발생할 수 있다.
        - 이 경우에는 정상 동작을 한다.

<br/>

## ViewBinding
findViewById를 쓰지 않고, XML의 view component에 접근하는 object(Android Studio에서 자동 생성)를 반환받아 view에 접근하는 방식

<br/>

### 장점
- Null Safety
    - 잘못된 id를 대입하여 null pointer 오류가 발생하는 등의 문제가 일어나지 않는다.
- Type Safety
    - 바인딩 클래스 내 필드는 레이아웃 내 선언된 뷰의 타입을 갖는다.
    - 따라서 잘못된 타입으로 캐스팅하는 실수를 원천 봉쇄한다.

<br/>
<br/>

# ✅ 정리
- Kotlin android extensions이 항상 좋은 것은 아니다.
- Kotlin android extensions은 실수할 여지가 매우 많다.
- 일부는 _findCachedViewById를 이용하여 성능 향상에 도움을 주지만 그렇지 않은 경우도 있다.
- 잘 알고 써야 하는 kotlin android extensions보다 ViewBinding으로 명확하게 사용하는 편이 좋다.
- Android Studio 4.1부터는 플러그인도 기본 제공하지 않지만 추가해 사용하는 것은 가능하다.
- Android Studio 4.2부터는 findViewById 대신 ViewBinding을 기본 샘플로 제공한다.
- ViewBinding을 잘 활용하면 편하다.
- Fragment에서는 ViewBinding의 Nullable 처리를 필요로 한다.

<br/>
<br/>

# 🗂 참고
- [Kotlin Android Extension(KTX) 적용하기 | by Hudson Park | Medium](https://medium.com/@logishudson0218/kotlin-android-extension-ktx-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0-100eb53c59df)
- [Android KTX  |  Kotlin  |  Android Developers](https://developer.android.com/kotlin/ktx?hl=ko)
- [Android-Study/AndroidKTX.md at master · taeiim/Android-Study (github.com)](https://github.com/taeiim/Android-Study/blob/master/study/week11/AndroidKTX/AndroidKTX.md)
- [Kotlin 합성 합성에서 Jetpack 뷰 결합으로 이전 | Android 개발자](https://developer.android.com/topic/libraries/view-binding/migration)
- [Android 개발자 블로그: Kotlin Android 확장 프로그램의 미래 (googleblog.com)](https://android-developers.googleblog.com/2020/11/the-future-of-kotlin-android-extensions.html)
- [Android 개발자 블로그: 조회수에 대한 Kotlin 합성 기능 중단 (googleblog.com)](https://android-developers.googleblog.com/2022/02/discontinuing-kotlin-synthetics-for-views.html)
- [[Android] Kotlin Android Extensions deprecated (tistory.com)](https://junyoung-developer.tistory.com/27)
- [[Android] 코틀린 Extension 대신 ViewBinding 사용하기 (tistory.com)](https://hanyeop.tistory.com/169)
- [Android Studio 4.1에서 제거된 Kotlin Android Extensions을 알아보자. (thdev.tech)](https://thdev.tech/android/2020/10/07/Remove-kotlinx-synthetic/)
