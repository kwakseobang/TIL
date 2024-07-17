# MVVM 
- MVVM(Model-View-ViewModel)은 깨끗하고 유지 관리 가능하며 테스트 가능한 코드를 만들기 위해 iOS 앱 개발에 널리 사용되는 디자인 패턴입니다. MVVM은 View를 Model과 분리하고 프레젠테이션 로직을 관리하기 위해 ViewModel이라는 중간 구성 요소를 도입합니다. 
  

- Model
  - 데이터와 비즈니스 논리를 정의 및 관리
  - 여기에는 데이터 구조, 데이터베이스, 네트워크 통화 및 데이터 관리를 담당하는 기타 구성 요소가 포함됩니다.
  - 모델은 View와 ViewModel과 독립적이다.
  
- ViewModel
  - ViewModel은 View의 데이터와 프레젠테이션 로직을 관리한다.
  - Model에서 데이터를 가져와서 View에서 사용할 수 있는 형태로 가공합니다.
  - View에 표시할 데이터를 ViewModel이 가지고 있음.
  - ViewModel은 View를 알지 못하지만, View는 ViewModel을 참조합니다.
 
  
- View
  -  애플리케이션의 모델 객체의 데이터를 표시하고 해당 데이터의 편집을 가능하게 하는 것이다. 
  - View는 ViewModel로부터 데이터를 가져와서 표현한다.
  - View는 ViewModel의 데이터를 관찰하고 변경되면 감지 후 뷰를 업데이트
  - Model을 직접 알고 있어서는 안된다.  ViewModel을 통해 데이터와 상호작용합니다.
  
  ## 단방향 데이터 흐름
- 데이터는 Model에서 ViewModel로, ViewModel에서 View로 흐름 
- 사용자 입력은 View에서 ViewModel로 전달되고, ViewModel은 Model을 업데이트
- Model의 변경사항은 ViewModel을 통해 View로 전달

  ## MMVM 장점
 -  유지보수 용이성:
     -   UI 로직과 비즈니스 로직이 분리되어 있어 각각을 독립적으로 수정 가능
- 테스트 용이성:

    - ViewModel은 View에 대한 의존성이 없기 때문에 단위 테스트가 용이
- 재사용성:

    - ViewModel은 View에 대한 의존성이 없기 때문에 다른 View에서도 재사용 가능
- 코드 가독성:

  - 역할과 책임이 명확히 분리되어 코드의 가독성 up
  


# MVC 
- Model: 
  - 모델 객체는 애플리케이션과 관련된 데이터를 캡슐화하고 해당 데이터를 조작하고 처리하는 논리와 계산을 정의
  - 즉,  데이터와 비즈니스 논리를 정의 및 관리
  - View나 Controller에 대해서 어떤 정보도 알지 못한다. 

- View: 
  -  애플리케이션의 모델 객체의 데이터를 표시하고 해당 데이터의 편집을 가능하게 하는 것이다. 
  - 화면에 데이터를 표시
  - 
   
-  Controller:
   -  컨트롤러 객체는 하나 이상의 애플리케이션의 뷰 객체와 하나 이상의 모델 객체 사이의 중개자 역할
   -  사용자 입력을 받아 모델과 뷰 사이에서 통신을 관리
-  뷰와 모델은 직접적으로 연결되어 있으면 안된다. Controller를 통해 데이터
-  
컨트롤러는 모델이나 뷰에 대해서 알고 있다. 모델이나 뷰는 서로의 존재를 모르지만, 변경 사항이 있을 경우 컨트롤러로 알리고 수신한다. 따라서 컨트롤러는 모델이나 뷰에 대한 사항에 대해 알고 있어야 한다.


## 참고자료
- 출처: https://code-lab1.tistory.com/220 [코드 연구소:티스토리]
- https://velog.io/@jeunghun2/iOS-MVVM-패턴에-대한-고찰-1-SwiftUI편
- https://medium.com/@zebayasmeen76/mvvm-in-ios-swift-6afb150458fd