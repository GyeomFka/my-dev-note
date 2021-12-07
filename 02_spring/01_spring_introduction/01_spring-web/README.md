### 1.스프링-웹 동작방식
1) 정적 컨텐츠
2) MVC + Template Engine
3) API

/*
스프링에서 웹이 동작하는 세 가지
1. 정적 컨텐츠 - 파일 그대로 클라에게 전달
    - 스프링에서 기본적으로 제공함. resources/static 에 아무 html
    - 프로그래밍은 하지 못한다.

- model, view, controller
2. MVC + template engine ex) jsp, php -> html그냥 주는것이 아닌
   프로그래밍 해서  html을 동적으로 바꿔준다
    - 렌더링 된 html파일을 클라이언트에게 전달한다.


3. API -> 다양한 클라이언트로 인해
   json 포맷(대부분이 사용json) 으로 클라이언트에게 전달해준다.
   <-> 프론트엔드와 협업에 용의
   <-> 서버끼리의 통신

-객체를 반환한다
*/