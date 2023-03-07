[https://medium.com/@futureofdev/android-constraintlayout-쉽게-알아가자-62d2ded79c17](https://medium.com/@futureofdev/android-constraintlayout-%EC%89%BD%EA%B2%8C-%EC%95%8C%EC%95%84%EA%B0%80%EC%9E%90-62d2ded79c17)

[https://recipes4dev.tistory.com/158](https://recipes4dev.tistory.com/158)

[https://coding-food-court.tistory.com/128](https://coding-food-court.tistory.com/128)



레이아웃 구성 시, 뷰 위젯의 위치와 크기를 유연하게 조절할 수 있게 만들어주는 레이아웃


<br>

왜 쓰나요?

제약 조건을 이용하여 UI Component를 제어하는 방식은 중첩된 layout을 피할 수 있도록 설계됨

Linear Layout을 써야만 했던 뷰 비율 조절도 간단히 가능(depth가 깊어지는 것 방지)

뷰 계층 간단히 할 수 있어 유지보수도 좋고 성능이 좋음

구글이 기존의 많은 layout 기능들을 deprecated함.

<br>

뷰의 왼쪽 사이드를 대상 뷰의 오른쪽 사이드에 배치 → layout_constraintLeft_toRightOf
