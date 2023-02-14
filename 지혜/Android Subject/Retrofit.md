# Retrofit

안드로이드와 서버간의 REST API통신을 도와주는 라이브러리

okhttp에 기반을 두고 현재 가장 많이 쓰이는 통신 라이브러리

### 장점

1. AsyncTask,Volley에 비해 빠른 성능
2. 가독성이 뛰어나다 

Annotation으로 HTTP메소드를 정의함으로써 직관적으로 코드 설계 가능

1. 유지보수가 쉽다

서버 연동 시 주고 받는 데이터인 JSON, XML을 자동으로 파싱해주는 cONVERTER연동을 지원하기 때문에 유지보수가 편리하다.

### Annotation

GET, PUT, POST, DELETE, Headers 

@Field @Body @Query @Path을 함께 보낼 수 있다.

### 실습

1. 의존성 부여

```
implementation 'com.squareup.retrofit2:retrofit:2.3.0'
implementation 'com.squareup.retrofit2:converter-gson:2.3.0'
implementation 'com.squareup.retrofit2:converter-scalars:2.5.0'
```

1. 모델 생성

```kotlin
data class advPostBody(val name:Int?,val title:String?,val content:String?,val category:Int?,val state:Int?,val party:String?)
```

1. 서비스 인터페이스 정의

```
package com.example.mafriend.Service

import com.example.mafriend.DataClass.*
import okhttp3.ResponseBody
import retrofit2.Call
import retrofit2.http.*

interface AdvService {
    companion object{
        public val API_URL = "http://10.0.2.2:8000/"
    }

    //게시판 등록
    @POST("adv/")
    fun post_adv(@Body request:advPostBody

    ):Call<boardGetBody>

    //댓글 등록
    @POST("adv/comment/")
    fun post_comment(@Body  request:commentPostBody

    ):Call<commentGetBody>

    //게시판 단건 조회
    @GET("adv/{advId}/")
    fun get_advById(@Path("advId") advId:Int):Call<boardGetBody>

   
    //게시판 목록 조회
    @GET("adv/")
    fun get_adv():Call<List<boardGetBody>>

}

```

1. Retorifit 객체 생성

```
fun getreview(categorys : Int) {
    //layoutmanager설정
    val layoutManager = LinearLayoutManager(requireActivity())
    recyclerview_review.layoutManager= layoutManager
    lateinit var adapter: AdvAdapter

    // 목록 가져오기
    val gson = GsonBuilder()
        .setDateFormat("yyyy-MM-dd'T'HH:mm:ss")
        .registerTypeAdapter(LocalDateTime::class.java, LocalDateTimeConverter()).create()

    var retrofit = Retrofit.Builder()
        .baseUrl(AdvService.API_URL)
        .addConverterFactory(GsonConverterFactory.create(gson)).build()
 
    var apiService = retrofit.create(AdvService::class.java)
    var tests = apiService.get_advByCt(categorys+1)
    tests.enqueue(object : Callback<categoryBody> {
        override fun onResponse(call: Call<categoryBody>, response: Response<categoryBody>) {
            if (response.isSuccessful) {
                var mList = response.body()!!
                Log.e("team",mList.toString())
                adapter = AdvAdapter(mList.post_list)
                recyclerview_review.adapter= adapter

               
            } }

        override fun onFailure(call: Call<categoryBody>, t: Throwable) {
            Log.e("team", "OnFailuer+${t.message}")
        } })
}

```

참조

[http://devflow.github.io/retrofit-kr/](http://devflow.github.io/retrofit-kr/)

[https://velog.io/@hoyaho/Retrofit2에-대해-알아보자](https://velog.io/@hoyaho/Retrofit2%EC%97%90-%EB%8C%80%ED%95%B4-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90)

[https://velog.io/@seokzoo/Retrofit-파헤치기](https://velog.io/@seokzoo/Retrofit-%ED%8C%8C%ED%97%A4%EC%B9%98%EA%B8%B0)
