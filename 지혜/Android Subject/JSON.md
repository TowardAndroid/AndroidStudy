특징

- Json 포맷에서 []는 배열을 나타내며, {}는 객체를 나타낸다.
- 자료구조의 Map과 같은 구조이다.
- Json은 XML과 더불어 데이터 형식으로 가장 많이 사용되고 있으며, XML보다 간결하고 이해하기 쉽다.
- Json은 실제 데이터에 집중하므로 전송되는 데이터의 용량이 적다.
- 데이터를 분석해서 사용하기 편한 파싱도 비교적 쉽다.

실습

```kotlin
{
  "code": 200,
  "data": {
    "store_list": [
      {
        "store_name": "서울지점",
        "image_url": "//images.unsplash.com/photo-1546874177-9e664107314e?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1169&q=80"
      },
      {
        "store_name": "부산지점",
        "image_url": "//images.unsplash.com/photo-1625899139925-57f71ba783b4?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1634&q=80"
      },
      {
        "store_name": "전주지점",
        "image_url": "//images.unsplash.com/photo-1548115184-bc6544d06a58?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1170&q=80"
      }
    ]
  }
}
```

Assets Folder를 생성해서 json파일을 위치시켜준다.

activity : json파일을 열어서 adapter에 연결

```kotlin
val json = assets.open("test.json").reader().readText()
        val data = JSONObject(json).getJSONObject("data")

        adapter = CustomAdapter(data)
```

adapter

```kotlin
class CustomAdapter(private val datas: JSONObject) :
    RecyclerView.Adapter<CustomAdapter.CustomViewHolder>() {
    private val listStore = datas.getJSONArray("store_list")

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): CustomViewHolder {
        return CustomViewHolder(
            LayoutInflater.from(parent.context).inflate(R.layout.item_list, parent, false)
        )
    }

 ...

    class CustomViewHolder(view: View) : RecyclerView.ViewHolder(view) {
        val tvStoreNm: TextView = view.findViewById(R.id.store_name)
        val tvStoreImg: ImageView = view.findViewById(R.id.img_url)

        fun bind(listStore: JSONArray) {
            val iObj = listStore.getJSONObject("$position".toInt())
            val name = iObj.getString("store_name")
            var imgUrl = iObj.getString("image_url")
            
            tvStoreNm.text = name
            Glide.with(itemView)
                .load("http:"+ imgUrl)
                .circleCrop()
                .into(tvStoreImg)
        }
    }
}
```

# **GSON**

Gson은 구글에서 개발한 JSON 데이터와 자바 오브젝트를 상호 변환할 수 있는 라이브러리이다.

### 4.1. 특징

- 자바에서 JSON을 다루는 라이브러리는 그 외에도 Jackson, JSONIC 등 다양하다.
- Gson은 내부적으로 자바의 리플랙션이라는 기법을 사용하는데, 리플랙션은 실행시간 비용이 많이 드는 기법이므로 실행시간에 민감한 앱을 개발할 때는 적합하지 않다.

[https://steady-coding.tistory.com/609](https://steady-coding.tistory.com/609)

**Retrofit**

Retrofit 라이브러리는 내부적으로는 OKHttp를 사용하면서 Gson 라이브러리를 결합하여 모델 클래스나 List<모델> 형태의 결과를 얻을 수 있는 라이브러리

참조

[https://mimah.tistory.com/entry/AndroidKotlin-Kotlin을-사용하여-JSON-데이터-파싱](https://mimah.tistory.com/entry/AndroidKotlin-Kotlin%EC%9D%84-%EC%82%AC%EC%9A%A9%ED%95%98%EC%97%AC-JSON-%EB%8D%B0%EC%9D%B4%ED%84%B0-%ED%8C%8C%EC%8B%B1)

[https://github.com/taeiim/Android-Study/blob/master/study/week10/JSON_sieun.md](https://github.com/taeiim/Android-Study/blob/master/study/week10/JSON_sieun.md)
