리팩토링

겉으로 드러나는 코드의 기능은 바꾸지 않으면서 내부 구조를 개선하는 방식으로 소프트웨어 시스템을 수정하는 과정

리소스 리팩토링

`colors.xml`과 `dimens.xml`부터 수정하는 것이 좋다 → `style.xml`과 `themes.xml` 이 color와 dimens에 의존하기 때문이다

**colors.xml**

사용하는 모든 색을 정의

섹션을 나누어 컬러를 관리하는 것이 좋은 방법

**dimens.xml**

`dimens_base.xml`과 `dimens.xml`두 파일을 정의하는 것이 좋다

`dimens_base.xml` : 아이콘, 텍스트, 버튼 등 기본 구성요소의 기본 크기를 정의

space, text, button, radius, elevation 등으로 섹션을 만든다.

**themes.xml**

테마를 사용해서 각 컴포넌트의 윈도우 백그라운드, 컬러, 사이즈 등 공통 속성을 적용

테마로 적용하면 적용한 경우에 따라 범위 (액티비티나 애플리케이션) 의 모든 내용이 변경

**styles.xml**

더 로컬

`style.xml`을 파일 몇개로 분리.

`styles_login.xml` 이나 `styles_messages.xml` 등 과 같이 특정 페이지를 위한 다른 스타일을 만든다.

`styles.xml` 에는 아이콘, 텍스트, 버튼 처럼 기본 스타일을 정의

미리 속성들을 정의해놓고 사용! 레이아웃을 간단히 만들 수 있음

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e8759509-6bc7-4fb4-8340-979d113cba58/Untitled.png)

코드 리팩토링

**메서드 정리 > 메서드 추출 (Extract Method)**

메서드가 너무 길거나 코드에 주석을 달아야만 의도를 이해할 수 있을 때, 그 코드를 빼내어 별도의 메서드로 만든다.

직관적인 이름의 간결한 메서드가 좋다

간결한 메소드

1. 메서드가 적절히 잘게 쪼개져 있으면 다른 메서드에서 쉽게 사용할 수 있다.
2. 상위 계층의 메서드에서 주석 같은 더 많은 정보를 읽어들일 수 있다.
3. 재정의하기도 훨씬 수월하다.

기타

삼항연산자, for eache문 사용이가독성이좋다!

[https://academy.realm.io/kr/posts/android-resources-refactoring/](https://academy.realm.io/kr/posts/android-resources-refactoring/)
