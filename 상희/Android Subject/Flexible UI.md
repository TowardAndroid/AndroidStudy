# 💡 Flexible UI

# ✅ Flexible UI
## 리소스 분기
안드로이드 프로젝트에서 아이콘이 있는 mipmap 디렉터리는 기기의 밀도(density)에 따라 분기하도록 되어 있다. 앱이 실행될 때 기기의 밀도에 따라 해당 폴더의 아이콘이 선택되는 것이다.

<br/>

![image](https://github.com/C0012S/AndroidStudy/assets/66476874/410ab741-3905-484c-8ed6-0951741225ca)

<br/>

레이아웃도 이런 식으로 분기하도록 처리할 수 있다.

<br/>

## 레이아웃 분기
1. 레이아웃 분기를 위해 res 디렉터리에서 마우스 오른쪽을 누르고 [New -> Android resource directory]를 클릭하여 리소스 디렉터리를 추가한다.
2. New Resource Directory 창에서 Resource type:은 'layout'을 선택하고, 왼쪽 하단에 Available qualifiers 상자에서 'Orientation'을 선택한 다음, 가운데에 있는 >> 버튼을 누른다.
3. Screen orientation: 항목에서 'Landscape'를 선택한다. 그러면 Directory name:이 layout-land로 설정되며, 이 디렉터리에 있는 레이아웃 XML은 가로 모드에 우선으로 적용되는 레이아웃이 된다.
4. layout/activity_main.xml 파일을 layout-land 디렉터리에 복사해서 붙여 넣는다.
5. 가로 모드와 세로 모드의 레이아웃을 설정한다.

<br/>

레이아웃 분기를 프래그 먼트와 조합하면 다양한 화면 구성을 보다 쉽게 구성할 수 있다.

<br/>

## 유연한 사용자 인터페이스 구축
다양한 화면 크기를 지원하도록 애플리케이션을 디자인할 경우, 프래그먼트를 다양한 레이아웃 구성에서 다시 사용하여 사용 가능한 화면 공간에 따라 사용자 환경을 최적화할 수 있다.  
예를 들어 핸드폰인 경우, 단일 창 사용자 인터페이스에 프래그먼트를 한 번에 하나씩만 표시하는 것이 적합할 수 있다. 반대로 화면 너비가 큰 태블릿에서는 프래그먼트를 나란히 설정하여 사용자에게 더 많은 정보를 표시할 수 있다.

<br/>

![Untitled](https://developer.android.com/static/images/training/basics/fragments-screen-mock.png?hl=ko)

> 서로 다른 화면 크기에서 같은 활동이 다른 구성으로 표시된 두 프래그먼트. 큰 화면에서는 두 프래그먼트를 모두 나란히 표시하지만, 핸드폰에서는 프래그먼트가 한 번에 하나씩 표시되므로 사용자가 이동할 때 프래그먼트가 서로 교체되어야 한다.
> 

<br/>

FragmentManager 클래스는 동적 경험을 연출하기 위해 런타임 시 활동에 프래그먼트를 추가, 삭제 및 교체할 수 있는 메서드를 제공한다.

<br/>
<br/>

# 🗂 참고
- [Android-Study/study/week12/FlexibleUI/FlexibleUI.md at master · taeiim/Android-Study (github.com)](https://github.com/taeiim/Android-Study/blob/master/study/week12/FlexibleUI/FlexibleUI.md)
- [플렉시블한(동적인) UI 만들기( Building a Flexible UI ) : 네이버 블로그 (naver.com)](https://m.blog.naver.com/kitesoft/220310618795)
- [유연한 UI 빌드  |  Android 개발자  |  Android Developers](https://developer.android.com/training/basics/fragments/fragment-ui?hl=ko)
- [프래그먼트  |  Android 개발자  |  Android Developers](https://developer.android.com/guide/components/fragments?hl=ko)
