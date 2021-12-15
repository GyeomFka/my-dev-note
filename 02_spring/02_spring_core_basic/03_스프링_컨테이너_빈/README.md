### 스프링 컨테이너가 생성되는 과정
```java
public class MemberApp {
    ApplicationContext applicationContext = new AnnotationConfigApplicationContext(AppConfig.class);
    //applicationContext.getBean("메서드명", 타입.class);
    MemberService memberService = applicationContext.getBean("memberService", MemberService.class);
}
```
- ApplicationContext == 스프링 컨테이너 == Interface → 다형성 적용
- 1)컨테이너가 객체 생성 → 2)의존관계 설정
    - 실행 시점에 결정되는 ***동적인 객체 의존 관계***
    
### 컨테이너에 등록된 빈 조회
  
### 스프링 빈 조회 - 기본
- ac.getBean(빈이름, 타입)
- ac.getBean(타입)