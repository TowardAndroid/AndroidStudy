# 💡 Custom UI

# ✅ Custom UI란?
Android에서는 기본적으로 Button, TextView 등 기본적인 UI를 제공해 준다.  
모든 UI들은 View 클래스를 상속받아 만들어진다.  
이 중에서 ViewGroup을 상속받은 UI들을 Layout이라고 하고 나머지를 Widget이라고 한다.  
ViewGroup을 상속받은 Layout들은 자식 뷰를 가질 수 있기 때문에 이를 배치하는 역할을 한다.

<br/>

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://t1.daumcdn.net/cfile/tistory/2459953A571670000F](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://t1.daumcdn.net/cfile/tistory/2459953A571670000F)

<br/>

하지만 자신이 custom해서 직접 UI를 만들어 사용할 수도 있다.  
자신만의 Button이나 View를 만들고 싶다면 View 클래스를 상속받아서 필요한 메소드들을 오버라이드하면 된다.

<br/>

CustomView는 View 클래스를 상속하여 만든다.  
CustomLayout은 ViewGroup 클래스를 상속하여 만든다.

<br/>

## View 메소드 호출 순서
![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/DskeA/btqNXdSkcpk/RR6CN1AIUyXi591TObdK6K/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/DskeA/btqNXdSkcpk/RR6CN1AIUyXi591TObdK6K/img.png)

<br/>

### View 오버라이드할 메소드
- onMeasure
    - 하는 일        
        : View의 크기를 결정할 때 불리는 함수다.        
    - 함수 호출 과정        
        : View.measure() → View.onMeasure() → View.setMeasuredDimension()        
    - 설명        
        : view 자신의 크기를 지정하는 함수이다.        
        인자로는 (int widthMeasureSpec, int heightMeasureSpec) 넓이, 높이 값이 각 모드와 함께 조합된 값이다. 이 값들을 사용하기 위해서는 MeausreSpce의 getMode()와 getSize()를 사용해야 한다.        
        - int widthMode = MeasureSpec.getMode(widthMeasureSpec)
        - int width = MeasureSpec.getSize(widthMeasureSpec)
        
        <br/>
        
        이 때 Mode는 3가지가 존재한다.        
        - MeasureSpec.UNSPECIFIED : 소스상에서 View를 생성했을 때 해당 모드가 넘어 온다. 이 경우 그냥 인자로 넘어온 그대로 사용하면 된다.
        - MeasureSpec.AT_MOST : 이 경우는 View 내부의 크기를 계산한 값을 넘겨 주면 된다. View의 layout_width, layout_height가  wrap_content로 설정된 경우 이 모드가 넘어오게 된다. MeasureSpec.getSize()를 통해 나온 값은 View가 최대로 가질 수 있는 크기이다. 이를 바탕으로 내부 크기를 계산해야 한다. 내부 크기가 이 값보다 크다면 문제가 될 수 있다.
        - MeasureSpec.EXACTLY : 해당 View의 layout_width, layout_height가 fill_parent나 match_parent일 경우 부모 layout(viewGroup)이 해당 View의 크기를 미리 지정해서 width와 height를 넘겨 주므로 MeasureSpec.getSize()으로 반환된 값을 그냥 사용하면 된다.
        
        <br/>
        
        onMeasure() 함수 override시 내부에서는 setMeasuredDimesion()함수를 호출해서 자신의 크기를 설정하여야만 한다. (기본 동작은 super.onMeasure()을 호출해라.)        
        setMeasuredDimension()함수는 자신의 크기를 설정하는 함수로 view의 width,height 값에 상관없이 실제 크기는 이 함수를 통해 지정된다. (view의 width,height은 view의 크기를 권고하는 것이다. 실제는 setMeasuredDimension()에 지정한 값으로 크기가 결정된다.)        
        만약 onMeasure()에서 setMeasuredDimension()을 호출하지 않으면 java.lang.IllegalStateException 예외가 발생한다.        
    - 내부에서 많이 쓰이는 함수
        - this.measureChild() : 자식 뷰의 크기를 계산시킨다.
        - this.getChildMeasureSpec() : measureChildren()에서 사용하는 하나의 메소드이다. 이 메소드를 통해 특정 자식 view의 MeasureSpce을 만들 수 있다.

<br/>

- onLayout
    - 하는 일        
        : child view의 위치를 잡아주는 일을 한다. onMeasure 호출 후에 onLayout이 호출되므로 자신의 크기를 이미 인지하는 상태에서 위치를 잡아 줄 수 있다.        
        주의할 점은 이 위치가 장비 디스플레이의 절대적 위치이다. 부모를 기준으로 한 상대적인 위치가 아니다.        
        만약 한 view의 Layout의 크기가 width 100, height 100이고 measure된 크기가 width 20, height이라면 공간은 100x100을 할당하지만 크기는 20x20으로 그려진다.        
    - 함수 호출 과정        
        : ViewGroup.layout() → View.layout() → View.onLayout()        
    - 설명        
        : ViewGroup을 상속하여 layout을 만드는 경우 child view의 위치를 잡아주는 역할을 한다.        
        넘어 오는 파라미터는 어플리케이션 전체를 기준으로 위치가 넘어오므로 주의해야 한다.        
    - 내부에서 많이 쓰이는 함수
        - this.getPaddingLeft() : 자신의 왼쪽 패딩 값
        - this.getPaddingTop() : 자신의 위쪽 패딩 값
        - this.getPaddingRight() : 자신의 오른쪽 패딩 값
        - this.getPaddingBottom() : 자신의 아래쪽 패딩 값
        - this.getMeasuredWidth() : 자신의 크기 계산 후 나온 넓이
        - this.getMeasuredHeight() : 자신의 크기 계산 후 나온 높이
        - getChildCount() : 자식 뷰의 개수를 반환한다.
        - child.measure() : 자식 뷰의 크기를 반환한다. 이 때 MeasureSpec.AT_MOST로 거의 호출한다.
        - child.getMeasuredWidth() : 자식 뷰의 넓이를 가져온다. child.measure() 호출 후 호출한다.
        - child.getMeasuredHeight() : 자식 뷰의 길이를 가져온다. child.measure() 호출 후 호출한다.
        - child.layout() : 자식 뷰의 위치를 지정한다.

<br/>

- onDraw
    - 하는 일        
        : 화면을 그리는 일을 한다.        
        주의할 점은 이때 좌표의 기준은 디스플레이의 절대적인 위치가 아니다. 자신을 기준으로 한 좌표이다.        
    - 설명        
        : 자신을 그리고 자식이 있는 경우 자식들을 그리면 된다.        
    - 내부에서 많이 쓰이는 함수
        - cavans() : Canvas 의 모든 그리는 함수는 다 사용한다.
        - this.getMeasuredWidth() : view 자신의 넓이를 반환한다. 이를 바탕으로 그리면 된다.
        - this.getMeasuredHeight() : view 자신의 높이를 반환한다. 이를 바탕으로 그리면 된다.

<br/>

- 기타
    - 쓰이는 함수        
        : MeasureSpec.makeMeasureSpec : 길이와 모드를 조합하여 measurespec 값을 만든다.        
    - 참고 사항
        - padding 과 margin 의 차이 : padding은 내부 여백, margin은 외부 여백
            - 마진(margin) vs 패딩(padding) : [마진(margin)과 패딩(padding)의 차이점을 알아보자!! (tistory.com)](http://clason.tistory.com/321)
        - invalidate()와 requestLayout() 의 차이 : invalidate는 화면이 유효하지 않으니 다시 그리도록 하라는 것이고 requestLayout()은 layout을 갱신하라는 것이다.
            - 참고 : [android - Usage of forceLayout(), requestLayout() and invalidate() - Stack Overflow](https://stackoverflow.com/questions/13856180/usage-of-forcelayout-requestlayout-and-invalidate)

<br/>
<br/>

# ✅ CustomView
## CustomView란?
![http://labs.brandi.co.kr///assets/2021/1014/01.png](http://labs.brandi.co.kr///assets/2021/1014/01.png)

<br/>

위 그림에서 최상단에 위치하고 있는 뷰는 사용자 인터페이스를 구축하고 유저의 모든 입력 이벤트를 처리하는 기본적인 클래스이다. 스크린의 직사각형 영역을 차지하며 해당 자식 요소들과 함께 측정, 배치, 그리는 역할을 합니다. ViewGroup은 하위(자식) 뷰를 포함하고 자체 레이아웃 속성을 정의할 수 있다.

<br/>

CustomView는 아래와 같을 때 도움이 될 수 있다.  
- 현재 일반적인 안드로이드 구성 요소로는 원하는 작용이나 애니메이션 또는 UI를 만들 수 없을 때
- 코드 재사용성을 위해
- nested view 등으로 성능 저하가 예상될 때

<br/>

CustomView의 핵심은 onMeasure, onDraw, onLayout이다.  
도화지 크기를 선택하고(onMeasure), 어느 위치에(onLayout) 어떤 그림을 그릴지(onDraw) 설정해 주면 CustomView는 완성된다.  
뷰는 포커스를 얻게 되면 레이아웃의 루트 노드에서 시작하여 전위 순회로 그려진다. 따라서 부모가 자식들보다 먼저 그려지고, 형제들은 트리에 나타난 순서대로 그려진다.

<br/>

![http://labs.brandi.co.kr///assets/2021/1014/03.png](http://labs.brandi.co.kr///assets/2021/1014/03.png)

<br/>

## Constructor
뷰는 최대 4개의 생성자를 가진다.  
- View(Context context) : 코드에서 동적으로 뷰를 생성할 때 사용할 수 있는 간단한 생성자이다. 파라미터 context를 통해 현재 실행 중인 뷰의 리소스 등에 액세스 할 수 있다.
- View(Context context, AttributeSet attrs) : xml에서 생성할 때
- View(Context context, AttributeSet attrs, int defStyleAttr) : ThemeStyle과 함께 뷰를 생성할 때
- View(Context context, AttributeSet attrs, int defStyleAttr, int defStyleRes) : ThemeStyle 또는 Style로 xml에서 뷰를 생성할 때

<br/>

코틀린에서는 @JvmOverloads 어노테이션을 통해 생성자를 간편하게 선언할 수 있다.

```kotlin
class CustomTextView @JvmOverloads constructor(
    context: Context,
    attrs: AttributeSet? = null,
    defStyleAttr: Int = 0,
) : View(context, attrs, defStyleAttr) {
  ...
}
```

<br/>

JvmOverloads를 이용하면 1개의 파라미터를 가지는 Constructor부터 n-parameter 생성자까지 만들어 준다.  
API < 21의 디바이스에서 JvmOverloads 어노테이션으로 4-parameter 생성자를 만들게 되면 StackOverflow를 야기할 수 있다.

<br/>

![http://labs.brandi.co.kr///assets/2021/1014/02.png](http://labs.brandi.co.kr///assets/2021/1014/02.png)

<br/>

## CustomView를 만드는 과정
- 예시 참고 : [[Android] Custom View, Custom Layout ( 커스텀 레이아웃, 커스텀 뷰, 직접 뷰 레이아웃 만들기 ) (tistory.com)](https://onecellboy.tistory.com/344)

<br/>

- CustomView의 클래스를 만든다. (View 상속)
- attrs.xml에 CustomView에서 사용할 속성들을 정의한다. (Custom Attribute 정의)
- CustomView에서 attrs를 읽어오고 오버라이딩 메서드(주로 onMeasure, onDraw가 될 것이다.)를 구현한다.

<br/>

이 정도의 과정을 거칠 것이며, 구현할 CustomView가 무엇이고 필요한 메서드가 무엇이냐에 따라 추가적인 단계가 있을 것이다.

<br/>

## 핵심
- 예시 참고 : [[Android] Custom View, Custom Layout ( 커스텀 레이아웃, 커스텀 뷰, 직접 뷰 레이아웃 만들기 ) (tistory.com)](https://onecellboy.tistory.com/344)

<br/>

1. View를 상속 받아 사용할 때는 onLayout(), onMeasure()는 오버라이드하지 않아도 된다. (View 클래스는 크기와 위치에 대한 행동이 기본적으로 정의되어있다.)
2. xml을 통해 속성을 정의하는 방법과 사용 방법
3. onDraw()를 통해 그리는 방법
4. 깜빡깜빡하는 거와 같은 계속적인 애니메이션을 Handler와 invalidate()를 통해 하는 방법

<br/>
<br/>

# ✅ CustomLayout
## CustomLayout을 만드는 과정
- 예시 참고 : [[Android] Custom View, Custom Layout ( 커스텀 레이아웃, 커스텀 뷰, 직접 뷰 레이아웃 만들기 ) (tistory.com)](https://onecellboy.tistory.com/344)

<br/>

- Custom Attribute 정의
- CustomLayout 클래스 생성 및 Attribute 처리하기
- onMeasure, onLayout 처리하기

<br/>

## Compose CustomLayout
Compose에서 UI는 호출될 때 UI 요소를 내보내는 컴포저블 함수로 표현된다. 각 UI 요소에는 하나의 상위 요소와 여러 개의 하위 요소가 있을 수 있고, 각 요소는 (x, y) 위치로 지정된 상위 요소 내에 배치되며 width, height으로 크기가 지정된다.

<br/>

상위 요소는 하위 요소의 제약 조건을 정의하고, 이러한 제약 조건 내에서 요소의 크기를 정의해야 한다.

<br/>

UI 트리에 각 노드를 배치하는 작업은  
1. 모든 하위 요소 측정  
2. 자체 크기 결정  
3. 하위 요소 배치  

순서로 진행된다.

<br/>

Custom Layout을 구현하기 위해 `Layout`  컴포저블을 사용한다. 이 컴포저블을 사용하면 하위 요소를 수동으로 측정하고 배치할 수 있다.  
많이 사용하는 `Column`  및 `Row`와 같은 모든 상위 수준 레이아웃은 Layout 컴포저블을 사용하여 빌드된다.

<br/>
<br/>

# 🗂 참고
- [android custom ui — 뀨도리의 디지털세상 (tistory.com)](https://jade314.tistory.com/entry/android-custom-ui)
- [[Android] Custom View, Custom Layout ( 커스텀 레이아웃, 커스텀 뷰, 직접 뷰 레이아웃 만들기 ) (tistory.com)](https://onecellboy.tistory.com/344)
- [[Android] CustomView 만들기 - CircleDotsLineView (tistory.com)](https://doitddo.tistory.com/99)
- [CustomView 이해하기 (brandi.co.kr)](https://labs.brandi.co.kr/2021/10/14/jeonhs.html)
- [Compose CustomLayout 만들기(원형 레이아웃) - 1 (velog.io)](https://velog.io/@haem99/Compose-CustomLayout-%EB%A7%8C%EB%93%A4%EA%B8%B0%EC%9B%90%ED%98%95-%EB%A0%88%EC%9D%B4%EC%95%84%EC%9B%83-1)
