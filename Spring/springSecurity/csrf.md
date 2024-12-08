# CSRF

- CSRF(Cross-Site Request Forgery)는 요청을 위조하여 사용자가 원하지 않아도 서버측으로 특정 요청을 강제로 보내는 방식이다. (회원 정보 변경, 게시글 CRUD를 사용자 모르게 요청)

## 개발 환경에서 csrf disable()
-  배포 환경에서는 csrf 공격 방지를 위해 csrf disable 설정을 제거하고 추가적인 설정을 진행해야 한다.
~~~ java
  @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception{

        http
                .csrf((auth) -> auth.disable());


        return http.build();
    }
~~~

## 배포 환경에서 설정
- security config 클래스에서 csrf.disable() 설정을 진행하지 않으면 자동으로 enable 설정이 진행된다. 
- enable 설정시 스프링 시큐리티는 CsrfFilter를 통해 POST, PUT, DELETE 요청에 대해서 토큰 검증을 진행한다.

- post 요청 시(mustache 기준)
~~~ html
<form action="/loginReceiver" method="post" name="loginForm">
    <input type="text" name="username" placeholder="아이디"/>
    <input type="password" name="password" placeholder="비밀번호"/>
    <input type="hidden" name="_csrf" value="{{_csrf.token}}"/>
    <input type="submit" value="로그인"/>
</form>
~~~
- ajax 요청시
  - head 요소
~~~ html
<meta name="_csrf" content="{{_csrf.token}}"/>
<meta name="_csrf_header" content="{{_csrf.headerName}}"/>
~~~

## GET 방식 로그아웃을 진행할 경우 설정 방법
- csrf 설정시 POST 요청으로 로그아웃을 진행해야 하지만 아래 방식을 통해 GET 방식으로 진행할 수 있다.

 ~~~ java
@Bean
public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception{

    http
            .logout((auth) -> auth.logoutUrl("/logout")
                    .logoutSuccessUrl("/"));

    return http.build();
}
~~~

- logoutcontroller
~~~ java
@Controller
public class logoutController {

    @GetMapping("/logout")
    public String logout(HttpServletRequest request, HttpServletResponse response) throws Exception {

        Authentication authentication = SecurityContextHolder.getContext().getAuthentication();
        if(authentication != null) {
            new SecurityContextLogoutHandler().logout(request, response, authentication);
        }

        return "redirect:/";
    }
}
~~~

## 오류 발생 시
- mustache에서 csrf 토큰 변수 오류 발생시 아래 구문을 변수 설정 파일에 추가
- application.properties
~~~
spring.mustache.servlet.expose-request-attributes=true
~~~

## API 서버의 경우 csrf.disable() ?
- 앱에서 사용하는 API 서버의 경우 보통 세션을 STATELESS로 관리하기 때문에 스프링 시큐리티 csrf enable 설정을 진행하지 않아도 된다.


## 참고 자료
- 개발자 유미 youtube