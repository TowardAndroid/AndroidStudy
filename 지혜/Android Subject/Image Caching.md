# Image Caching ****Bitmap Cache****

<br>


[https://kotlinworld.com/368](https://kotlinworld.com/368)

[https://developer.android.com/topic/performance/graphics/cache-bitmap?hl=ko](https://developer.android.com/topic/performance/graphics/cache-bitmap?hl=ko)

[https://yoon-dailylife.tistory.com/110](https://yoon-dailylife.tistory.com/110)

[https://minchanyoun.tistory.com/121](https://minchanyoun.tistory.com/121)

[https://velog.io/@dear_jjwim/안드로이드-Glide-없이-LruCache로-이미지-캐싱하기-Bitmap-Cache](https://velog.io/@dear_jjwim/%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-Glide-%EC%97%86%EC%9D%B4-LruCache%EB%A1%9C-%EC%9D%B4%EB%AF%B8%EC%A7%80-%EC%BA%90%EC%8B%B1%ED%95%98%EA%B8%B0-Bitmap-Cache)

<br>

## **LruCache**


 1.**LinkedHashMap**을 사용하여 최근에 사용된 object의 strong reference를 보관하고 있다가 정해진 사이즈를 넘어가게 되면 가장 최근에 사용되지 않은 놈부터 쫓아내는 **LRU**알고리즘을 사용하는 **메모리 캐시**

2.안드로이드에서 캐시를 관리하기 위해 제공하는 메모리 캐시 객체

3. **LRU Cache**를 사용하는 대표적인 예가 **[비트맵 캐싱](https://developer.android.com/topic/performance/graphics/cache-bitmap?hl=ko)**
4.  리사이클러뷰와 같은 대량의 이미지를 한 번에 로드하고 스크롤하여 재사용되는 경우 **LRU Cache**의 사용은 퍼포먼스 개선에 많은 도움
5. 그러므로 **LRU Cache**를 사용할 때는 자주 참조되는 객체일 수록 빠르게 캐시를 통해 객체에 접근할 수 있습니다
6. 많은 **Bitmap**을 메모리에 캐시하는 것은 부담될 수 있으므로(용량 한계가 작음), **DiskLruCache**와 같은 디스크 캐싱을 같이 사용하면 좀 더 메모리 부담을 줄일 수 있습니다.
7. **디스크**에서 이미지를 가져오는 것은 **메모리**에서 로드하는 것보다 **느리며** 디스크 읽기 시간을 예측할 수 없기 때문에 백그라운드 스레드에서 실행되어야 합니다.

### **LRU**알고리즘

이를 위해 **LRU** 알고리즘은 메모리 상에서 가장 최근에 사용된 적이 없는 캐시의 메모리부터 대체하며 새로운 데이터로 갱신시켜줍니다.

- **LRU** 알고리즘의 구현은 **Linked List**를 이용한 **Queue**로 이루어지고, 접근의 성능 개선을 위한 **Map**을 같이 사용

### **Glide**에 **URL**을 넘기면, 아래와 같이 동작합니다.

1. 메모리에 URL Key에 해당하는 이미지가 있는지 확인
2. 메모리에 캐시에 비트맵이 있다면 그대로 가져와서 사용
3. 메모리 캐시에 비트맵이 없다면, 디스크 캐시에서 이미지를 가져온다
4. 디스크 캐시에 이미지가 있다면, 디스크로부터 Bitmap을 로딩 후 메모리 캐시로 옮기고, Bitmap을 View에 로딩
5. 디스크 캐시에 없다면, 네트워크에서 이미지를 다운로드하고 디스크 캐시에 옮긴 후 또 한 번 메모리 캐시에 옮긴다. 그리고 Bitmap을 View에 로드

```
public class LruCache<K, V> { // 제네릭으로 선언됨, <K : 캐시에 접근하기 위한 키 값, V : 캐시에서 가져올 객체 타입>

    public LruCache(int maxSize) { // 생성자 인자로 maxSize를 int 값으로 받음
        throw new RuntimeException("Stub!");
    }

    . . .
}
```
