### KVO
- object의 변화를 지켜볼 수 있다
- KVO는 서로 알고있어야한다
- 1:1
- NSObject를 상속받아야해서 클래스
  - ex. 모델의 데이터가 바뀌면 컨트롤러가 그것을 뷰에 반영
  - ex. 과일 추가창에서 과일 재고를 변경하면 컨트롤러가 뷰의 과일 수량을 수정

### Notification Center
- 변화가 생기면 모든 구독자에게 알리는 것
- 1:n
- 구조체는 Notification으로
