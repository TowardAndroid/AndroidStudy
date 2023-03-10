# ๐ก AAC

# โ AAC๋?
AAC(Android Architecture Components)๋ ํ์คํธ์ ์ ์ง ๋ณด์๊ฐ ์ฌ์ด ์ฑ์ ๋์์ธํ  ์ ์๋๋ก ๋๋ ๋ผ์ด๋ธ๋ฌ๋ฆฌ์ ๋ชจ์์ด๋ค.

<br/>

Google I/O 2017์์ ์๋ก์ด ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ฅผ AAC๋ก ๋ฌถ์ด์ ๋ฐํ๋ฅผ ํ์ฌ AAC๋ผ๋ ๊ฒ์ด ์ฌ์ฉ๋๊ฒ ๋์๊ณ ,  
Google I/O 2018์์ Android Jetpack์ ๋ฐํํ  ๋๋ Jetpack์ ๊ตฌ์ฑ ์์ ์ค ํ๋๋ก AAC๊ฐ ๋ค์ด๊ฐ ์๋ค.

<br/>

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/bMk7kC/btrDxpmTmlo/daWm7VbPDJEXU6CBnCLeqK/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/bMk7kC/btrDxpmTmlo/daWm7VbPDJEXU6CBnCLeqK/img.png)

<br/>

Google I/O 2018์ ๋ฐํ ์๋ฃ๋ฅผ ๋ณด๋ฉด ๋ค์๊ณผ ๊ฐ์ ์ด๋ฏธ์ง๋ฅผ ํ์ธํ  ์ ์๋๋ฐ, ์ฌ๊ธฐ์ Architecture ๋ถ๋ถ์ด AAC๋ผ๊ณ  ๋ณผ ์ ์๋ค.  
New๋ก ๋ถ์ด์๋ ๊ฒ๋ค์ด Jetpack์์ ์ถ๊ฐ๋ AAC์ด๊ณ , ๊ทธ๋ ์ง ์์ ๋ถ๋ถ์ด 2017๋๋ Google I/O์์ ๋ฐํ๋ AAC๋ผ๊ณ  ์๊ฐํ๋ฉด ๋๋ค.

<br/>

![https://velog.velcdn.com/images/hwi_chance/post/f8773023-1064-4259-b0e6-65eced0e2210/final-architecture.png](https://velog.velcdn.com/images/hwi_chance/post/f8773023-1064-4259-b0e6-65eced0e2210/final-architecture.png)

<br/>

AAC๋ 2017๋๋์ ๋ฐํํ 5๊ฐ์ ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ก  
- Lifecycles(Easy handling lifecycles)    
    : ์ฑ์ ์๋ช ์ฃผ๊ธฐ๋ฅผ ๊ด๋ฆฌ    
- LiveData(Lifecycle aware observable)    
    : ๊ธฐ๋ณธ ๋ฐ์ดํฐ๋ฒ ์ด์ค๊ฐ ๋ณ๊ฒฝ๋๋ฉด ๋ทฐ์ ์๋ฆฌ๋ ๋ฐ์ดํฐ ๊ฐ์ฒด ๋น๋    
- ViewModel(Managing data in a lifecycle)    
    : ์ฑ ํ์  ์ ์ ๊ฑฐ๋์ง ์๋ UI ๊ด๋ จ ๋ฐ์ดํฐ ์ ์ฅ    
- Room(object Mapping for SQLite)    
    : SQLite ๊ฐ์ฒด ๋งคํ ๋ผ์ด๋ธ๋ฌ๋ฆฌ    
- Paging(Gradually loading information)    
    : ํ์ด์ง ๊ธฐ๋ฒ์ ์ฝ๊ฒ ์ ์ฉ    
- Databinding    
    : ํ๋ก๊ทธ๋๋งคํฑ ๋ฐฉ์์ด ์๋ ์ ์ธ์  ํ์์ผ๋ก UI ๊ตฌ์ฑ ์์๋ฅผ ์ฑ์ ๋ฐ์ดํฐ ์์ค์ ๋งคํ    
- Navigation    
    : ํ๋๊ทธ๋จผํธ์ ์งํ์ ๋ณด๊ธฐ ์ฝ๊ฒ ์ ๋ฆฌํด ์ค๋ค.    
- WorkManager    
    : ์ง์ฐ ๊ฐ๋ฅํ ๋น๋๊ธฐ ์์์ ์ฝ๊ฒ ์์ฝํ  ์ ์๋ API    

๋ค์๊ณผ ๊ฐ์ด ๊ตฌ์ฑ๋์ด ์๋ค.

<br/>
<br/>

# โ AAC ViewModel
## MVVM ํจํด์ ViewModel๊ณผ AAC์ ViewModel

> AAC์์ ๋งํ๋ ViewModel๊ณผ MVVM ํจํด์์์ ViewModel์ ViewModel์ด๋ผ๋ ์ด๋ฆ๋ง ๊ฐ์ ๋ฟ, ์ ํ ๋ค๋ฅธ ๊ฒ์ด๋ค.
> 

<br/>

### MVVM ํจํด์ ViewModel
- MVP ํจํด์์ ํ์๋ ํจํด์ผ๋ก, ๋น์ฆ๋์ค ๋ก์ง๊ณผ ํ๋ ์  ํ์ด์ ๋ก์ง์ UI๋ก๋ถํฐ ๋ถ๋ฆฌํ๋ ๊ฒ์ ๋ชฉํ๋ก ์ฌ์ฉ๋๋ค. View์ Model ์ฌ์ด์ ์์กด์ฑ์ ์์  ํ์คํธ, ์ ์ง ๋ณด์, ์ฌ์ฌ์ฉ์ฑ์ ๋์ธ๋ค.
- ViewModel์ ์ฝ๊ฒ ๋งํด์, ๋ทฐ์ ๋ชจ๋ธ ์ฌ์ด์์ ๋ฐ์ดํฐ๋ฅผ ๊ด๋ฆฌํ๊ณ , ๋ฐ์ธ๋ฉํด ์ฃผ๋ ์ญํ ์ ํ๊ฒ ๋๋ค.
- MVVM์์์ ViewModel์ View๊ฐ ViewModel์์์ ๊ฐ์ Observeํ์ฌ Updateํ๊ณ , ViewModel์ Model์ Updateํ๋ ์ญํ ์ ๋ด๋นํ๋ค.

<br/>

### AAC์ ViewModel
- [์๋๋ก์ด๋ ๊ณต์ ๋ฌธ์](https://developer.android.com/topic/libraries/architecture/viewmodel)์ ๋ฐ๋ฅด๋ฉด ์๋ช ์ฃผ๊ธฐ๋ฅผ ๊ณ ๋ คํ์ฌ UI ๊ด๋ จ ๋ฐ์ดํฐ๋ฅผ ์ ์ฅํ๊ณ  ๊ด๋ฆฌํ๋๋ก ์ค๊ณ๋์ด ์๋ค, ํ๋ฉด ํ์ ๊ณผ ๊ฐ์ด ๊ตฌ์ฑ์ ๋ณ๊ฒฝํ  ๋๋ ๋ฐ์ดํฐ๋ฅผ ์ ์งํ  ์ ์๋ค, ๋ผ๊ณ  ๋์์๋ค.
- ํ๋ฉด ํ์ ์ด ๋ฐ์ํ์ ๋ ์กํฐ๋นํฐ๊ฐ ์ข๋ฃ๋๊ณ  ๋ค์ ์์ฑ๋๋ ๊ณผ์ ์ ๊ฑฐ์น๋๋ฐ, ์ด๋ย ์๋ช ์ฃผ๊ธฐ๋ฅผ ๊ด๋ฆฌํ์ฌ ๋ฐ์ดํฐ๋ฅผ ์ ์คํ์ง ์๊ณ  ๊ทธ๋๋ก ๋ณด์กดํด ๋๊ณ  ์ฌ์ฉํ  ์ ์๊ฒย ํด ์ค๋ค.
- Activity/Fragment๋น ํ๋์ ViewModel๋ง ์์ฑ ๊ฐ๋ฅํ๋ค.
- ๋ฉ๋ชจ๋ฆฌ ๋์, ํ๋ฉด ํ์ ๊ณผ ๊ฐ์ ์ํฉ์์๋ Data๋ฅผ ์ ์ฅํ  ์ ์๋ค.

<br/>

AAC์์์ ViewModel์ ๊ฐ๋จํ๊ฒ ์๊ฐํด์ LifeCycle์ ๊ด๋ฆฌํ์ฌ ํ๋ฉด์ ํ์ ํ์ ๋ ๋ฐ์ดํฐ๋ฅผ ์ ์คํ์ง ์๊ณ  ์ฌ์ฉํ  ์ ์๊ฒ ํด์ฃผ๋ ์ญํ , MVVM์์์ ViewModel์ ๋ทฐ์ ๋ชจ๋ธ ์ฌ์ด์์ ๋ฐ์ดํฐ๋ฅผ ๊ด๋ฆฌํ๊ณ  ๋ฐ์ธ๋ฉํด ์ฃผ๋ ์ญํ ๋ก ๋์ ์์ ํ ๋ค๋ฅด๋ค.

<br/>

### MVVM ํจํด์์์ AAC์ ViewModel
MVVM ํจํด์ ์์ ๋ฅผ ํ์ธํด๋ณด๋ฉด, AAC์ ViewModel์ ์ฌ์ฉํ์ฌ ๊ตฌํํ๊ณ  ์๋ ๋ชจ์ต์ ๋ณผ ์ ์๋ค.  
MVVM์์์ ViewModel์ ๊ทธ๋ฌํ ์ญํ ์ ํ๋ Class๋ฅผ ๋ง๋ค์ด์ ๊ตฌํํ  ์ ์๋ค.  
์ฌ๊ธฐ์ ์ค์ํ ๊ฒ์, MVVM์์์ ViewModel์ด๋ผ๊ณ  ํ๋ ๊ฒ์ ๊ทธ๋ฌํ ์ญํ ์ ํ๋ ํด๋์ค๋ผ๋ ์ ์ด๋ค.  
์ฆ, AAC์ ViewModel์ MVVM์ ViewModel์ด ํด์ผ ํ๋ ์ญํ ์ ์ค๋ค๋ฉด AAC ViewModel์ด๋ฉด์ MVVM์ ViewModel์ด ๋  ์ ์๋ค.  
AAC์ ViewModel์ ํ๋ฉด ํ์ ๊ณผ ๊ฐ์ ์ด๋ฒคํธ์์๋ ๋ฐ์ดํฐ๊ฐ ์ ์ค๋์ง ์๊ณ  ๊ทธ๋๋ก ์ฌ์ฉํ  ์ ์์ผ๋ ์คํ๋ ค ๋ ์ข์ ํ๊ฒฝ์์ MVVM์ ViewModel์ ๋ง๋ค ์ ์๊ฒ ๋๋ ์์ด๋ค.

<br/>

**MVVM ํจํด์์์ ViewModel๊ณผ AAC์์์ ViewModel์ ์ฐจ์ด์ **  
- AAC์ ViewModel์ ํด๋น ์กํฐ๋นํฐ์์ ์ฑ๊ธํค์ผ๋ก ํ๋๋ง ์กด์ฌํ๋ค.
    - ๋ฐ๋ผ์ ์ฌ๋ฌ ๋ฒ ViewModel์ ์์ฑํ์ฌ ์ฌ์ฉํ๋ค๊ณ  ํด๋, ์ฑ๊ธํค์ด๊ธฐ ๋๋ฌธ์ ์ต์ด์ ์์ฑํ ํ๋์ ๊ฐ์ฒด๋ง ์ฌ์ฉํ๊ฒ ๋๋ค.
- MVVM์์ View์ ViewModel์ 1:N ๊ด๊ณ์ด๊ธฐ ๋๋ฌธ์ ํ๋์ ์กํฐ๋นํฐ์ ์ฌ๋ฌ ๊ฐ์ ViewModel์ ์ฌ์ฉํ  ์ ์๋ค.
    - ๋ฐ๋ผ์ A๋ผ๋ ์กํฐ๋นํฐ์ AViewModel, BViewModel, CViewModel๊ณผ ๊ฐ์ด ์ฌ๋ฌ ๊ฐ์ ViewModel์ ์ฌ์ฉํ  ์ ์์ผ๋ฉฐ, AAC ViewModel์ ํน์ฑ์ ๊ฐ ViewModel์ ์ฑ๊ธํค์ผ๋ก ์์ฑ๋์ด ์ฌ์ฉํ๊ฒ ๋๋ ๊ฒ์ด๋ค.
    - ํ์ง๋ง ๊ตฌ๊ธ์์ ๊ถ์ฅํ๋ ViewModel์ ํ๋์ ์กํฐ๋นํฐ์ ํ๋์ ViewModel์ ์ฌ์ฉํ๊ณ , LiveData์ ์ฌ๋ฌ ๊ฐ์ Model์ ์ฌ์ฉํ์ฌ ๊ตฌํํ๋ ๊ฒ์ ๊ถ์ฅํ๊ณ  ์๋ค. ๊ฐ๋ฐ์๊ฐ ํ๋จํ์ฌ ํ๋ก์ ํธ์ ์๋ง๊ฒ ViewModel์ ์ ์ธํด์ ์ฌ์ฉํ๋ฉด ๋  ๊ฒ์ด๋ค.

<br/>

## AAC ViewModel
- ์๋๋ก์ด๋ ์๋ช ์ฃผ๊ธฐ๋ฅผ ๊ณ ๋ คํด์ ๋ง๋ค์ด์ง ViewModel์ด๋ค.
    - Activity/Fragment๋น ํ๋์ ViewModel๋ง ์์ฑ ๊ฐ๋ฅํ๋ค.
    - ๋ฉ๋ชจ๋ฆฌ ๋์, ํ๋ฉด ํ์ ๊ณผ ๊ฐ์ ์ํฉ์์๋ Data๋ฅผ ์ ์ฅํ  ์ ์๋ค.

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/KfCgk/btrnHS7ds66/Ieo5zkpaGBGzV022H7eVv1/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/KfCgk/btrnHS7ds66/Ieo5zkpaGBGzV022H7eVv1/img.png)

> ํ๋ฉด ํ์  ์ํฉ์์ AAC ViewModel๊ณผ Activity์ ์๋ช ์ฃผ๊ธฐ
> 

Activity Scope ViewModel์ ๊ฒฝ์ฐ์๋ ํ๋ฉด ํ์ ์์๋ ์ด์์๋ ๊ฒ์ ์ ์ ์๋ค. (Fragment Scope์ ๊ฒฝ์ฐ์๋ ํ๋ฉด ํ์ ์์ ์์ ๋กญ์ง ๋ชปํ ๊ฒ ๊ฐ๋ค. ๋ฌผ๋ก  Manifest์์ ConfigureChange ์์ฑ์ ์ฌ์ฉํ๋ฉด ๋  ๊ฒ ๊ฐ๋ค.)

<br/>

- UI ๊ด๋ จ ์์๋ฅผ ์ ์ฅํ๊ณ  ๊ด๋ฆฌํ๋ค.
    - ๋ฐ๋ผ์ Activity Scope์ ViewModel์ ํ๋ ๋ง๋ค์ด ๋์ผ๋ฉด ํด๋น Activity ์์ ์กด์ฌํ๋ Fragment๋ค์ ๋ฐ์ดํฐ๋ฅผ ์ฝ๊ฒ ๊ณต์ ํ  ์ ์๊ฒ ๋๋ค.

<br/>

- ViewModel์ด ๋ก๋ ์ญํ ์ ๋์ฒดํ  ์ ์๋ค.

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/A7edd/btrnJAZsBJz/9Enzz7JgTLfAXSTmlljQSk/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/A7edd/btrnJAZsBJz/9Enzz7JgTLfAXSTmlljQSk/img.png)

> ๋ก๋๋ฅผ ์ฌ์ฉํ ๋ฐ์ดํฐ ๋ก๋ & UI ์๋ฐ์ดํธ ๋ก์ง
> 

<br/>

์๋๋ ๋ก๋๋ฅผ ์ฌ์ฉํด์ ๋ฐ์ดํฐ๋ฅผ ๋ก๋ํ๊ณ , ๋ก๋ ๋งค๋์ ๊ฐ ์ฝ๋ฐฑ์ ํตํด์ UI Controller์๊ฒ ์๋ ค ์ฃผ๋ฉด UI Controller๊ฐ ๊ทธ ๋ ๋ฐ์ํด์ UI๋ฅผ ์๋ฐ์ดํธ ์์ผฐ๋ค.

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/btkt8e/btrnClvzsWO/UredyrsnGDzHpkjT9ReAik/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/btkt8e/btrnClvzsWO/UredyrsnGDzHpkjT9ReAik/img.png)

> ViewModel์ ์ฌ์ฉํ ๋ฐ์ดํฐ ๋ก๋ & UI ์๋ฐ์ดํธ ๋ก์ง
> 

<br/>

ViewModel์ ์ฌ์ฉํ๋ฉด UI Controller๋ ViewModel(LiveData)์ Observeํ๋ค๊ฐ ๊ฐ์ด ์๋ฐ์ดํธ๋๋ฉด ๊ทธ ๋ UI๋ฅผ ์๋ฐ์ดํธํ๋ฉด ๋๋ค. ์ฆ, UI ์ปจํธ๋กค๋ฌ๋ ๋ฐ์ดํฐ ๋ก๋ ์์์์ ๋ถ๋ฆฌ๋๋ฏ๋ก ํด๋์ค ๊ฐ ์์กด์ฑ์ด ์ฌ๋ผ์ง๊ฒ ๋๋ค.

<br/>

- ์ฝ๋ฃจํด์ ๊ณต์์ ์ผ๋ก ์ง์ํ๋ค.
    - ์์ธํ ์ ๋ณด๋ ์๋๋ฅผ ์ฐธ์กฐํ๋ฉด ๋๋ค.
        - [์๋ช ์ฃผ๊ธฐ ์ธ์ ๊ตฌ์ฑ์์์ ํจ๊ป Kotlin ์ฝ๋ฃจํด ์ฌ์ฉ ย |ย  Android ๊ฐ๋ฐ์ ย |ย  Android Developers](https://developer.android.com/topic/libraries/architecture/coroutines?hl=ko)

<br/>

> AAC ViewModel์ ์ฌ์ฉํ๋ค ํด์ MVVM ํจํด์ด ๋๋ ๊ฒ์ ์๋๋ค.  
> ๊ทธ๋ฌ๋ AAC ViewModel์ MVVM ํจํด์ผ๋ก ๊ตฌํํ  ์ ์๊ธฐ ๋๋ฌธ์(LiveData, Flow ๋ฑ ์ฌ์ฉ) AAC ViewModel๋ก MVVM ํจํด์ ๊ตฌํํ๋ฉด, ์๋ช ์ฃผ๊ธฐ๋ฅผ ๊ณ ๋ คํ MVVM ํจํด์ ๋ง๋ค ์ ์๊ฒ ๋๋ค.
> 

<br/>
<br/>

# ๐ ์ฐธ๊ณ 
- [[Android] ์๋๋ก์ด๋ AAC (velog.io)](https://velog.io/@hwi_chance/Android-%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-AAC)
- [์๋๋ก์ด๋ AAC(Android Architecture Components)๋? (velog.io)](https://velog.io/@heetaeheo/%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-AAC)
- [[Android] ์๋๋ก์ด๋ AAC & MVVM (tistory.com)](https://hanyeop.tistory.com/167)
- [[Android] AAC (Android Architecture Components) ๋ ? (Feat. ViewModel) (tistory.com)](https://heegs.tistory.com/m/119)
- [[Kotlin] ์๋๋ก์ด๋ AAC ViewModel๊ณผ ์ฑ ์ํคํ์ฒ ๊ฐ์ด๋ (feat. SharedPreferences) - ์ฌ๋ฌ Fragment์์ AAC ViewModel ๊ณต์ ํด์ ์ฌ์ฉํ๊ธฐ. โ For Better Code Tomorrow (tistory.com)](https://kimyunseok.tistory.com/152)
