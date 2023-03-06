# 230307 Android 면접 준비

## Q1. 모바일 애플리케이션 테스트와 모바일 테스트의 차이점은 무엇인가요?
모바일 앱 테스트는 주로 애플리케이션의 기능과 특징에 초점을 맞춘 디바이스에서 애플리케이션을 테스트하는 것이다.  
그리고 모바일 테스트는 실제 모바일 장치의 테스트이며 통화, SMS, 연락처, 미디어 플레이어, 내장 브라우저 등과 같은 모바일 기능에 중점을 둔다.

<br/>
<br/>

## Q2. Android에서 .apk 확장자는 무엇인가요?
Android 운영체제에서 사용하는 기본 파일 형식이다. 애플리케이션 패키지 키트(APK)는 모바일 앱 설치에 사용된다. .apk에는 리소스 파일, 인증서, 매니페스트 파일 및 기타 코드가 포함된다.  
APK 파일은 확장자가 .apk인 zip 형식의 아카이브 파일이다.

<br/>
<br/>

## Q3. Vector와 Bitmap의 차이점을 말씀해 주세요.
- Vector는 리사이징 되어도 전혀 깨지지 않는다. 모든 해상도에서 자유자재로 활용할 수 있기 때문에 특정 해상도에 제한되어 있지 않다는 것이 핵심이다. (ex : SVG)
- Bitmap은 픽셀로 구성되어 있으며 자유자재로 바꿀 수 없고 움직일 수도 없다. (ex : PNG, JPEG)

<br/>
<br/>

## Q4. FragmentManager vs SupportFragmentManager vs ChildFragmentManager
- FragmentManager : fragment 객체를 관리하기 위한 것이다.
- Activity에서 FragmentManager의 경우 Activity class에서 가져오고, SupportFragmentManager는 FragmentActivity에서 가져온다. FragmentActivity 역시 Activity를 상속받지만, 상속받으면서 androidx로 마이그레이션 된다. 즉, supportFragmentManager는 androidX에서 사용하기 위한 fragmentManager이다.
- Fragment에서 fragmentManager는 Activity와 Fragment 둘 다에서 관리가 가능하며, childFragmentManager는 Fragment에서만 관리가 가능하다.

<br/>
<br/>

## Q5. 백그라운드에서 UI 업데이트하는 방법을 말씀해 주세요.
- Handler.post, Looper Handler, mainThread 안에 Handler 만들어 놓고 다른 스레드에서 메시지 넣어 주기
- runOnUIThread
- AsyncTask

<br/>
<br/>

## 🗂 참고
- [상위 35 개 Android 인터뷰 질문 및 답변 - 다른 (myservername.com)](https://ko.myservername.com/top-35-android-interview-questions)
- [Android Interview (notion.site)](https://www.notion.so/3ce7ddf12ddb413a9d2213173654d52c)
- [Android 관련 (notion.site)](https://www.notion.so/f6a62f46c5954fa2ae01a7fae36feeef)
- [Android-Study/신입 안드로이드 개발자로 취업하기 - 면접.md at master · taeiim/Android-Study (github.com)](https://github.com/taeiim/Android-Study/blob/master/study/week16/%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C%20%EA%B0%9C%EB%B0%9C%EC%9E%90%EB%A1%9C%20%EC%B7%A8%EC%97%85%ED%95%98%EA%B8%B0%20-%20%EB%A9%B4%EC%A0%91/%EC%8B%A0%EC%9E%85%20%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C%20%EA%B0%9C%EB%B0%9C%EC%9E%90%EB%A1%9C%20%EC%B7%A8%EC%97%85%ED%95%98%EA%B8%B0%20-%20%EB%A9%B4%EC%A0%91.md)
