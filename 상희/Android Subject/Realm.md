# 💡 Realm

# ✅ Realm이란?
## Android Realm Database
Realm(렘)은 오픈소스 데이터베이스 관리 시스템(DBMS)이며 모바일 환경을 주요 타깃으로 삼은 데이터베이스이다.  
Realm은 매우 작은 리소스를 사용하고 사용하기 쉽고 더 빠르게 데이터와 상호 작용 가능하다.  
NoSQL 데이터베이스를 지향하며 rawSQL을 사용할 수 없어 Realm API를 통해서 실행된다.

<br/>

## 안드로이드에서 데이터를 저장하는 방식
### SharedPreferences
- 적은 양의 원시 데이터를 (key, value) 형태로 앱 안에 XML 파일로 저장한다.

<br/>

### Room
- AAC(Android Architecture Component) 중 하나이다.
- SQLite 위에 있는 추상화 레이어를 제공해 SQLite의 기능을 사용하면서 데이터베이스 접근을 보다 편리하게 한다.
- 객체의 맵핑을 통해 DB에 접근하는 ORM 방식의 라이브러리이다.

<br/>

### Realm
- 쿼리 문을 통해 테이블 내 컬럼에 데이터를 저장하는 SQLite의 방식과 달리 데이터를 객체 형태로 저장한다.
- 크로스 플랫폼 데이터베이스로 Android, iOS 간 DB 공유가 가능하다.
- 타 데이터베이스들에 비해 데이터 처리 속도가 빠르다.

<br/>

### Realm을 사용하면 좋은 이유
- SharedPreference는 자동 로그인 여부와 같은 간단한 값을 저장할 때엔 적합하지만, 저장할 데이터의 양이 많고 간단하지 않은 경우에는 적합하지 않은 것 같다.
- iOS 개발자와 모델 객체를 같이 짜고 구성할 수 있어 협업에 좀 더 편리할 것 같다.
- 데이터 컨테이너 모델을 사용해 직접 객체를 데이터베이스에 저장하는 방식이기 때문에 저장, 불러오기와 같은 동작들도 좀 더 빠르게 처리할 수 있다.
- 빠르고 가벼움
    - Realm의 지연 로딩 및 제로 카피 아키텍처로 장치 리소스를 소모하지 않고 데이터가 풍부한 앱을 구축
- 간편한 시작 및 확장
    - 객체 지향 데이터 모델을 통해 개발자는 ORM 또는 DAO가 필요하지 않은 네이티브 객체로 직접 작업할 수 있다.
- 내장 모바일 · 클라우드 동기화
    - 실시간 모바일 · 클라우드 데이터 동기화를 사용하면 여러 장치, 사용자 및 백엔드에서 데이터를 최신 상태로 유지하는 대화형 기능을 쉽게 구축할 수 있다.

<br/>
<br/>

# ✅ Realm 사용 방법
## 초기 설정
### app 레벨의 build.gradle에 플러그인 추가

```groovy
plugins {
    id "realm-android" // 가장 하단에 위치시키기
}
```

<br/>

### project 레벨의 build.gradle에 의존성 추가

```groovy
dependencies {
    classpath 'io.realm:realm-gradle-plugin:10.8.0'
    // 최신 버전은 realm 릴리즈 노트 확인
}
```

<br/>

## Realm 초기화하기
realm 초기화는 앱을 실행하는 동안 한 번만 하면 되므로 Application class에서 해 주는 것이 좋다.

```kotlin
class OffoffApplication : MultiDexApplication() {

    override fun onCreate() {
        super.onCreate()

        // Realm 초기화
        Realm.init(this)
        val config : RealmConfiguration = RealmConfiguration.Builder()
            .allowWritesOnUiThread(true)
            .name("user.realm") // 생성할 realm db 이름
            .deleteRealmIfMigrationNeeded()
            .build()

        Realm.setDefaultConfiguration(config)
    }
}
```

<br/>

## 객체 클래스 모델 만들기

```kotlin
open class User  (
    @PrimaryKey
    var id: Int? = 0,
    var name: String? = null,
    var age: Int? = 0,
) : RealmObject()
```

<br/>

- 클래스는 open 키워드를 붙여주고 RealmObject를 상속받아야 한다.
- PK로 사용할 필드는 @PrimaryKey 어노테이션을 붙여 준다.

<br/>

## Realm 인스턴스 얻기
realm을 사용할 곳에서 realm 인스턴스를 가져와 사용할 수 있다.

```kotlin
val realm = Realm.getDefaultInstance()
```

<br/>

## 데이터 다루기(CRUD)
### Create, Update - 데이터 저장 또는 갱신하기

```kotlin
// 사용자 저장 또는 갱신하기
fun insert(user: User) {
    realm.executeTransactionAsync {
        it.insertOrUpdate(user)
    }
}
```

<br/>

### Read - 데이터 읽기

```kotlin
// 모든 사용자 읽어오기
fun getAllUser(): RealmResults<User> {
    return realm.where<User>()
        .findAll()
        .sort("id", Sort.ASCENDING)
}
        
// 특정 사용자 읽어오기
fun getUser(id: Int): User? = realm.where<User>()
    .equalTo("id", id)
    .findFirst()
```

<br/>

### Delete - 데이터 삭제하기

```kotlin
// 모든 사용자 삭제
fun deleteAllUser() {
    realm.executeTransaction {
        it.where<User>().findAll().deleteAllFromRealm()
    }
}

// 특정 사용자 삭제
fun deleteUser(id: Int) {
    realm.executeTransaction {
        it.where<User>().equalTo("id", id).findAll().deleteAllFromRealm()
    }
}
```

<br/>
<br/>

# 🗂 참고
- [Android Database - Realm | YunzaiDev](https://yunzai.dev/posts/Andorid_Database_Realm/)
- [[Android] Realm DB로 데이터 관리하기 (velog.io)](https://velog.io/@yuuuzzzin/realm)
- [렐름 홈 | Realm.io](https://realm.io/)
- Realm 사용 방법 최신 버전
    - [Realm Kotlin SDK — Realm (mongodb.com)](https://www.mongodb.com/docs/realm/sdk/kotlin/)
    - [Android Kotlin Realm Database: #1 - Create Realm Database | ViewModel LiveData 2023. - YouTube](https://www.youtube.com/watch?v=KX_JS1PV5_o&list=PLKqtGJUS11t9PBKqtxKnKMgzph9yGniRA)
    
