# 💡 Java

# ✅ Java
## Java란?
자바(Java)는 C 언어에 객체 지향적 기능을 추가하여 만든 C++과는 달리 처음부터 객체 지향 언어로 개발된 프로그래밍 언어이다.  
자바는 자바 가상 머신(JVM, Java Virtual Machine)을 사용하여 운영체제와는 독립적으로 동작할 수 있다.  
따라서 자바는 어느 운영체제에서나 같은 형태로 실행될 수 있다.  
현재 자바는 전 세계에서 가장 많이 사용하는 프로그래밍 언어 중 하나이다.

<br/>

## Java의 역사
처음에 자바는 가전제품 내에서 동작하는 임베디드 프로그램을 위한 언어로 썬 마이크로시스템즈(Sun Microsystems)사의 제임스 고슬링(James Gosling) 팀에 의해 개발되었다.  
1991년에 오크(Oak)라는 이름으로 시작하여 1996년에 발표된 1.0.2 버전부터 자바(Java)라는 이름을 사용하게 된다.  
1998년 발표된 J2SE 1.2에서는 웹에서도 자바를 돌릴 수 있게 해 주는 자바 애플릿(Java Applet)이 추가되며 자바의 인기는 급상승하게 된다.  
그 후 버전이 업데이트될 때마다 다양한 기능이 지원되며 자바는 꾸준한 인기를 누리게 된다.  
이후 2009년에 썬 마이크로시스템즈사가 오라클과 인수 합병됨에 따라 자바 또한 오라클로 소유권이 넘어간다.

<br/>

## Java의 장단점
### Java의 장점
1. 자바는 운영체제와는 독립적으로 실행할 수 있다.
2. 자바는 불필요한 기능을 과감히 제거하여 다른 언어에 비해 배우기가 쉽다.
3. 자바는 자동 메모리 관리 등을 지원하여 다른 언어에 비해 안정성이 높다
4. 자바는 연산자 오버로딩을 금지하고 제네릭을 도입함으로써 코드의 가독성을 높였다.
5. 자바에 관한 수많은 참고 자료를 찾을 수 있다.

<br/>

### Java의 단점
1. 자바는 실행을 위해 자바 가상 머신을 거쳐야 하므로, 다른 언어에 비해 실행 속도가 느리다.
2. 자바는 예외 처리가 잘 되어 있지만, 개발자가 일일이 처리를 지정해 줘야 한다는 불편함이 있다.
3. 자바는 다른 언어에 비해 작성해야 하는 코드의 길이가 긴 편이다.

<br/>
<br/>

# ✅ Java 문법
## 자료형
자료형은 변수에 어떤 형태의 변수를 넣을 것인지 정하는 것이다.

<br/>

<table>
    <tr>
        <th>자료형</th>
        <th>키워드</th>
        <th>크기</th>
        <th>기본값</th>
        <th>표현 범위</th>
    </tr>
    <tr>
        <td rowspan="4">정수형</td>
        <td>byte</td>
        <td>1byte</td>
        <td>0</td>
        <td>-128 ~ 127</td>
    </tr>
    <tr>
        <td>short</td>
        <td>2byte</td>
        <td>0</td>
        <td>-32768 ~ 32767</td>
    </tr>
    <tr>
        <td>int</td>
        <td>4byte</td>
        <td>0</td>
        <td>-2147483648 ~ 2147483647</td>
    </tr>
    <tr>
        <td>long</td>
        <td>8byte</td>
        <td>0</td>
        <td>-9223372036854775808 ~ 9223372036854775807</td>
    </tr>
    <tr>
        <td>문자형</td>
        <td>char</td>
        <td>1byte</td>
        <td>\u0000</td>
        <td>0 ~ 65.535</td>
    </tr>
    <tr>
        <td rowspan="2">실수형</td>
        <td>float</td>
        <td>4byte</td>
        <td>0.0</td>
        <td>-3.4E38 ~ 3.4E38</td>
    </tr>
    <tr>
        <td>double</td>
        <td>8byte</td>
        <td>0.0</td>
        <td>-1.7E308 ~ 1.7E308</td>
    </tr>
    <tr>
        <td>논리형</td>
        <td>boolean</td>
        <td>1bit</td>
        <td>false</td>
        <td>true of false</td>
    </tr>
</table>

<br/>

## if, switch
주로 코드에 어떤 조건을 걸고 싶을 때 사용하는 문법이다.

<br/>

### if

```java
if (...) {
    // 구현 내용
}
else if (...) {
    // 구현 내용
}
else {
    // 구현 내용
}
```

<br/>

### switch

```java
switch (변수) {
    case ... :
    case ... :
        System.out.println("...");
        break;
    case ... :
    default ... :
        System.out.println("...");
```

switch 문에서는 default 생략이 가능하고, case에 해당하는 조건이 없을 시 실행되는 구문이다.

<br/>

## 반복문
어떤 행위를 반복할 때 사용하는 문법이다.

### for()

```java
for (int i = 0; i < 100; i++) {
    // 구현 내용
}
```

<br/>

### while()

```java
while (true) {
    // 구현 내용
}
```

<br/>

### do-while()

```java
do {
    // 구현 내용
} while (조건)
```

do-while() 문은 반복문 내부에 있는 내용을 최초로 먼저 실행한 다음 조건문을 검사한다.

<br/>

## Array
배열(Array)이란 선형 자료구조(Data Structure)중 하나로, 동일한 타입의 연관된 데이터를 메모리에 연속적으로 저장하여 하나의 변수에 묶어서 관리하기 위한 자료구조이다. 가장 기본적인 자료구조인 만큼 C, Java, Python 등 거의 모든 언어에 구현되어 있다.  
수많은 데이터를 저장할 때 배열을 사용하면 편리하다.  
1 차원부터 다차원까지 차수를 늘릴 수 있지만, 많으면 복잡해지기 때문에 보통 3 차원까지 사용한다.

<br/>

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://t1.daumcdn.net/cfile/tistory/99948E495E61E2BF0A](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://t1.daumcdn.net/cfile/tistory/99948E495E61E2BF0A)

<br/>

배열의 길이는 최초 선언한 값으로 고정되며 위와 같이 인덱스(Index)를 통해 데이터에 접근 할 수 있다.

<br/>

선언 및 초기화 방법은 다음과 같다.

```java
// 크기 할당과 초기화 없이 배열 참조 변수만 선언
int[] array;
int array[];

// 선언과 동시에 배열 크기 할당
int[] array = new int[5];
String array[] = new String[10];

// 기존 배열의 참조 변수에 초기화 할당
int[] array;
array = new int[5]; // 5의 크기를 가지고 초기값 0으로 채워진 배열 생성

// 선언과 동시에 배열의 크기 지정 및 값 초기화
int[] arr = {1, 2, 3, 4, 5}; 
int[] arr = new int[]  {1, 3, 5, 2, 4};    
int[] odds = {1, 3, 5, 7, 9};  
String[] weeks = {"월", "화", "수", "목", "금", "토", "일"};

// 2차원 배열 선언
int[][] arr = new int[4][3]; // 3의 크기의 배열을 4 개 가질 수 있는 2 차원 배열 할당  
int[][] arr = { {2, 5, 3}, {4, 4, 1}, {1, 7, 3}, {3, 4, 5}};
```

<br/>

## 접근 제한자
보통 클래스나 객체 사용 시 많이 사용되는 항목이다. 접근을 제한해 외부에서 데이터 접근을 하지 못하도록 막거나 모든 접근을 허용할 수 있도록 만드는 것이 바로 접근 제한자이다.  
이는 자바의 특징 중 하나인 캡슐화와도 연관되어 있는 내용이다.

<br/>

| 범위 | public | protected | default | private |
| --- | --- | --- | --- | --- |
| 클래스 내부 | O | O | O | O |
| 동일 패키지 | O | O | O | X |
| 다른 패키지 | O | X | X | X |
| 하위 패키지 | O | O | X | X |

<br/>

## final, static
### final
final이 사용되면 보통 상수화를 하기 위해 많이 사용된다고 알고 있다.  
자바에서도 비슷한 개념이다. final 필드에서 사용하게 되면 상수화를 하는 것이고, 메소드는 오버라이딩 불가, 클래스는 상속받을 수 없음을 의미한다.

<br/>

### static
자바에서 static을 쓴다는 것은 메모리에 한 번 할당되어 프로그램이 시작 시 단 한 번만 실행이 되며 프로그램이 종료될 때까지 해제되는 것을 말한다.  
그래서 주로 값이 변하지 않는 값에 static을 쓰게 되며 final과 같이 자주 쓰이는 문법이다.  
또한 동일한 클래스의 모든 객체들에 의해 공유된다. (공통 멤버)

<br/>

## Method
메소드는 어떤 한 가지의 특정 기능을 수행하기 위한 문법이다. 메소드를 사용하면 코드의 가독성이 좋아지며 코드 해석을 더욱 쉽게 할 수 있다.

<br/>

메소드 사용 방법은 다음과 같다.

```java
// 반환형 없음, 파라미터 없음
public void A() {
    // 구현 내용
}

// 반환형 없음, 파라미터 있음
public void A(int a) {
    // 구현 내용
}

// 반환형 int, 파라미터 없음
public int B() {
    // 구현 내용
}

// 반환형 int, 파라미터 있음
public int B(int b) {
    // 구현 내용
}
```

<br/>

보통 하나의 메소드당 하나의 기능을 수행하는 것을 권장한다. 이는 CleanCode를 하는 기법 중 하나이다.

<br/>

## Overloading & Overriding
자바에서 다형성을 지원하는 방법이다.

<br/>

### Overloading
오버로딩은 같은 이름의 메소드 여러 개를 가지면서 매개변수의 유형과 개수가 다르도록 하는 기술이다.

```java
public void A(int a) {
    // 구현 내용
}

public void A(int a, int b) {
    // 구현 내용
}
```

<br/>

### Overriding
오버라이딩은 상위 클래스가 가지고 있는 메소드를 하위 클래스가 재정의해서 사용한다.  
보통 부모 & 자식 관계에서 많이 사용되며 가져온 메소드는 기존 메소드와 동일한 구조를 가지고 있어야 한다.

```java
class Parent {
    public int A(int a) {
        return a;
    }
}

class Child extends Parent {
    @Override
    public int A(int a) {
        return a;
    }
}
```

<br/>

오버라이딩 시 Annotation으로 @Override를 붙여 주면 이 메소드는 오버라이딩되었다는 것을 더욱 쉽게 알아볼 수 있다.

<br/>

## Class
클래스는 객체 지향 프로그래밍(OOP)에서 자주 사용되는 문법이다.  
예를 들어, 어떤 제품을 만드는 데 부품을 먼저 개발하고 이 부품들을 하나씩 조립해서 완성된 제품을을 만들듯이 소프트웨어를 개발할 때에도 부품에 해당하는 객체들을 먼저 만들고, 이것들을 하나씩 조립해서 완성된 프로그램을 만드는 것이 객체 지향 프로그래밍이다.  
객체를 설계한 틀 혹은 설계도라고 이해하면 좋다.

<br/>

## Object
객체는 실제로 존재하거나 추상적으로 생각할 수 있는 것 중에서 자신의 속성을 가지고 있고 다른 것과 식별 가능한 것을 뜻한다.  
예를 들어, 자동차에는 다양한 부품이 있지만, 그 중 바퀴가 있다. 이 바퀴에는 A 업체의 바퀴와 B 업체의 바퀴, C 업체의 바퀴가 있다. 여기서 이 업체들의 바퀴를 객체라고 할 수 있고, 바퀴를 장착하는 행위를 클래스에서 한다. (정확히는 클래스 내부에 있는 메소드가 수행한다.)  
여기서 바퀴를 나열하는 것은 Interface를 사용할 수도 있고, Abstract Class를 사용할 수도 있다.

<br/>

## Casting
캐스팅은 한국말로 타입 변환이라는 뜻이다. 예를 들어, byte 타입을 int 타입으로 변환한다거나 그 반대로 변환하는 행위를 말한다.  
캐스팅은 자료형에도 자주 쓰이지만, 객체의 개념에서도 매우 많이 사용되는 기법이다.  
캐스팅에는 두 가지 방법이 있는데, 하나는 자동(묵시적) 타입 변환이고, 하나는 강제(명시적) 타입 변환이다.

<br/>

### 자동(묵시적) 타입 변환(Promotion)
자동 타입 변환은 프로그램 실행 도중 자동으로 타입 변환이 일어나는 것을 의미한다. 이것은 작은 크기를 가지는 타입이 큰 크기를 가지는 타입에 저장될 때 발생한다.

```java
// 큰 크기 타입 = 작은 크기 타입
ex : int a = char b
```

<br/>

큰 크기의 타입과 작은 크기의 타입을 구별하는 방법은 메모리의 크기이다. 자료형의 크기에 따라 나뉘게 된다. 또한 지정된 범위(표현 범위) 내에 포함된 자료형이어야만 자동 타입 변환을 사용할 수 있다.

<br/>

### 강제 타입 변환(Demotion)
큰 크기의 타입은 작은 크기의 타입으로 자동 타입 변환이 불가능하다. 그러나 메모리의 크기를 작게 쪼개어서 저장한다면 캐스팅이 가능하다.  
예를 들어, byte 타입에 int 타입을 캐스팅하고 싶을 때 int의 4byte를 1byte씩 쪼개서 1byte씩 byte 타입에 저장한다는 뜻이다. 이를 강제 타입 변환(Casting)이라고 한다.

<br/>

다음은 캐스팅을 사용하는 방법이다.

```java
// 작은 크기 타입 = (작은 크기 타입) 큰 크기 타입
ex : byte a = (byte) int b
```

<br/>

### 객체의 형 변환
서로 상속 관계에 있고, 왼쪽이 부모, 오른쪽이 자식의 형태를 띤다.

```java
Parent parent = new Child();
```

<br/>

이는 하위 클래스에서 상위 클래스 유형으로 할당하는 것은 가능하나 그 반대의 경우에는 강제 형 변환을 해야 한다. 앞서 얘기하는 것처럼 다음과 같이 사용하면 된다.

```java
// 자식 객체 = (자식 클래스) 부모 객체
ex : Child child = (Child) new Parent();
```

<br/>

이 외에도 인터페이스도 캐스팅이라는 것이 존재한다.

<br/>
<br/>

# 🗂 참고
- [코딩의 시작, TCP School](http://www.tcpschool.com/java/java_intro_basic)
- [[Android] 안드로이드 앱 개발을 위한 필요한 자바 문법 (tistory.com)](https://50billion-dollars.tistory.com/entry/Android-%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-%EC%95%B1-%EA%B0%9C%EB%B0%9C%EC%9D%84-%EC%9C%84%ED%95%9C-%ED%95%84%EC%9A%94%ED%95%9C-%EC%9E%90%EB%B0%94-%EB%AC%B8%EB%B2%95)
- [[Java] 배열(Array) 선언 및 초기화 하기 :: IfUwanna IT (tistory.com)](https://ifuwanna.tistory.com/231)
- [[Java]배열 초기화 방법(Initializing Array) (tistory.com)](https://developer-talk.tistory.com/773)
- [오버로딩과 오버라이딩 차이와 예제 (tistory.com)](https://private.tistory.com/25)
- [코딩의 시작, TCP School](http://www.tcpschool.com/java/java_usingMethod_overloading)
- [[Java] 메소드 오버로딩(Method Overloading) :: 데니스의 놀이터 (tistory.com)](https://2018-start.tistory.com/46)
