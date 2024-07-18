## Identity
- Identifiable Protocol
~~~swift
public protocol Identifiable<ID> {
    associatedtype ID: Hashable
    var id: Self.ID {get}
}
~~~
### View Identity
  - 앱의  요소를 업데이트하기 위해 동일한지 아닌지를 인식하는 방법
  - 데이터 및 업데이트 주기에 영향을 미침.

### View Identity의 종류
- 명시적 Identity

- 구조적 Identity                                                                                                                  