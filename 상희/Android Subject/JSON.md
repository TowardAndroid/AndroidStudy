# 💡 JSON

# ✅ JSON이란?
JSON은 JavaScript Object Notation의 약자이다.  
JSON은 좀 더 쉽게 데이터를 교환하고 저장하기 위하여 만들어진 텍스트 기반의 데이터 교환 표준이다.

<br/>

다음은 JSON 예제이다.

```json
{
    "language": [
        {
            "name": "HTML",
            "category": "web",
            "developer": "W3C"
        },
        {
            "name": "CSS",
            "category": "web",
            "developer": "W3C"
        },
        {
            "name": "Java",
            "category": "application",
            "developer": "Oracle"
        },
        {
            "name": "Python",
            "category": "application",
            "developer": "Python"
        }
    ]
}
```

<br/>

이러한 JSON은 XML의 대안으로서 좀 더 쉽게 데이터를 교환하고 저장하기 위하여 고안되었다.  
또한 JSON은 텍스트 기반이므로 어떠한 프로그래밍 언어에서도 JSON 데이터를 읽고 사용할 수 있다.

<br/>

## JSON의 특징
1. JSON은 자바스크립트를 확장하여 만들어졌다.
2. JSON은 자바스크립트 객체 표기법을 따른다.
3. JSON은 사람과 기계가 모두 읽기 편하도록 고안되었다.
4. JSON은 프로그래밍 언어와 운영체제에 독립적이다.

<br/>
<br/>

# ✅ JSON 문법 및 구조
## JSON 문법
JSON은 자바스크립트의 객체 표기법에서 리터럴(literal)과 프로퍼티(property)를 표현하는 방법만 가져와서 사용한다.  
따라서 JSON 데이터는 모양과 규칙이 매우 단순하다.  
그로 인해 브라우저 영역에서도 쉽고 빠르게 그 의미를 해석할 수 있으며 다른 프로그래밍 언어에서도 구현하기 쉽다.

<br/>

### 리터럴(literal)
리터럴(literal)은 변수와 다르게 해석되는 값 그 자체를 의미한다.  
다음 예제에서 등장하는 값은 모두 리터럴이다.

```json
12     // 숫자 리터럴
"JSON" // 문자열 리터럴
true   // 불리언 리터럴
```

<br/>

> 변수(variable)란 데이터(data)를 저장할 수 있는 메모리 공간을 의미하며 그 값이 변경될 수 있다.
> 

<br/>

### 객체(object)
객체(object)란 실생활에서 우리가 인식할 수 있는 사물로 이해할 수 있다.  
JSON에서 객체란 이름(name)과 값(value)으로 구성된 프로퍼티(property)의 정렬되지 않은 집합이다.  

<br/>

다음 예제는 이름과 값으로 이루어진 네 쌍의 프로퍼티를 가지는 "강아지" 객체를 나타내는 예제이다.

```json
{
    "name": "식빵",
    "family": "웰시코기",
    "age": 1,
    "weight": 2.14
}
```

<br/>

### JSON 주석
JSON 표준의 창시자인 더글라스 크록포드는 JSON에는 주석이 들어가지 않는 것이 바르다고 규정하고 있다.  
그것은 서로 다른 시스템 간의 연동과 호환성을 위한 조치였다.

<br/>

반드시 주석을 사용해야 한다면, 주석이 포함된 JSON 데이터를 파싱하기 전에 주석만을 먼저 제거해야 한다.  
하지만 되도록 JSON에는 주석을 사용하지 않는 것이 좋다.

<br/>

## JSON 구조
JSON은 자바스크립트의 객체 표기법으로부터 파생된 부분 집합이다.  
따라서 JSON 데이터는 다음과 같은 자바스크립트 객체 표기법에 따른 구조로 구성된다.  
1. JSON 데이터는 이름과 값의 쌍으로 이루어진다.
2. JSON 데이터는 쉼표(,)로 나열된다.
3. 객체(object)는 중괄호({})로 둘러싸서 표현한다.
4. 배열(array)은 대괄호([])로 둘러싸서 표현한다.

<br/>

### JSON 데이터
JSON 데이터는 이름과 값의 쌍으로 구성된다.  
이러한 JSON 데이터는 데이터 이름, 콜론(:), 값의 순서로 구성된다.

```json
// 문법
"데이터이름": 값
```

<br/>

다음 예제는 데이터의 이름이 "name"이고, 값은 "식빵"이라는 문자열을 갖는 JSON 데이터의 예제이다.

```json
"name": "식빵"
```

<br/>

데이터의 이름도 문자열이므로, 항상 큰따옴표("")와 함께 입력해야 한다.

<br/>

데이터의 값으로는 다음과 같은 타입이 올 수 있다.  
1. 숫자(number)
2. 문자열(string)
3. 불리언(boolean)
4. 객체(object)
5. 배열(array)
6. NULL

<br/>

### JSON 객체
JSON 객체는 중괄호({})로 둘러싸서 표현한다.  
또한 JSON 객체는 쉼표(,)를 사용하여 여러 프로퍼티를 포함할 수 있다.

```json
{
    "name": "식빵",
    "family": "웰시코기",
    "age": 1,
    "weight": 2.14
}
```

<br/>

JSON 객체를 그림으로 나타내면 다음과 같다.

![http://www.tcpschool.com/lectures/img_json_object.png](http://www.tcpschool.com/lectures/img_json_object.png)

<br/>

### JSON 배열
JSON 배열은 대괄호([])로 둘러싸서 표현한다.  
또한 JSON 배열은 쉼표(,)를 사용하여 여러 JSON 데이터를 포함할 수 있다.

<br/>

다음 예제는 배열의 이름이 "dog"이고, 3개의 JSON 객체를 요소로 가지는 JSON 배열의 예제이다.

```json
"dog": [
    {"name": "식빵", "family": "웰시코기", "age": 1, "weight": 2.14},
    {"name": "콩콩", "family": "포메라니안", "age": 3, "weight": 2.5},
    {"name": "젤리", "family": "푸들", "age": 7, "weight": 3.1}
]
```

<br/>

JSON 배열을 그림으로 나타내면 다음과 같다.

![http://www.tcpschool.com/lectures/img_json_array.png](http://www.tcpschool.com/lectures/img_json_array.png)

<br/>
<br/>

# ✅ Android JSON
안드로이드에서는 JSON 데이터를 조작하기 위해 4 가지 클래스를 제공한다.

<br/>

- JSONArray
- JSONObject
- JSONStringer
- JSONTokener

<br/>
<br/>

# 🗂 참고
- [코딩의 시작, TCP School](http://www.tcpschool.com/json/intro)
- [[Android] 안드로이드 - JSON 이란 무엇인가??? (tistory.com)](https://salix97.tistory.com/74)
- [org.json | 안드로이드 개발자 (android.com)](https://developer.android.com/reference/org/json/package-summary)
