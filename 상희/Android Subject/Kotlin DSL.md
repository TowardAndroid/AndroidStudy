# 💡 Kotlin DSL

# ✅ DSL(Domain Specific Language)이란?
DSL은 Domain Specific Language의 약자로 특정 도메인에 국한해 사용하는 언어이다.  
자연어처럼 만들어 기존 코드보다 더 표현적이고 가독성이 좋게 만들어 사용한다.  
SQL도 DSL 언어 중 하나다.  
반대 개념으로는 General Purpose Language가 있으며 우리가 일반적으로 사용하는 C, C++, Kotlin, Swift 등의 프로그래밍 언어들이 이에 해당한다.

<br/>

## DSL 종류
DSL은 내부 DSL과 외부 DSL로 나누어진다.  
그 중, 이번에 알아볼 DSL은 내부 DSL이다.

<br/>

### 내부 DSL
- 호스트 언어(기존 언어)의 틀을 벗어나지 않으며 구성하는 것을 의미한다.  
- 기존 언어의 새로운 구문으로 도입되어 언어 확장을 할 수 있다.  
- 인라인 코드 형태로 표현이 가능하다.

<br/>

### 외부 DSL
- 기존 언어와 다른 언어를 통해 생성된 DSL의 의미한다.  
- XML, CSS 등

<br/>

## Kotlin에서의 DSL?
Kotlin으로 안드로이드를 개발하면서도 꽤나 자주 이러한 DSL들을 접하고 있다.  
예를 들면, 다음과 같이 빌드 스크립트에서 안드로이드 관련 옵션을 명시한다.  

```groovy
android {
    compileOptions {
        sourceCompatibility(JavaVersion.VERSION_11)
        targetCompatibility(JavaVersion.VERSION_11)
    }

    kotlinOptions {
        jvmTarget = "11"
    }

    buildFeatures {
        viewBinding = true
    }

    hilt {
        enableExperimentalClasspathAggregation = true
    }
}
```

<br/>

Coil(이미지 로딩 라이브러리 중 하나)을 사용하면서 이미지 로딩에 필요한 옵션들을 명시할 때 사용한다.

```kotlin
imageView.load("https://www.example.com/image.jpg") {
    crossfade(true)
    placeholder(R.drawable.image)
    transformations(CircleCropTransformation())
}
```

<br/>

위 예제들을 살펴보면 빌더나 팩토리를 이용하여 필요한 옵션을 명시하고 객체를 생성하는 구현 패턴과 비교하여 더 간략하고 읽기 쉽게 작성되어 있다는 것을 알 수 있다.  
이처럼 라이브러리 개발 시 DSL을 적절히 활용하여 제공하면 라이브러리 사용자는 보다 쉽고 간결하게 호출 코드들 작성할 수 있고, 잘 정의된 DSL은 상대적으로 자연어에 가까워 가독성도 높일 수 있다.

<br/>

코틀린에서 `Koin`, `Anko`  등 코틀린 전용 라이브러리에서도 DSL을 사용하는 것을 볼 수 있다.

```kotlin
val values = ContentValues()
values.put("id", 5)
values.put("name", "John Smith")
values.put("email", "user@domain.org")
db.insert("User", null, values)
```

<br/>

`Anko Sqlite`  라이브러리를 사용하지 않았을 때

```kotlin
db.insert("User", 
    "id" to 42,
    "name" to "John",
    "email" to "user@domain.org"
)
```

<br/>

`Anko Sqlite`  라이브러리를 사용하였을 때  
DSL을 적용했을 경우, 가독성이 더 뛰어나다.

```kotlin
inline fun Activity.verticalLayout(theme: Int = 0, init: (@AnkoViewDslMarker _LinearLayout).() -> Unit)
```

<br/>

위 함수는 `Anko Layout`의 DSL인데, 보다시피 확장 함수와 고차 함수를 사용하고 있다.  
물론, 이 예시 이외에도 DSL은 고차 함수나 확장 함수로 구현되어있는 경우가 많다.

<br/>

우리는 Kotlin 언어가 제공하는 다음의 몇 가지 기능들을 조합하여 간단히 DSL을 정의하고 사용할 수 있다.  
- 람다 표현식(Lambda Expression)
- 고차 함수(Higher-order Function)
- 확장 함수(Extension Function)

<br/>
<br/>

# ✅ Kotlin DSL 작성
코틀린이란 언어는 상당히 문법적으로 코드를 간결하게 작성할 수 있는 기능을 많이 제공한다.  
"중위 연산자", "확장 함수", "람다 구문의 it" 등을 지원하고 있다.  
우리는 이러한 방법을 이용해 좀 더 간결하게 코드를 작성할 수 있다.

<br/>

## 람다 표현식(Lambda Expression)
어떤 함수를 파라미터와 반환 값만으로 나타낸 표현식으로 식의 형태는 언어마다 조금씩 다르지만, Kotlin에서는 다음과 같이 add 함수를 나타낼 수 있다.

<br/>

### 함수 표현

```kotlin
fun add(num1: Int, num2: Int): Int
```

<br/>

### 람다 표현

```kotlin
(Int, Int) -> Int
```

<br/>

## 고차 함수(Higher-order Function)
고차 함수를 충족하려면 다음 조건 중 하나를 만족해야 한다.  
- 함수를 함수의 인자로 받는다.  
- 함수의 반환 값이 함수다.  
보통 이렇게 전달되거나 반환되는 함수는 람다 표현식으로 나타내게 된다.

<br/>

다음과 같이 calculate 함수를 정의하면 세 번째 파라미터로 수행하고자 하는 연산을 구현하는 함수를 전달하여 동적으로 다른 연산이 수행되도록 할 수 있다.

```kotlin
fun calculate(num1: Int, num2: Int, operation: (Int, Int) -> Int): Int {
    return operation(num1, num2)
}
```

<br/>

코틀린에서 자주 사용하는 `let`, `run`, `apply`, `with`도 모두 고차 함수다.

<br/>

### Apply
apply()를 예시로 들어보며 고차 함수가 어떻게 진행되는지 알아본다.

```kotlin
public inline fun <T> T.apply(block: T.() -> Unit): T {
    block()
    return this
}
```

<br/>

(Kotlin 1.2 버전부터는 apply 안에 contract 메소드가 추가되어있으나, 편한 설명을 위해 제외시켰다.)

```kotlin
val test = Test(3,5).apply {
    square()
}

data class Test(var x: Int, var y: Int){
    fun square(){
        x *= x
        y *= y
    }
}
```

`T.apply`는 함수를 호출한 객체를 블록의 리시버(this)에 전달하고, 객체를 반환하는 함수다.

<br/>

#### apply() 함수 진행도
1. `apply()`는 `block: T.() -> Unit` 라는 T의 확장 함수를 인자로 받는다.
2. 고로 `Test(3, 5).apply{}`를 호출하며 T의 확장 함수인 익명 함수를 생성한다.
3. 익명 함수 블록 안에서 리시버의 함수나 멤버를 사용한다.
4. `apply()` 에서 방금 선언한 익명 함수인 `block()`을 호출하고, 객체를 반환한다.

<br/>

#### 결론
다른 고차 함수도 apply() 처럼 인자로 받은 함수를 동작되게 하는 방식으로 수행된다.

<br/>

## 확장 함수(Extension Function)
확장 함수는 이미 정의된 클래스나 인터페이스에 상속 없이 함수를 추가 정의할 수 있도록 Kotlin에서 제공되는 기능이다.  
- ex 1 : Calculator 클래스에 clear() 함수를 추가 정의한다면 다음과 같이 정의하고 Calculator 클래스의 함수처럼 호출할 수 있다.
    
    ```kotlin
    fun Calculator.clear() { ... }
    ```

<br/>

- ex 2 : 문자열의 마지막 문자만 뽑아내려면 어떻게 해야 할까?    
    호출할 때마다 str[str.length - 1]처럼 긴 코드가 필요하다.    
    확장 함수를 이용해 조금 더 편하게 메소드를 만들 수 있다.
    
    ```kotlin
    fun String.lastIndex() = this[this.length - 1]
    ```
    
    확장 함수 기능을 이용해서 String 객체의 함수를 만들었고, 이제는 str.lastIndex()로 마지막 문자를 뽑아낼 수 있다.    
    - 확장 함수에서 this는 메소드를 호출한 객체를 가리킨다.
    - 만약 확장 함수의 이름과 원래 멤버 함수의 이름이 같다면, 무조건 멤버 함수가 호출된다.

<br/>
<br/>

# 🗂 참고
- [Kotlin DSL 간단히 알아보기. 나만의 언어 만들기 | by Myungpyo Shim | Medium](https://myungpyo.medium.com/kotlin-dsl-%EA%B0%84%EB%8B%A8%ED%9E%88-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0-5f95fddf00f9)
- [Android-Study/Kotlin-DSL.md at master · taeiim/Android-Study (github.com)](https://github.com/taeiim/Android-Study/blob/master/study/week11/Kotlin-DSL.md)
- [Kotlin DSL (tistory.com)](https://devroach.tistory.com/97?category=1035492)
- [Kotlin DSL을 이해해보자 - 1. 확장함수타입 (tistory.com)](https://deque.tistory.com/141)
