# ๐ก Custom UI

# โ Custom UI๋?
Android์์๋ ๊ธฐ๋ณธ์ ์ผ๋ก Button, TextView ๋ฑ ๊ธฐ๋ณธ์ ์ธ UI๋ฅผ ์ ๊ณตํด ์ค๋ค.  
๋ชจ๋  UI๋ค์ View ํด๋์ค๋ฅผ ์์๋ฐ์ ๋ง๋ค์ด์ง๋ค.  
์ด ์ค์์ ViewGroup์ ์์๋ฐ์ UI๋ค์ Layout์ด๋ผ๊ณ  ํ๊ณ  ๋๋จธ์ง๋ฅผ Widget์ด๋ผ๊ณ  ํ๋ค.  
ViewGroup์ ์์๋ฐ์ Layout๋ค์ ์์ ๋ทฐ๋ฅผ ๊ฐ์ง ์ ์๊ธฐ ๋๋ฌธ์ ์ด๋ฅผ ๋ฐฐ์นํ๋ ์ญํ ์ ํ๋ค.

<br/>

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://t1.daumcdn.net/cfile/tistory/2459953A571670000F](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://t1.daumcdn.net/cfile/tistory/2459953A571670000F)

<br/>

ํ์ง๋ง ์์ ์ด customํด์ ์ง์  UI๋ฅผ ๋ง๋ค์ด ์ฌ์ฉํ  ์๋ ์๋ค.  
์์ ๋ง์ Button์ด๋ View๋ฅผ ๋ง๋ค๊ณ  ์ถ๋ค๋ฉด View ํด๋์ค๋ฅผ ์์๋ฐ์์ ํ์ํ ๋ฉ์๋๋ค์ ์ค๋ฒ๋ผ์ด๋ํ๋ฉด ๋๋ค.

<br/>

CustomView๋ View ํด๋์ค๋ฅผ ์์ํ์ฌ ๋ง๋ ๋ค.  
CustomLayout์ ViewGroup ํด๋์ค๋ฅผ ์์ํ์ฌ ๋ง๋ ๋ค.

<br/>

## View ๋ฉ์๋ ํธ์ถ ์์
![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/DskeA/btqNXdSkcpk/RR6CN1AIUyXi591TObdK6K/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/DskeA/btqNXdSkcpk/RR6CN1AIUyXi591TObdK6K/img.png)

<br/>

### View ์ค๋ฒ๋ผ์ด๋ํ  ๋ฉ์๋
- onMeasure
    - ํ๋ ์ผ        
        : View์ ํฌ๊ธฐ๋ฅผ ๊ฒฐ์ ํ  ๋ ๋ถ๋ฆฌ๋ ํจ์๋ค.        
    - ํจ์ ํธ์ถ ๊ณผ์         
        : View.measure() โ View.onMeasure() โ View.setMeasuredDimension()        
    - ์ค๋ช        
        : view ์์ ์ ํฌ๊ธฐ๋ฅผ ์ง์ ํ๋ ํจ์์ด๋ค.        
        ์ธ์๋ก๋ (int widthMeasureSpec, int heightMeasureSpec) ๋์ด, ๋์ด ๊ฐ์ด ๊ฐ ๋ชจ๋์ ํจ๊ป ์กฐํฉ๋ ๊ฐ์ด๋ค. ์ด ๊ฐ๋ค์ ์ฌ์ฉํ๊ธฐ ์ํด์๋ MeausreSpce์ getMode()์ getSize()๋ฅผ ์ฌ์ฉํด์ผ ํ๋ค.        
        - int widthMode = MeasureSpec.getMode(widthMeasureSpec)
        - int width = MeasureSpec.getSize(widthMeasureSpec)
        
        <br/>
        
        ์ด ๋ Mode๋ 3๊ฐ์ง๊ฐ ์กด์ฌํ๋ค.        
        - MeasureSpec.UNSPECIFIED : ์์ค์์์ View๋ฅผ ์์ฑํ์ ๋ ํด๋น ๋ชจ๋๊ฐ ๋์ด ์จ๋ค. ์ด ๊ฒฝ์ฐ ๊ทธ๋ฅ ์ธ์๋ก ๋์ด์จ ๊ทธ๋๋ก ์ฌ์ฉํ๋ฉด ๋๋ค.
        - MeasureSpec.AT_MOST : ์ด ๊ฒฝ์ฐ๋ View ๋ด๋ถ์ ํฌ๊ธฐ๋ฅผ ๊ณ์ฐํ ๊ฐ์ ๋๊ฒจ ์ฃผ๋ฉด ๋๋ค. View์ layout_width, layout_height๊ฐ  wrap_content๋ก ์ค์ ๋ ๊ฒฝ์ฐ ์ด ๋ชจ๋๊ฐ ๋์ด์ค๊ฒ ๋๋ค. MeasureSpec.getSize()๋ฅผ ํตํด ๋์จ ๊ฐ์ View๊ฐ ์ต๋๋ก ๊ฐ์ง ์ ์๋ ํฌ๊ธฐ์ด๋ค. ์ด๋ฅผ ๋ฐํ์ผ๋ก ๋ด๋ถ ํฌ๊ธฐ๋ฅผ ๊ณ์ฐํด์ผ ํ๋ค. ๋ด๋ถ ํฌ๊ธฐ๊ฐ ์ด ๊ฐ๋ณด๋ค ํฌ๋ค๋ฉด ๋ฌธ์ ๊ฐ ๋  ์ ์๋ค.
        - MeasureSpec.EXACTLY : ํด๋น View์ layout_width, layout_height๊ฐ fill_parent๋ match_parent์ผ ๊ฒฝ์ฐ ๋ถ๋ชจ layout(viewGroup)์ด ํด๋น View์ ํฌ๊ธฐ๋ฅผ ๋ฏธ๋ฆฌ ์ง์ ํด์ width์ height๋ฅผ ๋๊ฒจ ์ฃผ๋ฏ๋ก MeasureSpec.getSize()์ผ๋ก ๋ฐํ๋ ๊ฐ์ ๊ทธ๋ฅ ์ฌ์ฉํ๋ฉด ๋๋ค.
        
        <br/>
        
        onMeasure() ํจ์ override์ ๋ด๋ถ์์๋ setMeasuredDimesion()ํจ์๋ฅผ ํธ์ถํด์ ์์ ์ ํฌ๊ธฐ๋ฅผ ์ค์ ํ์ฌ์ผ๋ง ํ๋ค. (๊ธฐ๋ณธ ๋์์ super.onMeasure()์ ํธ์ถํด๋ผ.)        
        setMeasuredDimension()ํจ์๋ ์์ ์ ํฌ๊ธฐ๋ฅผ ์ค์ ํ๋ ํจ์๋ก view์ width,height ๊ฐ์ ์๊ด์์ด ์ค์  ํฌ๊ธฐ๋ ์ด ํจ์๋ฅผ ํตํด ์ง์ ๋๋ค. (view์ width,height์ view์ ํฌ๊ธฐ๋ฅผ ๊ถ๊ณ ํ๋ ๊ฒ์ด๋ค. ์ค์ ๋ setMeasuredDimension()์ ์ง์ ํ ๊ฐ์ผ๋ก ํฌ๊ธฐ๊ฐ ๊ฒฐ์ ๋๋ค.)        
        ๋ง์ฝ onMeasure()์์ setMeasuredDimension()์ ํธ์ถํ์ง ์์ผ๋ฉด java.lang.IllegalStateException ์์ธ๊ฐ ๋ฐ์ํ๋ค.        
    - ๋ด๋ถ์์ ๋ง์ด ์ฐ์ด๋ ํจ์
        - this.measureChild() : ์์ ๋ทฐ์ ํฌ๊ธฐ๋ฅผ ๊ณ์ฐ์ํจ๋ค.
        - this.getChildMeasureSpec() : measureChildren()์์ ์ฌ์ฉํ๋ ํ๋์ ๋ฉ์๋์ด๋ค. ์ด ๋ฉ์๋๋ฅผ ํตํด ํน์  ์์ view์ MeasureSpce์ ๋ง๋ค ์ ์๋ค.

<br/>

- onLayout
    - ํ๋ ์ผ        
        : child view์ ์์น๋ฅผ ์ก์์ฃผ๋ ์ผ์ ํ๋ค. onMeasure ํธ์ถ ํ์ onLayout์ด ํธ์ถ๋๋ฏ๋ก ์์ ์ ํฌ๊ธฐ๋ฅผ ์ด๋ฏธ ์ธ์งํ๋ ์ํ์์ ์์น๋ฅผ ์ก์ ์ค ์ ์๋ค.        
        ์ฃผ์ํ  ์ ์ ์ด ์์น๊ฐ ์ฅ๋น ๋์คํ๋ ์ด์ ์ ๋์  ์์น์ด๋ค. ๋ถ๋ชจ๋ฅผ ๊ธฐ์ค์ผ๋ก ํ ์๋์ ์ธ ์์น๊ฐ ์๋๋ค.        
        ๋ง์ฝ ํ view์ Layout์ ํฌ๊ธฐ๊ฐ width 100, height 100์ด๊ณ  measure๋ ํฌ๊ธฐ๊ฐ width 20, height์ด๋ผ๋ฉด ๊ณต๊ฐ์ 100x100์ ํ ๋นํ์ง๋ง ํฌ๊ธฐ๋ 20x20์ผ๋ก ๊ทธ๋ ค์ง๋ค.        
    - ํจ์ ํธ์ถ ๊ณผ์         
        : ViewGroup.layout() โ View.layout() โ View.onLayout()        
    - ์ค๋ช        
        : ViewGroup์ ์์ํ์ฌ layout์ ๋ง๋๋ ๊ฒฝ์ฐ child view์ ์์น๋ฅผ ์ก์์ฃผ๋ ์ญํ ์ ํ๋ค.        
        ๋์ด ์ค๋ ํ๋ผ๋ฏธํฐ๋ ์ดํ๋ฆฌ์ผ์ด์ ์ ์ฒด๋ฅผ ๊ธฐ์ค์ผ๋ก ์์น๊ฐ ๋์ด์ค๋ฏ๋ก ์ฃผ์ํด์ผ ํ๋ค.        
    - ๋ด๋ถ์์ ๋ง์ด ์ฐ์ด๋ ํจ์
        - this.getPaddingLeft() : ์์ ์ ์ผ์ชฝ ํจ๋ฉ ๊ฐ
        - this.getPaddingTop() : ์์ ์ ์์ชฝ ํจ๋ฉ ๊ฐ
        - this.getPaddingRight() : ์์ ์ ์ค๋ฅธ์ชฝ ํจ๋ฉ ๊ฐ
        - this.getPaddingBottom() : ์์ ์ ์๋์ชฝ ํจ๋ฉ ๊ฐ
        - this.getMeasuredWidth() : ์์ ์ ํฌ๊ธฐ ๊ณ์ฐ ํ ๋์จ ๋์ด
        - this.getMeasuredHeight() : ์์ ์ ํฌ๊ธฐ ๊ณ์ฐ ํ ๋์จ ๋์ด
        - getChildCount() : ์์ ๋ทฐ์ ๊ฐ์๋ฅผ ๋ฐํํ๋ค.
        - child.measure() : ์์ ๋ทฐ์ ํฌ๊ธฐ๋ฅผ ๋ฐํํ๋ค. ์ด ๋ MeasureSpec.AT_MOST๋ก ๊ฑฐ์ ํธ์ถํ๋ค.
        - child.getMeasuredWidth() : ์์ ๋ทฐ์ ๋์ด๋ฅผ ๊ฐ์ ธ์จ๋ค. child.measure() ํธ์ถ ํ ํธ์ถํ๋ค.
        - child.getMeasuredHeight() : ์์ ๋ทฐ์ ๊ธธ์ด๋ฅผ ๊ฐ์ ธ์จ๋ค. child.measure() ํธ์ถ ํ ํธ์ถํ๋ค.
        - child.layout() : ์์ ๋ทฐ์ ์์น๋ฅผ ์ง์ ํ๋ค.

<br/>

- onDraw
    - ํ๋ ์ผ        
        : ํ๋ฉด์ ๊ทธ๋ฆฌ๋ ์ผ์ ํ๋ค.        
        ์ฃผ์ํ  ์ ์ ์ด๋ ์ขํ์ ๊ธฐ์ค์ ๋์คํ๋ ์ด์ ์ ๋์ ์ธ ์์น๊ฐ ์๋๋ค. ์์ ์ ๊ธฐ์ค์ผ๋ก ํ ์ขํ์ด๋ค.        
    - ์ค๋ช        
        : ์์ ์ ๊ทธ๋ฆฌ๊ณ  ์์์ด ์๋ ๊ฒฝ์ฐ ์์๋ค์ ๊ทธ๋ฆฌ๋ฉด ๋๋ค.        
    - ๋ด๋ถ์์ ๋ง์ด ์ฐ์ด๋ ํจ์
        - cavans() : Canvas ์ ๋ชจ๋  ๊ทธ๋ฆฌ๋ ํจ์๋ ๋ค ์ฌ์ฉํ๋ค.
        - this.getMeasuredWidth() : view ์์ ์ ๋์ด๋ฅผ ๋ฐํํ๋ค. ์ด๋ฅผ ๋ฐํ์ผ๋ก ๊ทธ๋ฆฌ๋ฉด ๋๋ค.
        - this.getMeasuredHeight() : view ์์ ์ ๋์ด๋ฅผ ๋ฐํํ๋ค. ์ด๋ฅผ ๋ฐํ์ผ๋ก ๊ทธ๋ฆฌ๋ฉด ๋๋ค.

<br/>

- ๊ธฐํ
    - ์ฐ์ด๋ ํจ์        
        : MeasureSpec.makeMeasureSpec : ๊ธธ์ด์ ๋ชจ๋๋ฅผ ์กฐํฉํ์ฌ measurespec ๊ฐ์ ๋ง๋ ๋ค.        
    - ์ฐธ๊ณ  ์ฌํญ
        - padding ๊ณผ margin ์ ์ฐจ์ด : padding์ ๋ด๋ถ ์ฌ๋ฐฑ, margin์ ์ธ๋ถ ์ฌ๋ฐฑ
            - ๋ง์ง(margin) vs ํจ๋ฉ(padding) : [๋ง์ง(margin)๊ณผ ํจ๋ฉ(padding)์ ์ฐจ์ด์ ์ ์์๋ณด์!! (tistory.com)](http://clason.tistory.com/321)
        - invalidate()์ requestLayout() ์ ์ฐจ์ด : invalidate๋ ํ๋ฉด์ด ์ ํจํ์ง ์์ผ๋ ๋ค์ ๊ทธ๋ฆฌ๋๋ก ํ๋ผ๋ ๊ฒ์ด๊ณ  requestLayout()์ layout์ ๊ฐฑ์ ํ๋ผ๋ ๊ฒ์ด๋ค.
            - ์ฐธ๊ณ  : [android - Usage of forceLayout(), requestLayout() and invalidate() - Stack Overflow](https://stackoverflow.com/questions/13856180/usage-of-forcelayout-requestlayout-and-invalidate)

<br/>
<br/>

# โ CustomView
## CustomView๋?
![http://labs.brandi.co.kr///assets/2021/1014/01.png](http://labs.brandi.co.kr///assets/2021/1014/01.png)

<br/>

์ ๊ทธ๋ฆผ์์ ์ต์๋จ์ ์์นํ๊ณ  ์๋ ๋ทฐ๋ ์ฌ์ฉ์ ์ธํฐํ์ด์ค๋ฅผ ๊ตฌ์ถํ๊ณ  ์ ์ ์ ๋ชจ๋  ์๋ ฅ ์ด๋ฒคํธ๋ฅผ ์ฒ๋ฆฌํ๋ ๊ธฐ๋ณธ์ ์ธ ํด๋์ค์ด๋ค. ์คํฌ๋ฆฐ์ ์ง์ฌ๊ฐํ ์์ญ์ ์ฐจ์งํ๋ฉฐ ํด๋น ์์ ์์๋ค๊ณผ ํจ๊ป ์ธก์ , ๋ฐฐ์น, ๊ทธ๋ฆฌ๋ ์ญํ ์ ํฉ๋๋ค. ViewGroup์ ํ์(์์) ๋ทฐ๋ฅผ ํฌํจํ๊ณ  ์์ฒด ๋ ์ด์์ ์์ฑ์ ์ ์ํ  ์ ์๋ค.

<br/>

CustomView๋ ์๋์ ๊ฐ์ ๋ ๋์์ด ๋  ์ ์๋ค.  
- ํ์ฌ ์ผ๋ฐ์ ์ธ ์๋๋ก์ด๋ ๊ตฌ์ฑ ์์๋ก๋ ์ํ๋ ์์ฉ์ด๋ ์ ๋๋ฉ์ด์ ๋๋ UI๋ฅผ ๋ง๋ค ์ ์์ ๋
- ์ฝ๋ ์ฌ์ฌ์ฉ์ฑ์ ์ํด
- nested view ๋ฑ์ผ๋ก ์ฑ๋ฅ ์ ํ๊ฐ ์์๋  ๋

<br/>

CustomView์ ํต์ฌ์ onMeasure, onDraw, onLayout์ด๋ค.  
๋ํ์ง ํฌ๊ธฐ๋ฅผ ์ ํํ๊ณ (onMeasure), ์ด๋ ์์น์(onLayout) ์ด๋ค ๊ทธ๋ฆผ์ ๊ทธ๋ฆด์ง(onDraw) ์ค์ ํด ์ฃผ๋ฉด CustomView๋ ์์ฑ๋๋ค.  
๋ทฐ๋ ํฌ์ปค์ค๋ฅผ ์ป๊ฒ ๋๋ฉด ๋ ์ด์์์ ๋ฃจํธ ๋ธ๋์์ ์์ํ์ฌ ์ ์ ์ํ๋ก ๊ทธ๋ ค์ง๋ค. ๋ฐ๋ผ์ ๋ถ๋ชจ๊ฐ ์์๋ค๋ณด๋ค ๋จผ์  ๊ทธ๋ ค์ง๊ณ , ํ์ ๋ค์ ํธ๋ฆฌ์ ๋ํ๋ ์์๋๋ก ๊ทธ๋ ค์ง๋ค.

<br/>

![http://labs.brandi.co.kr///assets/2021/1014/03.png](http://labs.brandi.co.kr///assets/2021/1014/03.png)

<br/>

## Constructor
๋ทฐ๋ ์ต๋ 4๊ฐ์ ์์ฑ์๋ฅผ ๊ฐ์ง๋ค.  
- View(Context context) : ์ฝ๋์์ ๋์ ์ผ๋ก ๋ทฐ๋ฅผ ์์ฑํ  ๋ ์ฌ์ฉํ  ์ ์๋ ๊ฐ๋จํ ์์ฑ์์ด๋ค. ํ๋ผ๋ฏธํฐ context๋ฅผ ํตํด ํ์ฌ ์คํ ์ค์ธ ๋ทฐ์ ๋ฆฌ์์ค ๋ฑ์ ์ก์ธ์ค ํ  ์ ์๋ค.
- View(Context context, AttributeSet attrs) : xml์์ ์์ฑํ  ๋
- View(Context context, AttributeSet attrs, int defStyleAttr) : ThemeStyle๊ณผ ํจ๊ป ๋ทฐ๋ฅผ ์์ฑํ  ๋
- View(Context context, AttributeSet attrs, int defStyleAttr, int defStyleRes) : ThemeStyle ๋๋ Style๋ก xml์์ ๋ทฐ๋ฅผ ์์ฑํ  ๋

<br/>

์ฝํ๋ฆฐ์์๋ @JvmOverloads ์ด๋ธํ์ด์์ ํตํด ์์ฑ์๋ฅผ ๊ฐํธํ๊ฒ ์ ์ธํ  ์ ์๋ค.

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

JvmOverloads๋ฅผ ์ด์ฉํ๋ฉด 1๊ฐ์ ํ๋ผ๋ฏธํฐ๋ฅผ ๊ฐ์ง๋ Constructor๋ถํฐ n-parameter ์์ฑ์๊น์ง ๋ง๋ค์ด ์ค๋ค.  
API < 21์ ๋๋ฐ์ด์ค์์ JvmOverloads ์ด๋ธํ์ด์์ผ๋ก 4-parameter ์์ฑ์๋ฅผ ๋ง๋ค๊ฒ ๋๋ฉด StackOverflow๋ฅผ ์ผ๊ธฐํ  ์ ์๋ค.

<br/>

![http://labs.brandi.co.kr///assets/2021/1014/02.png](http://labs.brandi.co.kr///assets/2021/1014/02.png)

<br/>

## CustomView๋ฅผ ๋ง๋๋ ๊ณผ์ 
- ์์ ์ฐธ๊ณ  : [[Android] Custom View, Custom Layout ( ์ปค์คํ ๋ ์ด์์, ์ปค์คํ ๋ทฐ, ์ง์  ๋ทฐ ๋ ์ด์์ ๋ง๋ค๊ธฐ ) (tistory.com)](https://onecellboy.tistory.com/344)

<br/>

- CustomView์ ํด๋์ค๋ฅผ ๋ง๋ ๋ค. (View ์์)
- attrs.xml์ CustomView์์ ์ฌ์ฉํ  ์์ฑ๋ค์ ์ ์ํ๋ค. (Custom Attribute ์ ์)
- CustomView์์ attrs๋ฅผ ์ฝ์ด์ค๊ณ  ์ค๋ฒ๋ผ์ด๋ฉ ๋ฉ์๋(์ฃผ๋ก onMeasure, onDraw๊ฐ ๋  ๊ฒ์ด๋ค.)๋ฅผ ๊ตฌํํ๋ค.

<br/>

์ด ์ ๋์ ๊ณผ์ ์ ๊ฑฐ์น  ๊ฒ์ด๋ฉฐ, ๊ตฌํํ  CustomView๊ฐ ๋ฌด์์ด๊ณ  ํ์ํ ๋ฉ์๋๊ฐ ๋ฌด์์ด๋์ ๋ฐ๋ผ ์ถ๊ฐ์ ์ธ ๋จ๊ณ๊ฐ ์์ ๊ฒ์ด๋ค.

<br/>

## ํต์ฌ
- ์์ ์ฐธ๊ณ  : [[Android] Custom View, Custom Layout ( ์ปค์คํ ๋ ์ด์์, ์ปค์คํ ๋ทฐ, ์ง์  ๋ทฐ ๋ ์ด์์ ๋ง๋ค๊ธฐ ) (tistory.com)](https://onecellboy.tistory.com/344)

<br/>

1. View๋ฅผย ์์ย ๋ฐ์ย ์ฌ์ฉํ  ๋๋ย onLayout(), onMeasure()๋ย ์ค๋ฒ๋ผ์ด๋ํ์งย ์์๋ย ๋๋ค. (View ํด๋์ค๋ย ํฌ๊ธฐ์ย ์์น์ย ๋ํย ํ๋์ดย ๊ธฐ๋ณธ์ ์ผ๋กย ์ ์๋์ด์๋ค.)
2. xml์ย ํตํดย ์์ฑ์ย ์ ์ํ๋ย ๋ฐฉ๋ฒ๊ณผย ์ฌ์ฉ ๋ฐฉ๋ฒ
3. onDraw()๋ฅผย ํตํดย ๊ทธ๋ฆฌ๋ย ๋ฐฉ๋ฒ
4. ๊น๋นก๊น๋นกํ๋ย ๊ฑฐ์ย ๊ฐ์ย ๊ณ์์ ์ธย ์ ๋๋ฉ์ด์์ย Handler์ย invalidate()๋ฅผย ํตํดย ํ๋ย ๋ฐฉ๋ฒ

<br/>
<br/>

# โ CustomLayout
## CustomLayout์ ๋ง๋๋ ๊ณผ์ 
- ์์ ์ฐธ๊ณ  : [[Android] Custom View, Custom Layout ( ์ปค์คํ ๋ ์ด์์, ์ปค์คํ ๋ทฐ, ์ง์  ๋ทฐ ๋ ์ด์์ ๋ง๋ค๊ธฐ ) (tistory.com)](https://onecellboy.tistory.com/344)

<br/>

- Custom Attribute ์ ์
- CustomLayout ํด๋์ค ์์ฑ ๋ฐ Attribute ์ฒ๋ฆฌํ๊ธฐ
- onMeasure, onLayout ์ฒ๋ฆฌํ๊ธฐ

<br/>

## Compose CustomLayout
Compose์์ UI๋ ํธ์ถ๋  ๋ UI ์์๋ฅผ ๋ด๋ณด๋ด๋ ์ปดํฌ์ ๋ธ ํจ์๋ก ํํ๋๋ค. ๊ฐ UI ์์์๋ ํ๋์ ์์ ์์์ ์ฌ๋ฌ ๊ฐ์ ํ์ ์์๊ฐ ์์ ์ ์๊ณ , ๊ฐ ์์๋ (x, y) ์์น๋ก ์ง์ ๋ ์์ ์์ ๋ด์ ๋ฐฐ์น๋๋ฉฐ width, height์ผ๋ก ํฌ๊ธฐ๊ฐ ์ง์ ๋๋ค.

<br/>

์์ ์์๋ ํ์ ์์์ ์ ์ฝ ์กฐ๊ฑด์ ์ ์ํ๊ณ , ์ด๋ฌํ ์ ์ฝ ์กฐ๊ฑด ๋ด์์ ์์์ ํฌ๊ธฐ๋ฅผ ์ ์ํด์ผ ํ๋ค.

<br/>

UI ํธ๋ฆฌ์ ๊ฐ ๋ธ๋๋ฅผ ๋ฐฐ์นํ๋ ์์์  
1. ๋ชจ๋  ํ์ ์์ ์ธก์   
2. ์์ฒด ํฌ๊ธฐ ๊ฒฐ์   
3. ํ์ ์์ ๋ฐฐ์น  

์์๋ก ์งํ๋๋ค.

<br/>

Custom Layout์ ๊ตฌํํ๊ธฐ ์ํด `Layout`  ์ปดํฌ์ ๋ธ์ ์ฌ์ฉํ๋ค. ์ด ์ปดํฌ์ ๋ธ์ ์ฌ์ฉํ๋ฉด ํ์ ์์๋ฅผ ์๋์ผ๋ก ์ธก์ ํ๊ณ  ๋ฐฐ์นํ  ์ ์๋ค.  
๋ง์ด ์ฌ์ฉํ๋ `Column`  ๋ฐ `Row`์ ๊ฐ์ ๋ชจ๋  ์์ ์์ค ๋ ์ด์์์ Layout ์ปดํฌ์ ๋ธ์ ์ฌ์ฉํ์ฌ ๋น๋๋๋ค.

<br/>
<br/>

# ๐ ์ฐธ๊ณ 
- [android custom ui โ ๋จ๋๋ฆฌ์ ๋์งํธ์ธ์ (tistory.com)](https://jade314.tistory.com/entry/android-custom-ui)
- [[Android] Custom View, Custom Layout ( ์ปค์คํ ๋ ์ด์์, ์ปค์คํ ๋ทฐ, ์ง์  ๋ทฐ ๋ ์ด์์ ๋ง๋ค๊ธฐ ) (tistory.com)](https://onecellboy.tistory.com/344)
- [[Android] CustomView ๋ง๋ค๊ธฐ - CircleDotsLineView (tistory.com)](https://doitddo.tistory.com/99)
- [CustomView ์ดํดํ๊ธฐ (brandi.co.kr)](https://labs.brandi.co.kr/2021/10/14/jeonhs.html)
- [Compose CustomLayout ๋ง๋ค๊ธฐ(์ํ ๋ ์ด์์) - 1 (velog.io)](https://velog.io/@haem99/Compose-CustomLayout-%EB%A7%8C%EB%93%A4%EA%B8%B0%EC%9B%90%ED%98%95-%EB%A0%88%EC%9D%B4%EC%95%84%EC%9B%83-1)
