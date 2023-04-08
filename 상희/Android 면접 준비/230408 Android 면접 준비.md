# 230408 Android 면접 준비

## Q1. Android에서 BroadcastReceiver란 무엇인가요?
- 안드로이드에서 BroadcastReceiver는 앱에서 발생하는 이벤트를 수신하는 앱 구성 요소이다.
- BroadcastReceiver는 등록된 이벤트가 발생할 때마다 실행된다.
- 예를 들어, 배터리가 부족해지면 BroadcastReceiver를 사용하여 알림을 받을 수 있다.

<br/>
<br/>

## Q2. Android에서 AsyncTask란 무엇인가요?
- 안드로이드에서 AsyncTask는 비동기적인 작업을 수행하기 위한 클래스다.
- AsyncTask는 메인 스레드에서는 실행되지 않으며, 백그라운드 스레드에서 실행된다.
- AsyncTask는 doInBackground() 메서드에서 백그라운드 작업을 수행하고, 결과 값을 onPostExecute() 메서드에서 반환한다.

<br/>
<br/>

## Q3. Android에서 Retrofit이란 무엇인가요?
- 안드로이드에서 Retrofit은 RESTful API를 호출하는 라이브러리이다.
- Retrofit은 OkHttp 라이브러리와 함께 사용되며, JSON 형식으로 데이터를 주고받을 수 있다.
- Retrofit은 인터페이스를 사용하여 API 호출을 정의하고, Retrofit 라이브러리가 자동으로 구현한다.

<br/>
<br/>

## Q4. Android에서 Room이란 무엇인가요?
- 안드로이드에서 Room은 SQLite 데이터베이스를 사용하기 쉽게 만든 라이브러리이다.
- Room은 ORM(Object-Relational Mapping) 패턴을 사용하여 데이터베이스 작업을 추상화한다.
- Room은 데이터베이스 쿼리를 컴파일하고, SQLite 데이터베이스에 대한 코드를 생성하여 작성을 용이하게 한다.

<br/>
<br/>

## Q5. Android에서 ProGuard란 무엇인가요?
- 안드로이드에서 ProGuard는 코드 난독화, 최적화, 제거를 수행하는 도구이다.
- ProGuard를 사용하면 앱의 크기를 줄이고, 보안을 강화할 수 있다.
- ProGuard는 안드로이드 스튜디오에서 쉽게 사용할 수 있으며, 프로젝트의 build.gradle 파일에 설정할 수 있다.

<br/>
<br/>

## 🗂 참고
- [[Android] 기술 면접 질문 준비 (tistory.com)](https://blacktrees.tistory.com/entry/Android-%EA%B8%B0%EC%88%A0-%EB%A9%B4%EC%A0%91-%EC%A7%88%EB%AC%B8-%EC%A4%80%EB%B9%84)
