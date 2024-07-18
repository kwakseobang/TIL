### SwiftUI Layout 프로세스
1. Parent는 Child에게 사이즈 제안
2. Child는 자신의 사이즈를 선택(크기 결정)
3. Parent는 Parent의 좌표 공간에 child 배치(위치 결정)

## Layout Container
- 뷰의 배치 및 레이아웃을 구성하는데 사용
- Hstack,Vstack
- Grid
- Zstack

## Lazy Layout Container

- 화면에 표시할 뷰들을 지연하여 로드해 효율적으로 처리하기 위한 컨테이너
- Item을 재사용
- LazyHstack, LazyVstack
- LazyHGrid, LazyVGrid



## layout 중립
- body를 가지고 있는 뷰는 레이아웃 중립이다. (바디 뷰와 동일한 크기를 갖는다)