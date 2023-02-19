# 디자인패턴

효율적인 코딩 방법 또는 구조

필요이유: 명확하고 단순한 코딩, 높은 재사용성, 쉬운 유지보수 등

# Builder

객체를 생성할 때 흔하게 사용하는 패턴

복잡한 인스턴스를 조립하여 만드는 구조

생성자에 파라미터가 많은 클래스인 경우 빌더 패턴을 사용하여 가독성을 높일 수 있음

android에서는 NotificationCompat.Builder와 AlertDialog.Builder와 같은 클래스를 사용할 때 Builder패턴이 나타남

```
Notification notification =new NotificationCompat.Builder(this)
                                      .setSmallIcon(R.drawable.ic_notification)
                                      .setContentIntent(pendingIntent)
                                      .setTicker(message)
                                      .build();
```

### 장점

각 인자가 어떤 의미인지 알기 쉽다

setter메소드가 없으므로 변경 불가능 객체를 만들 수 있다

한번에 객체를 생성하므로 객체 일관성이 깨지지 않는다.

build()함수가 잘못된 값이 입력되었는지 검증하게 할 수도 있다

# adapter

기존시스템 업체에서 제공한 클래스

RecyclerView.Adapter클래스에서 자주보임

### 장점

호환되지 않는 인터페이스를 사용하는 클라이언트를 그대로 활용할 수 있음

클라이언트와 구현된 인터페이스를 분리시킬 수 있으며, 향후 인터페이스가

바뀌더라도 그 변경내역은 어댑터에 캡슐화 되기 때문에 클라이언트는 바뀔 필요가 없어짐

# observer

객체와의 관계를 맺고 끊으며 객체의 상태가 변경되면 그 정보를 observer에게 알려는 방법

```
apiService.getData(someData)
    .observeOn(AndroidSchedulers.mainThread())
    .subscribe (/* an Observer */);
```

값을 방출할 Observable객체를 정의

Observable들은 한 번 또는 연속적으로 스트림, 값,이벤트를 방출함

Subscriber는 이러한 값을 수신하고 도착한 대로 응답

### 예시

```
Button button = (Button) findViewById(R.id.button);
button.setOnClickListener(new OnClickListener() {
    @Override
    public void onClick(...) {
        // ACTION
    }
})
```

Button 객체 Publisher가 되고 OnClickListener가 Observer가 됨

상태가 변경(클릭되면) OnClickListener로 알려줌

### 장점

느슨한 결합성 유지
