## 구조체
  - 구조체 정의 
    - struct 키워드로 정의
    ``` swift 
    struct 구조체 이름 {

    }
    ```
- 구조체의 인스턴스 생성 및 초기화
  -  구조체의 인스턴스 생성 및 초기화 시 사용자 정의 생성자가 없다면 기본적으로 자동 생성되는 memberwise   생성자 사용
       - memberwise 생성자 : 프로퍼티 명들을 매개변수로 하는 생성자
  - 구조채의 인스턴스는 **값 타입** 이다.
  ~~~swift 
  struct Info {
    var name: String
    let age: Int
  }

  var aInfo: Info = Info(name: "Kim", age: 23) // memberwise 생성자를 이용한 초기화
  ~~~
- Stack 영역에 저장
-  값타입이므로 원본 보호 가능  



## 클래스
- 클래스 정의
  - class 키워드로 정의
  ~~~ swift
  class 클래스 이름 {

  }
  ~~~

- 클래스의 인스턴스 생성 및 초기화
  -  클래스의 인스턴스 생성 및 초기화 시 생성자 사용
     -  memberwise 생성자 없음.
  
  - 클래스의 인스턴스는 **참조 타입** 이다.
    - 참조 타입의 메모리 관리는 **ARC**(Automatic Reference Counting) 를 통해 관리된다.
    - 메모리 공유 가능
- 클래스의 인스턴스 소멸
  - 클래스의 인스턴스는 참조 타입이므로 인스턴스가 메모리에서 해제되기 직전 처리해야될 코드들을 소멸자에 정의해놓았다. 
  - 소멸자 존재
    - 소괄호 없음
    - 매개변수, 반환값 없음
- 상속 가능
- Heap 영역에 저장
  - 참조타입이므로 메모리 효율적으로 사용 가능 
  - 실질적인 값은 **Heap** 영역에, 참조 주소를 가리키는 변수는 **Stack** 영역에 저장된다.


## 구조체와 클래스의 공통점
- 프로퍼티와 메소드 정의 가능
- 생성자 정의 가능
- 속성값에 접근할 수 있는 방법을 제공하는 서브스크립트 정의 가능
- extension을 통해 확장 가능
- protocol 채택 가능

## 구조체와 클래스의 차이점
- ```구조체는 값 타입, 클래스는 참조 타입```
- 타입 캐스팅은 클래스만 가능하다.
- 구조체는 상속 불가
- 소멸자는 클래스에만 존재
- reference counting은 클래스에의 인스턴스에만 존재
