# 💡 Image Caching

# ✅ Image Caching
## 캐싱이란?
컴퓨팅에서 캐시는 일반적으로 일시적인 특징이 있는 데이터 하위 집합을 저장하는 고속 데이터 스토리지 계층이다. 따라서 이후에 해당 데이터에 대한 요청이 있을 경우 데이터의 기본 스토리지 위치에 액세스할 때보다 더 빠르게 요청을 처리할 수 있다. 캐싱을 사용하면 이전에 검색하거나 계산한 데이터를 효율적으로 재사용할 수 있다.

<br/>

## 캐싱은 어떻게 작동하는가?
캐시의 데이터는 일반적으로 RAM(Random Access Memory)과 같이 빠르게 액세스할 수 있는 하드웨어에 저장되며, 소프트웨어 구성 요소와 함께 사용될 수도 있다. 캐시의 주요 목적은 더 느린 기본 스토리지 계층에 액세스해야 하는 필요를 줄임으로써 데이터 검색 성능을 높이는 것이다.  
속도를 위해 용량을 절충하는 캐시는 일반적으로 데이터의 하위 집합을 일시적으로 저장한다. 보통 완전하고 영구적인 데이터가 있는 데이터베이스와는 대조적이다.

<br/>

## 이미지 캐싱
캐시의 정의를 이미지와 접목해 본다면 매번 서버에서 이미지를 받아오기에는 시간이 오래 걸리니 임시적인 장소에 저장해 놨다가, 필요할 때 꺼내서 쓰겠다, 라는 개념이 될 것이다.  
즉, 로컬 스토리지에 저장해 놨다가 필요할 때 불러온다면 서버와 통신하는 비용을 줄일 수 있을 것이다.

<br/>
<br/>

# ✅ Android Image Caching
특정 URL 이미지를 목록에서 보여주어야 할 때, 동일 URL 이미지를 매번 다운로드 받아 출력하면 비효율적일 뿐만 아니라 사용자에게 보여지는 응답도 느려지게 된다. 사용자에게 응답을 빠르게 보여주기 위해서는 URL 이미지를 메모리나 로컬 파일에 캐싱하도록 구현해야 한다. 이미지를 캐싱함으로써, 동일 URL 이미지를 보여주어야 할 때 다운로드 없이 빠르게 이미지를 사용자에게 보여줄 수 있게 된다.

<br/>

단일 비트맵을 사용자 인터페이스(UI)에 로드하는 것은 간단하지만 한 번에 더 큰 이미지 집합을 로드해야 하면 더 복잡해진다. 많은 경우(ListView, GridView 또는 ViewPager와 같은 구성 요소를 사용하는 경우) 화면에 곧 스크롤될 수 있는 이미지 수가 합산된 화면 내 총 이미지 수는 기본적으로 제한되지 않는다.  
이미지가 화면에서 사라질 때 하위 뷰를 재활용함으로써 이런 구성 요소를 사용하여 메모리 사용량을 줄인다. 또한 가비지 컬렉터는 개발자가 오랫동안 활성화된 참조는 유지하지 않는 것으로 간주하며 로드된 비트맵을 해제한다.  
이러한 것들은 모두 훌륭하지만, UI를 끊김 없이 빠르게 로드하도록 유지하려면 이미지가 스크린으로 다시 표시될 때마다 매번 계속 처리하는 것을 피해야 한다. 메모리와 디스크 캐시를 사용하면 구성 요소가 처리된 이미지를 빨리 다시 로드하여 이 부분에 종종 도움을 줄 수 있다.

<br/>

### 비트맵 캐시
이미지를 비트맵으로 바꾸어 메모리에 저장하는 것이다.

<br/>

### 메모리 캐시
메모리 캐시는 원본의 압축된 형식으로 저장된다. 이미지는 화면에 표시되기 전에 이 캐시에서 디코드되어 가져온다.  
이 캐시는 앱이 백그라운드로 가면 지워진다.

<br/>

### 디스크 캐시
디스크 캐시는 데이터가 지속적으로 남아있고 용량도 메모리 캐시보다 더 많이 쓸 수 있다. 하지만 메모리 캐시보다 느리다.  
이 캐시는 앱이 백그라운드 상태거나, 종료, 장치가 꺼져 있을 때 없어지지 않는다. 사용자는 안드로이드 설정 메뉴에서 디스크 캐시를 없앨 수 있다.

<br/>

## 메모리 캐시 사용
메모리 캐시는 중요한 애플리케이션 메모리를 사용하는 대신 비트맵에 빠르게 액세스할 수 있다.  [`LruCache`](https://developer.android.com/reference/android/util/LruCache?hl=ko) 클래스(API 수준 4를 다시 사용하려고 할 때도 [지원 라이브러리](https://developer.android.com/reference/androidx/collection/LruCache?hl=ko)에서 사용 가능함)는 비트맵을 캐싱하는 작업과 최근에 참조된 객체를 강한 참조 [`LinkedHashMap`](https://developer.android.com/reference/java/util/LinkedHashMap?hl=ko)에 유지하는 작업, 캐시가 지정된 크기를 초과하기 전에 가장 오래전에 사용된 항목을 제거하는 작업에 특히 적합하다.

<br/>

> 이전에는 SoftReference 또는 WeakReference 비트맵 캐시가 메모리 캐시 구현으로 많이 사용되었지만, 지금은 권장되지 않는다.
> 

<br/>

LruCache에 적합한 크기를 선택하려면 다음과 같은 몇 가지 요인을 고려해야 한다.  
- 활동 및 애플리케이션의 나머지 부분이 얼마나 많은 메모리를 사용하나요?
- 한 번에 몇 개의 이미지가 화면에 표시되나요? 화면에 표시할 준비가 되어야 할 이미지 수는 몇 개인가요?
- 기기의 화면 크기와 밀도는 어떻게 되나요? Galaxy Nexus와 같은 초고밀도 화면(xhdpi) 기기는 메모리에 동일한 수의 이미지를 저장하려면 Nexus S(hdpi)와 같은 기기와 비교해 볼 때 더 큰 캐시가 필요합니다.
- 비트맵의 크기와 구성은 어떻게 되며 그에 따른 각각의 메모리 사용량은 어떻게 되나요?
이미지는 얼마나 자주 액세스되나요? 다른 이미지보다 더 자주 액세스되는 이미지가 있나요? 그런 경우 특정 항목을 항상 메모리에 두거나 서로 다른 그룹의 비트맵에 여러 개의 `LruCache`  객체를 두고 싶을 수 있습니다.
- 품질과 수량의 균형을 맞출 수 있나요? 때로 더 낮은 품질의 비트맵을 다수 저장하여 잠재적으로 다른 백그라운드 작업에 더 높은 품질 버전을 로드할 수 있도록 하는 것이 더 유용할 수 있습니다.

<br/>

모든 애플리케이션에 적합한 특정 크기나 수식은 없으며 사용량을 분석하여 적합한 해결책을 찾아야 한다. 캐시가 너무 작으면 아무런 이점 없이 추가 오버헤드가 발생하고 캐시가 너무 크면 또다시 `java.lang.OutOfMemory`  예외가 발생하여 앱의 나머지 부분에 사용할 메모리가 거의 남아 있지 않을 수 있다.

<br/>

## 디스크 캐시 사용
메모리 캐시를 통해 최근에 본 비트맵에 더욱 빨리 액세스할 수 있지만, 이 캐시에서 제공되는 이미지는 사용할 수 없다. 데이터 세트 크기가 큰 GridView 같은 구성 요소는 메모리 캐시를 쉽게 채울 수 있다. 애플리케이션은 전화 통화와 같은 다른 작업에 의해 중단될 수 있으며 백그라운드에서 애플리케이션이 종료되고 메모리 캐시가 삭제될 수 있다. 사용자가 계속하면 애플리케이션에서 각 이미지를 다시 처리해야 한다.  
이러한 경우 디스크 캐시를 사용하여 처리된 비트맵을 유지하고 메모리 캐시에서 이미지가 더 이상 사용 가능하지 않을 때 로드 시간을 줄일 수 있다. 물론, 디스크에서 이미지를 가져오는 것은 메모리에서 로드하는 것보다 느리며 디스크 읽기 시간을 예측할 수 없기 때문에 백그라운드 스레드에서 실행되어야 한다.

<br/>

> 이미지가 이미지 갤러리 애플리케이션 같은 곳에서 자주 액세스된다면 캐시된 이미지를 저장하기에 ContentProvider가 더 적합한 장소가 될 수 있습니다.
> 

<br/>

`DiskLruCache`  구현을 사용하여 예시 코드를 작성할 수 있다.  
다음은 기존 메모리 캐시 외에 디스크 캐시를 추가하는 업데이트된 코드의 예이다.

```kotlin
private const val DISK_CACHE_SIZE = 1024 * 1024 * 10 // 10MB
private const val DISK_CACHE_SUBDIR = "thumbnails"
...
private var diskLruCache: DiskLruCache? = null
private val diskCacheLock = ReentrantLock()
private val diskCacheLockCondition: Condition = diskCacheLock.newCondition()
private var diskCacheStarting = true

override fun onCreate(savedInstanceState: Bundle?) {
    ...
    // Initialize memory cache
    ...
    // Initialize disk cache on background thread
    val cacheDir = getDiskCacheDir(this, DISK_CACHE_SUBDIR)
    InitDiskCacheTask().execute(cacheDir)
    ...
}

internal inner class InitDiskCacheTask : AsyncTask<File, Void, Void>() {
    override fun doInBackground(vararg params: File): Void? {
        diskCacheLock.withLock {
            val cacheDir = params[0]
            diskLruCache = DiskLruCache.open(cacheDir, DISK_CACHE_SIZE)
            diskCacheStarting = false // Finished initialization
            diskCacheLockCondition.signalAll() // Wake any waiting threads
        }
        return null
    }
}

internal inner class  BitmapWorkerTask : AsyncTask<Int, Unit, Bitmap>() {
    ...

    // Decode image in background.
    override fun doInBackground(vararg params: Int?): Bitmap? {
        val imageKey = params[0].toString()

        // Check disk cache in background thread
        return getBitmapFromDiskCache(imageKey) ?:
                // Not found in disk cache
                decodeSampledBitmapFromResource(resources, params[0], 100, 100)
                        ?.also {
                            // Add final bitmap to caches
                            addBitmapToCache(imageKey, it)
                        }
    }
}

fun addBitmapToCache(key: String, bitmap: Bitmap) {
    // Add to memory cache as before
    if (getBitmapFromMemCache(key) == null) {
        memoryCache.put(key, bitmap)
    }

    // Also add to disk cache
    synchronized(diskCacheLock) {
        diskLruCache?.apply {
            if (!containsKey(key)) {
                put(key, bitmap)
            }
        }
    }
}

fun getBitmapFromDiskCache(key: String): Bitmap? =
        diskCacheLock.withLock {
            // Wait while disk cache is started from background thread
            while (diskCacheStarting) {
                try {
                    diskCacheLockCondition.await()
                } catch (e: InterruptedException) {
                }

            }
            return diskLruCache?.get(key)
        }

// Creates a unique subdirectory of the designated app cache directory. Tries to use external
// but if not mounted, falls back on internal storage.
fun getDiskCacheDir(context: Context, uniqueName: String): File {
    // Check if media is mounted or storage is built-in, if so, try and use external cache dir
    // otherwise use internal cache dir
    val cachePath =
            if (Environment.MEDIA_MOUNTED == Environment.getExternalStorageState()
                    || !isExternalStorageRemovable()) {
                context.externalCacheDir.path
            } else {
                context.cacheDir.path
            }

    return File(cachePath + File.separator + uniqueName)
}
```

<br/>

> 디스크 캐시를 초기화하는 것도 디스크 작업이 필요하므로 기본 스레드에서 실행하면 안 된다. 하지만 이는 초기화 전에 캐시에 액세스할 기회가 있음을 의미한다. 이 문제를 해결하기 위해 위의 구현에서 잠금 객체는 캐시가 초기화될 때까지 앱이 디스크 캐시에서 읽지 않도록 한다.
> 

<br/>

UI 스레드에서 메모리 캐시를 확인하는 동안 백그라운드 스레드에서는 디스크 캐시를 확인한다. 디스크 작업은 UI 스레드에서 발생해서는 안 된다. 이미지 처리가 완료되면 나중에 사용할 수 있도록 최종 비트맵을 메모리와 디스크 캐시에 모두 추가한다.

<br/>
<br/>

# 🗂 참고
- [캐싱이란 무엇이고 어떻게 작동합니까 | AWS (amazon.com)](https://aws.amazon.com/ko/caching/)
- [개린이의 관점에서 Kingfisher 살펴보기(1) - 이미지 캐싱이란? | 1Consumption](https://1consumption.github.io/posts/about-kingfisher(1)/)
- [안드로이드 이미지 캐시 구현 :: 자바캔(Java Can Do IT) (tistory.com)](https://javacan.tistory.com/entry/android-image-cache-implementation)
- [비트맵 캐싱  |  Android 개발자  |  Android Developers](https://developer.android.com/topic/performance/graphics/cache-bitmap?hl=ko)
- [[Android] LruCache 사용해 이미지 캐싱하기(Bitmap Cache) — Dev World (kotlinworld.com)](https://kotlinworld.com/368)
