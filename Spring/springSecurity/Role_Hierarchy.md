# 계층 권한 : Role Hierarchy
- 권한 A, 권한 B, 권한 C가 존재하고 권한의 계층은 “A < B < C”라고 설정을 진행하고 싶은 경우 RoleHierarchy 설정을 진행할 수 있다.

## 변경된 RoleHierarchyImpl() 방식 사용 : fromHierarchy 메소드 활용
~~~ java
@Bean
public RoleHierarchy roleHierarchy() {

    return RoleHierarchyImpl.fromHierarchy("""
            ROLE_C > ROLE_B
            ROLE_B > ROLE_A
            """);
}
~~~

## 메소드 형식 : 명시적으로 접두사 작성

~~~ java
@Bean
public RoleHierarchy roleHierarchy() {

    return RoleHierarchyImpl.withRolePrefix("접두사_")
            .role("C").implies("B")
            .role("B").implies("A")
            .build();
}
~~~

## 메소드 형식 : 자동으로 ROLE_ 접두사 붙임

~~~ java
@Bean
public RoleHierarchy roleHierarchy() {

    return RoleHierarchyImpl.withDefaultRolePrefix()
            .role("C").implies("B")
            .role("B").implies("A")
            .build();
}
~~~

