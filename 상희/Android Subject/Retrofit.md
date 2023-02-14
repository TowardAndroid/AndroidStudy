# 💡 Retrofit

# ✅ Retrofit이란?
- Retrofit은 HTTP API를 자바 인터페이스 형태로 사용할 수 있다.
- HTTP 요청은 어노테이션을 사용하여 명시한다.
    - URL 파라미터 치환과 쿼리 파라미터가 지원된다.
    - 객체를 요청 body로 변환한다. (예: JSON, protocol buffers)
    - 멀티파트 요청 body와 파일 업로드가 가능하다.

<br/>

## Retrofit 장점
기본적으로 서버와 통신을 하려면 HTTP 통신을 해야 했다. 기본적으로 HttpUrlConnection을 이용하면 매번 connection 설정 등 반복적인 작업이 발생하게 된다. 이때 이것을 도와주는 라이브러리가 OkHttp이다. 하지만 OkHttp는 사용 시 대개 Asynctask를 통해 비동기로 실행하게 되는데 성능상 느리다는 이슈가 발생했다.

<br/>

반면에 Retrofit은 Asynctask를 사용하지 않고 자체적인 비동기 실행과 스레드 관리를 통해 속도가 많이 개선되었다.  
또한 Retrofit에서는 Request, Response 설정 등 반복적인 작업을 라이브러리에서 넘겨서 처리하므로 작업량이 줄어들고 사용하기 굉장히 편리하다.

<br/>

그래서 Retrofit의 장점을 요약하자면, **속도**, **편의성**, **가독성**이라고 할 수 있다.

<br/>
<br/>

# ✅ API 정의
인터페이스의 어노테이션과 메소드 매개변수들은 요청을 어떻게 다룰지 지시한다.

<br/>

## 요청 메소드
모든 메소드들은 반드시 상대 URL과 요청 메소드를 명시하는 어노테이션을 가지고 있어야 한다.  
기본으로 제공하는 요청 메소드 어노테이션은 다음과 같이 5개가 있다. : `GET`, `POST`, `PUT`, `DELETE`, `HEAD`.

```java
@GET("/users/list")
```

<br/>

정적 쿼리 인자를 URL에 명시할 수도 있다.

```java
@GET("/users/list?sort=desc")
```

<br/>

## URL 다루기
요청 URL은 동적으로 부분 치환 가능하며, 이는 메소드 매개변수로 변경이 가능하다.  
부분 치환은 영문/숫자로 이루어진 문자열을 { 와 } 로 감싸 정의해 준다. 반드시 이에 대응하는 `@Path`를 메소드 매개변수에 명시해 줘야 한다.

```java
@GET("/group/{id}/users")
Call<List<User>> groupList(@Path("id") int groupId);
```

<br/>

쿼리 매개변수도 명시 가능하다.

```java
@GET("/group/{id}/users")
Call<List<User>> groupList(@Path("id") int groupId, @Query("sort") String sort);
```

<br/>

보다 동적이며 다양한 쿼리 매개변수들은 `Map`으로도 사용할 수 있다.

```java
@GET("/group/{id}/users")
Call<List<User>> groupList(@Path("id") int groupId, @QueryMap Map<String, String> options);
```

<br/>

## 요청 본문
HTTP 요청 본문에 객체를 `@Body`  어노테이션을 통해 명시가 가능하다.

```java
@POST("/users/new")
Call<User> createUser(@Body User user);
```

이러한 객체들은 Retrofit 인스턴스에 추가된 컨버터에 따라 변환된다. 만약 해당 타입에 맞는 컨버터가 추가되어있지 않다면, `RequestBody`만 사용할 수 있다.

<br/>

### FORM-ENCODED과 MULTIPART
메소드는 form-encoded 데이터와 multipart 데이터 방식으로 정의 가능하다.  
`@FormUrlEncoded`  어노테이션을 메소드에 명시하면 form-encoded 데이터로 전송된다. 각 key-value pair의 key는 어노테이션 값에, value는 객체를 지시하는 `@Field`  어노테이션으로 매개변수에 명시하면 된다.

```java
@FormUrlEncoded
@POST("/user/edit")
Call<User> updateUser(@Field("first_name") String first, @Field("last_name") String last);
```

<br/>

Multipart 요청은 `@Multipart`  어노테이션을 메소드에 명시하면 된다. 각 파트들은 `@Part`  어노테이션으로 명시한다.

```java
@Multipart
@PUT("/user/photo")
Call<User> updateUser(@Part("photo") RequestBody photo, @Part("description") RequestBody description);

```

<br/>

Multipart의 part는 `Retrofit` 의 컨버터나, `RequestBody`를 통하여 직렬화(serialization) 가능한 객체를 사용할 수 있다.

<br/>

## 헤더 다루기
### 정적 헤더
정적 헤더들은 `@Headers`  어노테이션을 통해 명시할 수 있다.

```java
@Headers("Cache-Control: max-age=640000")
@GET("/widget/list")
Call<List<Widget>> widgetList();
```

<br/>

```java
@Headers({
    "Accept: application/vnd.github.v3.full+json",
    "User-Agent: Retrofit-Sample-App"
})
@GET("/users/{username}")
Call<User> getUser(@Path("username") String username);
```

<br/>

참고할 점은, 헤더들은 이름에 기준하여 각각의 값을 덮어 씌우지 않는다. 동일한 이름의 헤더를 추가한다면 모든 헤더들은 동일한 이름으로 모두 요청에 추가된다.

<br/>

### 동적 헤더
동적인 헤더는 `@Header`  어노테이션을 통해 명시 가능하다. 반드시 이에 대응하는 `@Header`  어노테이션을 매개변수에 명시해야 한다. 만약 값이 null이라면 해당 헤더는 추가되지 않는다. 아니라면, 매개변수 객체의 `toString`  메소드를 호출하여 반환된 값을 헤더의 값으로 추가한다.

```java
@GET("/user")
Call<User> getUser(@Header("Authorization") String authorization)

```

<br/>

헤더를 모든 요청마다 추가해야 한다면 [OkHttp interceptor](https://github.com/square/okhttp/wiki/Interceptors)를 사용하면 된다.

## 동기 VS. 비동기
`Call`  인스턴스는 동기 혹은 비동기로 요청 실행이 가능하다. 각 인스턴스들은 동기 혹은 비동기 중 한 가지 방식만 사용 가능하다. 하지만 `clone()`  메소드를 통해 새 인스턴스를 생성하면 이전과 다른 방식을 사용할 수 있다.  
안드로이드에서의 콜백들은 메인 스레드에서 실행된다. JVM에서는 HTTP 요청을 호출한 스레드와 동일한 스레드에서 콜백들이 실행된다.

<br/>

자주 사용 될 법한 **비동기식 방식의 통신**은 위에서 이미 사용해 본 `enqueue()`  method를 이용하는 것이다.  
반대로 **동기식 방식의 통신**을 하려면, 생성된 클라이언트 객체가 제공하고 있는 `execute()`  method를 `enqueue()`  method 대신 이용하면 된다.

<br/>
<br/>

# ✅ Retrofit 설정
Retrofit은 API 인터페이스를 호출 가능한 객체로 바꿔 준다. 기본적으로 Retrofit은 실행 중인 플랫폼에 최적화된 설정을 제공하지만, 사용자 정의도 가능하다.

<br/>

## 컨버터
기본적으로 Retrofit은 HTTP 요청 본문을 OkHttp의 `ResponseBody`  형식과 `@Body`에 이용하는 `RequestBody`  타입만 역직렬화(deserialization) 할 수 있다.

<br/>

컨버터들은 이외의 형식들을 변환해주는 역할을 한다. 아래에 많이 사용하고 편리한 자사의 컨버터 6개의 라이브러리들을 사용할 수 있다.
- [Gson](https://github.com/google/gson) : `com.squareup.retrofit:converter-gson`
- [Jackson](http://wiki.fasterxml.com/JacksonHome) : `com.squareup.retrofit:converter-jackson`
- [Moshi](https://github.com/square/moshi/) : `com.squareup.retrofit:converter-moshi`
- [Protobuf](https://developers.google.com/protocol-buffers/) : `com.squareup.retrofit:converter-protobuf`
- [Wire](https://github.com/square/wire) : `com.squareup.retrofit:converter-wire`
- [Simple XML](http://simple.sourceforge.net/) : `com.squareup.retrofit:converter-simplexml`

<br/>

### 예시
Gson을 사용하는 GitHubService 인터페이스가 Gson을 역직렬화가 가능하게 GsonConverterFactory 클래스를 통해 컨버터를 추가하는 예제이다.

```java
Retrofit retrofit = new Retrofit.Builder()
    .baseUrl("[https://api.github.com](https://api.github.com/)")
    .addConverterFactory(GsonConverterFactory.create())
    .build();
GitHubService service = retrofit.create(GitHubService.class);
```

addConverterFactory()는 통신이 완료된 후, 어떤 Converter를 이용하여 데이터를 파싱할 것인지에 대한 설정이다.

<br/>

**주의할 점**

공식 문서상에는 `baseURL()`에 설정된 서버 URL에 `/`가 없다.  
하지만 실질적으로 여러가지 통신을 하면서 로깅을 해보면 `baseURL()`에 `/`가 없을 경우, 요청되어야 할 URL의 일부가 잘려나가는 현상이 발생하여 잘못된 경로로 요청하는 현상이 발생할 수 있다.  
그러니 꼭 `baseURL()`에 설정되는 URL의 마지막 경로에는 `/`를 함께 포함해 주도록 해야 한다.

<br/>

## 사용자 정의 컨버터
만약 API와 통신하는데 Retrofit이 지원하지 않는 형식(e.g. YAML, txt, custom format)이거나 현재 사용 가능한 형식이지만 다른 라이브러리를 통해 구현하길 원한다면, 쉽게 나만의 컨버터를 만들 수 있다.  
`Converter.Factory`  클래스를 상속하여 만들고, 이를 Retrofit 객체를 만들 때 추가하면 된다.

<br/>
<br/>

# 🗂 참고
- 공식 문서 : [Retrofit - 한글 문서 (devflow.github.io)](http://devflow.github.io/retrofit-kr/)
- [[Android] Retrofit - API 통신을 쉽게 구현해보자 (tistory.com)](https://ardor-dev.tistory.com/59)
- [Android-Study/retrofit.md at master · taeiim/Android-Study (github.com)](https://github.com/taeiim/Android-Study/blob/master/study/week05/retrofit.md)
