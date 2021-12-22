#### Controller 생성
- 화면연결
- Controller 우선
```java
@Controller
public class HomeController {
    @GetMapping("/")
    public String home() {
        return "home";
    }
}
```
- "/" welcome페이지가 아닌이유 ? → Spring의 우선순위 
    - 요청 후 탐색 순위 
      1. 스프링 컨테이터 내부 매핑
      2. 스태틱 화면