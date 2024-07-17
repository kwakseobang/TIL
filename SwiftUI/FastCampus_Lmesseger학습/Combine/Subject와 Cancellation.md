### Subject
- Publisher와 Subscriber 두 역할 모두 가능
- send 메서드를 통해서 Data Stream에 값 주입 가능

## Subject 종류
- PassthroughSubject
  - 방출된 값과 이벤트를 전달


- CurrentValueSubject
  - 버퍼가 존재하여 마지막에 방출된 값을 저장

## 필요에 따라 구독 취소 방법

- Cancellable
  - 어떠한 작업에 취소가 가능함을 나타내는 프로토콜
  - cancel 함수 제공
  - Subscription은 Cancellable 프로토콜 채택

- AnyCancellable
  - 구독 시 해당 객체 반환됨
  - 구독을 쉽게 취소 가능

- Type Erase
  - 원래의 Publisher의 타입을 지우고 AnyPublisher로 변환
  - 실제 Publisher의 타입 정보가 감춰져 다양한 유형의 Publisher를 처리하거나 반환 가능
  - 일반화와 유연성이 높아짐