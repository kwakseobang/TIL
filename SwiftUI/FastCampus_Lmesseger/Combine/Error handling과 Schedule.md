### Error Handling
- 모든 Publisher와 Subscriber에 Failure 타입이 명시되어 있음
- 에러가 발생하기 전에 미리 대응하고 복구할 수 있음.
- ReplaceError, Catch
- SetFailureType, MapError

## 연산자
- ReplaceError
  - 스트림 내에 에러가 발생했을 때, 대체 값을 제공하는 Publisher
- Catch
  - Upstream Publisher에서 발생한 에러를 다른 Publisher로 대체하여 처리하는 Publisher 
  - 에러 방출 후 스트림 종료된다.

## error를 맵핑하는 데 사용되는 연산자
- SetFailureType
  - Publisher의 Failure 타입을 변형하는데 사용되는 Publisher
- MapError
  - Upstream Publisher에서 발생한 에러를 새로운 에어로 변환하는 Publisher

### Schedule
- 데이터 스트림 지연 및 특정 스레드 또는 큐에서 작업을 수행
- 언제, 어디서 처리할지 정의 가능
- RceiveOn, SubscribeOn
- Delay, Debounce

## 연산자
- RceiveOn
  - 하위에 위치한 연산자나 구독자에게 전달되는 이벤트를 지정된 스케줄러에서 처리하도록 하는 Publisher
  - 백그라운드 작업이나 UI 업데이트때 많이 사용된다.
- SubscribeOn
  - 데이터 스트림이 생성되는 스케줄러를 지정하는 Publisher
  - 