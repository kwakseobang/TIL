### Operator 종류
- 변환 연산자: Map, TryMap, FlatMap
- 필터 연산자: Filter, CompactMap
- 조합 연산자: Zip

## 변환 연산자
- Map
  - transform 클로저를 사용하여 Upstream Publisher에서 나오는 모든 값들을 변환하는 Publisher
- TryMap
  - Map과 유사하지만 transform 클로저에서 에러를 throw할 수 있는 Publisher 
- FlatMap
  - Upstream Publisher에서 오는 값들을 새로운 Publisher로 변환하는 Publisher
## 필터 연산자
- Filter
  - 클로저의 조건과 일치하는 값을 발행하는 Publisher
- CompactMap
  - 클로저에서 nil이 아닌 값을 발행하는 Publisher

##  조합 연산자
- Zip
  - 두 . 개이상의 Upstream Publisher로부터 나온 값을 받아와 조합하고 그 값을 방출해주는 Publisher