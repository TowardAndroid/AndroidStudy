# 230219 Android 면접 준비

## Q1. 안드로이드 데이터 전달 방법
- Activity 간 : Intent
- Fragment 간, Activity-Fragment 간 : Bundle

<br/>
<br/>

## Q2. Intent
Intent는 Messaging Object(메세지 객체)이다. 이 객체를 통해 다른 컴포넌트 간에 정보를 주고 받을 수 있다.

<br/>

> 안드로이드 어플리케이션을 구성하는 네 가지 기본 요소에는 Activity, Service, Broadcast Receiver, Content Provider가 있다. Intent(인텐트)란 이러한 어플리케이션 구성 요소(컴포넌트) 간에 작업 수행을 위한 정보를 전달하는 역할을 한다.  
인텐트를 가장 손쉽게 사용한 예로는 액티비티 간의 화면 전환을 들 수 있다.
> 

<br/>

### Intent Types
1. Explicit Intents (명시적)
    - 명시적 인텐트는 인텐트에 클래스 객체나 컴포넌트 이름을 지정하여 호출할 대상을 확실히 알 수 있는 경우에 사용한다. (주로 애플리케이션 내부에서 사용)
2. Implicit Intents (암시적)
    - 암시적 인텐트는 호출할 대상이 달라질 수 있는 경우에는 암시적 인텐트를 사용한다. (안드로이드 시스템이 인텐트를 이용해 요청한 정보를 처리할 수 있는 적절한 컴포넌트를 찾아 사용자에게 그 대상과 처리 결과를 보여 준다.)
    - ex :
        
        ```java
        Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse("http://m.naver.com"));
        startActivity(intent);
        
        ...
        
        Intent intent = new Intent(Intent.ACTION_VIEW,Uri.parse("tel:010-0000-0000"));
        startActivity(intent);
        ```
        
    - 암시적 인텐트는 보통 액션(Action)과 데이터(Data)라는 속성으로 구성되어있다. 이 두 가지 속성 말고도 Category, Type, Component, Extras라는 속성을 가진다. 
    Component라는 속성을 지정할 경우 컴포넌트 클래스 이름을 명시적으로 지정하게 되는데, 이 경우가 명시적 인텐트에 속하게 된다. 
    결국 암시적 인텐트는 Component 속성을 제외한 나머지 속성들로 구성되며, 이러한 속성들에 부합하는 컴포넌트가 실행된다.(호출할 대상들이 달라질 수 있다.)
    - ex :
        
        ```java
        ...
        
        public void onClick(View v){
          Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse("http://m.naver.com"));
          startActivity(intent);
        }
        ```

        <br/>

        위 코드를 실행했을 때의 화면은 다음과 같다.
        
        ![https://newgenerationkorea.files.wordpress.com/2015/07/intent.png](https://newgenerationkorea.files.wordpress.com/2015/07/intent.png)
        
        <br/>
        
        이와 같이 암시적 인텐트는 그 속성에 부합하는 컴포넌트가 여러 개 있을 때 선택할 수 있도록 해 준다.
        
<br/>

![https://blog.mindorks.com/images/what-are-intents-in-android-intent-flow.png](https://blog.mindorks.com/images/what-are-intents-in-android-intent-flow.png)

<br/>

### IntentFilter
암시적 인텐트를 통해 사용자로 하여금 어느 앱을 사용할지 선택하도록 할 때 IntentFilter가 필요하다.

<br/>

### PendingIntent
Intent를 가지고 있는 클래스로, 기본 목적은 다른 애플리케이션(다른 프로세스)의 권한을 허가하여 가지고 있는 Intent를 마치 본인 앱의 프로세스에서 실행하는 것처럼 사용하는 것이다.  
Notification은 안드로이드 시스템의 NotificationManager가 Intent를 실행한다. 즉, 다른 프로세스에서 수행하기 때문에 Notification으로 Intent 수행 시 PendingIntent의 사용이 필수다.  

<br/>
<br/>

## Q3. Intent와 Bundle의 용도
Intent는 저장이 아닌 전달하는 수단으로의 객체이고, Bundle은 상태, 값 등을 저장하기 위한 객체이다.  
Bundle의 보관은 Shut Down후 다시 초기화할 때 보관할 수 있다. 
- ex :
    - 메모리 부족으로 Shut Down되는 경우
    - 디바이스를 가로, 세로 모드로 바꿀 때 Shut Down되는 경우
- Bundle은 꾸러미, 묶음이라는 느낌을 가지고 있으며, 안드로이드에서도 비슷하게 어떤 값을 보관하고 있다고 생각하면 된다. 여기서 어떤 값을 보관할 때 안드로이드에서는 Hash Map형태로 저장한다.(Key, Value값을 put해서 보관)
- protected void onCreate(Bundle savedInstanceState)를 보자면, 처음 onCreate에 들어올 때 Bundle값인 savedInstanceState는 null값이 된다. 앱 실행 시 Key, Value값을 put해서 보관하지 않았기 때문이다. 앱 최초 실행 시에는 날아갈 데이터도 없기 때문에 따로 보관하는 과정이 없어도 된다.
- Shut Down이 발생하면 데이터가 날아가기 때문에 이 시점에 우리는 Bundle에 값을 보관해야 한다. 그럼 Shut Down될 때 데이터를 put 하기 위해서 protected void onSaveInstanceState(Bundle outState) 이 메서드를 오버라이드 해서 여기서 처리해주면 된다. 여기서 값을 보관하고 값을 다시 받아올 때는 protected void onRestoreInstanceState(Bundle savedInstanceState) 이 메서드를 오버라이드해서 get해서 값을 받아오면 된다. Key 값으로 접근하면 Value 값을 받아올 수 있다.

<br/>

## Q4. Android Architecture
안드로이드 아키텍처는 4 가지의 Key Componets로 이루어져 있다.  
1. Linux Kernel
2. Libraries
3. Android Framework
4. Android Applications

<br/>

![https://www.tutorialspoint.com/android/images/architecture.jpg](https://www.tutorialspoint.com/android/images/architecture.jpg)

<br/>

### Linux Kernel
- 리눅스 커널을 기반으로 구성되어 있으며 메모리 관리, 보안 설정, 네트워크 시스템 관리 등을 한다.

<br/>

### Libraries and Runtime
- 안드로이드 기능 라이브러리와 가상 머신의 역할을 하고 모바일 데이터베이스, 그래픽 등을 담당한다.

<br/>

### Android Framework
- 생명 주기, 환경 설정 등의 역할을 하고 대표적으로 GPS, 리소스 관리 등이 있다.

<br/>

### Android Applications
- 안드로이드에서 기본적으로 제공하는 역할을 한다.
- ex : 전화 걸기, 웹 브라우저 등

<br/>
<br/>

## Q5. OkHttp 라이브러리 & Retrofit 라이브러리
클라이언트와 서버 간 HTTP 통신을 쉽게 하기 위해 사용한다.

<br/> 

### OkHttp
- Interceptor를 통해 로그인을 위한 JWT 토큰을 자동으로 헤더에 붙여주는 등의 편리를 제공한다.
- HTTP NW 통신을 하는 동안, 빠르게 텍스트나 미디어 데이터를 전송하도록 하는 라이브러리다.
- OkHttp는 NW 통신 중에 오류가 발생하였을 때, 빠르게 상태를 회복한다. 이는 서비스 상에서 여러 개의 IP 주소들을 제공하였을 때, 오류가 발생하면 다른 IP 주소로 시도해봄으로써 이루어진다.
- request와 responce API를 제공하며, 이는 immutable하다. 이는 동시에 여러 blocking call을 수행하며, callback을 통해 비동기 작업을 지원한다.

<br/>

### Retrofit
- OkHttp라는 HTTP 통신 라이브러리 바탕으로 이루어져 있으며, Annotation을 사용하여 가독성을 제공한다.
- Java 기반 Android 상에서 HTTP client 역할을 수행하는 라이브러리다.
- Retrofit은 HTTP API(ex : JSON, XML)를 Java 객체로 변환하거나, HTTP API Service(HTTP client)를 생성하며, 이 HTTP Service의 Call을 통해 동기나 비동기 요청을 만들 수 있다.

<br/>

### 차이
Retrofit은 서버와 클라이언트 간의 인터페이스이며, 인터페이스 만으로는 통신을 수행할 수 없다. 이 때 사용하는 것이 OkHttp로 효율적인 NW 통신을 제공한다.

<br/>
<br/>

## 🗂 참고
- [안드로이드 앱개발자 기술면접 준비하기 (velog.io)](https://velog.io/@gina5757/%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-%EC%95%B1%EA%B0%9C%EB%B0%9C%EC%9E%90-%EA%B8%B0%EC%88%A0%EB%A9%B4%EC%A0%91%EC%A4%80%EB%B9%84%ED%95%98%EA%B8%B0)
- [Android Interview (notion.so)](https://www.notion.so/3ce7ddf12ddb413a9d2213173654d52c)
- [인텐트(Intent)란 무엇인가? – NEWGENERATION (wordpress.com)](https://newgenerationkorea.wordpress.com/2015/07/09/%EC%9D%B8%ED%85%90%ED%8A%B8intent%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80/)
- [Bundle(번들)이란? :: ProgrammingSource (tistory.com)](https://programmingsource.tistory.com/34)
- [OkHttp 와 Retrofit 차이 (tistory.com)](https://imomelet.tistory.com/47)
