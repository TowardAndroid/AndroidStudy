# 💡 DataBinding

# ✅ DataBinding이란?
DataBinding은 XML 레이아웃에서 데이터를 사용할 수 있게 해 주는 라이브러리이다.  
Android JetPack 라이브러리의 하나의 기능이다.  
즉, DataBinding은 애플리케이션 로직과 레이아웃을 binding하는 데 필요한 글루 코드를 최소화한다.

<br/>

> 글루 코드란?  
프로그램의 요구 사항 구현에는 기여하지 않지만, 본래 호환성이 없는 부분끼리 결합하기 위해 작동하는 코드
> 

<br/>

내용이 이렇다 보니 findViewById를 사용하지 않아도 되며 보통 MVVM 패턴을 구현할 때 LiveData와 함께 거의 필수적으로 사용한다.

<br/>
<br/>

# ✅ DataBinding 사용 방법
## gradle 설정
DataBinding 설정부터 활성화시켜 줘야 한다.  
App 레벨의 build.gradle에서 아래 코드를 추가한다.

```groovy
android {
    ...
    dataBinding {    
 	      enabled = true
    }
}
```

<br/>

이렇게 설정 후 kotlin-kapt 플러그인이 적용되어야 한다고 알림이 뜨게 된다면, 아래와 같이 Plugin id를 적용시켜 준다.  
마찬가지로 App 레벨의 build.gradle을 수정한다.

```groovy
plugins {
    id 'com.android.application'
    id 'kotlin-android'
    id 'kotlin-kapt' // 추가
}
```

<br/>

## Layout 설정
DataBinding을 사용하는 layout에는 특별히 레이아웃 설정을 추가해 줘야 한다.  
기존 레이아웃과는 조금 다르다. XML상에서 View(Activity나 Fragment)에 의해 전달된 이벤트를 처리하는 표현식을 사용하기 때문이다. 그래서 특정한 형식으로 구성된다.

<br/>

layout을 루트 태그로 시작하고 사용한 데이터들이 data 태그에 선언된다.  
그리고 나서 흔히 사용되는 view 태그들이 나타나게 된다.

<br/>

이렇게 DataBinding을 사용하기 위한 형식으로 구성해 줘야 DataBinding 라이브러리에서 해당 레이아웃을 클래스 형태로 자동 생성해 줄 수 있다.  
이 Binding 클래스를 통해 변수 값들을 설정해서 레이아웃에 변화를 줄 수 있기 때문에 꼭 아래 형식으로 레이아웃을 만들어 준다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<layout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    >

<androidx.constraintlayout.widget.ConstraintLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="PSH"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
</layout>
```

<br/>

## Layout에서 데이터 다루기
### 변수 설정하기

```xml
<?xml version="1.0" encoding="utf-8"?>
<layout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools">

    <data>
        <variable
            name="user"
            type="com.example.databinding_sample.data.User" />
    </data>

<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

<TextView
    android:id="@+id/firstname_textView"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="@{user.firstName, default=defaults}" />

<TextView
    android:id="@+id/lastname_textView"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="@{user.lastName, default=defaults}" />
    
</layout>
```

<br/>

레이아웃에서 사용할 변수를 설정하려면 layout 태그 밑에 data 태그를 선언해 준다.  
그리고 그 밑에 variable 태그를 위와 같이 설정해 주면 된다.

<br/>

variable 태그에는 아래 두 가지 속성 값을 반드시 입력해 주어야 한다.
- name : 레이아웃에서 사용할 변수 이름을 의미한다.
- type : 변수 타입을 설정한다. 직접 구현한 클래스부터 기본 타입까지 모두 설정이 가능하다.

<br/>

변수를 설정할 때, 아래와 같은 양식으로 사용한다.

```xml
android:text="@{변수명}"
```

<br/>

\<data>, \<variable>을 정의하여 클래스 파일을 하나의 객체로 인지하여 접근할 수 있게 했다.  
TextView에 보면 android:text="@{user.lastName}" 형태로 되어 있는 것을 확인 할 수 있는데, 이는 user라고 명시되어 있는 data class의 파라미터를 접근하는 방식이다.  
향후에는 DataBinding을 이용해 xml 파일 형태의 layout에서 함수를 실행하기도 한다.

<br/>  
  
### 기본 값 설정하기

```xml
<?xml version="1.0" encoding="utf-8"?>
<layout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools">

    <data>
        <import type="android.view.View" />
        <variable
            name="isEmpty"
            type="Boolean" />

        <variable
            name="user"
            type="com.example.databinding_sample.data.User" />

        <variable
            name="activity"
            type="com.example.databinding_sample.MainActivity" />
    </data>

    <androidx.constraintlayout.widget.ConstraintLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".MainActivity">

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:orientation="vertical"
            android:gravity="center"
            app:layout_constraintBottom_toBottomOf="parent"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintHorizontal_bias="0.0"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toTopOf="parent"
            app:layout_constraintVertical_bias="1.0">

            <TextView
                android:id="@+id/firstName"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="@{user.firstName}"
                android:visibility="@{isEmpty ? View.VISIBLE : View.GONE, default=gone}" />

            <TextView
                android:id="@+id/lastName"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="@{user.lastName}" />

            <Button
                android:id="@+id/changeBtn"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="Change Me" />

            <Button
                android:id="@+id/changeDataBtn"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="UserClassChange" />
        </LinearLayout>
    </androidx.constraintlayout.widget.ConstraintLayout>
</layout>
```

<br/>  
  
View의 요소에 기본 값을 적용하려면 아래와 같이 사용한다.

```xml
android:visibility="@{isEmpty ? View.VISIBLE : View.GONE, default=gone}" />
```

<br/>  
  
이 경우 visibility 요소에 대해 기본 값을 정의하는 것이기 때문에 gone으로 해 주었다.  
이렇게 하려면 data 태그에 Android View가 import되어 있어야 한다.  
만약 visibility가 아닌 text인 경우에는 기본 값으로 문자열을 설정할 수 있다.  
즉, 요소에 따라 기본 값이 달라지게 되니 그에 맞는 값을 넣어 주어야 한다는 것이다.

<br/>  
  
## xml에 Binding할 데이터 클래스 생성

```kotlin
data class User(
    val firstName : String,
    val lastName : String
}
```

<br/>  
  
## MainActivity.kt

```kotlin
class MainActivity : AppCompatActivity() {

    private lateinit var binding: ActivityMainBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        binding = DataBindingUtil.setContentView(this, R.layout.activity_main)
        binding.activity = this
        binding.user = User("테", "스트")

        binding.changeBtn.setOnClickListener {
            binding.invalidateAll()
        }

        binding.changeDataBtn.setOnClickListener {
            binding.user = User("입", "니다")
        }
    }
}
```

<br/>  
  
위에 작성한 xml을 레이아웃으로 가지는 MainActivity다.  
먼저 binding 변수를 만들어 ActivityMainBinding으로 초기화한다. (ActivityMainBinding은 따로 클래스를 파일 형태로 만들어서 하는 것이 아니라 자동으로 생성되니 걱정 X)  
이후 binding에 DataBindingUtil.setContentView를 이용하여 레이아웃을 지정해주고, binding을 통해 layout에 있는 모든 view에 접근이 가능하다.  
여기서 주의해야 할 점은 binding.user = User("테", "스트") 인데 이 부분은 User 데이터 클래스를 만들어서 layout에 명시된  user에 넣어 주어야 android:text="@{user.lastName}" 코드가 정상 동작한다.

<br/>  
  
invalidateAll()은 UI를 새로고침 하기 위해서 모든 바인딩 표현식을 무효화하고 새로운 리바인드를 요청한다.

<br/>  
  
> 1. DataBinding을 적용시키면 해당 xml 이름에 맞는 Binding 클래스가 생성된다.  
>   → activity_main xml에 데이터 바인딩을 적용시켜서 ActivityMainBinding이 만들어진다. (파스칼 표기법 기준)  
> 2. 생성된 바인딩 클래스를 DataBinidngUtil 객체의 setContentView 메서드를 이용해서 xml과 연결시킨다.  
> 3. xml에서 생성했던 variable들을 해당하는 것들에 연결시켜 준다.  
>   → 연결시켜 줄 때 해당 Binding 클래스.아이디값 으로 호출한다. 예를 들어 위젯의 아이디가 et_firstNumber 였다면 binding.etFirstNumber로 불러온다. (카멜 표기법 기준)  
>   → findViewById()가 필요 없다.
> 

<br/>  
  
## 이벤트 처리
데이터 바인딩을 사용하여 뷰에 발송되는 이벤트를 처리하는 식으로 onClick을 예로 들 수 있다. 이벤트 처리 방법은 두 가지가 있다.

<br/>  
  
### 메서드 참조
이벤트를 핸들러 메서드에 직접 바인딩하는 방법이다.

<br/>  
  
MainActivity.kt

```kotlin
class MainActivity : AppCompatActivity() {

    private lateinit var binding: ActivityMainBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        binding = DataBindingUtil.setContentView(this, R.layout.activity_main)
        binding.activity = this@MainActivity
    }

    fun btnClick(view: View) {
        Toast.makeText(this, "btnClick",Toast.LENGTH_SHORT).show()
    }
}
```

<br/>  
  
메서드 참조 식일 경우 btnClick()에 View 파라미터를 꼭 지정해 주어야 한다. 이벤트 처리 방법의 또 하나인 리스너 바인딩에서는 반대로 View 파라미터를 빼 주어야 정상적으로 동작한다.

<br/>  
  
activity_main.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<layout>

    <data>
        <variable
            name="activity"
            type="com.example.databinding_sample.MainActivity" />
    </data>

    <LinearLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        android:orientation="vertical"
        android:gravity="center"
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <Button
            android:text="activity"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="@{activity::btnClick}"/>

    </LinearLayout>
</layout>
```

<br/>  
  
acitivity라는 variable을 \<layout> 안에 선언해 준다.  
Button의 onClick에 actvitiy:btnClick라고 입력해 주면 원하는 동작이 이뤄진다.

<br/>  
  
### 리스너 바인딩

이벤트 발생 시 실행되는 바인딩 식이다. 메서드 참조와 비슷하지만, 리스너 바인딩을 사용하면 임의의 데이터 바인딩 식을 실행할 수 있습니다. 이 기능은 Android Gradle Plugin for Gradle 버전 2.0 이상에서 사용할 수 있다.

<br/>  
  
- 데이터가 없는 경우

MainActivity.kt

```kotlin
fun btnClick() {
    Toast.makeText(this, "btnClick",Toast.LENGTH_SHORT).show()
}
```

<br/>  
  
메서드 참조와 달리 View 파라미터를 제거해 주어야 한다.

<br/>  
  
activity_main.xml

```xml
<Button
    android:text="activity"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:onClick="@{() -> activity.btnClick()}"/>
```

<br/>  
  
- 데이터가 있는 경우

SimpleModel.kt

```kotlin
class SampleModel(mTitle: String) {

    val title =  ObservableField<String>()

    init {
        title.set(mTitle)
    }
}
```

<br/>  
  
데이터를 넣어 주기 위해서는 model을 생성해 주어야 한다. title 변수 1개를 가지는 모델을 위와 같이 만들어 준다.

<br/>  
  
MainActivity.kt

```kotlin
val simpleModel = SampleModel("Android DataBinding")

binding.model = simpleModel
```

<br/>  
  
SimpleModel 의 mTitle 파라미터에 "Android DataBinding" 변수를 넣어 선언 후 바인딩 연결

<br/>  
  
```kotlin
fun btnClick(title: String) {
    Toast.makeText(this, "title : $title",Toast.LENGTH_SHORT).show()
}
```

<br/>  
  
btnClick에 title 변수를 추가해 준다.

<br/>  
  
activity_main.xml

```xml
<variable
    name="model"
    type="com.example.databinding_sample.SampleModel"/>
```

<br/>  
  
\<data> \</data> 사이에 SampleModel을 추가해 준다.

<br/>  
  
```xml
<Button
    android:text="activity"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:onClick="@{() -> activity.btnClick(model.title)}"/>
```

<br/>  
  
activity.btnClick 변수에 model.title을 설정해 주면 SampleModel을 선언할 때 설정해 둔 "Android DataBinding"을 출력하게 된다.

<br/>

## 조건문 사용하기

```xml
<?xml version="1.0" encoding="utf-8"?>
<layout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools">

    <data>
        <variable
            name="isEmpty"
            type="Boolean" />
        <variable
            name="likeProductVal"
            type="Integer" />
    </data>

<androidx.constraintlayout.widget.ConstraintLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/main_like_product_num"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text='@{"전체 " + String.valueOf(likeProductVal != null ? likeProductVal : 0) + "개"}'
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>    
</layout>
```

<br/>  
  
DataBinding에서는 if 문을 쓸 수 없는 대신 삼항 연산자를 통해 조건문을 구현할 수 있다.

<br/>  
  
```xml
android:text='@{"전체 " + String.valueOf(likeProductVal != null ? likeProductVal : 0) + "개"}'
```

<br/>  
  
위처럼 likeProductVal이 null이 아닐 때에만 적용할 수 있게 조건을 적용할 수 있다.  
이때 주의할 점은 데이터 타입이다. 위의 조건으로 리턴되는 데이터 타입이 Integer이기 때문에 아래와 같은 에러가 날 수 있다.

```xml
failed to call Observer method
```

<br/>  
  
text 속성의 경우 string 타입이 적용되는 것이 맞다. 따라서 삼항 연산자를 통해 리턴된 값을 String으로 타입을 변경해 주면 된다.

<br/>
<br/>  

# 🗂 참고
- [[Android] Data Binding 기본 활용법 총정리 (tistory.com)](https://show-me-the-money.tistory.com/entry/Android-Data-Binding-%EA%B8%B0%EB%B3%B8-%ED%99%9C%EC%9A%A9%EB%B2%95-%EC%B4%9D%EC%A0%95%EB%A6%AC)
- [[Android] Databinding을 알아보자!😎 (velog.io)](https://velog.io/@jojo_devstory/Android-Databinding%EC%9D%84-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90)
- [[Android] DataBinding 사용해보기 - Junghoon's Blog (junghun0.github.io)](https://junghun0.github.io/2019/05/22/android-databinding/)
- [Android - DataClass, DataBinding (tistory.com)](https://ddunnimlabs.tistory.com/173)
- [Databinding 사용법 (brunch.co.kr)](https://brunch.co.kr/@mystoryg/150)
- [[Android/kotlin] DataBinding 파헤치기 (tistory.com)](https://gaybee.tistory.com/23)
- [[Android, Databinding] 데이터 바인딩 이벤트 처리 (tistory.com)](https://black-jin0427.tistory.com/134)
