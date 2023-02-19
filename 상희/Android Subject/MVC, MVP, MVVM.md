# 💡MVC, MVP, MVVM

# ✅ 디자인 패턴(Design Pattern)
디자인 패턴이란 기존 환경 내에서 반복적으로 일어나는 문제들을 어떻게 풀어나갈 것인가에 대한 일종의 솔루션이다.  
디자인 패턴은 개발자로 하여금 재사용하기 용이한 설계를 선택하고, 재사용하기 어려운 설계는 배제하도록 도와준다. 또한 개발자끼리 협업을 잘할 수 있도록 코드들의 패턴을 짬과 동시에 코드의 질, 효율성을 높이는 것이다.

<br/>
<br/>

# ✅ 아키텍처(Architecture)
![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/V6FSv/btrGQ06Snn3/bqStOAbmVGiuIk4LqEXvi0/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/V6FSv/btrGQ06Snn3/bqStOAbmVGiuIk4LqEXvi0/img.png)

<br/>

소프트웨어를 구성하는 구성 요소(모듈 / 컴포넌트 / 서브 시스템) 간의 관계를 관리하는 시스템의 구조이자 소프트웨어의 설계와 업그레이드를 통제하는 지침과 원칙이다.

<br/>

## 디자인 패턴과 아키텍처의 차이
소프트웨어 아키텍처는 프로그램 내에서 큰 구조로 구성되어 다른 구성 요소들을 관리하는 역할을 한다. 반면에 디자인 패턴은 특정 유형의 문제를 해결하는 방법으로 소프트웨어 아키텍처보다는 조금 더 좁은 개념에 포함된다. 이 둘은 유사성을 가지나 범위의 제한이 존재하는 것이다.

<br/>
<br/>

# ✅ 안드로이드 아키텍처 패턴
안드로이드 앱을 개발할 때, 이용할 수 있는 여러 아키텍처 패턴들이 존재한다.
  - MVC(Model - View - Controller)
  - MVP(Model - View - Presenter)
  - MVVM(Model - View - ViewModel)
  - MVI(Model - View - Intent)
  - 기타

<br/>

대표적으로 MVVM이 MVC, MVP를 의 단점을 보완하기 위해 가장 많이 쓰이는 방법론이라고는 하지만, 어느 게 더 낫다는 정답은 없다.

<br/>

위 아키텍처 패턴들을 살펴보면, 공통적으로 Model과 View가 존재한다. 
  - Model : 데이터 or 데이터를 생성하거나 업데이트
  - View : UI or 화면을 표시

이는 안드로이드 앱(프로그램의 Presentation Logic과 Businees Logic)을 개발함에 있어서 데이터와 UI는 필수적이기 때문이다. 따라서 자연스럽게 Model과 View 사이의 의존성 역시 생길 수밖에 없다.

> · Presentation Logic : 브라우저에 보이는 화면처럼 실제 눈에 보이는 GUI(Graphic User Interface) 화면을 구성하는 코드를 뜻한다.  
> · Businees Logic : 데이터를 보여주기 위해서 데이터베이스를 검색하는 코드 및 GUI(Graphic User Interface)화면에서 새롭게 발생된 데이터를 데이터베이스에 저장하는 코드 등 실제적인 작업을 하는 코드를 뜻한다.
> <br/>
> [출처] [Presentation Logic과 Busin.. : 네이버블로그 (naver.com)](https://blog.naver.com/blayan/220569833085)
> 

<br/>

Logic들이 커지고 복잡해짐에 따라 의존성은 더 강해지고, 결국 앱을 유지 보수하기가 점점 더 어려워지게 된다.  
이러한 문제들을 해결하기 위해 여러 패턴들이 나왔는데, 결국 M - V 사이의 관계를 어떻게 처리하느냐에 따라 패턴들을 구분 지을 수 있다.

<br/>
<br/>

# ✅ MVC(Model - View - Controller)
프로그램을 각각의 역할에 따라 Model, View, Controller로 나누어 설계한 아키텍처 패턴이다.

<br/>

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/ccvfx0/btrEcv1XMTU/t3OMVhzMmZae9KvQpjXae1/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/ccvfx0/btrEcv1XMTU/t3OMVhzMmZae9KvQpjXae1/img.png)

<br/>

### Model
- 애플리케이션에서 사용되는 실제 데이터 및 데이터 조작 로직을 처리하는 부분이다.
- View에 의존적이지 않다.

<br/>

### View
- 사용자에게 제공되어 보이는 UI 부분이다.
- 모바일이라면 앱의 화면이 View에 해당된다.

<br/>

### Controller
- 사용자의 입력을 받고 처리하는 부분이다.
- 안드로이드에서는 주로 Activity나 Fragment로 표현된다. Compose라면 Composable이 될 수도 있겠다.
- Model의 데이터 변화에 따라 View를 선택한다.

<br/>

## MVC 동작 순서
- 사용자의 Action들은 Controller에 들어온다. (모든 입력(Input)들은 Controller로 전달된다.)
- Controller는 사용자의 Action를 확인하고, Model을 업데이트한다.
- Controller는 Model을 나타내 줄 View를 선택한다.
    - 하나의 Controller는 View를 선택할 수 있기 때문에 1 : n 관계로, 여러 개의 View를 관리할 수 있다.
    - Controller는 View를 선택만 할 뿐, 직접 업데이트하지 않는다. (View는 Controller를 알지 못한다.)
- View는 Model을 이용하여 화면을 나타내게 된다.
    - View를 업데이트하기 위해서는 다음과 같은 방법이 있다.
        - View가 Model을 직접 이용하여 업데이트
        - Model에서 View에서 Notify하여 업데이트
        - View가 Polling하여 Model의 변화를 감지해서 업데이트
        
        > View를 업데이트하기 위해서는 결국 M - V 사이에 의존성이 존재하게 된다.  
        게다가 안드로이드는 Activity(or Fragment)가 Controller와 View 모두 처리하기 때문에, 한 클래스에서 M - V - C 모두 처리하게 되는 문제점이 발생한다.
        > 

<br/>

## MVC 패턴의 특징
- Controller는 여러 개의 View를 선택할 수 있는 1 : n 구조이다.
- Controller는 Model에 직접적인 영향을 끼칠 수 있다.

<br/>

## MVC 패턴의 장점
- 단순한 패턴이기 때문에 러닝 커브가 낮고 널리 사용된다.

<br/>

## MVC 패턴의 단점
- View와 Model 사이의 의존성이 존재한다.
    - 앱이 커지고 복잡해질수록 유지 보수가 어렵다.
- Controller가 안드로이드에 종속되기 때문에 테스트가 어려워진다.
- Controller에 많은 코드가 모이게 되어 Activity가 비대해진다.
- 안드로이드 특성 상 Activity가 View 표시와 Controller 역할을 같이 수행해야 하기 때문에 두 요소의 결합도가 높아진다.

<br/>
<br/>

# ✅ MVP(Model - View - Presenter)
Model과 View는 MVC와 동일하다. 다만 Controller 대신 Presenter가 존재한다.  
MVC에서 파생된, Model과 View 간의 의존성이 없는 아키텍처 패턴이다.

<br/>

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/q7nXu/btrD3yS2pNY/xdQRAbVqOBKJHAaQcp7wuK/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/q7nXu/btrD3yS2pNY/xdQRAbVqOBKJHAaQcp7wuK/img.png)

<br/>

### Model
- 애플리케이션에서 사용되는 실제 데이터 및 데이터 조작 로직을 처리하는 부분이다.
- View에 의존적이지 않다.

<br/>

### View
- 사용자에게 제공되어 보이는 UI 부분이다.
- 웹이라면 웹 페이지, 모바일이라면 앱의 화면이 View에 해당

<br/>

### Presenter
- View에서 요청한 정보를 Model로부터 가공하여 View로 전달하는 부분이다.
- View와 Model 사이를 이어주는 역할을 한다.

<br/>

## MVP 동작 순서
- 사용자의 Action들은 View를 통해 들어온다.
- View는 데이터를 Presenter에게 요청한다.
- Presenter는 Model에게 데이터를 요청한다.
- Model은 Presenter에서 요청받은 데이터를 응답한다.
- Presenter는 View에게 데이터를 응답한다.
- View는 Presenter가 응답한 데이터를 이용하여 화면을 나타낸다.

<br/>

## MVP 패턴의 특징
- Preseter와 View는 1:1 관계이다.
- View와 Model은 서로를 알 필요가 전혀 없다.

<br/>

## MVP 패턴의 장점
- View와 Model의 의존성이 없다. (Presentor를 통해서만 데이터를 전달받기 때문이다.)
- 따라서 MVC 패턴의 단점을 해결할 수 있다.

<br/>

## MVP 패턴의 단점
- View와 Presenter가 1:1로 강한 의존성을 가지게 된다.
- 각각의 View마다 Presenter가 존재하게 되어서 코드양이 많아져 유지 보수가 힘들어질 수 있다.

<br/>
<br/>

# ✅ MVVM(Model - View - ViewModel)
Model과 View는 MVC, MVP와 동일하다. 하지만 이번에는 Presenter 대신 ViewModel이 존재한다.

<br/>

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/I0Ia7/btrEaN93m03/QvgBPWN6BlfR7dcRQ9g2a0/img.jpg](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/I0Ia7/btrEaN93m03/QvgBPWN6BlfR7dcRQ9g2a0/img.jpg)

<br/>

### Model
- 애플리케이션에서 사용되는 실제 데이터 및 데이터 조작 로직을 처리하는 부분이다.
- View에 의존적이지 않다.

<br/>

### View
- 사용자에게 제공되어 보이는 UI 부분이다.
- 웹이라면 웹페이지, 모바일이라면 앱의 화면이 View에 해당된다.

<br/>

### ViewModel
- View에서 사용되는 데이터를 관리하는 View를 위한 Model이다.
- View에 종속되지 않는다.

<br/>

## MVVM 동작 순서
- View에 입력이 들어오면 Command 패턴으로 ViewModel에 명령 전달
- ViewModel은 필요한 데이터를 Model에 요청
- Model은 ViewModel에 필요한 데이터를 응답
- ViewModel은 응답받은 데이터를 가공해서 저장

<br/>

## MVVM 패턴의 장점
- View와 Model 사이의 의존성이 없다.
- View는 ViewModel을 알지만 ViewModel은 View를 알지 못하고 ViewModel은 Model을 알지만 Model은 ViewModel을 알지 못한다.
- 즉, 한 쪽 방향으로만 의존 관계가 있어서 각 모듈별로 분리하여 개발을 할 수 있다.
- 모듈화 개발에 적합한 만큼 테스트가 수월하다.

<br/>

## MVVM 패턴의 단점
- 장점이 많은 만큼 러닝 커브가 높다.

<br/>
<br/>

# 🗂 참고
- [안드로이드 [Kotlin] - 아키텍처 패턴 with MVC, MVP, MVVM (feat 코드 예제) (tistory.com)](https://jminie.tistory.com/168#1.%20%EB%94%94%EC%9E%90%EC%9D%B8%20%ED%8C%A8%ED%84%B4(Design%20Pattern)%20%EC%9D%B4%EB%9E%80?)
- [MVC, MVP, MVVM, MVI (brunch.co.kr)](https://brunch.co.kr/@oemilk/113)
- [MVC, MVP 그리고 MVVM 패턴에 대하여 — 오웬의 개발 이야기 (devowen.com)](https://devowen.com/457)
