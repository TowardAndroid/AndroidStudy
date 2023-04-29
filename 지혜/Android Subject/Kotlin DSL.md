DSL

DSL은 Domain Specific Language의 약자로 특정 도메인에 국한해 사용하는 언어입니다. 반대 개념으로는 General Purpose Language가 있으며 우리가 일반적으로 사용하는 C, C++, Kotlin, Swift 등의 프로그래밍 언어들이 이에 해당

사용예

빌드 스크립트에서 안드로이드 관련 옵션을 명시

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/500a9364-eb1a-42e3-96d9-e764c8fe00b5/Untitled.png)

Coil (이미지 로딩 라이브러리 중 하나)을 사용하면서 이미지 로딩에 필요한 옵션들을 명시할 때 사용

DSL사용 장점

DSL을 적절히 활용하여 제공하면 라이브러리 사용자는 보다 쉽고 간결하게 호출 코드들 작성할 수 있고, 잘 정의된 DSL은 상대적으로 자연어에 가까워 가독성도 높일 수 있습니다

DSL 정의

## **람다 표현식**

어떤 함수를 파라미터와 반환값 만으로 나타낸 표현식으로, 식의 형태는 언어마다 조금씩 다르지만 Kotlin에서는 다음과 같이 `add` 함수를 나타낼 수 있습니다.

```
함수 표현 : fun add(num1: Int, num2: Int): Int람다 표현 : (Int, Int) -> Int
```

## **고계함수**

어떤 함수가 하나 이상의 함수를 파라미터로 갖거나, 함수를 반환하는 경우 고계함수라고 부릅니다. 그리고 보통 이렇게 전달되거나 반환되는 함수는 람다 표현식으로 나타내게 됩니다.

```java
fun calculate(num1: Int, num2: Int, operation: (Int, Int) -> Int): Int {
  return operation(num1, num2)
}
```

## **확장함수**

확장 함수는 이미 정의된 클래스나 인터페이스에 상속 없이 함수를 추가 정의할 수 있도록 Kotlin에서 제공되는 기능입니다. 예를 들어 Calculator 클래스에 clear() 함수를 추가 정의한다면 다음과 같이 정의하고 Calculator 클래스의 함수처럼 호출할 수 있습니다.

```
fun Calculator.clear() { ... }
```

**Kotlin-DSL**

Kotlin-DSL은 코틀린의 언어적 특성을 살려 Gradle(빌드 배포 도구) 스크립트를 작성하는 것을 목적으로 하는 DSL인 것입니다.

### 장단점

- 익숙하지 않아 이해가 어려웠던 Groovy대신 Kotlin을 사용할 수 있다
- 코드를 강조할 수 있고, 자동완성이 지원되며, 오류 코드가 강조되고 변수 리팩토링이 가능한 향상된 편집환경을 지원한다.
- 멀티 모듈 사용 시 중복 의존성 선언이 필요가 없어진다.

• 빌드 시간은 Groovy DSL이 Kotlin DSL보다 빠릅니다.

참조

[https://velog.io/@jeongminji4490/Android-Kotlin-DSL](https://velog.io/@jeongminji4490/Android-Kotlin-DSL)

[https://myungpyo.medium.com/kotlin-dsl-간단히-알아보기-5f95fddf00f9](https://myungpyo.medium.com/kotlin-dsl-%EA%B0%84%EB%8B%A8%ED%9E%88-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0-5f95fddf00f9)

[https://deque.tistory.com/141](https://deque.tistory.com/141)
