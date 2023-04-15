realm은 자바 객체를 해석해 그 객체의 데이터를 그대로 데이터베이스에 저장,획득

사용이유

기존 데이터베이스보다 속도가 빠르다

orm제공

크로스 플랫폼 데이터베이스로 Android, iOS 간 DB 공유가 가능

오픈소스라서 사용하기 쉬움

코드가 간단하다

사용

build.gradle (App)

```java
plugins {
    id "realm-android" // 가장 하단에 위치시키기
}
```

build.gradle(project)

```java
dependencies {
        classpath 'io.realm:realm-gradle-plugin:10.8.0'
        // 최신 버전은 realm 릴리즈 노트 확인
    }
```

realm 초기화

```java
Realm.init(this)
        val config : RealmConfiguration = RealmConfiguration.Builder()
            .allowWritesOnUiThread(true)
            .name("user.realm") // 생성할 realm db 이름
            .deleteRealmIfMigrationNeeded()
            .build()

        Realm.setDefaultConfiguration(config)
```

[https://velog.io/@yuuuzzzin/realm](https://velog.io/@yuuuzzzin/realm)

[https://develop-writing.tistory.com/56](https://develop-writing.tistory.com/56)
