# 💡 View Lifecycle

# ✅ View
안드로이드 앱을 실행할 때 우리가 가장 먼저 스크린에서 볼 수 있는 것이 View라고 말할 수 있다.

<br/>

![https://cdn-images-1.medium.com/max/1600/1*HApOQUK3-G7X9wU50GF49A.png](https://cdn-images-1.medium.com/max/1600/1*HApOQUK3-G7X9wU50GF49A.png)

<br/>

View 클래스는 사용자 인터페이스 기본적인 구성 요소를 가지고 있다.  
View 는 드로잉, 이벤트 처리를 담당하는 UI 구성 요소의 기본 클래스이다. View를 상속받아 구현하는 TextView, Button 등 어떤 특수 목적을 가지고 있는 View를 위젯, 컴포넌트라고 부르기도 한다.  
View의 또 다른 서브 클래스인 ViewGroup은 보이지는 않는 컨테이너로써 다른 View들을 다른 View(또는 다른 ViewGroup)들을 포함할 수 있다.  
새로운 위젯을 만들기 위해선 View를 반드시 상속하여 구현해야 한다. 그리고 그러한 위젯들을 담는 부모 뷰 즉, Layout 역시 View를 상속받는 ViewGroup을 상속받아 구현한다.

<br/>
<br/>

# ✅ View Lifecycle
부모 뷰가 addView()를 호출하게 되면, 뷰의 생애는 본격적으로 시작된다.

<br/>

![Untitled](https://velog.velcdn.com/images/haero_kim/post/fd84afaa-b760-4a2a-9b7b-7f111ed4913f/%E1%84%83%E1%85%A1%E1%84%8B%E1%85%AE%E1%86%AB%E1%84%85%E1%85%A9%E1%84%83%E1%85%B3%20(23).png)

<br/>

## Constructor
- 모든 뷰는 생성자에 의해 생명 주기가 시작된다. (AttributeSet을 갖게 된다.)
- addView() 메소드를 갖게 된다.

<br/>

### View(Context context)
코드에서 View를 동적으로 만들 때 사용하는 간단한 생성자다. 여기서 매개 변수 context는 뷰가 실행될 때 현재 테마, 리소스 등을 구성하는 데 사용된다.

<br/>

### View(Context context, @Nullable AttributeSet attrs)
XML에서 View를 전개(Inflation)할 때 호출되는 생성자로 XML 파일에서 지정된 속성을 제공하여 XML 파일에서 View를 구성할 때 호출된다. 이 생성자는 기본 스타일인 0을 사용하므로 컨텍스트의 테마 및 지정된 AttributeSet의 속성 값만 적용된다.

<br/>

### View(Context context, @Nullable AttributeSet attrs, int defStyleAttr)
XML을 통해 전개를 하고 테마 속성에서 클래스별 기본 스타일을 적용한다. 이 View 생성자는 서브 클래스가 전개할 때 자체 기본 스타일을 사용할 수 있도록 한다.  
  - ex : Button 클래스의 생성자는 수퍼 클래스 생성자를 호출하고 defStyleAttr에 R.attr.buttonStyle을 제공한다. 이를 통해 테마의 버튼 스타일은 모든 기본 View 속성(특히 배경)과 Button 클래스의 속성을 수정할 수 있다.

defStyleAttr 매개 변수는 View의 기본 값을 제공하는 Style 리소스 대한 참조를 포함하는 현재 테마의 속성이다. 기본 값을 찾지 않으려면 0으로 지정할 수 있다.

<br/>

### View(Context context, @Nullable AttributeSet attrs, int defStyleAttr, int defStyleRes)
XML을 전개하고 테마 속성 또는 Style 리소스에서 클래스별 기본 스타일을 적용한다. 이 생성자는 서브 클래스가 전개할 때 자체 기본 스타일을 사용할 수 있도록 한다. 위와 유사하다.  
매개변수 defStyleRes는 View의 defStyleAttr가 0이거나 테마에서 찾을 수 없는 경우에만 기본 값을 제공하는 Style 리소스 ID다. 기본 값을 찾지 않으려면 0으로 지정한다.

<br/>

## onAttachedToWindow()
- 부모 뷰가 addView()를 호출함으로써 View가 윈도우에 붙을 때 호출된다.
- 고유 ID를 통해 View 에 접근 가능해진다.
- 이 순간부터는 뷰를 그리기 위한 surface를 가진다.
  - 단, onDetachedFromWindow() 호출 이후에는 surface가 없다.
  - 액티비티 onDestroyed() 호출될 때, 혹은 부모 뷰에서 해당 뷰를 제거할 때 호출
- 따라서 이 순간부터는 리소스 할당 및 리스너 설정 등이 가능해진다.

<br/>

## onMeasure()
- measure()에서 호출하는 콜백 메소드(View의 크기를 측정하기 위해 호출된다.)
  - 부모 뷰의 경우에는 모든 자식 뷰들의 measure()를 호출한 뒤 자신의 크기 결정
  - setMeasuredDimenstion() 호출하여 명시적으로 너비와 높이 설정

<br/>

## onLayout()
- layout()에서 호출하는 콜백 메소드(뷰의 크기와 위치 지정)
- 즉, 뷰의 크기와 위치를 지정하여 화면에 배치한 후에 호출한다. (주로 부모 뷰일 때 호출)
- 아직 뷰가 그려지는 단계는 아니다.

<br/>

## dispatchDraw()
- ViewGroup에 속한 메소드
- 뷰가 다시 그려져야 할 경우에 자식 뷰들도 싹 다 다시 그려지도록 한다.

<br/>

## onDraw()
- 실제로 뷰를 그리는 단계
  - Canvas : 뷰의 모양을 그리는 객체
  - Paint : 뷰의 색상을 칠하는 객체
- 크기와 위치는 이전에 계산되기 때문에 그것들을 기준으로 뷰를 그리게 된다.
- 해당 콜백 메소드는 언제든 다시 호출될 수 있기 때문에 이 안에서 객체 생성은 하면 안 된다.
  - 스크롤, 스와이프 등 인터랙션이 발생하면 언제든 호출될 수 있다.

```kotlin
override fun onDraw(canvas: Canvas?) {
    super.onDraw(canvas)

    val width = measuredWidth + 0.0f
    val height = measuredHeight + 0.0f

    val circle = Paint()
    circle.color = this.lineColor
    circle.strokeWidth = 10f
    circle.isAntiAlias = false
    circle.style = Paint.Style.STROKE

    canvas?.drawArc(
        RectF(
            10f, 10f, width - 10f, height - 10f
        ), -90f,
        (this.curValue + 0.0f) / (this.maxValue + 0.0f) * 360, false, circle
    )

    val textp = Paint()
    textp.color = Color.BLACK
    textp.textSize = 30f
    textp.textAlign = Paint.Align.CENTER

    if (System.currentTimeMillis() / 1000 % 2 == 0L) {
        canvas?.drawText(
            "${this.curValue} / ${this.maxValue}",
            (width / 2),
            (height / 2),
            textp
        )
    }

    Observable.interval(1, TimeUnit.SECONDS)
        .observeOn(AndroidSchedulers.mainThread())
        .subscribe({
            invalidate()
        }, {

        })
        .addTo(disposable)
}
```

<br/>

### invalidate()
- 글자나 색상 등 크기 변화는 없이 단순히 뷰의 속성 등이 변경되어 다시 그려야 하는 경우 View를 다시 그리기 위해 호출하는 메소드

<br/>

### requestLayout()
- 위에서 ‘크기 변화 없이’ 라고 했는데 만약 뷰의 크기 변화가 발생할 경우, 레이아웃의 배치도 달라질 수 있기 때문에 해당 메소드를 호출함으로써 뷰들의 크기 측정부터 다시 하게 된다.

<br/>
<br/>

# 🗂 참고
- [Android에서 View의 생명주기 | 찰스의 안드로이드 (charlezz.com)](https://www.charlezz.com/?p=29013)
- [[Android] View 의 한 평생 살펴보기 (velog.io)](https://velog.io/@haero_kim/Android-View-%EC%9D%98-%ED%95%9C-%ED%8F%89%EC%83%9D-%EC%82%B4%ED%8E%B4%EB%B3%B4%EA%B8%B0)
