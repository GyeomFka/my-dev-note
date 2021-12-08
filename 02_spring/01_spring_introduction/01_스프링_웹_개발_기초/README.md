### 1. View 환결성정
- static → welcome page 만들어보기
   - resources/static/index.html 생성 후 서버 시작 → welcompage 기능제공
   
```java

@Controller
public class HelloController {
   
   @GetMapping("hello")
   public String hello(Model model) {
      model.addAttribute("data", "data from controller");
      return "hello";
   }
   
}
```
- 실행 : http://localhost:8080/hello → thymeleaf template engine 동작 확인
- 컨트롤러에서 문자열을 return하면 viewResolver가 해당 화면을 찾아 처리한다.
   - resources:templates/ + {viewName} + .html
   

### 2. gradle을 활용하여 빌드하고 실행하기
- 해당프로젝트 dir로 이동한다
- gradlew 명령어를 이용해 build한다
- build/libs dir이 생긴다.
- java -jar xxx-0.0.1-SNAPSHOT.jar 실행
- localhost:8080 확인 
> 실제 서버 배포시 위 방식을 활용하여 서버로 전송

### 3. Spring - Web : 기초
1) static contents → html파일을 그대로 client에게 전달
   - 스프링 부트 정적 컨텐츠 기능
   - 요청받은 내용이 controller에 없어, 바로 전달한다. 
   - 별도 로직 처리 불가능

2) MVC + Template Engine
```java
@Controller
public class HelloController {

    @GetMapping("hello-mvc")
    public String helloMvc(@RequestParam("name") String name, Model model) {
        model.addAttribute("name", name);
        return "hello-template";
    }
}
```
- viewResolver + model(name:name) → thymeleaf 템플릿 엔진 처리
- 렌더링 된 html파일을 client에게 전달한다.

3) API
```java
@Controller
public class HelloController {

    @GetMapping("hello-string")
    @ResponseBody // → viewResolver를 사용하지 않음
    public String helloString(@RequestParam("name") String name) {
        return "hello " + name;
    }
}
```
- @ResponseBody 
    - Http프로토콜 Body부분에 data를 직접 주입 하겠다.
    - viewResolver를 사용하지 않음
    
- http://localhost:8080/hello-string?name=aksrua → 단순 문자열만 출력 확인

```java
@Controller
public class HelloController {

    @GetMapping("hello-api")
    @ResponseBody // → viewResolver를 사용하지 않음
    public String helloApi(@RequestParam("name") String name) {
        Hello hello = new Hello();
        hollo.setName(name);
        return hello;
    }
    
    static class Hello {
        private String name;
        public getter();
        public setter();
    }
}
```
- 다양한 client로 인해(web, mobile ...) 통일된 format으로 전달하는 서버를개발
- controller에서의 ***ResponseBody + 객체반환*** ? json반환 기본값
    - {"key" : "value"} 형태로 client에게 전달
    - front-end 개발과 협업에 적합
    - 서버간 통신 적합

#### 3.1. ResponseBody 사용원리
- Http Body부에 내용 직접 반환
- ***viewResolver 대신 HttpMessageConverter가 동작***