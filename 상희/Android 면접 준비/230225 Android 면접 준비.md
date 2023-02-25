# 230225 Android 면접 준비

## Q1. 메인 스레드는 Looper(루퍼)를 가지고 있나요?
메인 스레드는 핸들러 스레드라서 활성화된 루퍼를 가지고 있다.  
일반 스레드 루퍼는 비활성화 모드가 되고 핸들러 스레드는 활성화된 루퍼를 가지고 있다. 그러나 원한다면 일반 스레드를 위한 루퍼를 준비할 수 있다.

<br/>
<br/>

## Q2. View와 ViewGroup에 대해 설명해 주세요.
### View
안드로이드 화면의 구성 요소다. 화면에 보이는 모든 것은 View이다.

<br/>

EditText : 사용자 직접 입력할 수 있는 뷰  
Button : 사용자가 터치할 수 있는 뷰  
TextView : 사용자에게 텍스트를 출력하는 뷰  
ImageView : 사용자에게 이미지를 출력하는 뷰

<br/>

- View 클래스 상속도

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FKPC9X%2FbtqAfT7a283%2FhRVYDjz57om5SHzOwIKRX1%2Fimg.png)

<br/>

View는 자신이 화면 어디에 배치되어야 하는지에 대한 정보가 없다. View만으로 화면에 나타날 수 없다. View를 화면에 배치하기 위해서는 반드시 무언가가 필요하다. 그것이 바로 ViewGroup 혹은 View Container이다.

<br/>

### ViewGroup
n개의 View를 담을 수 있는 Container이다. ViewGrop 또한 View를 상속받아 만든 클래스. 또 다른 말로는 Layout이라고도 한다.

<br/>

- ViewGroup 클래스 상속도

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbzZwfL%2FbtqAhdDR1UW%2FKrl2KfuKwQU2VPOX3xFwmk%2Fimg.png)

<br/>

- View와 ViewGroup의 관계

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FoyJis%2FbtqAei0Tg1C%2F9NJI4LDFXgNrDLnMeCoRh0%2Fimg.png)

<br/>

ViewGroup은 View만 배치 가능하며 ViewGroup조차 View로 다룬다.  
그래서 자식 ViewGroup을 배치할 수 있다.

<br/>
<br/>

## Q3. Android Jetpack에 대해 설명해 주세요.
안드로이드 앱을 구축하는데 도움이 되는 훌륭한 도구 모음이다.  
즉, Jetpack은 안드로이드 개발자들이 더욱 쉽게 높은 퀄리티의 앱을 개발할 수 있도록 도와주는 라이브러리들의 모음집이다.

<br/>

Jetpack은 크게 4가지로 분류해서 생각할 수 있다.
- Foundation Components
- Architecture Components
- Behavior Components
- UI Components

<br/>
<br/>

## Q4. Android Manifest가 무엇인가요?
프로그램에서 필수적이며 루트 디렉터리에 선언되며 코드를 실행하기 전에 Android 시스템이 알아야 하는 애플리케이션에 대한 정보를 포함하는 곳이다.

<br/>
<br/>

## Q5. ObservableField 와 LiveData의 차이점은 무엇인가요?
ObservableField는 Lifecycle을 모르나 LiveData는 Lifecycle을 알고 있다.

<br/>
<br/>

## 🗂 참고
- [안드로이드 면접 질문 #04 (brunch.co.kr)](https://brunch.co.kr/@oemilk/17)
- [Android Interview (notion.so)](https://www.notion.so/3ce7ddf12ddb413a9d2213173654d52c)
- [안드로이드 뷰(View) 뷰그룹(ViewGrop) (tistory.com)](https://class-programming.tistory.com/21?category=790455)
