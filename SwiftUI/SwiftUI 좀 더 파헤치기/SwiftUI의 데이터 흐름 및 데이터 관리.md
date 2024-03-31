### SwiftUI Data 흐름 원리
1. 데이터 의존성
2. SSOT(Single Source Of Truth)
   - 유일한 본질적인 데이터
   - 일관성 유지, 데이터 동기화 문제 방지
   - 모든 @State와 @StateObject는 source of truth
   - @Binding으로 연결
## Property Wrapper Type
- Swift 5.1
- Property의 getter와 setter를 이용해 사용자 패턴을 정의함
- Wrapper Type을 채택한 프로퍼티는 정의된 기능을 사용할 수 있음.
- 코드 재사용 및 가독성 향상

##Property Wrapper

- @State
  - 영구적인 저장소를 생성
  - 뷰에 대한 의존성 추적

### View Update 방식
1. @State에 선언된 프로퍼티의 영구적인 저장소 할당
2. 프로퍼티 변경 후 관련 뷰들 재생성

### 관련 기능
- ObservableObject

View 업데이트 방식
- @StateObject
- @ObservableObject
- @Published
- @EnvironmentObject