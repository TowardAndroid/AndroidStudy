# ๐ก ConstraintLayout

# โ ConstraintLayout์ด๋?
ConstraintLayout์ ViewGroup์ ์์๋ฐ์ ํ์ฅ์ํจ ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ค.  
2017๋ 2์์ 1.0 ๋ฒ์ ์ด ์ถ์๋์ด ๋ง์ ๊ฐ๋ฐ์๋ค์ด ์ด ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ฅผ ์ ์ฉํ๊ฒ ์จ์๋ค. ์ถ์ ๋๋ Android API 9 ์์ค๊น์ง ์ง์ ํ์๋ค. 2.0๋ถํฐ๋ API 14 ์์ค๋ถํฐ ์ง์ํ๊ฒ ๋์๋ค. ์ฌ์ค์ API 14 ์ด์๋ง ๋์ด๋ ์๋๋ก์ด๋ ์ ์ฒด ์ด์ฉ์ 99.9%๊ฐ ์ด์ ํด๋นํ๊ธฐ ๋๋ฌธ์ ํน์ํ ๊ฐ๋ฐ ๋ชฉ์  ๋๋ ํ๊ฒฝ์ ์ ์ธํ๊ณ ๋ ๋ฒ์ฉ์ ์ผ๋ก ์ฐ์ผ ์ ์๋ ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ค.

<br/>

Constraint์ ์ฌ์ ์ ์ธ ์๋ฏธ๋ '์ ์ฝ'์ธ๋ฐ, ์ฌ๋ฌ ๊ฐ์ง ์ ์ฝ ์กฐ๊ฑด๋ค์ ์ด์ฉํด์ ๋ทฐ์ ํฌ๊ธฐ์ ์์น๋ฅผ ๊ฒฐ์ ํ๋ค.  
์ฌ๋ฌ ์ข๋ฅ์ Layout์ ํน์ฑ์ ํฉ์น ํน์ง์ ๊ฐ๊ณ  ์๋ค.  
RelativeLayout์ "์๋์ ์ธ ์์น ๊ด๊ณ", LinearLayout์ "๊ฐ์ค์น", Chain์ "์์ ๊ทธ๋ฃนํ" ๋ฑ์ ํน์ง์ ๊ฐ๊ณ  ์๋ค.

<br/>

## ConstraintLayout์ ์ฌ์ฉํด์ผ ํ๋ ์ด์ 
ConstraintLayout ์ด์ ์ ๋ ์ด์์๋ค๋ ๋ฉ์ง๊ณ  ์๋ฆ๋ค์ด UI๋ฅผ ํํํ  ์ ์์๋ค. ํ์ง๋ง ๊ฐ๋ฐ์๋ค์ ๊ทธ๊ฒ๋ค์ ํํํ๊ธฐ ์ํด ๊ณจ์น๊ฐ ์ํ ๊ณ , ๋ค์ํ ๋น์จ๊ณผ ํด์๋๊น์ง ์ง์ํ๋ ค๋ฉด ์ด์ฉ ์ ์์ด ๊ฐ์ ์ด๋ฆ์ผ๋ก ํด๋น ์กฐ๊ฑด์ ํด๋นํ๋ ์ฌ๋ฌ ๋ฒ์ ๋ ์ด์์์ ๋ง๋ค์ด์ผ ํ๋ค. ์ด๋ ์์ฐ์ฑ๊ณผ ์ ์ง ๋ณด์๋ฅผ ํ๋ค๊ฒ ํ๋ค. ์ฌ์ง์ด ๋ณต์กํ ๋ ์ด์์์ ๊ฒฝ์ฐ ์ฌ๋ฌ ๊ณ์ธต์ ๊ตฌ์กฐ๋ก ๋ง๋ค์ด์ผ ํ๋ค ๋ณด๋ ๊น์ด๊ฐ ๊น์ด์ง๊ณ  ์ดํดํ๊ธฐ๊ฐ ์ ์  ํ๋ค์๋ค.   
ConstraintLayout์ ์ด๋ฐ ์ด๋ ค์๋ค์ ๋ชจ๋ ํด๊ฒฐํด ์ค๋ค. ํ๋์ ๋ ์ด์์์ผ๋ก ๋ค์ํ ์ ์ค์ผ์ด์ค์ ๋์์ด ๋๋ฉฐ ๋จ์ํ ๊ณ์ธต ๊ตฌ์กฐ๋ก ์ดํดํ๊ธฐ๋ ์ฝ๊ณ , flatํ ๊ตฌ์กฐ๋ฅผ ์ ์งํ๋ค๋ฉด ๋ทฐ๋ฅผ ๊ทธ๋ฆฌ๋ ํผํฌ๋จผ์ค ํฅ์์ ๋ค์ผ๋ก ์ป์ด๊ฐ ์ ์๋ค.

<br/>
<br/>

# โ ConstLayout ์ ์ฝ ์กฐ๊ฑด
์๋๋ก์ด๋์์ ์ ๊ณตํ๋ ConstraintLayout์ ์ ์ฝ ์กฐ๊ฑด์ 9 ๊ฐ์ง์ ์นดํ๊ณ ๋ฆฌ๋ก ๊ตฌ์ฑ๋์ด ์๋ค.

<br/>

| ์นดํ๊ณ ๋ฆฌ | ์ค๋ช |
| --- | --- |
| Relative positioning | ์์ ๊ฐ ์๋ ์์น ์ง์  |
| Margins | ์์ ๊ฐ ์ฌ๋ฐฑ ์ค์  |
| Centering positioning and bias | ๋ทฐ๋ฅผ ๋ถ๋ชจ ๋ ์ด์์ ๋๋ ์ ์ฝ ์์ญ์ ์ค์์ ๋ฐฐ์น ๋๋ ํธ์ค |
| Circular positioning | ๋์ ๋ทฐ๋ฅผ ๊ธฐ์ค์ผ๋ก ๊ฐ๋(angle)์ ๋ฐ์ง๋ฆ(radius)์ผ๋ก ์๋ ์์น ์ง์  |
| Visibility behavior | ๋ทฐ์ Visibility ์ํ์ ๋ฐ๋ฅธ ์ต์ข ์์น ๊ฒฐ์  ๋ฐ ์ฌ๋ฐฑ |
| Dimension constraints | ๋ทฐ์ ์ ์ฉ๋ ์ ์ฝ์ ๋ฐ๋ฅธ ๋ทฐ์ ํฌ๊ธฐ ๊ฒฐ์  |
| Chains | ์ํ ๋๋ ์์ง ๋ฐฉํฅ์ผ๋ก ๋์ด๋ ๋ทฐ์ ๋ํ ๊ทธ๋ฃนํ. ๋ฐฐ์น ์คํ์ผ ์ง์  |
| Virtual Helpers objects | ๋ ์ด์์ ๋ด ํจ์จ์ ์ธ ๋ทฐ ๋ฐฐ์น์ ์ฌ์ฉ ๊ฐ๋ฅํ ๋ช๊ฐ์ง Helper ๊ฐ์ฒด๋ค |
| Optimizer | ์ ์ฝ ์นดํ๊ณ ๋ฆฌ์ ๋ํ ์ต์ ํ |

<br/>

## Relative positioning(์๋์  ๋ฐฐ์น)
์๋์ ์ธ ๋ฐฐ์น๋ RelativeLayout๊ณผ ํก์ฌํ๋ฉฐ ConstraintLayout์ ๊ฐ์ฅ ๊ธฐ๋ณธ์ ์ธ ๊ธฐ๋ฅ์ด๋ค.  
์ด ๊ธฐ๋ฅ์ View์ View ๊ฐ์ ์ ์ฝ ์กฐ๊ฑด์ ํตํด ์์น๋ฅผ ๊ฒฐ์ ์ง๊ฒ ๋๋ค.

<br/>

![https://developer.android.com/reference/android/support/constraint/resources/images/relative-positioning-constraints.png](https://developer.android.com/reference/android/support/constraint/resources/images/relative-positioning-constraints.png)

๊ฐ๋ก์ถ ์์ ๋ฐฐ์น๋ left, right, start, ๊ทธ๋ฆฌ๊ณ  end ์์ฑ์ผ๋ก ํ  ์ ์๋ค.  
์ธ๋ก์ถ ์์ ๋ฐฐ์น๋ top, bottom, ๊ทธ๋ฆฌ๊ณ  text์ ํํด์ baseline์ ์ง์ ํ  ์ ์๋ค.

<br/>

์ผ๋ฐ์ ์ผ๋ก ์๋์ ๊ฐ์ ์ฝ์์ ๊ฐ์ง๊ณ  View๋ฅผ ๋ฐฐ์นํ๋ค.

![https://developer.android.com/reference/android/support/constraint/resources/images/relative-positioning.png](https://developer.android.com/reference/android/support/constraint/resources/images/relative-positioning.png)

<br/>

```xml
<androidx.constraintlayout.widget.ConstraintLayout ...>
    <Button android:id="@+id/buttonA" ... />
    <Button android:id="@+id/buttonB" ...
            app:layout_constraintLeft_toRightOf="@+id/buttonA" />
</androidx.constraintlayout.widget.ConstraintLayout>
```

buttonB์ ์ผ์ชฝ ํธ์ buttonA์ ์ค๋ฅธ์ชฝ์ ๋ฐฐ์นํ๋ผ๋ ๊ฒ์ ์ ์ ์๋ค.

<br/>

๋ง์ฝ buttonB ์์ฅ์์ ๋ถ๋ชจ ๋ทฐ์ธ ConstraintLayout์ ๊ด๋ จํ์ฌ ๋ฐฐ์น๋ฅผ ํ๊ณ  ์ถ๋ค๋ฉด ID ๋์  parent ํค์๋๋ฅผ ์ฌ์ฉํ๋ฉด ๋๋ค.

```xml
<Button android:id="@+id/buttonB" ...
        app:layout_constraintLeft_toLeftOf="parent" />
```

<br/>

์๋ ์์น ์ง์  ๊ด๋ จ ์์ฑ์ ๋ค์๊ณผ ๊ฐ์ด ์๋ค.

| ์์ฑ | ์ค๋ช |
| --- | --- |
| layout_constraintLeft_toLeftOf | ๋ทฐ์ ์ผ์ชฝ์ ๋์ ๋ทฐ์ ์ผ์ชฝ์ ๋ง์ถค |
| layout_constraintLeft_toRightOf | ๋ทฐ์ ์ผ์ชฝ์ ๋์ ๋ทฐ์ ์ค๋ฅธ์ชฝ์ ๋ง์ถค |
| layout_constraintRight_toRightOf | ๋ทฐ์ ์ค๋ฅธ์ชฝ์ ๋์ ๋ทฐ์ ์ค๋ฅธ์ชฝ์ ๋ง์ถค |
| layout_constraintRight_toLeftOf | ๋ทฐ์ ์ค๋ฅธ์ชฝ์ ๋์ ๋ทฐ์ ์ผ์ชฝ์ ๋ง์ถค |
| layout_constraintTop_toTopOf | ๋ทฐ์ ์๋ฅผ ๋์ ๋ทฐ์ ์์ ๋ง์ถค |
| layout_constraintTop_toBottomOf | ๋ทฐ์ ์๋ฅผ ๋์ ๋ทฐ์ ์๋์ ๋ง์ถค |
| layout_constraintBottom_toBottomOf | ๋ทฐ์ ์๋๋ฅผ ๋์ ๋ทฐ์ ์๋์ ๋ง์ถค |
| layout_constraintBottom_toTopOf | ๋ทฐ์ ์๋๋ฅผ ๋์ ๋ทฐ์ ์์ ๋ง์ถค |
| layout_constraintBaseline_toBottomOf | ๋ทฐ์ ํ์คํธ ๋ฒ ์ด์ค๋ผ์ธ์ ๋์ ๋ทฐ์ ํ์คํธ ๋ฒ ์ด์ค๋ผ์ธ์ ๋ง์ถค |
| layout_constraintStart_toStartOf | ๋ทฐ์ ์์์ ๋์ ๋ทฐ์ ์์์ ๋ง์ถค |
| layout_constraintStart_toEndOf | ๋ทฐ์ ์์์ ๋์ ๋ทฐ์ ๋์ ๋ง์ถค |
| layout_constraintEnd_toEndOf | ๋ทฐ์ ๋์ ๋์ ๋ทฐ์ ๋์ ๋ง์ถค |
| layout_constraintEnd_toStartOf | ๋ทฐ์ ๋์ ๋์ ๋ทฐ์ ์์์ ๋ง์ถค |

<br/>

์์ ์์ฑ๋ค์ ์์ฑ ๊ฐ์ผ๋ก "parent" ๋๋ ID ๊ฐ์ ์ฌ์ฉํ๋ค.

<br/>

## Margins(์ฌ๋ฐฑ)
![https://developer.android.com/reference/android/support/constraint/resources/images/relative-positioning-margin.png](https://developer.android.com/reference/android/support/constraint/resources/images/relative-positioning-margin.png)

<br/>

์ฌ๋ฐฑ์ ์ฃผ๊ณ  ์ถ๋ค๋ฉด margin์ ์ด์ฉํ๋ฉด ๋๋ค.  
์ฌ๋ฐฑ์ ๋ค์ด๊ฐ๋ ๊ฐ์ ์ค์ง 0 ๋๋ ์์ ๊ฐ๋ง ์ ์ฉํ  ์ ์๋ค.  
๊ธฐ๋ณธ์ ์ผ๋ก ์ฌ๋ฐฑ์ ์ค์ ํ๋ ๋ฐฉ๋ฒ์ ๋ค๋ฅธ ๋ ์ด์์์์์ ๋์ผํ๋ค.

<br/>

์ฌ๋ฐฑ์ ์ค ์ ์๋ ๋ฐฉ๋ฒ์ ๋ค์๊ณผ ๊ฐ๋ค.  
- `android:layout_marginStart`
- `android:layout_marginEnd`
- `android:layout_marginLeft`
- `android:layout_marginTop`
- `android:layout_marginRight`
- `android:layout_marginBottom`

<br/>

ConstraintLayout์ layout_margin ์ธ์ ๋์ View๊ฐ ๋ณด์ด์ง ์๋ ์ํ(View.GONE)๊ฐ ๋์์ ๋(์ฐ๊ฒฐ๋์๋ ๋ทฐ์ ๊ฐ์์ฑ(Visibility)์ด ์จ๊น ์ํ(GONE)์ผ ๋)์ ์ฌ๋ฐฑ ์์ฑ๋ ์ ๊ณตํ๋ค.

<br/>

| ์์ฑ | ์ค๋ช |
| --- | --- |
| layout_goneMarginLeft | ๋ทฐ์ ์ผ์ชฝ ๋์ ๋ทฐ๊ฐ View.GONE ์ํ์ผ ๋ ์ฌ๋ฐฑ ์ค์  |
| layout_goneMarginRight | ๋ทฐ์ ์ค๋ฅธ์ชฝ ๋์ ๋ทฐ๊ฐ View.GONE ์ํ์ผ ๋ ์ฌ๋ฐฑ ์ค์  |
| layout_goneMarginTop | ๋ทฐ์ ์์ชฝ ๋์ ๋ทฐ๊ฐ View.GONE ์ํ์ผ ๋ ์ฌ๋ฐฑ ์ค์  |
| layout_goneMarginBottom | ๋ทฐ์ ์๋์ชฝ ๋์ ๋ทฐ๊ฐ View.GONE ์ํ์ผ ๋ ์ฌ๋ฐฑ ์ค์  |
| layout_goneMarginStart | ๋ทฐ์ ์์์ชฝ ๋์ ๋ทฐ๊ฐ View.GONE ์ํ์ผ ๋ ์ฌ๋ฐฑ ์ค์  |
| layout_goneMarginEnd | ๋ทฐ์ ๋์ชฝ ๋์ ๋ทฐ๊ฐ View.GONE ์ํ์ผ ๋ ์ฌ๋ฐฑ ์ค์  |

<br/>

![https://images.contentful.com/emmiduwd41v7/1GHCNcZjC0OwIKQkGQ644a/1339b7d26f91de400d2c3ea97ba9282c/constraintlayout-gone.gif](https://images.contentful.com/emmiduwd41v7/1GHCNcZjC0OwIKQkGQ644a/1339b7d26f91de400d2c3ea97ba9282c/constraintlayout-gone.gif)

<br/>

## Centering positioning and bias
์๋์  ์ ์ฝ ์กฐ๊ฑด์ด ๋ฐ๋ ๋ฐฉํฅ์ผ๋ก ๋ ๊ฐ์ง๊ฐ ๋์์ ์ ์ฉ๋๋ฉด, ๋ทฐ๋ ๋ ๊ฐ์ง ์ ์ฝ์ ๊ฐ์ด๋ฐ ๋ฐฐ์น๋๋ค.  
์ด ์ ์ ์ด์ฉํด์ Centering positioning์ ํ  ์ ์๋ค.

<br/>

### Centering positioning(์ค์ ๋ฐฐ์น)
![https://developer.android.com/reference/android/support/constraint/resources/images/centering-positioning.png](https://developer.android.com/reference/android/support/constraint/resources/images/centering-positioning.png)

<br/>

View๋ฅผ ์ค์ ์ ๋ ฌํ๊ณ  ์ถ๋ค๋ฉด ๋ค์๊ณผ ๊ฐ์ด ๋ฐฐ์นํ๋ฉด ๋๋ค.

```xml
<androidx.constraintlayout.widget.ConstraintLayout ...>
    <Button android:id="@+id/button" ...
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintRight_toRightOf="parent/>
</androidx.constraintlayout.widget.ConstraintLayout ...>
```

<br/>

๋ง์ฝ ๊ฐ์ด๋ฐ ์์น ์ํค๋ ๊ฒ์ด ์๋๋ผ ๊ฐ์ด๋ฐ์์ ์กฐ๊ธ ์์ผ๋ก ๋๋ ์์๋๋ก ๋ฐฐ์น์ํค๊ณ  ์ถ์ ๋๋ ์ด๋ป๊ฒ ํด์ผ ํ ๊น?  
ConstraintLayout์๋ bias๊ด๋ จ ์์ฑ์ด ์๋ค.

<br/>

### bias
bias์ ์ฌ์ ์  ์ ์๋ "์น์ฐ์นจ", "ํธ์ค"์ด๋ค.  
bias ์์ฑ์ ํตํด์ ์ด๋ฏธ ์ ๋ ฌ๋ View๋ฅผ ํ์ชฝ์ผ๋ก ์น์ฐ์น๊ฒ ๋ง๋ค ์๋ ์๋ค.

<br/>

![https://developer.android.com/reference/android/support/constraint/resources/images/centering-positioning-bias.png](https://developer.android.com/reference/android/support/constraint/resources/images/centering-positioning-bias.png)

<br/>

์ค์์ผ๋ก ๋ฐฐ์น๋ A๋ฅผ ์ผ์ชฝ์ผ๋ก 30% ์น์ฐ์น๊ฒ ๋ง๋  ๋ชจ์ต

```xml
<androidx.constraintlayout.widget.ConstraintLayout ...>
    <Button android:id="@+id/button" ...
            app:layout_constraintHorizontal_bias="0.3"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintRight_toRightOf="parent/>
</androidx.constraintlayout.widget.ConstraintLayout>
```

<br/>

bias์ ๊ธฐ๋ณธ ๊ฐ์ 0.5(50%)์ด๋ค.  
์ธ๋ก์ถ ๋ฐ ๊ฐ๋ก์ถ ๊ธฐ์ค์ผ๋ก ์น์ฐ์น๊ฒ ๋ง๋ค ์ ์๋ค.

<br/>

bias ๊ด๋ จ ์์ฑ์ ๋ค์๊ณผ ๊ฐ๋ค.

| ์์ฑ | ์ค๋ช |
| --- | --- |
| layout_constraintHorizontal_bias | ์ํ ๋ฐฉํฅ(Left/Right ๋๋ Start/End) ์ฌ์ด๋ ์ ์ฝ ์, ์ ์ฌ์ด๋ ๊ฐ ์์น ๋น์จ |
| layout_constraintVertical_bias | ์์ง ๋ฐฉํฅ(Top/Bottom) ์ฌ์ด๋ ์ ์ฝ ์, ์ ์ฌ์ด๋ ๊ฐ ์์น ๋น์จ |

<br/>

์์ ์์ฑ๋ค์ 0์์ 1 ์ฌ์ด์ ์์ ๊ฐ์ ์์ฑ ๊ฐ์ผ๋ก ๊ฐ๋๋ค.

<br/>

## Circular positioning(์ํ ๋ฐฐ์น)
1.1 ๋ฒ์ ์์ ์ถ๊ฐ๋์๋ค.  
ํ View์ ์ค์ ์ ๊ธฐ์ค์ผ๋ก ๋ค๋ฅธ View์ ์ค์ ์ ๋ฐฐ์นํ  ์ ์๋ค. ๊ฐ๋์ ๊ฑฐ๋ฆฌ์ ๊ฐ์ด ํ์ํ๋ฉฐ ๋ทฐ๊ฐ ๋ฐฐ์น๋  ์ ์๋ ๊ณณ์ ์ด์ผ๋ฉด ์์ด ๋๋ค.

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

์ํ ์์น ์ง์ ์ ๋์ ๋ทฐ์ ์์ด๋์ ๊ฑฐ๋ฆฌ, ๊ฐ๋ ๊ฐ์ ์๋ ฅํ์ฌ ๋ํ๋ผ ์ ์๋ค.

<br/>

์ํ ์์น ์ง์ ์ ์์ฑ์ ๋ค์๊ณผ ๊ฐ๋ค.

| ์์ฑ | ์ค๋ช |
| --- | --- |
| layout_constraintCircle | ๋์ ๋ทฐ์ ID(๊ธฐ์ค์ผ๋ก ์ฐธ์กฐํ  View์ ID) ์ง์  |
| layout_constraintCircleRadius | ๋ทฐ์ ๋์ ๋ทฐ ์ค์ฌ ์ฌ์ด์ ๊ฑฐ๋ฆฌ(์ฐธ์กฐํ View์์ ๊ฑฐ๋ฆฌ(๋ฐ์ง๋ฆ)) |
| layout_constraintCircleAngle | ๋ทฐ๊ฐ ๋ฐฐ์น๋  ๊ฐ๋(0๋ถํฐ 360๊น์ง ์ฐธ์กฐํ ๋ทฐ๋ก๋ถํฐ์ ๊ฐ๋) <br/> * ๊ฐ๋ ๊ณ์ฐ์ ์๊ณ์ฒ๋ผ 12์ ๊ธฐ์ค, ์๊ณ ๋ฐฉํฅ์ด๋ค. |

<br/>

## Visiblity behavior(๊ฐ์์ฑ์ ๋ฐ๋ฅธ ๋์)
Visiblity behavior ํน์ฑ์ Visibility ํน์ฑ๊ณผ, Margins์์ ์ค๋ชํ goneMargin ํน์ฑ์ ํฌํจํ๊ณ  ์๋ค.

<br/>

์ฌ๋ฐฑ(Margin) ๊ธฐ๋ฅ์ ๋ณด๋ฉด, ConstraintLayout ๋ด์ ์ฐ๊ฒฐ๋ View๋ค ๊ฐ์์ ํ๋์ View๊ฐ ์จ๊ฒจ์ง๋ฉด(GONE) ConstraintLayout์์ ํน์  ์ฒ๋ฆฌ๋ฅผ ํ๋๋ก ๋์ด ์๋ค.  
GONE๋ View๋ ํ์๋์ง๋ ์๊ณ  ๋ ์ด์์์ ์ผ๋ถ๋ก ์ทจ๊ธ๋์ง๋ ์์ง๋ง, ์์น๋ ์น์๋ฅผ ๊ณ์ฐํ๋ ์ธก๋ฉด์์๋ ์ฌ์ ํ ์๋ฏธ๊ฐ ์๋ค.  
๋ ์ด์์์ด ์ฌ์ด์ฆ๋ฅผ ๊ณ์ฐํ๊ณ  ๊ทธ๋ฆฌ๊ธฐ ์ํด์๋ GONE๋ View๋ ๊ธฐ๋ณธ์ ์ผ๋ก ํ๋์ ์ ์ฒ๋ผ ์ทจ๊ธ๋๋ค. ๋ค๋ฅธ View์ ์ ์ฝ ์กฐ๊ฑด์ด ์๋ค๋ฉด ์ฌ์ ํ ์ํฅ์ ๋ฏธ์น  ํ์ง๋ง, ๊ธฐ๋ณธ์ ์ผ๋ก ์ฌ๋ฐฑ(Margin)์ 0์ด๋ค.  
์ด๋ฌํ ๋์์ ์ฌ์ฉํ๋ฉด ๋ ์ด์์์ ํด์น์ง ์๋ ์ ์์ ๊ฐ๋จํ ๋ ์ด์์ ์ ๋๋ฉ์ด์์ ํ  ์๋ ์๋ค.

<br/>

## Dimension constraints(ํฌ๊ธฐ ๋ฐ ์น์์ ๋ํ ์ ์ฝ ์กฐ๊ฑด)
ConstraintLayout ๋ด์์ ์ต์๊ฐ ์ต๋๊ฐ์ ์ ์ํ  ์๋ ์๋ค.  
- `android:minWidth`ย  : ์ต์ ๊ฐ๋ก ๊ธธ์ด
- `android:minHeight`ย  : ์ต์ ์ธ๋ก ๊ธธ์ด
- `android:maxWidth`ย  : ์ต๋ ๊ฐ๋ก ๊ธธ์ด
- `android:maxHeight`ย  : ์ต๋ ์ธ๋ก ๊ธธ์ด

<br/>

์์ ์์ฑ๋ค์ ConstraintLayout ๋ด์์๋ง ์ฌ์ฉ ๊ฐ๋ฅํ๊ณ , android:layout_width ๋ฐ android:layout_height์ ๋ํ ๊ฐ์ด WRAP_CONTENT๋ก ์ง์ ๋์ด ์์ด์ผ ํ๋ค.

<br/>

### Widgets dimension constraints
View์ ๊ฐ๋ก, ์ธ๋ก ์ฌ์ด์ฆ(android:layout_width, android:layout_height) ์ฆ, ์์ ฏ์ ํฌ๊ธฐ๋ ํฌ๊ฒ 3 ๊ฐ์ง ๋ฐฉ์์ผ๋ก ๊ฒฐ์ ๋๋ค.  
- ์์น๋ฅผ ์ง์  ์๋ ฅํ  ๋(ex : 100dp๋ผ๊ณ  ์ง์  ์๋ ฅํ๋ ๊ฒฝ์ฐ) (ํน์  ํฌ๊ธฐ๋ก ์ง์ ํ๋ ๋ฐฉ๋ฒ)
- WRAP_CONTENT๋ฅผ ํตํด View ์ค์ค๋ก ์ฌ์ด์ฆ๋ฅผ ๊ฒฐ์ ์ง์ ๋
- width/height๋ฅผ 0dp๋ก ์๋ ฅํ๊ณ  ์ ์ฝ ์กฐ๊ฑด์ ์ํด ์ฌ์ด์ฆ๋ฅผ ๊ฒฐ์ ์ง์ ๋ (0dp = MATCH_CONSTRAINT)

<br/>

![https://developer.android.com/reference/android/support/constraint/resources/images/dimension-match-constraints.png](https://developer.android.com/reference/android/support/constraint/resources/images/dimension-match-constraints.png)

<br/>

์์ ๊ทธ๋ฆผ์ ๋ณด๋ฉด (a)์ ๊ฐ๋ก ๊ธธ์ด๋ WRAP_CONTENT๋ก ์ค์ค๋ก ์ฌ์ด์ฆ๋ฅผ ๊ฒฐ์  ์ง์๊ณ , (b)์ ๊ฐ๋ก ๊ธธ์ด๋ 0dp์ด๋ฉฐ ์ข์ฐ์ธก์ด ๋ถ๋ชจ ๋ทฐ์ ์ ์ฝ์ด ๊ฑธ๋ ค ๋ถ๋ชจ ๋ทฐ์ ๊ธธ์ด์ ๊ฐ๊ฒ ๋์ด๋ ์ํ์ด๋ค. (c)๋ (b)์ ๊ฐ์ด 0dp์ด์ง๋ง ์ฌ๋ฐฑ ๊ฐ์ด ์ ์ฉ๋ ๋ชจ์ต์ด๋ค.  
ConstraintLayout์์ ์ ์ฝ ์กฐ๊ฑด ์ด์ฉ ์ MATCH_PARENT๋ฅผ ์ฌ์ฉํ์ง ์๋ ๊ฒ์ ์ถ์ฒํ๋ค. ๋์  left/right ๋๋ top/bottom ์ ์ฝ ์กฐ๊ฑด๊ณผ ํจ๊ป MATCH_CONSTRAINT๋ฅผ ์ด์ฉํ๊ธธ ๋ฐ๋๋ค.

<br/>

Dimension constraints ์์ฑ์ ์์ ฏ์ ํฌ๊ธฐ๋ฅผ ์กฐ์ ํ๋ ๋ฐ ์ ์ฉํ๊ฒ ์ฌ์ฉ๋๋ค.  
Dimension constraints ์์ฑ์ ์ฌ์ฉํ๊ธฐ ์ํด์๋ 0dp(MATCH_CONSTRAINT) ์์ฑ ๊ฐ์ ๋ํด์ ์์์ผ ํ๋ค.  
์ผ๋ฐ์ ์ผ๋ก ๊ธธ์ด๋ฅผ ๊ฒฐ์ ํ  ๋, ํน์  ๊ฐ ๋๋ "wrap_content", "match_parent"๋ฅผ ๋ง์ด ์ฌ์ฉํ์ง๋ง, ConstraintLayout์ ์ํ ๋ทฐ๋ค์ ๋ํด์๋ "match_parent"๋ฅผ ์ง์ํ์ง ์๋๋ค.  
0dp ์์ฑ ๊ฐ๊ณผ Relative positioning, Margins๋ฅผ ํผํฉํด์ ์ฌ์ฉํ๋ฉด ๋ทฐ์ ํฌ๊ธฐ๋ฅผ ์์ ์์ฌ๋ก ์กฐ์ ํ  ์ ์๋ค.

<br/>

Dimension constraints ์์ฑ๋ค์ ๋ค์๊ณผ ๊ฐ๋ค.

| ์์ฑ | ์ค๋ช | ์์ฑ ๊ฐ |
| --- | --- | --- |
| layout_constraintDimensionRatio | ๋ทฐ์ ๊ฐ๋ก์ ์ธ๋ก์ ๋น์จ์ ์กฐ์ ํ๋ค. | ๋น์จ(n:m) / ๋ฐฉํฅ(H or W), ๋น์จ(n:m) |
| layout_constrainedWidth | ๋ทฐ๋ค์ด ๊ฐ๋ก ๋ฒ์ ๋ฐ์ผ๋ก ์ ๋๊ฐ๋๋ก ์กฐ์  | true / false |
| layout_constrainedHeight | ๋ทฐ๋ค์ด ์ธ๋ก ๋ฒ์ ๋ฐ์ผ๋ก ์ ๋๊ฐ๋๋ก ์กฐ์  | true / false |
| layout_constraintWidth_min | ๋ทฐ๋ค์ ๊ฐ๋ก ๊ธธ์ด ์ต์๊ฐ ์ค์  | ๊ธธ์ด ๊ฐ |
| layout_constraintHeight_min | ๋ทฐ๋ค์ ์ธ๋ก ๊ธธ์ด ์ต์๊ฐ ์ค์  | ๊ธธ์ด ๊ฐ |
| layout_constraintWidth_max | ๋ทฐ๋ค์ ๊ฐ๋ก ๊ธธ์ด ์ต๋๊ฐ ์ค์  | ๊ธธ์ด ๊ฐ |
| layout_constraintHeight_max | ๋ทฐ๋ค์ ์ธ๋ก ๊ธธ์ด ์ต๋๊ฐ ์ค์  | ๊ธธ์ด ๊ฐ |
| layout_constraintWidth_percent | ๋ทฐ๋ค์ ๊ฐ๋ก ๊ธธ์ด๋ฅผ parent์ percent๋ก ์ค์  | ๋น์จ(n:m) |
| layout_constraintHeight_percent | ๋ทฐ๋ค์ ์ธ๋ก ๊ธธ์ด๋ฅผ parent์ percent๋ก ์ค์  | ๋น์จ(n:m) |

<br/>

- ํน์  ํฌ๊ธฐ๋ก ์ง์ ํ๋ ๋ฐฉ๋ฒ    
    ๋ง ๊ทธ๋๋ก ๋์ ์์ ฏ์ width์ height์ ํฌ๊ธฐ๋ฅผ ์ง์  ์ง์ ํ๊ฑฐ๋ Dimension ๋ฆฌ์์ค๋ฅผ ํตํด ์ง์ ํ๋ ๊ฒ์ ์๋ฏธํ๋ค. ์ง์  ํฌ๊ธฐ๋ฅผ ์ง์ ํ  ๋์๋ ์๋์ ๊ฐ์ด ํ  ์ ์๋ค.
    
    ```xml
    <!-- ์ง์  ๊ฐ์ ์๋ ฅํ์ฌ ํฌ๊ธฐ๋ฅผ ์ง์ ํ๋ ๋ฐฉ๋ฒ -->
    <Button ...
        android:layout_width="100dp"
        android:layout_height="100dp" />
    ```
    
    <br/>
    
    Dimension ๋ฆฌ์์ค๋ฅผ ํตํด ์ง์ ํ๋ค๋ ๊ฒ์ ๋ฌด์์ผ๊น?     
    ์๋๋ก์ด๋์์๋ ์ด๋ฏธ์ง๋ ๋ฌธ์์ด๊ณผ ๊ฐ์ ์ ํ๋ฆฌ์ผ์ด์ ์ ๋ฆฌ์์ค๋ฅผ ๋๋ฆฝ์ ์ผ๋ก ๊ด๋ฆฌํ  ์ ์๋๋ก ์ง์ํ๋ค. dimension๊ณผ ๊ด๋ จ๋ ์์ฑ์ ๊ฒฝ์ฐ YourProject/res/values/dimens.xml ๊ฒฝ๋ก์ ํ์ผ์์ ๊ด๋ฆฌํ  ์ ์๋ค. (์ด ๊ฒฝ๋ก๋ ๊ท์น์ด๋ฏ๋ก ๊ผญ ์ง์ผ์ผ ์ ์ฉ์ด ๋๋ค.) ๋ฆฌ์์ค์ ๊ดํ ๊ฒ์ด ๋ ๊ถ๊ธํ๋ค๋ฉด [์๋๋ก์ด๋ ๊ณต์ ๋ฌธ์](https://developer.android.com/guide/topics/resources/providing-resources?hl=ko#QualifierRules)์์ ํ์ธํ  ์ ์๋ค.    
    ์ฃผ์ : MATCH_PARENT ์์ฑ์ ์ ์ฝ ๋ ์ด์์์ ์ํ ์์ ฏ์๋ ์ฌ์ฉํ์ง ์๋ ๊ฒ์ด ๊ถ์ฅ๋๋ค. ๋์  parent์ left/right ํน์ top/bottom ์ ์ฝ์ ์ง์ ํ์ฌ MATCH_CONSTRAINT ์์ฑ์ ์ฌ์ฉํ  ์ ์๋ค.

<br/>

- WRAP_CONTENT    
    WRAP_CONTENT๋ ๋์ ์์ ฏ ๋ด๋ถ์ ์ฝํ์ธ  ํฌ๊ธฐ์ ์์ ฏ์ ํฌ๊ธฐ๋ฅผ ์๋์ผ๋ก ๋ง์ถ๋ค. ์ด๋ ์๋์ ์์ฑ์ ์ฌ์ฉํ์ฌ ๋์ ์์ ฏ์ ํฌ๊ธฐ์ ์ ํ์ ๋ ์ ์๋ค.    
    - app:layout_constrainedWidth=โtrue|falseโ
    - app:layout_constrainedHeight=โtrue|falseโ
    
    <br/>
    
    ์์    
    : TextView์ width๋ฅผ wrap_content๋ก ์ง์ ํด ๋์๋ค. ๊ทธ๋ฐ๋ฐ TextView์ content ๊ธธ์ด๊ฐ ๋๋ฌด ๊ธธ์ด TextView์ width๊ฐ ๊ธธ์ด์ก๊ณ , ๊ทธ๋ก ์ธํด ํ๋ฉด์์ Button์ด ๋ณด์ด์ง ์๋๋ค.     
    ์ด๋ TextView์ app:layout_constrainedWidth=โtrueโ ์์ฑ์ ์ถ๊ฐํ์ฌ width์ ์ ํ์ ์ฃผ๋ฉด ์์ ฏ ์์ content ๊ธธ์ด๊ฐ ๊ธธ์ด์ง๋๋ผ๋ ์์ ๊ฐ์ด ๋ ์ด์์์ด ์ ์ง๋๋ค.    
    ![https://shinjekim.github.io/resources/images/constraint-width.png](https://shinjekim.github.io/resources/images/constraint-width.png)
    
<br/>

- MATCH_CONSTRAINT    
    ๊ฐ๋ก, ์ธ๋ก ๊ธธ์ด ์๋ ฅํ๋ ๋ถ๋ถ์ 0dp(= MATCH_CONSTRAINT)๋ฅผ ์ ์ฉํ  ๋, ๊ธฐ๋ณธ์ ์ธ ๋์์ MATCH_PARENT์ฒ๋ผ ๊ณต๊ฐ์ ๋ถ๋ชจ ๋ทฐ์ ๋ง๊ฒ ๊ฝ ์ฑ์ฐ๊ฒ ๋๋ค. ์ด๋ ์๋์ ์์ฑ์ ์ฌ์ฉํ์ฌ ์์ ฏ์ ํฌ๊ธฐ๋ฅผ ๋ณ๊ฒฝํ  ์ ์๋ค.    
    - layout_constraintWidth_min        
        : WRAP_CONTENT์ฒ๋ผ ๋์ํ๋ ์ต์๊ฐ์ ๊ฐ์ง๋ค.        
    - layout_constraintHeight_min        
        : WRAP_CONTENT์ฒ๋ผ ๋์ํ๋ ์ต์๊ฐ์ ๊ฐ์ง๋ค.        
    - layout_constraintWidth_max        
        : WRAP_CONTENT์ฒ๋ผ ๋์ํ๋ ์ต๋๊ฐ์ ๊ฐ์ง๋ค.        
    - layout_constraintHeight_max        
        : WRAP_CONTENT์ฒ๋ผ ๋์ํ๋ ์ต๋๊ฐ์ ๊ฐ์ง๋ค.        
    - layout_constraintWidth_percent        
        : 0์์ 1๊น์ง float ๊ฐ์ ์๋ ฅํ์ฌ ๋น์จ์ ์ผ๋ก ๊ธธ์ด๋ฅผ ๊ฒฐ์ ํ๋ค.        
    - layout_constraintHeight_percent        
        : 0์์ 1๊น์ง float ๊ฐ์ ์๋ ฅํ์ฌ ๋น์จ์ ์ผ๋ก ๊ธธ์ด๋ฅผ ๊ฒฐ์ ํ๋ค.
        
    <br/>

    - Min and Max
        
        min๊ณผ max๋ก ์ง์ ๋๋ ๊ฐ์ dp์ ๋จ์๋ก ์ง์  ํฌ๊ธฐ๋ฅผ ์ง์ ํ  ์๋ ์๊ณ , WRAP_CONTENT์ ๋์ผํ ๊ฒฐ๊ณผ๋ฅผ ๋ด๋ wrap์ ์ฌ์ฉํ์ฌ ์ง์ ํ  ์๋ ์๋ค.
        
    <br/>
    
    - Percent dimension        
        ํผ์ผํธ๋ฅผ ์ฌ์ฉํ๊ธฐ ์ํด์๋ ์๋์ ์ค์ ์ด ํ์ํ๋ค.        
        - ๋์ ์์ ฏ์ ํฌ๊ธฐ(dimension)๋ MATCH_CONSTRAINT(0dp)๋ก ์ง์ ๋์ด์ผ ํ๋ค.
        - app:layout_constraintWidth_default="percent" ํน์ app:layout_constraintHeight_default="percent"๋ฅผ ์ฌ์ฉํ์ฌ ๊ธฐ๋ณธ ๊ฐ์ ํผ์ผํธ๋ก ์ค์ ํ์ฌ์ผ ํ๋ค.
        - layout_constraintWidth_percent ํน์ layout_constraintHeight_percent ์์ฑ์ 0๊ณผ 1 ์ฌ์ด์ ๊ฐ์ผ๋ก ์ง์ ํด์ผ ํ๋ค.
    
    <br/>
    
    - Ratio        
        ์์ ฏ์ ์น์(dimension)์ ๋ํ ๋น์จ์ ์ด์ฉํ์ฌ ๋ค๋ฅธ ๋ถ๋ถ์ ์น์๋ฅผ ์ง์ ํ  ์๋ ์๋ค. ๋น์จ์ ์ฌ์ฉํ๊ธฐ ์ํด์๋ ์ต์ํ ํ๋์ ์น์(dimension)๋ฅผ 0dp(MATCH_CONSTRAINT)๋ก ์ง์ ํด์ผ๋ง ํ๋ค. ๊ทธ๋ฆฌ๊ณ  layout_constraintDimensionRatio๋ฅผ ์ฌ์ฉํ์ฌ ๋น์จ์ ์ง์ ํ๋ฉด ๋๋ค. ๋น์จ์ ์๋ ฅํ๋ ๋ฐฉ์์๋ ์๋์ ๊ฐ์ด ๋ ๊ฐ์ง์ ๋ฐฉ์์ด ์๋ค.        
        - app:layout_constraintDimensionRatio="1:1" (width:height๋ก ํํํ๋ ๋ฐฉ๋ฒ)
        - app:layout_constraintDimensionRatio="1.0" (width์ height์ ๋น์จ์ float๊ฐ์ผ๋ก ํํํ๋ ๋ฐฉ๋ฒ)
        
        <br/>
        
        ์๋์ ์ฝ๋์์๋ width๋ฅผ wrap_content๋ก ์ง์ ํ๊ณ  height๋ฅผ 0dp๋ก ์ง์ ํ ๋ค 1:1์ ๋น์จ์ ์๋ ฅํ๋ค. ๊ฒฐ๊ณผ๋ก๋ ๋ฒํผ์ content ํฌ๊ธฐ์ ๋ง์ถฐ์ง ์ ์ฌ๊ฐํ ๋ฒํผ์ด ๋ง๋ค์ด์ง๋ค.
        
        ```xml
        <Button ...
            android:layout_width="wrap_content"
            android:layout_height="0dp"
            app:layout_constraintDimensionRatio="1:1" />
        ```
        
        <br/>
        
        width์ height์ด ๋ชจ๋ MATCH_CONSTRAINT(0dp)๋ก ์ง์ ๋์ด ์์ ๋์๋ ๋น์จ์ ์ง์ ํ  ์ ์๋ค. ์ด ๊ฒฝ์ฐ์๋ ์๋์ ๊ฐ์ด W, ํน์ H,๋ฅผ ๋น์จ ์์ ์ถ๊ฐํ์ฌ ์ด๋ค ์ชฝ์ ์ ์ฝ์ ์ค ๊ฒ์ธ์ง๋ฅผ ์ง์ ํ  ์ ์๋ค. ์ด๋ ์ฃผ์ํด์ผ ํ  ์ ์ width์ height๋ฅผ ๋ชจ๋ 0dp๋ก ์ง์ ํ๋ ๊ฒ์ด๊ธฐ ๋๋ฌธ์ start/end, top/bottom์ ์ ์ฝ์ด ๊ฑธ๋ ค์์ด์ผ ์ ๋๋ก ํ์คํธํ  ์ ์๋ค.        
        - app:layout_constraintDimensionRatio = "H, x:y"            
            : width๋ฅผ constraint์ ๋ง์ถฐ ์ค์ ํ ๋ค ๋น์จ์ ๋ฐ๋ผ ๋์ด๋ฅผ ๊ฒฐ์ ํ๋ค.            
        - app:layout_constraintDimensionRatio = "W, x:y"            
            : height๋ฅผ constraint์ ๋ง์ถฐ ์ค์ ํ ๋ค ๋น์จ์ ๋ฐ๋ผ ๋์ด๋ฅผ ๊ฒฐ์ ํ๋ค.
            
<br/>

## Chains(๋ทฐ๋ผ๋ฆฌ ์ฐ๊ฒฐํ๊ธฐ)
Chain์ ๋ทฐ ๊ฐ์ ์ํธ ์ฐธ์กฐ ์ฐ๊ฒฐ์ ํ  ๋, ๋ทฐ๋ค์ ์ด๋ค ๋ฐฉ์์ผ๋ก ์ฐ๊ฒฐํด ํํํ ์ง๋ฅผ ๊ฒฐ์ ํ๋ค.

![https://developer.android.com/reference/android/support/constraint/resources/images/chains.png](https://developer.android.com/reference/android/support/constraint/resources/images/chains.png)

<br/>

Chain ์์ฑ์ ํตํด ์ฐ๊ฒฐ์ ํ  ๋๋ ์ํ ๊ธฐ์ค ๊ฐ์ฅ ์ผ์ชฝ์ ์๋ View ๋๋ ์์ง ๊ธฐ์ค์ผ๋ก ๊ฐ์ฅ ์๋จ์ ์๋ View๊ฐ ๊ธฐ์ค(Head)์ด ๋๋ค.

![https://developer.android.com/reference/android/support/constraint/resources/images/chains-head.png](https://developer.android.com/reference/android/support/constraint/resources/images/chains-head.png)

<br/>

chain ์คํ์ผ์ ์ฌ๋ฌ ํํ๊ฐ ์กด์ฌ ํ  ์ ์๋๋ฐ layout_constraintHorizontal_chianStyle ๋๋ layout_constraintVertical_chainStyle์ ์ฐ๊ฒฐ๋ ๋ทฐ๋ค์ head์๋ง ์ ์ด ์ฃผ๋ฉด ๋๋ค. ๊ธฐ๋ณธ chain ์คํ์ผ์ CHAIN_SPREAD์ด๋ค.  
- `CHAIN_SPREAD`  : ๋ทฐ๋ค์ ๊ณจ๊ณ ๋ฃจ ํผ์ณ ์ฌ๋ฐฑ์ ๊ฐ๊ฒ ํ๋ค. (๊ธฐ๋ณธ ๊ฐ)
- `CHAIN_SPREAD`์์์ `Weighted chain`์ ๋ง์ฝ ๋ทฐ์ ๊ธธ์ด๊ฐ 0dp๋ก ์ง์ ๋์ด ์๋ค๋ฉด ๋จ์ ๊ณต๊ฐ์ ์์น๋งํผ ๋น์จ์ ์ผ๋ก ๋๋  ๊ฐ๋๋ค.
    - `Weighted chain`  : ๊ฐ ์์๋ค์ ๊ฐ์ค์น์ ๋ฐ๋ผ ์ถ๊ฐ ๊ณต๊ฐ์ ํ๋ณดํ๊ฒ ๋๋ค. layout_constraintHorizontal_weight ํน์ layout_constraintVertical_weight ์์ฑ์ ์ด์ฉํ์ฌ ์ง์ ํ  ์ ์๋ค.
- `CHAIN_SPREAD_INSIDE`  : `CHAIN_SPREAD`์ ๋น์ทํ์ง๋ง ๊ฐ์ฅ ์ธ๊ณฝ์ ์๋ ๋ทฐ๋ค์ ๋ถ๋ชจ ๋ทฐ์ ์ฌ๋ฐฑ์ด ์๋ ์ํ๋ก ๊ณจ๊ณ ๋ฃจ ํผ์ณ์ง๋ค.
- `CHAIN_PACKED` : ๋ทฐ๋ค์ด ๋๋ ๋ญ์น๊ฒ ๋๊ณ  ๋ถ๋ชจ ๋ทฐ๋ก๋ถํฐ์ ์ฌ๋ฐฑ์ ๊ฐ๊ฒ ํ๋ค. ์ฌ๋ฐฑ์ ์กฐ์ ํ๊ณ  ์ถ๋ค๋ฉด bias ์กฐ์ ์ ํตํด ํ์ชฝ์ผ๋ก ์น์ฐ์น๊ฒ ๋ง๋ค ์ ์๋ค.

<br/>

![https://developer.android.com/reference/android/support/constraint/resources/images/chains-styles.png](https://developer.android.com/reference/android/support/constraint/resources/images/chains-styles.png)

<br/>

## Virtual Helper objects
์๋๋ก์ด๋๋ ConstraintLayout์ ์ฌ์ฉ์ ๋๊ธฐ ์ํด ํน๋ณํ ๊ฐ์ฒด ๋ช ๊ฐ์ง๋ฅผ ์ ๊ณตํ๋๋ฐ, ์ด๊ฒ์ด Virtual Helper objects์ด๋ค.

<br/>

### Guideline
์ค์  ์ดํ์์๋ ์ถ๋ ฅ๋์ง ์์ง๋ง, ๋ ์ด์์ ์์์ ๋๊ธฐ ์ํ ์ ์ ๊ทธ๋ ค ์ค๋ค.  
layout_constraintGuide_percent ์์ฑ์ ์ด์ฉํด์ 0์์ 1 ์ฌ์ด์ ์์ ๊ฐ์ ์๋ ฅํด์ ์ ์ ์์น๋ฅผ ๊ฒฐ์ ํ๋ค.

<br/>

๊ฐ์ด๋๋ผ์ธ(Guideline)์ ์ํ/์์ง ๋ชจ๋ ์ ์ฉํ  ์ ์๋ค.  
์ํ ๊ฐ์ด๋๋ผ์ธ(horizontal guidelines)์ height๋ 0์ด๊ณ  width๋ parent์ธ ConstraintLayout์ ๋ง์ถฐ์ง๋ค.  
์์ง ๊ฐ์ด๋๋ผ์ธ(vertical guidelines)์ width๋ 0์ด๊ณ  height๋ parent์ธ ConstraintLayout์ ๋ง์ถฐ์ง๋ค.

<br/>

๊ฐ์ด๋๋ผ์ธ์ ์์น๋ฅผ ์ง์ ํ๊ธฐ ์ํด์ ์๋์ ์ธ ๊ฐ์ง ๋ฐฉ๋ฒ์ ์ฌ์ฉํ  ์ ์๋ค.
- layout_constraintGuide_begin : ๋ ์ด์์์ left ๋๋ top์์๋ถํฐ์ ๊ณ ์  ๊ฑฐ๋ฆฌ๋ฅผ ์ง์ ํ๋ค.
- layout_constraintGuide_end : ๋ ์ด์์์ right ํน์ bottom์์๋ถํฐ์ ๊ณ ์  ๊ฑฐ๋ฆฌ๋ฅผ ์ง์ ํ๋ค.
- layout_constraintGuide_percent : ๋ ์ด์์์์์ width ํน์ height์ ํผ์ผํธ๋ฅผ ์ง์ ํ๋ค.

<br/>

### Group
ํน์  ๋ทฐ(View)๋ค์ ๋ฌถ์ด์ ์ ์ดํ  ์ ์๋ค. (ex : ์ฌ๋ฌ ๊ฐ์ ๋ทฐ๋ฅผ ํ ๋ฒ์ visibility ์ ์ดํ  ๋)  
constraint_referenced_ids ์์ฑ์ ์ด์ฉํด์ ์์ฑ ๊ฐ์ ID๋ก ์๋ ฅํ๋๋ฐ, ID๋ฅผ ','๋ก ๊ตฌ๋ถํด์ ์๋ ฅํ๋ค.

<br/>

๊ทธ๋ฃน(Group) ํฌํผ๋ฅผ ํตํด ๋ณต์์ ์์ ฏ์ ๊ทธ๋ฃนํํ์ฌ ์๋์ ๊ฐ์ด visibility ์์ฑ(visible | invisible | gone)์ ๋์์ ์ ์ดํ  ์ ์๋ค.

```xml
<androidx.constraintlayout.widget.Group
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" 
    android:visibility="invisible"
    app:constraint_referenced_ids="button, button2, button3" />
```

<br/>

์ ์ฝ๋์ย `android:visibility`ย  ๋ถ๋ถ์์ visibility ์์ฑ์ ์ง์ ํ  ์ ์์ผ๋ฉฐย `app:constraint_referenced_ids`์์ ๊ทธ๋ฃน์ผ๋ก ์ง์ ํ๊ณ ์ ํ๋ ์์ ฏ์ ์์ด๋๋ฅผ ์๋ ฅํ  ์ ์๋ค.

<br/>

### Barrier
์ฐธ์กฐํ๊ณ  ์๋ ๋ทฐ(View)๋ค ์ค์ ๊ฐ์ฅ ํฐ dimension์ position์ Guideline์ ์์ฑํ๋ค.  
barrierDirection ์์ฑ์ ์ด์ฉํด์ Guideline์ ์์ฑํ  ๋ฐฉํฅ์ ๊ฒฐ์ ํ๊ณ , ์์ฑ ๊ฐ์ ๋ฐฉํฅ์ผ๋ก ์๋ ฅํ๋ค.

<br/>

## Optimizer
์ ์ฝ ์นดํ๊ณ ๋ฆฌ์ ๋ํ ์ต์ ํ ๊ธฐ๋ฅ์ ํ๋ค.  
Constraint Layout 1.1 ๋ฒ์ ๋ถํฐ๋ ๋ ์ด์์์ ์๋๋ฅผ ๋์ด๊ธฐ ์ํด ์ต์ ํ ๋ฐฉ๋ฒ์ ์ ๊ณตํ๋ค.  
ConstraintLayout ์์์ app:layout_optimizationLevel ํ๊ทธ๋ฅผ ์ถ๊ฐํ์ฌ ์๋์ ๊ฐ์ด ์ต์ ํ ๋ ๋ฒจ์ ์ง์ ํ  ์ ์๋ค.  
- none : ์ต์ ํ ์ฌ์ฉ ์ ํจ
- standard : ๋ํดํธ ๋ ๋ฒจ
- direct : ๊ณ ์ ๋ ์์์ ์ฐ๊ฒฐ๋ ์ ์ฝ ์กฐ๊ฑด์ ๊ด๋ จ๋ ์ต์ ํ
- barrier : barrier ์ ์ฝ ์กฐ๊ฑด ๊ด๋ จ ์ต์ ํ
- chain : ์ฒด์ธ ์ ์ฝ ์กฐ๊ฑด ์ต์ ํ(์์ง ํ์คํธ ์ค์ธ ๊ธฐ๋ฅ)
- dimensions : ํฌ๊ธฐ(dimensions) ์ธก์  ์ต์ ํ(์์ง ํ์คํธ ์ค์ธ ๊ธฐ๋ฅ)

<br/>
<br/>

# ๐ ์ฐธ๊ณ 
- [Constraint Layout โ Part1. ๋ง๋ฅ ๋ ์ด์์ | ์ฐฐ์ค์ ์๋๋ก์ด๋ (charlezz.com)](https://www.charlezz.com/?p=669)
- [[์๋๋ก์ด๋ ์คํ๋์ค ์ ๋ฆฌ#1-6] ConstraintLayout :: ์ธ๋ฏผ์งฑ์ ๋ธ๋ก๊ทธ (tistory.com)](https://seminzzang.tistory.com/21)
- [์ ์ฝ ์กฐ๊ฑด ๋ ์ด์์ | ์๋๋ก์ด๋ ๊ฐ๋ฐ์ (android.com)](https://developer.android.com/reference/android/support/constraint/ConstraintLayout)
- [[Android] ConstraintLayout ํบ์๋ณด๊ธฐ (์๋๋ก์ด๋ ๊ณต์ ๋ฌธ์ ๋ฒ์ญ) ยท Challengist (shinjekim.github.io)](https://shinjekim.github.io/android/2019/08/07/Android-ConstraintLayout/)
