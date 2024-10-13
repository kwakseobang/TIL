# 리스너(Listener)
- 리스너 객체들은 이벤트가 발생되면 자동으로 실행되는 특징이 있다.
- 리스너를 이용하면 이벤트가 발생했을 때 미리 약속해둔 동작을 수행할 수 있다.


## ServletContextEvent와 ServletContext
- contextInitialized() 와 contextDestroyed()에는 파라미터로는 ServletContextEvent라는 객체가 전달된다. ServletContextEvent를 이용하면 현재 애플리케이션이 실행되는 공간인 ServletContext를 접근할 수 있다.
- **ServletContext**
  -  현재의 웹애플리케이션 내 모든 자원들을 같이 사용하는 공간이고 이 공간에 저장하면 모두가 사용 가능.
  
## ServletContextListener와 스프링 프레임워크
- ServletContextListener와 ServletContext를 이용하면 프로젝트가 실행될 떄 필요한 객체들을 준비하는 작업을 처리할 수 있다.
- 스프링 프레임워크를 웹 프로젝트에서 미리 로딩하는 작업을 처리할 때 ServletContextListener를 이용한다.

- HttpSession 관련 작업을 감시하는 리스너들을 등록할 . 수있음.
- HttpSessionListener나 HttpSessionAttributeListenr 등 등 이를 이용해서 HttpSession이 생성되거나 setAttribute()등의 작업이 이루어질 때 이를 감지함. 
- HttpSessionAttributeListener 인터페이스 구현
  -  이는 HTTP 세션의 속성 변화(추가, 수정, 삭제)를 감지하는 기능을 제공합니다.
attributeAdded(), attributeRemoved(), attributeReplaced()와 같은 메서드를 제공하는데, 여기서는 속성이 추가되었을 때(attributeAdded)만 사용하고 있습니다. 
    - HTTP 세션의 속성 변화(추가, 수정, 삭제)를 감지하는 기능