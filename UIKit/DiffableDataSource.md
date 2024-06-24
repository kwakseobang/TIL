# DiffableDataSource
- DiffableDataSource는 UIkit 프레임워크에서 사용되는 데이터 소스 유형이다. 이것은 주로 UITableView와 UIColletionView에서 사용되며, 데이터를 관리하고 UI 컴포넌트에 표시하는 데 도움이 된다.DiffableDataSource의 주요 목적은 데이터와 UI의 동기화를 보다 쉽고 효율적으로 만드는 것이다.


## DiffableDataSource 알아보기
1. 섹션과 아이템
   - DiffableDataSource는 섹션과 아이템으로 구성된다. 각 섹션은 하나 이상의 아이템을 포함할 수 있다.
2. 스냅샷
   - 데이터의 현재 상태를 나타내는 스냅샷을 사용한다. 스냅샷을 통해 데이터 소스에 변경 사항을 적용할 수 있다.
3. 자동 업데이트
   - 데이터가 변경될 때마다 view들을 수동으로 업데이트 할 필요가 없다.

## 비교
- 코드의 간결성과 가독성 up
- 오류 발생 가능성 감소
- 애니메이션과 전환 효과의 자동화
  

## 깊게 알아보기
- 섹션
  - 섹션은  UITableView와 UIColletionView 내에서 데이터를 그룹화하는 방법이다. 
  - 섹션은 데이터의 논리적인 구분을 나타내며, 각 섹션은 하나 이상의 아이템(데이터 항목)을 포함할 수 있다.
  - DiffableDataSource에서는 섹션을 열겨형(enum)으로 정의할 수 있으며, 이를 통해 스냅샷에서 섹션을 식별하고 관리한다.
~~~ swift
enum Section {
    case main
    case featured
    case categorires
}
~~~

- 아이템
  - 아이템은 개별 데이터 요소를 나타낸다.
  - 아이템은 일반적으로 구조체 또는 클래스로 정의된다. 이들은 고유하게 식별될 수 있어야하며, 이를 위해 Hashable 프로토콜을 채택해야된다.
  - DiffableDataSource에서는 이러한 아이템을 사용하여 각 셀의 표시될 데이터를 정의한다.
  
~~~ swift
struct Contact: Hashable {
    let id: UUID
    let name: String
    ...
}
~~~

- 섹션과 아이템의 상호작용
  - DiffableDataSource 사용할 때, 섹션과 아이템은 스냅샷을 통해 관리된다. 스냅샷은 현재의 데이터 상태를 나타내며, 데이터의 변경 사항을 ITableView와 UIColletionView에 적용하기 위해 사용된다.
  
~~~ swift
var snapshot = NSDiffableDataSourceSnapshot<Section,Contact>()
//섹션추가
snapshot.appendSections([.main,.featured])
//아이템 추가
snapshot.appendItems([/*main section들의 아이템들*/],toSections: .main)
snapshot.appendItems([/*featured section들의 아이템들*/],toSections: .featured)
dataSource.apply(snapshot,animatingDifferences: true) //기존 스냅샷과 비교 후 데이터 소스에 스냅샷 적용
~~~

- 스냅샷
  - 데이터 상태의 표현
    - 스냅샷은 특정 시점에서의 전체 데이터 세트를 표현한다. 이는 섹션과 아이템의 현재 상태를 포함한다.
- 변경 관리
  - 데이터의 변경이 발생할 떄, 새로운 스냅샷을 생성하고 이를 기존 데이터 소스에 적용하여 UI를 업데이트 한다.
- 유연한 데이터 조작
  - 스냅샷을 사용하면 추가, 삭제, 이동하는 등의 조작을 쉽고 유연하게 할 수 있다.

- 스냅샷 사용법
  - 데이터 추가
    - appendSections 및 appendItems 메서드를 통해 수행된다.
  - 데이터 삭제
    - deleteSections 및 deleteItems 메서드르 통해 수행된다.
  - 데이터 업데이트
    - 스냅샷을 새롭게 적용하면, DiffableDataSource는 현재 UI와 새 스냅샷의 차이를 계산하고 필요한 업데이트를 자동 수행한다.