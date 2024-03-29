### Publisher(공급자)

- 데이터 스트림 생성
- 데이터 전달
- 데이터 변환 및 조함


### Subscriber(관찰자)
- 데이터 스트림을 구독하고 받아서 처리하는 역할
- 데이터 처리
- 이벤트 처리
- 구독 제어


## Pub-Sub Pattern
반응형 프로그래밍 기반 패턴

Publisher와 Subscriber 중간에 이벤트 관리자를 두어 처리한다.

## 이벤트 관리자 == Subscription(구독권)
- 이벤트 및 데이터 전달
- 구독 관리
- 자원 해제 및 정리

### 구독 메커니즘 이해하기
1. Subscriber는 구독을 원하는 Publisher에게 subscribe(_:)메소드를 호출하여 구독 요청

2. 구독을 요청 받은 Publisher는 구독자에게 전달할 Subscription 생성

3. Publisher의 Subscription를 receive(subscription:) 메서드를 호출하여 구독자에게 전달

4. 구독권을 받은 구독자는 subscription애개 원하는 Demand를 request(_: Demand)를 이용해 요청

5. Publisher가 값을 생성하면 구독권에게 전달 후 Subscriber에게 receive(_:Input)을 통해 값 전달

6. 새로운 Demand가 있을 경우, 업데이트

7. 마지막으로 Subscriber가 Publisher에게 완료 이벤트를 받으면 구독 해제

- 구독권을 통해 소통한다!


## Apple 에서 구현해놓은 Publisher 알아보기

1. Just
   - 각 Subscriber에게 한 번 값을 방출한 후 완료되는 Publisher
   - 실패가 없으므로, Failure = Never
   - 그래서 Just는 combine에서 어떠한 값을 스트림으로 연결하고 싶을 때 사용한다.
2. Empty
   - 값을 생성하지 않고 완료만 하는 Publisher
   -  combine에서 스트림을 생성하지 않고 작업이 완료됐다는 걸 명시 하고 싶을 때 사용한다.
3. Fail
   - 특정 에러로 즉시 종료되는 Publisher

4. Future
   -  최종적으로 하나의 값을 생성한 후 완료되거나 실패하는 Publisher
  

  ## Apple 에서 구현해놓은 Subscriber 알아보기

  1. sink
   - 구독 시 무제한 개수의 값을 요청하는 Subscriber
   - receiveCompletion: 완료되었을 때 실행
   - receiveValue: 값을 받았을 때 실행
   - Publisher에 sink 메소드가 내장 되어있다.
  2. Assign
   - 지정된 Key path로 값을 프로퍼티에 할당하는 Subscriber