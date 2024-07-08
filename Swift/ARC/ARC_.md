# ARC(Automatic Reference Counting)
- 메모리 관리 기법
- 자동으로 메모리를 관리해주는 방식
- 스위프트는 자동 참조 카운팅(ARC)을 사용하여 앱의 메모리 사용을 추적하고 관리한다. ARC는 해당 인스턴스가 더 이상 필요하지 않을 때 클래스 인스턴스에 의해 사용된 메모리를 할당 해제해서 확보합니다.

- 참조 계산은 클래스의 인스턴스에만 적용됩니다. 구조와 열거는 참조 유형이 아닌 값 유형이며, 참조로 저장되고 전달되지 않습니다.

# ARC 작동 원리
- 클래스의 새 인스턴스를 만들 때마다, ARC는 해당 인스턴스에 대한 정보를 저장하기 위해 메모리 덩어리를 할당합니다. 이 메모리는 **해당 인스턴스와 관련된 저장된 속성의 값과 함께 인스턴스의 유형에 대한 정보** 를 보유합니다.

- 또한, 인스턴스가 더 이상 필요하지 않을 때, ARC는 해당 인스턴스에서 사용하는 메모리를 확보하여 메모리를 다른 목적으로 사용할 수 있습니다. 이것은 클래스 인스턴스가 더 이상 필요하지 않을 때 메모리 공간을 차지하지 않도록 한다.

- 그러나, ARC가 여전히 사용 중인 인스턴스의 할당을 해제한다면, 더 이상 해당 인스턴스의 속성에 액세스하거나 해당 인스턴스의 메소드를 호출 불가.  실제로, 만약 당신이 그 인스턴스에 접근하려고 한다면, 앱이 죽는다.

- 인스턴스가 여전히 필요한 동안 사라지지 않도록 하기 위해, **ARC는 현재 각 클래스 인스턴스를 참조하는 속성, 상수 및 변수의 수를 추적합니다.** ARC는 그 인스턴스에 대한 적어도 하나의 활성 참조가 여전히 존재하는 한 인스턴스를 할당 해제하지 않을 것이다.

- 이것을 가능하게 하려면 프로퍼티, 상수, 또는 변수에 클래스 인스턴스를 할당할 때마다 해당 프로퍼티, 상수, 또는 변수는 인스턴스에 **강한 참조** (strong reference) 를 만듭니다. 참조는 해당 인스턴스를 유지하고 강한 참조가 남아있는 한 할당 해제를 허용하지 않기 때문에 "강한" 참조라고 합니다.

# ARC in Action
```swift
class Person {
    let name: String
    init(name: String) {
        self.name = name
        print("\(name) is being initialized")
    }
    deinit {
        print("\(name) is being deinitialized")
    }
}
```
```swift
var reference1: Person?
var reference2: Person?
var reference3: Person?
```
```swift
reference1 = Person(name: "John Appleseed")
// Prints "John Appleseed is being initialized"
```
- "John Appleseed가 초기화되고 있습니다"라는 메시지는 Person 클래스의 이니셜라이저를 호출하는 지점에서 인쇄됩니다. 이것은 초기화가 이루어졌다는 것을 확인시켜 준다.

- 새로운 Person 인스턴스가 reference1 변수에 할당되었기 때문에, 이제 reference1에서 새로운 Person 인스턴스에 대한 강력한 참조가 있습니다. 적어도 하나의 강력한 참조가 있기 때문에, ARC는 이 사용자가 메모리에 저장되어 있고 할당 해제되지 않았는지 확인합니다.

```swift
reference2 = reference1
reference3 = reference1

reference1 = nil
reference2 = nil
```


- 두 개의 변수에 nil을 할당하여 이러한 두 개의 강력한 참조(원래 참조 포함)를 깨뜨리면 하나의 강력한 참조가 남아 있으며 Person 인스턴스는 할당해제 되지 않습니다.
  
~~~swift
reference3 = nil
// Prints "John Appleseed is being deinitialized"
~~~

- ARC는 세 번째이자 마지막 강력한 참조가 깨질 때까지 Person 인스턴스를 할당 해제하지 않으며, 이 시점에서 더 이상 Person 인스턴스를 사용하지 않는다는 것이 분명합니다.











### 참고 자료
1. https://velog.io/@ssionii/Swift-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EA%B4%80%EB%A6%AC-a.k.a-ARC-%EC%97%90-%EB%8C%80%ED%95%B4-%EC%95%84%EB%9D%BC%EB%B3%B4%EC%9E%90-ARC%EB%9E%80

2. Swift 공식문서 https://bbiguduk.gitbook.io/swift/language-guide-1/automatic-reference-counting#strong-reference-cycles-between-class-instances