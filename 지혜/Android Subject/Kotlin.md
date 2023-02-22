kotlin의 특성

1. 코틀린은 타입 추론을 지원하는 정적 타입 지정 언어 → 소스코드의 정확성과 성능을 보장하면서도 소스코드를 간결하게 유지
2. 객체지향과 함수형 프로그래밍 스타일 모두 지원
3. 안드로이드, 서버개발에서 활용가능
4. 무료, 오픈소스, 주요IDE와 빌드시스템을 완전히 지원
5. 실용적, 안전, 간결, 상호운용성이 좋다

코틀린 파일에도 패키지를 선언할 수 있는데, 반드시 파일의 첫 줄에 선언

코틀린에서는 이름을 먼저 적고 타입을 적는다.

타입선언

`val a: String = "foo"`

합수선언

```
fun greet(name: String) : Unit {
    println("Hello, $name!")
}

```

조건문

- if - else문은 자바와 사용 방법이 동일하다.
- when문은 자바의 switch와 동일한 역할을 한다.

반복문

for-each

let

이 함수를 호출한 객체를 이어지는 함수 블록의 인자로 전달한다

```
getPadding().let {
        it 은 패딩 값
        setPadding(it, 0, it, 0)
    }
```

apply

이 함수를 호출한 객체를 이어지는 함수 블록의 리시버로 전달한다.

```
params.apply {
        weight = 1f     params를 리시버로 전달 받았기 때문에 params.weight 이나 params.topMargin 바로사용
        topMargin = 100
    }
```

with

인자로 받은 객체를 이어지는 함수 블록의 리시버로 전달, block함수의 결과를 반환한다

```
with(textView) {
        text = "textView!!!"
        gravity = Gravity.CENTER_HORIZONTAL
    }
```

run

인자가 없는 익명 함수처럼 사용하는 형태와 객체에서 호출하는 형태 제공

함수형 인자 block을 호출하고 결과 반환 또는 호추랗ㄴ 객체를 함수형 인자 block의 리시버로 전달하고 그 결과를 반환한다.

```
val AplusB = run {
      val a = 1
      val b = 2
      a + b
  }

textView?.run {  with 와 비슷하지만 textView 의 널체크를 해야 하는경우 사용하면 좋다
        text = "textView!!!"
        gravity = Gravity.CENTER_HORIZONTAL
    }
```
