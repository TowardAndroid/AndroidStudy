# RecyclerView

- RecyclerView를 사용하면 대량의 데이터 세트를 효율적으로 표시 가능
- 데이터에 따라 RecyclerView 라이브러리가 요소를 동적으로 생성
- RecyclerView는 개별 요소를 재활용 한다  ⇒ 앱의 응답성 개선, 성능 개선

### 레이아웃 정렬

LinearLayoutManager 1차원 목록으로 정렬

GridLayoutManager 2차원 그리드로 정렬 

StraggeredGridLayoutManager 

### 어댑터 및 뷰 홀더 구현

Adapter와 ViewHolder 클래스가 함께 작동하여 데이터 표시 방식을 정의한다.

ViewHolder는 목록에 있는 개별 항목의 레이아웃을 포함하는 View의 래퍼이다.

Adapter는 필요에 따라 ViewHolder객체를 만들고 데이터를 설정한다. 

뷰를 데이터에 연결하는 프로세스를 바인딩이라고 한다.

`[onCreateViewHolder()](https://developer.android.com/reference/androidx/recyclerview/widget/RecyclerView.Adapter?hl=ko#onCreateViewHolder(android.view.ViewGroup,%20int))` : ViewHolder를 새로 만들어야 할 떄 

`[onBindViewHolder()](https://developer.android.com/reference/androidx/recyclerview/widget/RecyclerView.Adapter?hl=ko#onBindViewHolder(VH,%20int))`:ViewHolder를 데이터와 연결할 떄 

```kotlin
class CustomAdapter(private val dataSet: Array<String>) :
        RecyclerView.Adapter<CustomAdapter.ViewHolder>() {

  
    class ViewHolder(view: View) : RecyclerView.ViewHolder(view) {
        val textView: TextView

        init {
          
            textView = view.findViewById(R.id.textView)
        }
    }

  
    override fun onCreateViewHolder(viewGroup: ViewGroup, viewType: Int): ViewHolder {
     
        val view = LayoutInflater.from(viewGroup.context)
                .inflate(R.layout.text_row_item, viewGroup, false)

        return ViewHolder(view)
    }

   
    override fun onBindViewHolder(viewHolder: ViewHolder, position: Int) {
        viewHolder.textView.text = dataSet[position]
    }

    
    override fun getItemCount() = dataSet.size

}

```

참조

[https://developer.android.com/guide/topics/ui/layout/recyclerview?hl=ko](https://developer.android.com/guide/topics/ui/layout/recyclerview?hl=ko)
