# UICollectionViewCompositionalLayout
- UICollectionViewCompositionalLayout는 iOS 13이상부터 사용 가능한 UIColletionView의 레이아웃을 정의하는 방법이다. UICollectionViewCompositionalLayout를 사용하면 복잡한 레이아웃을 쉽게 구현할 수 있으며, 다양한 크기와 형태의 셀을 세밀하게 조정가능하다.

## 기본 개념
1. 섹션
   - 컬렉션 뷰는 여러 섹션으로 구성된다. 각 섹션은 독립적으로 레이아웃을 정의할 수 있다.
2. 그룹
   - 섹션 내에는 하나 이상의 그룹이 있으며, 이 그룹들은 하나의 레이아웃 패턴을 공유한다. 그룹은 여러 아이템을 포함할 수 있다.
3. 아이템 
   - 이는 컬렉션 뷰를 나타내며 각 아이템은 그룹 내에 배치된다.
  
## 특징
1. 유연성
   - 세로,가로 스크롤, 그리드, 리스트, 피드 등 다양한 레이아웃을 쉽게 조절할 수 있다.
2. 커스터마이징
   - 개별 섹션, 그륩, 아이템 레벨에서 레이아웃을 상세하게 조정할 수 있다.
3. 동적인 크기 조정
   - 콘텐츠에 따라 동적으로 아이템의 크기를 조정할 수 있다.

## CollectionView의 item 사이즈를 정하는 방법은 3가지
- .absolute - 고정 크기
- .estimated - 런타임에 변경
- .fractional - 비율
- 
### 예제 코드
~~~ swift
func createBasicListLayout() -> UICollectionViewLayout { 
    let itemSize = NSCollectionLayoutSize(widthDimension: .fractionalWidth(1.0),                                  
                                         heightDimension: .fractionalHeight(1.0))    

                                         
    let item = NSCollectionLayoutItem(layoutSize: itemSize)  
  
    let groupSize = NSCollectionLayoutSize(widthDimension: .fractionalWidth(1.0),                                          
                                          heightDimension: .absolute(44))    
    let group = NSCollectionLayoutGroup.horizontal(layoutSize: groupSize,                                                   
                                                     subitems: [item])  
  
    let section = NSCollectionLayoutSection(group: group)    


    let layout = UICollectionViewCompositionalLayout(section: section)    
    return layout
}
~~~


### 참고 자료
1. https://developer.apple.com/documentation/uikit/uicollectionviewcompositionallayout
2. 패스트캠퍼스 ios 강의