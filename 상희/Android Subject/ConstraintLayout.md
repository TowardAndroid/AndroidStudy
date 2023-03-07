# 💡 ConstraintLayout

# ✅ ConstraintLayout이란?
ConstraintLayout은 ViewGroup을 상속받아 확장시킨 라이브러리다.  
2017년 2월에 1.0 버전이 출시되어 많은 개발자들이 이 라이브러리를 유용하게 써왔다. 출시 때는 Android API 9 수준까지 지웠했었다. 2.0부터는 API 14 수준부터 지원하게 되었다. 사실상 API 14 이상만 되어도 안드로이드 전체 이용자 99.9%가 이에 해당하기 때문에 특수한 개발 목적 또는 환경을 제외하고는 범용적으로 쓰일 수 있는 라이브러리다.

<br/>

Constraint의 사전적인 의미는 '제약'인데, 여러 가지 제약 조건들을 이용해서 뷰의 크기와 위치를 결정한다.  
여러 종류의 Layout의 특성을 합친 특징을 갖고 있다.  
RelativeLayout의 "상대적인 위치 관계", LinearLayout의 "가중치", Chain의 "요소 그룹화" 등의 특징을 갖고 있다.

<br/>

## ConstraintLayout을 사용해야 하는 이유
ConstraintLayout 이전의 레이아웃들도 멋지고 아름다운 UI를 표현할 수 있었다. 하지만 개발자들은 그것들을 표현하기 위해 골치가 아팠고, 다양한 비율과 해상도까지 지원하려면 어쩔 수 없이 같은 이름으로 해당 조건에 해당하는 여러 벌의 레이아웃을 만들어야 했다. 이는 생산성과 유지 보수를 힘들게 했다. 심지어 복잡한 레이아웃의 경우 여러 계층의 구조로 만들어야 하다 보니 깊이가 깊어지고 이해하기가 점점 힘들었다.   
ConstraintLayout은 이런 어려움들을 모두 해결해 준다. 하나의 레이아웃으로 다양한 유스케이스에 대응이 되며 단순한 계층 구조로 이해하기도 쉽고, flat한 구조를 유지한다면 뷰를 그리는 퍼포먼스 향상은 덤으로 얻어갈 수 있다.

<br/>
<br/>

# ✅ ConstLayout 제약 조건
안드로이드에서 제공하는 ConstraintLayout의 제약 조건은 9 가지의 카테고리로 구성되어 있다.

<br/>

| 카테고리 | 설명 |
| --- | --- |
| Relative positioning | 요소 간 상대 위치 지정 |
| Margins | 요소 간 여백 설정 |
| Centering positioning and bias | 뷰를 부모 레이아웃 또는 제약 영역의 중앙에 배치 또는 편중 |
| Circular positioning | 대상 뷰를 기준으로 각도(angle)와 반지름(radius)으로 상대 위치 지정 |
| Visibility behavior | 뷰의 Visibility 상태에 따른 최종 위치 결정 및 여백 |
| Dimension constraints | 뷰에 적용된 제약에 따른 뷰의 크기 결정 |
| Chains | 수평 또는 수직 방향으로 나열된 뷰에 대한 그룹화. 배치 스타일 지정 |
| Virtual Helpers objects | 레이아웃 내 효율적인 뷰 배치에 사용 가능한 몇가지 Helper 객체들 |
| Optimizer | 제약 카테고리에 대한 최적화 |

<br/>

## Relative positioning(상대적 배치)
상대적인 배치는 RelativeLayout과 흡사하며 ConstraintLayout의 가장 기본적인 기능이다.  
이 기능은 View와 View 간의 제약 조건을 통해 위치를 결정짓게 된다.

<br/>

![https://developer.android.com/reference/android/support/constraint/resources/images/relative-positioning-constraints.png](https://developer.android.com/reference/android/support/constraint/resources/images/relative-positioning-constraints.png)

가로축 상의 배치는 left, right, start, 그리고 end 속성으로 할 수 있다.  
세로축 상의 배치는 top, bottom, 그리고 text에 한해서 baseline을 지정할 수 있다.

<br/>

일반적으로 아래와 같은 콘셉을 가지고 View를 배치한다.

![https://developer.android.com/reference/android/support/constraint/resources/images/relative-positioning.png](https://developer.android.com/reference/android/support/constraint/resources/images/relative-positioning.png)

<br/>

```xml
<androidx.constraintlayout.widget.ConstraintLayout ...>
    <Button android:id="@+id/buttonA" ... />
    <Button android:id="@+id/buttonB" ...
            app:layout_constraintLeft_toRightOf="@+id/buttonA" />
</androidx.constraintlayout.widget.ConstraintLayout>
```

buttonB의 왼쪽 편을 buttonA의 오른쪽에 배치하라는 것을 알 수 있다.

<br/>

만약 buttonB 입장에서 부모 뷰인 ConstraintLayout에 관련하여 배치를 하고 싶다면 ID 대신 parent 키워드를 사용하면 된다.

```xml
<Button android:id="@+id/buttonB" ...
        app:layout_constraintLeft_toLeftOf="parent" />
```

<br/>

상대 위치 지정 관련 속성은 다음과 같이 있다.

| 속성 | 설명 |
| --- | --- |
| layout_constraintLeft_toLeftOf | 뷰의 왼쪽을 대상 뷰의 왼쪽에 맞춤 |
| layout_constraintLeft_toRightOf | 뷰의 왼쪽을 대상 뷰의 오른쪽에 맞춤 |
| layout_constraintRight_toRightOf | 뷰의 오른쪽을 대상 뷰의 오른쪽에 맞춤 |
| layout_constraintRight_toLeftOf | 뷰의 오른쪽을 대상 뷰의 왼쪽에 맞춤 |
| layout_constraintTop_toTopOf | 뷰의 위를 대상 뷰의 위에 맞춤 |
| layout_constraintTop_toBottomOf | 뷰의 위를 대상 뷰의 아래에 맞춤 |
| layout_constraintBottom_toBottomOf | 뷰의 아래를 대상 뷰의 아래에 맞춤 |
| layout_constraintBottom_toTopOf | 뷰의 아래를 대상 뷰의 위에 맞춤 |
| layout_constraintBaseline_toBottomOf | 뷰의 텍스트 베이스라인을 대상 뷰의 텍스트 베이스라인에 맞춤 |
| layout_constraintStart_toStartOf | 뷰의 시작을 대상 뷰의 시작에 맞춤 |
| layout_constraintStart_toEndOf | 뷰의 시작을 대상 뷰의 끝에 맞춤 |
| layout_constraintEnd_toEndOf | 뷰의 끝을 대상 뷰의 끝에 맞춤 |
| layout_constraintEnd_toStartOf | 뷰의 끝을 대상 뷰의 시작에 맞춤 |

<br/>

위의 속성들은 속성 값으로 "parent" 또는 ID 값을 사용한다.

<br/>

## Margins(여백)
![https://developer.android.com/reference/android/support/constraint/resources/images/relative-positioning-margin.png](https://developer.android.com/reference/android/support/constraint/resources/images/relative-positioning-margin.png)

<br/>

여백을 주고 싶다면 margin을 이용하면 된다.  
여백에 들어가는 값은 오직 0 또는 양수 값만 적용할 수 있다.  
기본적으로 여백을 설정하는 방법은 다른 레이아웃에서와 동일하다.

<br/>

여백을 줄 수 있는 방법은 다음과 같다.  
- `android:layout_marginStart`
- `android:layout_marginEnd`
- `android:layout_marginLeft`
- `android:layout_marginTop`
- `android:layout_marginRight`
- `android:layout_marginBottom`

<br/>

ConstraintLayout은 layout_margin 외에 대상 View가 보이지 않는 상태(View.GONE)가 되었을 때(연결되었던 뷰의 가시성(Visibility)이 숨김 상태(GONE)일 때)의 여백 속성도 제공한다.

<br/>

| 속성 | 설명 |
| --- | --- |
| layout_goneMarginLeft | 뷰의 왼쪽 대상 뷰가 View.GONE 상태일 때 여백 설정 |
| layout_goneMarginRight | 뷰의 오른쪽 대상 뷰가 View.GONE 상태일 때 여백 설정 |
| layout_goneMarginTop | 뷰의 위쪽 대상 뷰가 View.GONE 상태일 때 여백 설정 |
| layout_goneMarginBottom | 뷰의 아래쪽 대상 뷰가 View.GONE 상태일 때 여백 설정 |
| layout_goneMarginStart | 뷰의 시작쪽 대상 뷰가 View.GONE 상태일 때 여백 설정 |
| layout_goneMarginEnd | 뷰의 끝쪽 대상 뷰가 View.GONE 상태일 때 여백 설정 |

<br/>

![https://images.contentful.com/emmiduwd41v7/1GHCNcZjC0OwIKQkGQ644a/1339b7d26f91de400d2c3ea97ba9282c/constraintlayout-gone.gif](https://images.contentful.com/emmiduwd41v7/1GHCNcZjC0OwIKQkGQ644a/1339b7d26f91de400d2c3ea97ba9282c/constraintlayout-gone.gif)

<br/>

## Centering positioning and bias
상대적 제약 조건이 반대 방향으로 두 가지가 동시에 적용되면, 뷰는 두 가지 제약의 가운데 배치된다.  
이 점을 이용해서 Centering positioning을 할 수 있다.

<br/>

### Centering positioning(중앙 배치)
![https://developer.android.com/reference/android/support/constraint/resources/images/centering-positioning.png](https://developer.android.com/reference/android/support/constraint/resources/images/centering-positioning.png)

<br/>

View를 중앙 정렬하고 싶다면 다음과 같이 배치하면 된다.

```xml
<androidx.constraintlayout.widget.ConstraintLayout ...>
    <Button android:id="@+id/button" ...
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintRight_toRightOf="parent/>
</androidx.constraintlayout.widget.ConstraintLayout ...>
```

<br/>

만약 가운데 위치 시키는 것이 아니라 가운데에서 조금 옆으로 또는 위아래로 배치시키고 싶을 때는 어떻게 해야 할까?  
ConstraintLayout에는 bias관련 속성이 있다.

<br/>

### bias
bias의 사전적 정의는 "치우침", "편중"이다.  
bias 속성을 통해서 이미 정렬된 View를 한쪽으로 치우치게 만들 수도 있다.

<br/>

![https://developer.android.com/reference/android/support/constraint/resources/images/centering-positioning-bias.png](https://developer.android.com/reference/android/support/constraint/resources/images/centering-positioning-bias.png)

<br/>

중앙으로 배치된 A를 왼쪽으로 30% 치우치게 만든 모습

```xml
<androidx.constraintlayout.widget.ConstraintLayout ...>
    <Button android:id="@+id/button" ...
            app:layout_constraintHorizontal_bias="0.3"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintRight_toRightOf="parent/>
</androidx.constraintlayout.widget.ConstraintLayout>
```

<br/>

bias의 기본 값은 0.5(50%)이다.  
세로축 및 가로축 기준으로 치우치게 만들 수 있다.

<br/>

bias 관련 속성은 다음과 같다.

| 속성 | 설명 |
| --- | --- |
| layout_constraintHorizontal_bias | 수평 방향(Left/Right 또는 Start/End) 사이드 제약 시, 양 사이드 간 위치 비율 |
| layout_constraintVertical_bias | 수직 방향(Top/Bottom) 사이드 제약 시, 양 사이드 간 위치 비율 |

<br/>

위의 속성들은 0에서 1 사이의 소수 값을 속성 값으로 갖는다.

<br/>

## Circular positioning(원형 배치)
1.1 버전에서 추가되었다.  
한 View의 중점을 기준으로 다른 View의 중점을 배치할 수 있다. 각도와 거리의 값이 필요하며 뷰가 배치될 수 있는 곳을 이으면 원이 된다.

<br/>

![https://developer.android.com/reference/android/support/constraint/resources/images/circle1.png](https://developer.android.com/reference/android/support/constraint/resources/images/circle1.png)

![https://developer.android.com/reference/android/support/constraint/resources/images/circle2.png](https://developer.android.com/reference/android/support/constraint/resources/images/circle2.png)

<br/>

```xml
<androidx.constraintlayout.widget.ConstraintLayout ...>
    <Button android:id="@+id/buttonA" ... />
        <Button android:id="@+id/buttonB" ...
            app:layout_constraintCircle="@+id/buttonA"
            app:layout_constraintCircleRadius="100dp"
            app:layout_constraintCircleAngle="45" />
</androidx.constraintlayout.widget.ConstraintLayout>
```

<br/>

원형 위치 지정은 대상 뷰의 아이디와 거리, 각도 값을 입력하여 나타낼 수 있다.

<br/>

원형 위치 지정의 속성은 다음과 같다.

| 속성 | 설명 |
| --- | --- |
| layout_constraintCircle | 대상 뷰의 ID(기준으로 참조할 View의 ID) 지정 |
| layout_constraintCircleRadius | 뷰와 대상 뷰 중심 사이의 거리(참조한 View와의 거리(반지름)) |
| layout_constraintCircleAngle | 뷰가 배치될 각도(0부터 360까지 참조한 뷰로부터의 각도) <br/> * 각도 계산은 시계처럼 12시 기준, 시계 방향이다. |

<br/>

## Visiblity behavior(가시성에 따른 동작)
Visiblity behavior 특성은 Visibility 특성과, Margins에서 설명한 goneMargin 특성을 포함하고 있다.

<br/>

여백(Margin) 기능을 보면, ConstraintLayout 내의 연결된 View들 간에서 하나의 View가 숨겨지면(GONE) ConstraintLayout에서 특정 처리를 하도록 되어 있다.  
GONE된 View는 표시되지도 않고 레이아웃의 일부로 취급되지도 않지만, 위치나 치수를 계산하는 측면에서는 여전히 의미가 있다.  
레이아웃이 사이즈를 계산하고 그리기 위해서는 GONE된 View는 기본적으로 하나의 점처럼 취급된다. 다른 View에 제약 조건이 있다면 여전히 영향을 미칠 테지만, 기본적으로 여백(Margin)은 0이다.  
이러한 동작을 사용하면 레이아웃을 해치지 않는 선에서 간단한 레이아웃 애니메이션을 할 수도 있다.

<br/>

## Dimension constraints(크기 및 치수에 대한 제약 조건)
ConstraintLayout 내에서 최솟값 최댓값을 정의할 수도 있다.  
- `android:minWidth`  : 최소 가로 길이
- `android:minHeight`  : 최소 세로 길이
- `android:maxWidth`  : 최대 가로 길이
- `android:maxHeight`  : 최대 세로 길이

<br/>

위의 속성들은 ConstraintLayout 내에서만 사용 가능하고, android:layout_width 및 android:layout_height에 대한 값이 WRAP_CONTENT로 지정되어 있어야 한다.

<br/>

### Widgets dimension constraints
View의 가로, 세로 사이즈(android:layout_width, android:layout_height) 즉, 위젯의 크기는 크게 3 가지 방식으로 결정된다.  
- 수치를 직접 입력할 때(ex : 100dp라고 직접 입력하는 경우) (특정 크기로 지정하는 방법)
- WRAP_CONTENT를 통해 View 스스로 사이즈를 결정지을 때
- width/height를 0dp로 입력하고 제약 조건에 의해 사이즈를 결정지을 때 (0dp = MATCH_CONSTRAINT)

<br/>

![https://developer.android.com/reference/android/support/constraint/resources/images/dimension-match-constraints.png](https://developer.android.com/reference/android/support/constraint/resources/images/dimension-match-constraints.png)

<br/>

위의 그림을 보면 (a)의 가로 길이는 WRAP_CONTENT로 스스로 사이즈를 결정 지었고, (b)의 가로 길이는 0dp이며 좌우측이 부모 뷰에 제약이 걸려 부모 뷰의 길이와 같게 늘어난 상태이다. (c)도 (b)와 같이 0dp이지만 여백 값이 적용된 모습이다.  
ConstraintLayout에서 제약 조건 이용 시 MATCH_PARENT를 사용하지 않는 것을 추천한다. 대신 left/right 또는 top/bottom 제약 조건과 함께 MATCH_CONSTRAINT를 이용하길 바란다.

<br/>

Dimension constraints 속성은 위젯의 크기를 조정하는 데 유용하게 사용된다.  
Dimension constraints 속성을 사용하기 위해서는 0dp(MATCH_CONSTRAINT) 속성 값에 대해서 알아야 한다.  
일반적으로 길이를 결정할 때, 특정 값 또는 "wrap_content", "match_parent"를 많이 사용했지만, ConstraintLayout에 속한 뷰들에 대해서는 "match_parent"를 지원하지 않는다.  
0dp 속성 값과 Relative positioning, Margins를 혼합해서 사용하면 뷰의 크기를 자유자재로 조정할 수 있다.

<br/>

Dimension constraints 속성들은 다음과 같다.

| 속성 | 설명 | 속성 값 |
| --- | --- | --- |
| layout_constraintDimensionRatio | 뷰의 가로와 세로의 비율을 조정한다. | 비율(n:m) / 방향(H or W), 비율(n:m) |
| layout_constrainedWidth | 뷰들이 가로 범위 밖으로 안 나가도록 조정 | true / false |
| layout_constrainedHeight | 뷰들이 세로 범위 밖으로 안 나가도록 조정 | true / false |
| layout_constraintWidth_min | 뷰들의 가로 길이 최솟값 설정 | 길이 값 |
| layout_constraintHeight_min | 뷰들의 세로 길이 최솟값 설정 | 길이 값 |
| layout_constraintWidth_max | 뷰들의 가로 길이 최댓값 설정 | 길이 값 |
| layout_constraintHeight_max | 뷰들의 세로 길이 최댓값 설정 | 길이 값 |
| layout_constraintWidth_percent | 뷰들의 가로 길이를 parent의 percent로 설정 | 비율(n:m) |
| layout_constraintHeight_percent | 뷰들의 세로 길이를 parent의 percent로 설정 | 비율(n:m) |

<br/>

- 특정 크기로 지정하는 방법    
    말 그대로 대상 위젯의 width와 height의 크기를 직접 지정하거나 Dimension 리소스를 통해 지정하는 것을 의미한다. 직접 크기를 지정할 때에는 아래와 같이 할 수 있다.
    
    ```xml
    <!-- 직접 값을 입력하여 크기를 지정하는 방법 -->
    <Button ...
        android:layout_width="100dp"
        android:layout_height="100dp" />
    ```
    
    <br/>
    
    Dimension 리소스를 통해 지정한다는 것은 무엇일까?     
    안드로이드에서는 이미지나 문자열과 같은 애플리케이선의 리소스를 독립적으로 관리할 수 있도록 지원한다. dimension과 관련된 속성의 경우 YourProject/res/values/dimens.xml 경로의 파일에서 관리할 수 있다. (이 경로는 규칙이므로 꼭 지켜야 적용이 된다.) 리소스에 관한 것이 더 궁금하다면 [안드로이드 공식 문서](https://developer.android.com/guide/topics/resources/providing-resources?hl=ko#QualifierRules)에서 확인할 수 있다.    
    주의 : MATCH_PARENT 속성은 제약 레이아웃에 속한 위젯에는 사용하지 않는 것이 권장된다. 대신 parent에 left/right 혹은 top/bottom 제약을 지정하여 MATCH_CONSTRAINT 속성을 사용할 수 있다.

<br/>

- WRAP_CONTENT    
    WRAP_CONTENT는 대상 위젯 내부의 콘텐츠 크기에 위젯의 크기를 자동으로 맞춘다. 이때 아래의 속성을 사용하여 대상 위젯의 크기에 제한을 둘 수 있다.    
    - app:layout_constrainedWidth=”true|false”
    - app:layout_constrainedHeight=”true|false”
    
    <br/>
    
    예시    
    : TextView의 width를 wrap_content로 지정해 놓았다. 그런데 TextView의 content 길이가 너무 길어 TextView의 width가 길어졌고, 그로 인해 화면에서 Button이 보이지 않는다.     
    이때 TextView에 app:layout_constrainedWidth=”true” 속성을 추가하여 width에 제한을 주면 위젯 안의 content 길이가 길어지더라도 위와 같이 레이아웃이 유지된다.    
    ![https://shinjekim.github.io/resources/images/constraint-width.png](https://shinjekim.github.io/resources/images/constraint-width.png)
    
<br/>

- MATCH_CONSTRAINT    
    가로, 세로 길이 입력하는 부분에 0dp(= MATCH_CONSTRAINT)를 적용할 때, 기본적인 동작은 MATCH_PARENT처럼 공간을 부모 뷰에 맞게 꽉 채우게 된다. 이때 아래의 속성을 사용하여 위젯의 크기를 변경할 수 있다.    
    - layout_constraintWidth_min        
        : WRAP_CONTENT처럼 동작하나 최솟값을 가진다.        
    - layout_constraintHeight_min        
        : WRAP_CONTENT처럼 동작하나 최솟값을 가진다.        
    - layout_constraintWidth_max        
        : WRAP_CONTENT처럼 동작하나 최댓값을 가진다.        
    - layout_constraintHeight_max        
        : WRAP_CONTENT처럼 동작하나 최댓값을 가진다.        
    - layout_constraintWidth_percent        
        : 0에서 1까지 float 값을 입력하여 비율적으로 길이를 결정한다.        
    - layout_constraintHeight_percent        
        : 0에서 1까지 float 값을 입력하여 비율적으로 길이를 결정한다.
        
    <br/>

    - Min and Max
        
        min과 max로 지정되는 값은 dp의 단위로 직접 크기를 지정할 수도 있고, WRAP_CONTENT와 동일한 결과를 내는 wrap을 사용하여 지정할 수도 있다.
        
    <br/>
    
    - Percent dimension        
        퍼센트를 사용하기 위해서는 아래의 설정이 필요하다.        
        - 대상 위젯의 크기(dimension)는 MATCH_CONSTRAINT(0dp)로 지정되어야 한다.
        - app:layout_constraintWidth_default="percent" 혹은 app:layout_constraintHeight_default="percent"를 사용하여 기본 값을 퍼센트로 설정하여야 한다.
        - layout_constraintWidth_percent 혹은 layout_constraintHeight_percent 속성을 0과 1 사이의 값으로 지정해야 한다.
    
    <br/>
    
    - Ratio        
        위젯의 치수(dimension)에 대한 비율을 이용하여 다른 부분의 치수를 지정할 수도 있다. 비율을 사용하기 위해서는 최소한 하나의 치수(dimension)를 0dp(MATCH_CONSTRAINT)로 지정해야만 한다. 그리고 layout_constraintDimensionRatio를 사용하여 비율을 지정하면 된다. 비율을 입력하는 방식에는 아래와 같이 두 가지의 방식이 있다.        
        - app:layout_constraintDimensionRatio="1:1" (width:height로 표현하는 방법)
        - app:layout_constraintDimensionRatio="1.0" (width와 height의 비율을 float값으로 표현하는 방법)
        
        <br/>
        
        아래의 코드에서는 width를 wrap_content로 지정하고 height를 0dp로 지정한 뒤 1:1의 비율을 입력했다. 결과로는 버튼의 content 크기에 맞춰진 정사각형 버튼이 만들어진다.
        
        ```xml
        <Button ...
            android:layout_width="wrap_content"
            android:layout_height="0dp"
            app:layout_constraintDimensionRatio="1:1" />
        ```
        
        <br/>
        
        width와 height이 모두 MATCH_CONSTRAINT(0dp)로 지정되어 있을 때에도 비율을 지정할 수 있다. 이 경우에는 아래와 같이 W, 혹은 H,를 비율 앞에 추가하여 어떤 쪽에 제약을 줄 것인지를 지정할 수 있다. 이때 주의해야 할 점은 width와 height를 모두 0dp로 지정하는 것이기 때문에 start/end, top/bottom에 제약이 걸려있어야 제대로 테스트할 수 있다.        
        - app:layout_constraintDimensionRatio = "H, x:y"            
            : width를 constraint에 맞춰 설정한 뒤 비율에 따라 높이를 결정한다.            
        - app:layout_constraintDimensionRatio = "W, x:y"            
            : height를 constraint에 맞춰 설정한 뒤 비율에 따라 높이를 결정한다.
            
<br/>

## Chains(뷰끼리 연결하기)
Chain은 뷰 간의 상호 참조 연결을 할 때, 뷰들을 어떤 방식으로 연결해 표현할지를 결정한다.

![https://developer.android.com/reference/android/support/constraint/resources/images/chains.png](https://developer.android.com/reference/android/support/constraint/resources/images/chains.png)

<br/>

Chain 속성을 통해 연결을 할 때는 수평 기준 가장 왼쪽에 있는 View 또는 수직 기준으로 가장 상단에 있는 View가 기준(Head)이 된다.

![https://developer.android.com/reference/android/support/constraint/resources/images/chains-head.png](https://developer.android.com/reference/android/support/constraint/resources/images/chains-head.png)

<br/>

chain 스타일은 여러 형태가 존재 할 수 있는데 layout_constraintHorizontal_chianStyle 또는 layout_constraintVertical_chainStyle을 연결된 뷰들의 head에만 적어 주면 된다. 기본 chain 스타일은 CHAIN_SPREAD이다.  
- `CHAIN_SPREAD`  : 뷰들을 골고루 펼쳐 여백을 같게 한다. (기본 값)
- `CHAIN_SPREAD`에서의 `Weighted chain`은 만약 뷰의 길이가 0dp로 지정되어 있다면 남은 공간을 수치만큼 비율적으로 나눠 갖는다.
    - `Weighted chain`  : 각 요소들의 가중치에 따라 추가 공간을 확보하게 된다. layout_constraintHorizontal_weight 혹은 layout_constraintVertical_weight 속성을 이용하여 지정할 수 있다.
- `CHAIN_SPREAD_INSIDE`  : `CHAIN_SPREAD`와 비슷하지만 가장 외곽에 있는 뷰들은 부모 뷰와 여백이 없는 상태로 골고루 펼쳐진다.
- `CHAIN_PACKED` : 뷰들이 똘똘 뭉치게 되고 부모 뷰로부터의 여백을 같게 한다. 여백을 조정하고 싶다면 bias 조정을 통해 한쪽으로 치우치게 만들 수 있다.

<br/>

![https://developer.android.com/reference/android/support/constraint/resources/images/chains-styles.png](https://developer.android.com/reference/android/support/constraint/resources/images/chains-styles.png)

<br/>

## Virtual Helper objects
안드로이드는 ConstraintLayout의 사용을 돕기 위해 특별한 객체 몇 가지를 제공하는데, 이것이 Virtual Helper objects이다.

<br/>

### Guideline
실제 어플상에는 출력되지 않지만, 레이아웃 작업을 돕기 위한 선을 그려 준다.  
layout_constraintGuide_percent 속성을 이용해서 0에서 1 사이의 소수 값을 입력해서 선의 위치를 결정한다.

<br/>

가이드라인(Guideline)은 수평/수직 모두 적용할 수 있다.  
수평 가이드라인(horizontal guidelines)의 height는 0이고 width는 parent인 ConstraintLayout에 맞춰진다.  
수직 가이드라인(vertical guidelines)의 width는 0이고 height는 parent인 ConstraintLayout에 맞춰진다.

<br/>

가이드라인의 위치를 지정하기 위해서 아래의 세 가지 방법을 사용할 수 있다.
- layout_constraintGuide_begin : 레이아웃의 left 또는 top에서부터의 고정 거리를 지정한다.
- layout_constraintGuide_end : 레이아웃의 right 혹은 bottom에서부터의 고정 거리를 지정한다.
- layout_constraintGuide_percent : 레이아웃에서의 width 혹은 height의 퍼센트를 지정한다.

<br/>

### Group
특정 뷰(View)들을 묶어서 제어할 수 있다. (ex : 여러 개의 뷰를 한 번에 visibility 제어할 때)  
constraint_referenced_ids 속성을 이용해서 속성 값을 ID로 입력하는데, ID를 ','로 구분해서 입력한다.

<br/>

그룹(Group) 헬퍼를 통해 복수의 위젯을 그룹화하여 아래와 같이 visibility 속성(visible | invisible | gone)을 동시에 제어할 수 있다.

```xml
<androidx.constraintlayout.widget.Group
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" 
    android:visibility="invisible"
    app:constraint_referenced_ids="button, button2, button3" />
```

<br/>

위 코드의 `android:visibility`  부분에서 visibility 속성을 지정할 수 있으며 `app:constraint_referenced_ids`에서 그룹으로 지정하고자 하는 위젯의 아이디를 입력할 수 있다.

<br/>

### Barrier
참조하고 있는 뷰(View)들 중에 가장 큰 dimension의 position에 Guideline을 생성한다.  
barrierDirection 속성을 이용해서 Guideline을 생성할 방향을 결정하고, 속성 값을 방향으로 입력한다.

<br/>

## Optimizer
제약 카테고리에 대한 최적화 기능을 한다.  
Constraint Layout 1.1 버전부터는 레이아웃의 속도를 높이기 위해 최적화 방법을 제공한다.  
ConstraintLayout 요소에 app:layout_optimizationLevel 태그를 추가하여 아래와 같이 최적화 레벨을 지정할 수 있다.  
- none : 최적화 사용 안 함
- standard : 디폴트 레벨
- direct : 고정된 요소에 연결된 제약 조건에 관련된 최적화
- barrier : barrier 제약 조건 관련 최적화
- chain : 체인 제약 조건 최적화(아직 테스트 중인 기능)
- dimensions : 크기(dimensions) 측정 최적화(아직 테스트 중인 기능)

<br/>
<br/>

# 🗂 참고
- [Constraint Layout – Part1. 만능 레이아웃 | 찰스의 안드로이드 (charlezz.com)](https://www.charlezz.com/?p=669)
- [[안드로이드 스튜디오 정리#1-6] ConstraintLayout :: 세민짱의 블로그 (tistory.com)](https://seminzzang.tistory.com/21)
- [제약 조건 레이아웃 | 안드로이드 개발자 (android.com)](https://developer.android.com/reference/android/support/constraint/ConstraintLayout)
- [[Android] ConstraintLayout 톺아보기 (안드로이드 공식 문서 번역) · Challengist (shinjekim.github.io)](https://shinjekim.github.io/android/2019/08/07/Android-ConstraintLayout/)
