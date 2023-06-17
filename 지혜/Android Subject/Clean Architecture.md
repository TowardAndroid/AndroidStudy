Uncle Bob인 [로버트 C. 마틴의 Clean Architecture](http://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html)에서 시작. 소스 코드만 보고 소프트웨어가 수행하는 작업이 무엇인지 식별할 수 있어야 하는 소프트웨어 개발 방법론

**계층(Layer)별로 역할(관심사)를 나누어 분리**함으로써 **다양한 요구**(대규모 업데이트, 새로운 기능, 버그수정, 테스트, 고객의 요청)등에 **유연하게 대처**하기 위해 사용

## **의존성 규칙(Dependency Rule)**

- 계층마다 경계를 나누어서
    
    관심사를 분리하기 위해 사용하는 규칙
    

1)**모든 소스코드 의존성은 반드시 바깥쪽에서 안쪽으로, 고수준 정책을 향해야 한다**

- 안쪽으로 갈수록 고수준에 해당하고,
    
    고수준과 저수준은 추상화의 정도에 따라 분류됩니다.
    
- 추상화가 많이 되어있을수록 안쪽에 위치해있고 고수준에 해당합니다.

2)고수준에 있는 계층은 저수준에 있는 계층에 대해 몰라야 한다.

- 안쪽에 있는
    
    Domain 계층은 DataLayer나 PresentationLayer에 의존하지 않고 독립적으로
    

실행되어야 한다는 규칙

## **Clean Architecture 장점**

- 코드는 표준 MVVM 보다 테스트하기 쉽다.
- 완벽하게 선별된 분리
- 사용자 친화적인 패키지 구조
- 프로젝트를 계속 실행하기 쉽다.
- 새로운 기능을 추가하기 용이하다.

## **Clean Architecture 단점**

- 러닝 커브가 가파르다.
- 많은 추가 클래스가 포함되므로 정교함이 낮은 소프트웨어에는 적합하지 않다.

## Layer

클린 아키텍처를 안드로이드에 접목시킬 때는 일반적으로 Presentation, Domain, Data 총 3개의 계층으로 나눠지게 됩니다. Presentation -> Domain, Data -> Domain 방향으로 의존성을 갖고 있습니다. 각각의 계층에 대한 설명은 다음과 같습니다.

### **1. Presentation**

화면과 입력에 대한 처리 등 UI와 관련된 부분을 담당합니다. Activity, Fragment, View, Presenter 및 ViewModel을 포함합니다. Presentation 계층은 Domain 계층에 대한 의존성을 가지고 있습니다.

### **2. Domain**

애플리케이션의 비즈니스 로직에서 필요한 UseCase와 Model을 포함하고 있습니다. UseCase는 각 개별 기능 또는 비즈니스 논리 단위이며, Presentation, Data 계층에 대한 의존성을 가지지 않고 독립적으로 분리되어 있습니다. 안드로이드의 의존성을 갖지 않고 java 및 kotlin 코드로만 구성하며 다른 애플리케이션에서도 사용할 수 있습니다. Repository 인터페이스도 포함되어 있습니다.

### **3. Data**

Domain 계층에 의존성을 가지고 있습니다. Domain 계층의 Repository 구현체를 포함하고 있으며, 데이터베이스, 서버와의 통신도 Data 계층에서 이루어집니다. 또한 mapper 클래스를 통해 Data 계층의 모델을 Domain 계층의 모델로 변환해주는 역할도 하게 됩니다.

## 1)Domain 계층(Layer)

- 사업의 핵심적인 서비스와 관련된 잘 변하지 않는들이 있음.
    
    비즈니스 로직
    

ex) 배달의민족 → 배달서비스(핵심서비스) 토스 → 금융 서비스(핵심서비스)

- 순수한 영역(어떠한 계층에도 의존성을 갖지않음)으로
    
    다른 외부 계층의 로직이 변경되어도 Domain에 있는 로직은 변경되지 않음
    
- Data, Presentation 계층이 하는일을 Domain 계층은 알지 못합니다.

### 1-1)Entity

- 가장 핵심적인 한 것이며 따라서 .
    
    고수준의 비즈니스 로직을 캡슐화
    
    외부계층(Data, Presentation)의 변경사항이 생겨도 바뀌지 않음
    
- UseCase에 필요한 데이터
- 아래 그림은 비즈니스  한 예시이다.
    
    로직을 캡슐화
    
### 1-2)UseCase

- Entity를 사용해서 서비스의 .
    
    핵심적인 비즈니스 로직을 수행하기 위한 하나의 작은 단위
    

ex)로그인하기, 게시물작성, 사진업로드

- 다른 계층(Data, Presentation)에 영향을 받지 않는다.
- UseCase안에는 어떠한 Repository(인터페이스)를 사용(주로 DI로 주입)하느냐에 따라 수행하는 비즈니스 로직이

달라진다.

- UseCase에
    
    Repository를 주입시 반드시 interface를 주입받아야 한다
    

- GetGithubReposUseCase안에 Repository(interface)객체가 DI로 주입받는 것을 확인할 수 있다.

### 1-3)Repository(interface)

- UseCase에 주입되는 인터페이스
- Data계층에 Repository 인터페이스의 구현체로 구현함으로써 Data계층의 로직이 수정되어도

Domain계층의 로직은 수정되지 않게 하기 위해 사용합니다.


## Domain 계층이 Repository 인터페이스를 사용하는 이유

- Domain 계층은 단순하게 Data 계층에게 인터페이스만 제공하고 Data계층은 Domain계층의 인터페이스를 구현함으로써 Domain 계층은 Data나 Presentation 계층에 의존성을 갖지 않게 로직을 구성할 수 있음.

## UseCase에 Repository 인터페이스를 주입(DI)받는 이유

- Data나 Presentation 계층의 로직이 수정되어도 입니다.
    
    핵심적인 고수준의 로직이 있는 Domain 계층의 수정을 피하기 위해서
    

ex) 만약 UseCase안에 Repository 인터페이스를 제공하는 것이 아닌 Data 계층의 가상의 클래스를 주입받아 바로 사용해버리면 이는 Domain계층안에 있는 UseCase가 Data계층에 영향을 받아 버립니다. 즉 Data 계층의 수정이 Domain 계층에 영향을 끼쳐버리므로 의존성을 갖게됩니다.

## 2)Data 계층

- Domain 계층의 함으로써 (DB, 서버)와 상호작용을 수행하는 영역
    
    Repository 인터페이스를 구현
    
- Domain 계층에 의존성을 가지며 Repository 패턴을 사용하기 때문에 Presentation 계층과는

의존성이 적다.

### 2-1)Repository(Implementaion)

- Domain 계층에 있는 Repository 인터페이스를 구현함으로써 Presentation계층과 상호작용을 할 수 있게 합니다.
- Presentation계층이 Domain계층에 있는 Repository 인터페이스의 추상메서드를 호출하면 합니다.
    
    실질적으로는 Data 계층에 있는 Repository 인터페이스 구현체의 로직을 수행
    

### 2-2)DataSource

- Data 계층의 되며 인터페이스이다.
    
    Repository 인터페이스 구현체안에서 실행
    
- DataSource의 변경이 Data 계층에 있는 Repository구현체에 영향을 주지 않기 위해서 사용합니다.

RemoteDataSource(외부 API 통신)와 LocalDataSource(내부 room이나 Realm과 통신)을 구분하는 등의 로직이 있다.


### 2-3)Model

- Data 계층에서 DB 통신에 필요한 데이터

ex) DB 통신(Retrofit, Room등등)에 필요한 데이터


### 2-4)Mapper

- Data 계층의 Model을 통해 가져온 데이터를 Entity에 맞게 바꿔주는 역할을 합니다.

ex) DB로 부터 받아온 데이터 Model을 Mapper클래스를 통해 Domain 계층에 Entity로 변환시킴으로써 UseCase를 수행하는데 사용

ex2) Domain계층의 Entity를 DB통신을 하기위해서 Mapper를 통해 Data계층의 Model로 변환시킨다.


- 위의 그림을 보시면 mapperGithub() 메서드의 반환값으로 Domain계층의 Entity를 가진 리스트를 반환하는 것을 확인할 수 있습니다.


- 위의 그림을 보시면 반환값에 사용하는 데이터가 GithubRepoEntity이고 이 Entity는 Mapper를 통해서 Data계층의 Model을 Domain 계층의 Entity로 변환시킨 것입니다.

## 3)Presentation 계층

- 모든 UI와 관련된 컴포넌트 또는 안드로이드 프레임워크와 관련된 코드들이 이 계층에서

다뤄지며 다양한 요구에 의해 수정이 빈번하게 일어나는 계층입니다.

- Domain 레이어에 의존성을 가집니다.

### 3-1)Activity & Fragment

### 3-2)ViewModel

- MVVM 패턴을 사용하는 경우 ViewModel에서 비즈니스 로직이 수행되기 떄문에 합니다.
    
    Domain 계층의 UseCase를 사용해서 비즈니스 로직을 수행
    


- UseCase안에서는 Domain 계층의 Repository 인터페이스의 추상메서드를 통해서 Data 계층의 접근해서 필요한 작업을 수행하는 것을 확인할 수 있습니다.
