# ๐ก DataBinding

# โ DataBinding์ด๋?
DataBinding์ XML ๋ ์ด์์์์ ๋ฐ์ดํฐ๋ฅผ ์ฌ์ฉํ  ์ ์๊ฒ ํด ์ฃผ๋ ๋ผ์ด๋ธ๋ฌ๋ฆฌ์ด๋ค.  
Android JetPack ๋ผ์ด๋ธ๋ฌ๋ฆฌ์ ํ๋์ ๊ธฐ๋ฅ์ด๋ค.  
์ฆ, DataBinding์ ์ ํ๋ฆฌ์ผ์ด์ ๋ก์ง๊ณผ ๋ ์ด์์์ bindingํ๋ ๋ฐ ํ์ํ ๊ธ๋ฃจ ์ฝ๋๋ฅผ ์ต์ํํ๋ค.

<br/>

> ๊ธ๋ฃจ ์ฝ๋๋?  
ํ๋ก๊ทธ๋จ์ ์๊ตฌ ์ฌํญ ๊ตฌํ์๋ ๊ธฐ์ฌํ์ง ์์ง๋ง, ๋ณธ๋ ํธํ์ฑ์ด ์๋ ๋ถ๋ถ๋ผ๋ฆฌ ๊ฒฐํฉํ๊ธฐ ์ํด ์๋ํ๋ ์ฝ๋
> 

<br/>

๋ด์ฉ์ด ์ด๋ ๋ค ๋ณด๋ findViewById๋ฅผ ์ฌ์ฉํ์ง ์์๋ ๋๋ฉฐ ๋ณดํต MVVM ํจํด์ ๊ตฌํํ  ๋ LiveData์ ํจ๊ป ๊ฑฐ์ ํ์์ ์ผ๋ก ์ฌ์ฉํ๋ค.

<br/>
<br/>

# โ DataBinding ์ฌ์ฉ ๋ฐฉ๋ฒ
## gradle ์ค์ 
DataBinding ์ค์ ๋ถํฐ ํ์ฑํ์์ผ ์ค์ผ ํ๋ค.  
App ๋ ๋ฒจ์ build.gradle์์ ์๋ ์ฝ๋๋ฅผ ์ถ๊ฐํ๋ค.

```groovy
android {
    ...
    dataBinding {    
 	      enabled = true
    }
}
```

<br/>

์ด๋ ๊ฒ ์ค์  ํ kotlin-kapt ํ๋ฌ๊ทธ์ธ์ด ์ ์ฉ๋์ด์ผ ํ๋ค๊ณ  ์๋ฆผ์ด ๋จ๊ฒ ๋๋ค๋ฉด, ์๋์ ๊ฐ์ด Plugin id๋ฅผ ์ ์ฉ์์ผ ์ค๋ค.  
๋ง์ฐฌ๊ฐ์ง๋ก App ๋ ๋ฒจ์ build.gradle์ ์์ ํ๋ค.

```groovy
plugins {
    id 'com.android.application'
    id 'kotlin-android'
    id 'kotlin-kapt' // ์ถ๊ฐ
}
```

<br/>

## Layout ์ค์ 
DataBinding์ ์ฌ์ฉํ๋ layout์๋ ํน๋ณํ ๋ ์ด์์ ์ค์ ์ ์ถ๊ฐํด ์ค์ผ ํ๋ค.  
๊ธฐ์กด ๋ ์ด์์๊ณผ๋ ์กฐ๊ธ ๋ค๋ฅด๋ค. XML์์์ View(Activity๋ Fragment)์ ์ํด ์ ๋ฌ๋ ์ด๋ฒคํธ๋ฅผ ์ฒ๋ฆฌํ๋ ํํ์์ ์ฌ์ฉํ๊ธฐ ๋๋ฌธ์ด๋ค. ๊ทธ๋์ ํน์ ํ ํ์์ผ๋ก ๊ตฌ์ฑ๋๋ค.

<br/>

layout์ ๋ฃจํธ ํ๊ทธ๋ก ์์ํ๊ณ  ์ฌ์ฉํ ๋ฐ์ดํฐ๋ค์ด data ํ๊ทธ์ ์ ์ธ๋๋ค.  
๊ทธ๋ฆฌ๊ณ  ๋์ ํํ ์ฌ์ฉ๋๋ view ํ๊ทธ๋ค์ด ๋ํ๋๊ฒ ๋๋ค.

<br/>

์ด๋ ๊ฒ DataBinding์ ์ฌ์ฉํ๊ธฐ ์ํ ํ์์ผ๋ก ๊ตฌ์ฑํด ์ค์ผ DataBinding ๋ผ์ด๋ธ๋ฌ๋ฆฌ์์ ํด๋น ๋ ์ด์์์ ํด๋์ค ํํ๋ก ์๋ ์์ฑํด ์ค ์ ์๋ค.  
์ด Binding ํด๋์ค๋ฅผ ํตํด ๋ณ์ ๊ฐ๋ค์ ์ค์ ํด์ ๋ ์ด์์์ ๋ณํ๋ฅผ ์ค ์ ์๊ธฐ ๋๋ฌธ์ ๊ผญ ์๋ ํ์์ผ๋ก ๋ ์ด์์์ ๋ง๋ค์ด ์ค๋ค.

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

## Layout์์ ๋ฐ์ดํฐ ๋ค๋ฃจ๊ธฐ
### ๋ณ์ ์ค์ ํ๊ธฐ

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

๋ ์ด์์์์ ์ฌ์ฉํ  ๋ณ์๋ฅผ ์ค์ ํ๋ ค๋ฉด layout ํ๊ทธ ๋ฐ์ data ํ๊ทธ๋ฅผ ์ ์ธํด ์ค๋ค.  
๊ทธ๋ฆฌ๊ณ  ๊ทธ ๋ฐ์ variable ํ๊ทธ๋ฅผ ์์ ๊ฐ์ด ์ค์ ํด ์ฃผ๋ฉด ๋๋ค.

<br/>

variable ํ๊ทธ์๋ ์๋ ๋ ๊ฐ์ง ์์ฑ ๊ฐ์ ๋ฐ๋์ ์๋ ฅํด ์ฃผ์ด์ผ ํ๋ค.
- name : ๋ ์ด์์์์ ์ฌ์ฉํ  ๋ณ์ ์ด๋ฆ์ ์๋ฏธํ๋ค.
- type : ๋ณ์ ํ์์ ์ค์ ํ๋ค. ์ง์  ๊ตฌํํ ํด๋์ค๋ถํฐ ๊ธฐ๋ณธ ํ์๊น์ง ๋ชจ๋ ์ค์ ์ด ๊ฐ๋ฅํ๋ค.

<br/>

๋ณ์๋ฅผ ์ค์ ํ  ๋, ์๋์ ๊ฐ์ ์์์ผ๋ก ์ฌ์ฉํ๋ค.

```xml
android:text="@{๋ณ์๋ช}"
```

<br/>

\<data>, \<variable>์ ์ ์ํ์ฌ ํด๋์ค ํ์ผ์ ํ๋์ ๊ฐ์ฒด๋ก ์ธ์งํ์ฌ ์ ๊ทผํ  ์ ์๊ฒ ํ๋ค.  
TextView์ ๋ณด๋ฉด android:text="@{user.lastName}" ํํ๋ก ๋์ด ์๋ ๊ฒ์ ํ์ธ ํ  ์ ์๋๋ฐ, ์ด๋ user๋ผ๊ณ  ๋ช์๋์ด ์๋ data class์ ํ๋ผ๋ฏธํฐ๋ฅผ ์ ๊ทผํ๋ ๋ฐฉ์์ด๋ค.  
ํฅํ์๋ DataBinding์ ์ด์ฉํด xml ํ์ผ ํํ์ layout์์ ํจ์๋ฅผ ์คํํ๊ธฐ๋ ํ๋ค.

<br/>  
  
### ๊ธฐ๋ณธ ๊ฐ ์ค์ ํ๊ธฐ

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
  
View์ ์์์ ๊ธฐ๋ณธ ๊ฐ์ ์ ์ฉํ๋ ค๋ฉด ์๋์ ๊ฐ์ด ์ฌ์ฉํ๋ค.

```xml
android:visibility="@{isEmpty ? View.VISIBLE : View.GONE, default=gone}" />
```

<br/>  
  
์ด ๊ฒฝ์ฐ visibility ์์์ ๋ํด ๊ธฐ๋ณธ ๊ฐ์ ์ ์ํ๋ ๊ฒ์ด๊ธฐ ๋๋ฌธ์ gone์ผ๋ก ํด ์ฃผ์๋ค.  
์ด๋ ๊ฒ ํ๋ ค๋ฉด data ํ๊ทธ์ Android View๊ฐ import๋์ด ์์ด์ผ ํ๋ค.  
๋ง์ฝ visibility๊ฐ ์๋ text์ธ ๊ฒฝ์ฐ์๋ ๊ธฐ๋ณธ ๊ฐ์ผ๋ก ๋ฌธ์์ด์ ์ค์ ํ  ์ ์๋ค.  
์ฆ, ์์์ ๋ฐ๋ผ ๊ธฐ๋ณธ ๊ฐ์ด ๋ฌ๋ผ์ง๊ฒ ๋๋ ๊ทธ์ ๋ง๋ ๊ฐ์ ๋ฃ์ด ์ฃผ์ด์ผ ํ๋ค๋ ๊ฒ์ด๋ค.

<br/>  
  
## xml์ Bindingํ  ๋ฐ์ดํฐ ํด๋์ค ์์ฑ

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
        binding.user = User("ํ", "์คํธ")

        binding.changeBtn.setOnClickListener {
            binding.invalidateAll()
        }

        binding.changeDataBtn.setOnClickListener {
            binding.user = User("์", "๋๋ค")
        }
    }
}
```

<br/>  
  
์์ ์์ฑํ xml์ ๋ ์ด์์์ผ๋ก ๊ฐ์ง๋ MainActivity๋ค.  
๋จผ์  binding ๋ณ์๋ฅผ ๋ง๋ค์ด ActivityMainBinding์ผ๋ก ์ด๊ธฐํํ๋ค. (ActivityMainBinding์ ๋ฐ๋ก ํด๋์ค๋ฅผ ํ์ผ ํํ๋ก ๋ง๋ค์ด์ ํ๋ ๊ฒ์ด ์๋๋ผ ์๋์ผ๋ก ์์ฑ๋๋ ๊ฑฑ์  X)  
์ดํ binding์ DataBindingUtil.setContentView๋ฅผ ์ด์ฉํ์ฌ ๋ ์ด์์์ ์ง์ ํด์ฃผ๊ณ , binding์ ํตํด layout์ ์๋ ๋ชจ๋  view์ ์ ๊ทผ์ด ๊ฐ๋ฅํ๋ค.  
์ฌ๊ธฐ์ ์ฃผ์ํด์ผ ํ  ์ ์ binding.user = User("ํ", "์คํธ") ์ธ๋ฐ ์ด ๋ถ๋ถ์ User ๋ฐ์ดํฐ ํด๋์ค๋ฅผ ๋ง๋ค์ด์ layout์ ๋ช์๋  user์ ๋ฃ์ด ์ฃผ์ด์ผ android:text="@{user.lastName}" ์ฝ๋๊ฐ ์ ์ ๋์ํ๋ค.

<br/>  
  
invalidateAll()์ UI๋ฅผ ์๋ก๊ณ ์นจ ํ๊ธฐ ์ํด์ ๋ชจ๋  ๋ฐ์ธ๋ฉ ํํ์์ ๋ฌดํจํํ๊ณ  ์๋ก์ด ๋ฆฌ๋ฐ์ธ๋๋ฅผ ์์ฒญํ๋ค.

<br/>  
  
> 1. DataBinding์ ์ ์ฉ์ํค๋ฉด ํด๋น xml ์ด๋ฆ์ ๋ง๋ Binding ํด๋์ค๊ฐ ์์ฑ๋๋ค.  
>   โ activity_main xml์ ๋ฐ์ดํฐ ๋ฐ์ธ๋ฉ์ ์ ์ฉ์์ผ์ ActivityMainBinding์ด ๋ง๋ค์ด์ง๋ค. (ํ์ค์นผ ํ๊ธฐ๋ฒ ๊ธฐ์ค)  
> 2. ์์ฑ๋ ๋ฐ์ธ๋ฉ ํด๋์ค๋ฅผ DataBinidngUtil ๊ฐ์ฒด์ setContentView ๋ฉ์๋๋ฅผ ์ด์ฉํด์ xml๊ณผ ์ฐ๊ฒฐ์ํจ๋ค.  
> 3. xml์์ ์์ฑํ๋ variable๋ค์ ํด๋นํ๋ ๊ฒ๋ค์ ์ฐ๊ฒฐ์์ผ ์ค๋ค.  
>   โ ์ฐ๊ฒฐ์์ผ ์ค ๋ ํด๋น Binding ํด๋์ค.์์ด๋๊ฐ ์ผ๋ก ํธ์ถํ๋ค. ์๋ฅผ ๋ค์ด ์์ ฏ์ ์์ด๋๊ฐ et_firstNumber ์๋ค๋ฉด binding.etFirstNumber๋ก ๋ถ๋ฌ์จ๋ค. (์นด๋ฉ ํ๊ธฐ๋ฒ ๊ธฐ์ค)  
>   โ findViewById()๊ฐ ํ์ ์๋ค.
> 

<br/>  
  
## ์ด๋ฒคํธ ์ฒ๋ฆฌ
๋ฐ์ดํฐ ๋ฐ์ธ๋ฉ์ ์ฌ์ฉํ์ฌ ๋ทฐ์ ๋ฐ์ก๋๋ ์ด๋ฒคํธ๋ฅผ ์ฒ๋ฆฌํ๋ ์์ผ๋ก onClick์ ์๋ก ๋ค ์ ์๋ค. ์ด๋ฒคํธ ์ฒ๋ฆฌ ๋ฐฉ๋ฒ์ ๋ ๊ฐ์ง๊ฐ ์๋ค.

<br/>  
  
### ๋ฉ์๋ ์ฐธ์กฐ
์ด๋ฒคํธ๋ฅผ ํธ๋ค๋ฌ ๋ฉ์๋์ ์ง์  ๋ฐ์ธ๋ฉํ๋ ๋ฐฉ๋ฒ์ด๋ค.

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
  
๋ฉ์๋ ์ฐธ์กฐ ์์ผ ๊ฒฝ์ฐ btnClick()์ View ํ๋ผ๋ฏธํฐ๋ฅผ ๊ผญ ์ง์ ํด ์ฃผ์ด์ผ ํ๋ค. ์ด๋ฒคํธ ์ฒ๋ฆฌ ๋ฐฉ๋ฒ์ ๋ ํ๋์ธ ๋ฆฌ์ค๋ ๋ฐ์ธ๋ฉ์์๋ ๋ฐ๋๋ก View ํ๋ผ๋ฏธํฐ๋ฅผ ๋นผ ์ฃผ์ด์ผ ์ ์์ ์ผ๋ก ๋์ํ๋ค.

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
  
acitivity๋ผ๋ variable์ \<layout> ์์ ์ ์ธํด ์ค๋ค.  
Button์ onClick์ actvitiy:btnClick๋ผ๊ณ  ์๋ ฅํด ์ฃผ๋ฉด ์ํ๋ ๋์์ด ์ด๋ค์ง๋ค.

<br/>  
  
### ๋ฆฌ์ค๋ ๋ฐ์ธ๋ฉ

์ด๋ฒคํธ ๋ฐ์ ์ ์คํ๋๋ ๋ฐ์ธ๋ฉ ์์ด๋ค. ๋ฉ์๋ ์ฐธ์กฐ์ ๋น์ทํ์ง๋ง, ๋ฆฌ์ค๋ ๋ฐ์ธ๋ฉ์ ์ฌ์ฉํ๋ฉด ์์์ ๋ฐ์ดํฐ ๋ฐ์ธ๋ฉ ์์ ์คํํ  ์ ์์ต๋๋ค. ์ด ๊ธฐ๋ฅ์ Android Gradle Plugin for Gradle ๋ฒ์  2.0 ์ด์์์ ์ฌ์ฉํ  ์ ์๋ค.

<br/>  
  
- ๋ฐ์ดํฐ๊ฐ ์๋ ๊ฒฝ์ฐ

MainActivity.kt

```kotlin
fun btnClick() {
    Toast.makeText(this, "btnClick",Toast.LENGTH_SHORT).show()
}
```

<br/>  
  
๋ฉ์๋ ์ฐธ์กฐ์ ๋ฌ๋ฆฌ View ํ๋ผ๋ฏธํฐ๋ฅผ ์ ๊ฑฐํด ์ฃผ์ด์ผ ํ๋ค.

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
  
- ๋ฐ์ดํฐ๊ฐ ์๋ ๊ฒฝ์ฐ

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
  
๋ฐ์ดํฐ๋ฅผ ๋ฃ์ด ์ฃผ๊ธฐ ์ํด์๋ model์ ์์ฑํด ์ฃผ์ด์ผ ํ๋ค. title ๋ณ์ 1๊ฐ๋ฅผ ๊ฐ์ง๋ ๋ชจ๋ธ์ ์์ ๊ฐ์ด ๋ง๋ค์ด ์ค๋ค.

<br/>  
  
MainActivity.kt

```kotlin
val simpleModel = SampleModel("Android DataBinding")

binding.model = simpleModel
```

<br/>  
  
SimpleModel ์ mTitle ํ๋ผ๋ฏธํฐ์ "Android DataBinding" ๋ณ์๋ฅผ ๋ฃ์ด ์ ์ธ ํ ๋ฐ์ธ๋ฉ ์ฐ๊ฒฐ

<br/>  
  
```kotlin
fun btnClick(title: String) {
    Toast.makeText(this, "title : $title",Toast.LENGTH_SHORT).show()
}
```

<br/>  
  
btnClick์ title ๋ณ์๋ฅผ ์ถ๊ฐํด ์ค๋ค.

<br/>  
  
activity_main.xml

```xml
<variable
    name="model"
    type="com.example.databinding_sample.SampleModel"/>
```

<br/>  
  
\<data> \</data> ์ฌ์ด์ SampleModel์ ์ถ๊ฐํด ์ค๋ค.

<br/>  
  
```xml
<Button
    android:text="activity"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:onClick="@{() -> activity.btnClick(model.title)}"/>
```

<br/>  
  
activity.btnClick ๋ณ์์ model.title์ ์ค์ ํด ์ฃผ๋ฉด SampleModel์ ์ ์ธํ  ๋ ์ค์ ํด ๋ "Android DataBinding"์ ์ถ๋ ฅํ๊ฒ ๋๋ค.

<br/>

## ์กฐ๊ฑด๋ฌธ ์ฌ์ฉํ๊ธฐ

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
        android:text='@{"์ ์ฒด " + String.valueOf(likeProductVal != null ? likeProductVal : 0) + "๊ฐ"}'
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>    
</layout>
```

<br/>  
  
DataBinding์์๋ if ๋ฌธ์ ์ธ ์ ์๋ ๋์  ์ผํญ ์ฐ์ฐ์๋ฅผ ํตํด ์กฐ๊ฑด๋ฌธ์ ๊ตฌํํ  ์ ์๋ค.

<br/>  
  
```xml
android:text='@{"์ ์ฒด " + String.valueOf(likeProductVal != null ? likeProductVal : 0) + "๊ฐ"}'
```

<br/>  
  
์์ฒ๋ผ likeProductVal์ด null์ด ์๋ ๋์๋ง ์ ์ฉํ  ์ ์๊ฒ ์กฐ๊ฑด์ ์ ์ฉํ  ์ ์๋ค.  
์ด๋ ์ฃผ์ํ  ์ ์ ๋ฐ์ดํฐ ํ์์ด๋ค. ์์ ์กฐ๊ฑด์ผ๋ก ๋ฆฌํด๋๋ ๋ฐ์ดํฐ ํ์์ด Integer์ด๊ธฐ ๋๋ฌธ์ ์๋์ ๊ฐ์ ์๋ฌ๊ฐ ๋  ์ ์๋ค.

```xml
failed to call Observer method
```

<br/>  
  
text ์์ฑ์ ๊ฒฝ์ฐ string ํ์์ด ์ ์ฉ๋๋ ๊ฒ์ด ๋ง๋ค. ๋ฐ๋ผ์ ์ผํญ ์ฐ์ฐ์๋ฅผ ํตํด ๋ฆฌํด๋ ๊ฐ์ String์ผ๋ก ํ์์ ๋ณ๊ฒฝํด ์ฃผ๋ฉด ๋๋ค.

<br/>
<br/>  

# ๐ ์ฐธ๊ณ 
- [[Android] Data Binding ๊ธฐ๋ณธ ํ์ฉ๋ฒ ์ด์ ๋ฆฌ (tistory.com)](https://show-me-the-money.tistory.com/entry/Android-Data-Binding-%EA%B8%B0%EB%B3%B8-%ED%99%9C%EC%9A%A9%EB%B2%95-%EC%B4%9D%EC%A0%95%EB%A6%AC)
- [[Android] Databinding์ ์์๋ณด์!๐ (velog.io)](https://velog.io/@jojo_devstory/Android-Databinding%EC%9D%84-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90)
- [[Android] DataBinding ์ฌ์ฉํด๋ณด๊ธฐ - Junghoon's Blog (junghun0.github.io)](https://junghun0.github.io/2019/05/22/android-databinding/)
- [Android - DataClass, DataBinding (tistory.com)](https://ddunnimlabs.tistory.com/173)
- [Databinding ์ฌ์ฉ๋ฒ (brunch.co.kr)](https://brunch.co.kr/@mystoryg/150)
- [[Android/kotlin] DataBinding ํํค์น๊ธฐ (tistory.com)](https://gaybee.tistory.com/23)
- [[Android, Databinding] ๋ฐ์ดํฐ ๋ฐ์ธ๋ฉ ์ด๋ฒคํธ ์ฒ๋ฆฌ (tistory.com)](https://black-jin0427.tistory.com/134)
