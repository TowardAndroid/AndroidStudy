# 10회

안드로이드에서 데이터를 전달하는 방법은 크게 Parcelable과 Serializable 두 가지가 있습니다.

이 두 가지 방법은 객체를 직렬화하여 전송하는 방법이지만, 각각의 방법은 내부적으로 다른 방식으로 동작

# serializable 이란?

Java에서 제공하는 인터페이스로, 객체를 직렬화하여 전달하기 위해 사용됩니다.

객체를 바이트 스트림으로 변환하여 전달할 수 있습니다.

Serializable 인터페이스를 구현한 객체는 Java에서 제공하는 ObjectOutputStream을 사용하여 전달할 수 있습니다.

장단점

마커 인터페이스이기때문에 사용자가 사용하기 쉬움

시스템 비용이 비쌈( 내부적으로 reflection이 사용되기 때문에)

# parcelable 이란?

안드로이드에서 제공하는 인터페이스로, 객체를 전달하기 위해 사용

객체를 직렬화하여 안드로이드 OS에서 처리할 수 있는 바이트 배열로 변환하여 전달할 수 있습니다.

Parcelable 인터페이스를 구현한 객체는 안드로이드 OS에서 Intent나 Bundle에 담아 전달할 수 있습니다.

장단점

직렬화 처리 방법을 사용자가 직접 작성하므로 내부적인 reflection이 필요없다 따라서 시스템 비용이 적음

구현에 필요한 메서드 때문에 보일러 플레이트 코드가 추가 됨, 유지보수 어려움

### 둘의 차이점

- 속도
    - Parcelable은 Java의 Serializable보다 빠릅니다.
    - Parcelable은 안드로이드 OS에서 직접 처리하기 때문에 직렬화와 역직렬화 시간이 적습니다.
    - Serializable은 Java의 Reflection을 사용하기 때문에 직렬화와 역직렬화 시간이 상대적으로 느립니다.
- 크기
    - Parcelable은 Java의 Serializable보다 객체를 직렬화할 때 생성되는 데이터 크기가 작습니다.
    - Parcelable은 객체의 멤버 변수들을 Parcel에 쓰기 때문에 필요한 데이터만 쓰게 됩니다.
    - Serializable은 객체의 모든 데이터를 직렬화하기 때문에 불필요한 데이터까지 모두 쓰게 됩니다.
- 안정성
    - Parcelable은 Java의 Serializable보다 안정성이 높습니다.
    - Parcelable은 직렬화와 역직렬화에 대한 오류 검사를 수행하기 때문입니다.

[https://juyoung-1008.tistory.com/33](https://juyoung-1008.tistory.com/33)

[https://blacktrees.tistory.com/entry/Android-Parcelable과-Serializable의-차이점](https://blacktrees.tistory.com/entry/Android-Parcelable%EA%B3%BC-Serializable%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90)
