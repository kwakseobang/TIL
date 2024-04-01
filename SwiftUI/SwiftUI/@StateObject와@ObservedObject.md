## 찾아내서 바로 쓴다..

- 프로젝트 진행하다가 상위 뷰에서 하위 뷰로 @StateObject를 넘길려고 하위 뷰도 @StateObject로 선언했더니 안넘겨져서 굉장히 고민이였다..
- 그래서 혹시 몰라 하위 뷰를 변수를 @ObservedObject로 바꿧는데 넘겨졌다.. 

@StateObject:

@StateObject는 뷰의 수명과 함께 유지되는 객체를 생성하고 초기화합니다.
뷰가 새로 고쳐지면 @StateObject가 다시 초기화되지 않습니다. 즉, 뷰가 다시 그려질 때마다 동일한 객체를 사용합니다.
따라서 @StateObject는 뷰 내에서 해당 뷰와 함께 동작하는 상태를 가지는 데 적합합니다.
@ObservedObject:

@ObservedObject는 외부에서 생성된 객체를 관찰하고, 해당 객체가 변경될 때마다 뷰를 다시 렌더링합니다.
@ObservedObject를 사용하여 외부에서 생성된 객체를 뷰에 주입할 수 있습니다. 이 객체의 상태가 변경되면 해당 변경 사항이 뷰에 반영됩니다.
따라서 @ObservedObject는 뷰 내에서 외부에서 생성된 객체의 변경을 감지하고 반응할 때 사용됩니다.
따라서 @StateObject로 할당된 ObservableObject 객체는 해당 뷰의 수명과 함께 유지되므로 뷰의 라이프사이클과 함께 동작하는 상태를 나타내는 데 적합합니다. 반면에 @ObservedObject는 외부에서 생성된 객체의 변경을 감지하여 해당 변경에 반응하는 데 사용됩니다. 따라서 @StateObject로 생성된 객체를 하위 뷰로 전달할 때는 해당 객체를 @ObservedObject로 선언하여 변경 사항을 감지하고 반영할 수 있습니다.