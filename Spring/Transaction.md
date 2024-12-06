# transaction

### 특징
- 쪼갤 수 없는 업무의 최소 단위
- 한번에 성공하거나 한번에 실패하자.
- 즉 한몸으로 묶어 저장한다는거다. 한 트랜잭션 안에 모든 작업이 성공적으로 끝나야 그 작업들이 완료된 것이다.
- 여러 SQL을 사용해야 할 떄 한 번에 성공시키거나, 하나라도 실패하면 다 실패하는 기능
- start
- commit 
	- 다 성공 시
- rollback 
	- 실패 시 취소한다는 의미.	

### 트랜잭션 적용과 영속성 컨텍스트
- @readonly
    - 데이터의 변경 기능이 없고, 조회 기능만 있을 때 사용 가능 
    - select 쿼리만 사용한다면  옵션 쓸 수 있음 즉 조회 부분에 readinly

- @Transactional 순서
    - 아래에 있는 함수가 시작될 때 start transacrion
    - 함수가 예외나 에러 없이 잘 끝나면 commit 아니면 rollback

    // 주의사항
    - 체크 예외는 롤백이 일어나지 않는다.

- 영속성 컨텍스트란?
    - 테이블과 매핑된 entity 객체를 관리/보관하는 역할
    - 스프링에서는 트랜잭션을 사용하면 영속성 컨텍스트가 생겨나고, 트랜잭션이 종료되면 영속성 컨텍스트가 종료된다.

    - 능력
    1. 변경 감지
	    - 영속성 컨텍스트 안에서 불러와진 entity는 명시적으로 save하지 않더라도, 변경을 감지해 자동으로 저장된다.
        - 트랜잭션 사용 시 위에 있는 특징으로 인해서 save메소드를 호출하지 않아도 저장된다.
    2. 쓰기 지연
        - DB의 SQL을 바로 날리는 것이 아니라 트랜잭션이 commit될 때 모아서 한번만 날린다.
    3. 1차 캐싱
        - id를 기준으로 entity 기억
        - 이렇게 캐싱된 객체는 완전 동일함.
        ~~~ java
        @Transactional(readOnly = true)
        public void saveUsers() {
          userRepository.findById(1L);
          userRepository.findById(1L);
          userRepository.findById(1L);
        } 
        ~~~
        - 위 코드는 영속성 컨텍스트에 의해 1번만 select 쿼리를 날린다.
        나머지 두 번은 영속성 컨텍스트가 보관하고 있는 데이터를 활용 (1차 캐싱)




# 참고 자료 
- [인프런 강의 - 자바와 스프링 부트로 생애 최초 서버 만들기, 누구나 쉽게 개발부터 배포까지!](https://www.inflearn.com/course/%EC%9E%90%EB%B0%94-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-%EC%84%9C%EB%B2%84%EA%B0%9C%EB%B0%9C-%EC%98%AC%EC%9D%B8%EC%9B%90/dashboard)