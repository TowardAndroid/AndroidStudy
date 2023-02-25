android Jetpack의 구성요소

데이터 결합 라이브러리는 선언적 형식으로 레이아웃의 ui구성요소를 앱의 데이터 소스와 결합할 수 있는 지원 라이브러리

```
<TextView
        android:text="@{viewmodel.userName}" />
```

장점

레이아웃 파일에서 구성요소를 결합하면 활동에서 많은 UI프레임워크 호출을 삭제할 수 있어 파일이 더욱 단순화되고 유지관리 쉬워짐

앱 성능 향상

메모리 누수 및 NULL 포인터 예외 방지

기본 데이터 소스가 변경될 떄 ui새로고침에 신경쓰지 않아도 된다 

ui개발 단순화

양방향 데이터 결합 지원(데이터 변경사항을 받는 동시에 속성의 사용자 업데이트를 수신 대기하는 기능(

적용

layout태그안에 data요소 내에서 변수를 연결하는 표현식, 레이아웃뷰 작성

build.gradle파일에 dataninding 요소 추가

```
dataBinding {
    enabled = true
}
```

```
<layout xmlns:android="http://schemas.android.com/apk/res/android">

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

데이터 클래스 생성

```
public class User {
    private final String firstName;
    private final String lastName;

    public User(String firstName, String lastName) {
        this.firstName = firstName;
        this.lastName = lastName;
    }

    public String getFirstName() {
        return firstName;
    }

    public String getLastName() {
        return lastName;
    }
}
```

데이터 바인딩 하기

```
public class MainActivity extends AppCompatActivity{
    ActivityMainBinding binding;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        binding = DataBindingUtil.setContentView(this, R.layout.activity_main);
        User user = new User("JungHoon", "Park");
        binding.setUser(user);
}
```

`MainActivityBinding binding = MainActivityBinding.inflate(getLayoutInflater());`

`ListItemBinding binding = DataBindingUtil.inflate(layoutInflater, R.layout.list_item, viewGroup, false);`

[https://junghun0.github.io/2019/05/22/android-databinding/](https://junghun0.github.io/2019/05/22/android-databinding/)

[https://developer.android.com/topic/libraries/data-binding?hl=ko](https://developer.android.com/topic/libraries/data-binding?hl=ko)
