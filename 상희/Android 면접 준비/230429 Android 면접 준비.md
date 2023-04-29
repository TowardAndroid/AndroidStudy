# 230429 Android 면접 준비

## Q1. 바이트 코드를 안드로이드에서 바로 실행할 수 있나요?
바로 실행할 수 없다. Java 바이트 코드를 실행하려면 JVM(Java Virtual Machine)이 필요하지만, 안드로이드는 JVM 대신 Dalvik VM을 사용하여 메모리, 배터리 수명 및 성능에 더 초점을 맞춰 개발이 되었기 때문에 실행할 수 없다. (라이센스 문제도 있었다고 한다.)  
또한  dx라는 안드로이드 도구를 사용하여 Java 클래스 파일을 Dalvik 실행 파일(.dex 파일)로 바꿔 실행한다.  
- Dalvik VM : 32비트만 지원 (JIT 컴파일러 - 실행하면 만들어 놓고)  
- ART VM : 32비트, 64 비트 모두 지원 (AOT 컴파일러 - 미리 만들어 놓고)

<br/>
<br/>

## Q2. lateinit에 대해 설명해 주세요.
초기화 지연 프로퍼티(Late-initialized property)라고 하며 프로퍼티의 초기화를 나중에 하기 위해 사용하는 키워드다.  
프로퍼티 선언에 사용되며 항상 사용 가능한 것은 아니다.  
사용하기에 몇 가지 제약 사항이 있다.  
- var(mutable) 프로퍼티만 사용 가능
- non-null 프로퍼티만 사용 가능
- 커스텀 getter/setter가 없는 프로퍼티만 사용 가능
- primitive type 프로퍼티는 사용 불가능
- 클래스 생성자에서 사용 불가능
- 로컬 변수로 사용 불가능

<br/>
<br/>

## Q3. lazy에 대해 설명해 주세요.
lazy도 lateinit과 마찬가지로 초기화를 지연시킬 때 사용하며 lateinit은 Modifier지만 lazy는 람다를 파라미터로 받고 Lazy<T> 인스턴스를 반환하는 함수다.  
lazy도 사용에 제약 사항이 있는데 lateinit과 차이점이 있다.  
- val(immutable) 프로퍼티만 사용 가능
- primitive type에도 사용 가능
- 커스텀 getter/setter가 없는 프로퍼티만 사용 가능
- Non-null, Nullable 둘 다 사용 가능
- 클래스 생성자에서 사용 불가능
- 로컬 변수에서 사용 가능

<br/>
<br/>  
  
## Q4. Kotlin Scope Function에 대해 설명해 주세요.
- apply : 생성과 동시에 초기화 하고 자기 자신을 return
- also : 자기 자신이 필요한데, 초기화를 좀 더 쉽게(수신 객체를 사용하지 않거나, 수신 객체의 속성을 변경하지 않고 사용할 때)
- with : (생성과 동시에 초기화, null이 될 수 없는) 결과가 필요하지 않을 경우
- run : 객체의 값의 접근을 쉽게 할 때
- let : 객체의 값이 명확해야 할 때

<br/>  
<br/>
  
## Q5. Kotlin Companion object에 대해 말씀해 주세요.
- 클래스가 메모리에 적재되면서 함께 생성되는 객체이다. (자바의 static처럼 사용이 가능)
- static처럼 사용 가능하지만, static과는 다르다. Companion object는 변수에 할당이 가능하고, 변수를 통해 멤버를 참조할 수도 있다. (static과 다르며 더 많은 일을 할 수 있다.)

<br/>
<br/>
  
## 🗂 참고
- [안드로이드 면접 질문 1 (tistory.com)](https://nanamare.tistory.com/99)
- [[android] 면접 질문 (colinch4.github.io)](https://colinch4.github.io/2021-06-04/%EB%AC%B4%EC%A0%9C-10/)
- [Android Interview (notion.site)](https://www.notion.so/3ce7ddf12ddb413a9d2213173654d52c)
