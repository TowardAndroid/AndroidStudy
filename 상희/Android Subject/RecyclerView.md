# 💡 RecyclerView

# ✅ RecyclerView란?
> RecyclerView는 이미지나 텍스트를 리스트화 해서 스크롤하며 볼 수 있게 해 주는 컨테이너다.
> 

<br/>

- 기존에 사용하던 ListView와 비슷하지만, 정확히는 ListView의 확장판이라고 이야기할 수 있다. ListView의 확장판이니 당연히 대부분 RecyclerView로 대체된 상태다.
- 기존의 ListView는 커스텀하기에는 구조적인 문제로 많은 제약이 따랐으며, 구조적인 문제로 인해 성능 문제가 있었다. 그래서 이 문제들을 해결하기 위해 좀 더 다양한 형태로 개발자가 커스텀할 수 있도록 만들어진 것이 RecyclerView다.
- RecyclerView는 기존의 ListView보다 유연하고 성능이 향상된 고급 위젯으로, ListView보다 향상된 성능을 제공하며, Adpater의 ViewHolder를 이용하고, RecyclerView 내의 View를 재활용하여 사용한다.
- ViewHolder를 사용하는 이유?
    - 맨 처음 화면에 보이는 뷰 객체를 홀딩(기억)하고 있어야 하기 때문에 ViewHolder를 사용한다.
- 리스트를 표시하기 위한 AdapterView를 좀 더 개선한 컴포넌트다.
- 큰 틀은 유지한 채 데이터만 바뀐다.

<br/>

![https://velog.velcdn.com/images%2Fhoyaho%2Fpost%2F9bbc5c00-4d42-4732-b26c-7a839380cd85%2Fimage.png](https://velog.velcdn.com/images%2Fhoyaho%2Fpost%2F9bbc5c00-4d42-4732-b26c-7a839380cd85%2Fimage.png)

<br/>

ListView는 사용자가 스크롤할 때마다 위에 있던 뷰는 삭제되고, 맨 아래의 뷰는 생성되길 반복하여 cost가 매우 높아지게 된다.  
반면, RecyclerView에서는 아이템이 100000개를 넘어가더라도 화면에 보이는 정도의 View만 생성하고, 스크롤할 때마다 삭제하지 않고 가장 아래의 아이템 쪽으로 객체를 이동시켜 재사용하게 된다.

<br/>

## AdapterView와의 차이점
- RecyclerView는 레이아웃 매니저(LayoutManager)를 지정해 줘야 한다.
- AdapterView에서는 선택 사항이었던 ViewHolder 패턴이 RecyclerView에서는 꼭 구현해야 한다.
- AdapterView는 미리 제공된 어댑터가 있는 반면 RecyclerView의 어댑터는 아무것도 제공해 주지 않는다.

<br/>

## 장점
- ViewHolder 패턴을 적용하여 뷰를 재활용
- Swipe를 이용하여 직관적인 Refresh UI구조 설계 가능
- position에 따라서 한 리스트 내에서 다양한 뷰를 표현 가능(MultiView)

<br/>

## 단점
- 이벤트 리스너와 커서(Cursor)를 지원하지 않는다.

<br/>
<br/>

# ✅ RecyclerView 주요 클래스
### RecyclerView.Adapter
: AdapterView의 어댑터와 같은 역할

<br/>

### RecyclerView.ViewHolder
: ViewHolder 클래스는 이것을 상속해야 한다.

<br/>

### LayoutManager
: 데이터를 배치하고, 뷰의 재사용 등을 결정하는 역할을 하여 기존의 AdapterView보다 성능이 개선된다.

<br/>

### LinearLayoutManager
: 데이터를 ListView처럼 세로나 가로 한 줄로 표시

<br/>

### GridLayoutManager
: GridView처럼 데이터를 그리드 형식으로 표시

<br/>

### StaggeredGridLayoutManager
: GridView처럼 데이터를 격자 형식으로 표시하면서 아이템의 높이가 일정하지 않아도 되는 지그재그형 그리드 형식으로 표시

<br/>

![https://raw.githubusercontent.com/taeiim/Android-Study/master/study/week04/RecyclerView/%EA%B7%B8%EB%A6%BC01.png](https://raw.githubusercontent.com/taeiim/Android-Study/master/study/week04/RecyclerView/%EA%B7%B8%EB%A6%BC01.png)

<br/>

### RecyclerView.ItemAnimation
: 아이템이 추가, 삭제 또는 재정렬될 때 애니메이션 정의

<br/>

### RecyclerView.ItemDecoration
: 아이템을 세부적으로 꾸민다.

<br/>
<br/>

# 🗂 참고
- [RecyclerView에 대해 알아보자! ｜ Android Study (velog.io)](https://velog.io/@hoyaho/RecyclerView)
- [Android-Study/Recyclerview_sieun.md at master · taeiim/Android-Study (github.com)](https://github.com/taeiim/Android-Study/blob/master/study/week04/RecyclerView/Recyclerview_sieun.md)
