# Spring Exception 


## @HandlerExceptionResloer를 통해 스프링은 자체적으로 예외 처리 함
- Java에서는 예외 처리를 위해 try-catch를 사용해야 하지만 try-catch를 모든 코드에 붙이는 것은 비효율적이다. Spring은 에러 처리라는 공통 관심사(cross-cutting concerns)를 메인 로직으로부터 분리(AOP 기법)하는 다양한 예외 처리 방식을 고안하였고, 예외 처리 전략을 추상화한 **HandlerExceptionResolver** 인터페이스를 만들었다. (전략 패턴이 사용된 것이다.)

``` java
public interface HandlerExceptionResolver {
    ModelAndView resolveException(HttpServletRequest request, 
            HttpServletResponse response, Object handler, Exception ex);
}
```
- Object 타입인 handler는 예외가 발생한 컨트롤러 객체이다. 예외가 던져지면 디스패처 서블릿까지 전달되는데, 적합한 예외 처리를 위해 HandlerExceptionResolver 구현체들을 빈으로 등록해서 관리
- 예외가 발생하면 가장 구체적인 예외 핸들러를 먼저 찾고, 없으면 부모 예외의 핸들러를 


## 구현체
- @ExceptionHandlerExceptionResolver
	- 예외 응답을 위한 controller,ControllerAdivce에 있는 ExceptionHandelr 처리
- @ResponseStatusExceptionResolver
	- http 상태 코드를 지정하는 @ResponseStatus 또는 ResponseStatusException을 처리
- @DefalutHandlerxceptionResolver
	- 스프링 내부의 기본 예외들을 처리
- @DefaultErrorAttributes
    - 에러 속성을 저장하며 직접 예외를 처리하지는 않는다.



# Error 처리 도구 들

## @ResponseStatus
- 에러 http 상태를 변경하도록 도와주는 어노테이션
-  @ResponseStatusExceptionResolver가 처리함.
- 다음과 같이 적용 가능
    - Exception 클래스 자체
    - 메소드에 @ExceptionHandler와 함께
    - 클래스에 @RestControllerAdvice와 함께
~~~ java
@ResponseStatus(value = HttpStatus.NOT_FOUND)
public class NoSuchElementFoundException extends RuntimeException {
  ...
}
 ~~~
- 단점 
    - 예외 응답의 내용 수정 불가
    - 예외 클래스와 강하게 결합
    - 별도의 응답 상태가 필요하다면 예외 클래스를 추가해야 됨
    - was까지 예외가 전달
    - 외부에서 정의한 exception 클래스에는 @ResponseStatus를 붙일 수 없음

## @ResponseStatusException
- 상태 코드와 함께 메시지를 포함한 예외를 직접 생성하여 클라이언트에게 응답
-  @ResponseStatusExceptionResolver가 처리함.


~~~ java
@GetMapping("/product/{id}")
public ResponseEntity<Product> getProduct(@PathVariable String id) {
    try {
        return ResponseEntity.ok(productService.getProduct(id));
    } catch (NoSuchElementFoundException e) {
        throw new ResponseStatusException(HttpStatus.NOT_FOUND, "Item Not Found");
    }
}

~~~

- 단점
    - 일관된 예외 처리의 어려움
    - 예외 처리 중복 가능성
    - 내부 예외 처리 어려움
    - was까지 예외가 전달

## @ExceptionHandler
- ExceptionHandlerExceptionResolver이 처리함
- Controller의 메소드에서 throw된 Exception에 대한 공통적인 처리
- 다음과 같이 적용 가능
    - 컨트롤러의 메소드
    - @ControllerAdvice나 @RestControllerAdvice가 있는 클래스의 메소드
~~~ java
@ExceptionHandler(NoSuchElementFoundException.class)
  public ResponseEntity<String> handleNoSuchElementFoundException(NoSuchElementFoundException exception) {
    return ResponseEntity.status(HttpStatus.NOT_FOUND).body(exception.getMessage());
  }

~~~
- 만약 ResponseEntity에서도 status를 지정하고 @ResponseStatus도 있다면 ResponseEntity가 우선순위를 갖는다.
-  @ExceptionHandler에 등록된 예외 클래스와 파라미터로 받는 예와 클래스가 동일해야 한다.

- 단점
    - 컨트롤러에 구현하므로 특정 컨트롤러에서만 발생하는 예외만 처리된다. 하지만 컨트롤러에 에러 처리 코드가 섞이며, 에러 처리 코드가 중복될 가능성도 큼.



## @ControllerAdvice
- @ControllerAdvice나@RestControllerAdvice이 붙여진 클래스
- 예외 처리와 같은 공통 관심사를 한곳으로 추출하여 유지 보수 하기 쉽게 함.
- 여러 controller에서 발생하는 예외를 처리함
- DispatcherSevlet에서 발생하는 예외를 전역적으로 처리.
	- 대부분 DispatcherSevlet에서 예외 발생함
~~~ java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@ControllerAdvice
@ResponseBody
public @interface RestControllerAdvice {
    ...
}

@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Component
public @interface ControllerAdvice {
    ...
}

~~~
- @componet가 적용되어서 ControllerAdvice가 선언된 클래스는 Bean으로 등록
- 일관성 있는 에러 응답
주의할점
- 한 프로젝트당 하나의 ContollerAdvice만 관리하는 것이 좋다.
- 직접 구현한 Exception 클래스들은 한 공간에서 관리한ㄷ,
@RestControllerAdvice
	@ControllerAdvice + @ResponseBody


# ExceptionHandlerExceptionResolver 동작원리
1. 예외 발생한 컨트롤러 안에 적합한 ExceptionHandler가 있는 지 확인 있으면 처리
2. 없으면 ControllerAdvice로 넘어가서 적합한 ExceptionHandler가 있는 지 확인 있으면 처리
3. 없으면 ResponseStatusExceptionResolver로 넘어감
4. ResponseStatus나 ResponseStatusException 이 있는 지 검사 있으면 예외를 서블렛으로 전달 후 BasicErrorController로 전달
5. 없으면 DefalutHandlerxceptionResolver에서 처리








## 참고 자료 
- https://www.youtube.com/watch?v=6ZrWR4Si7IQ
- https://www.youtube.com/watch?v=nEW0Dmi2E9o
- [MangKyu's Diary:티스토리](https://mangkyu.tistory.com/204 )