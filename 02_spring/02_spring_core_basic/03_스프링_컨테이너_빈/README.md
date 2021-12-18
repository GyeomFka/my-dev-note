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
- 타입으로 조회시 같은 타입의 스프링 빈이 둘 이상이면 오류가 발생한다. → 빈 이름을 지정
  - ac.getBeansOfType() → 타입으로 빈 조회
  
### 스프링 빈 조회 - 상속
- ***부모 타입 조회 → 자식 타입도 함께 조회***
  - Object 타입으로 조회를 하면, 모든 빈을 조회한다.
  

### 쓸 일은 없지만, 개념적으로 중요하다.
- 순수 자바 Application에서 가져다 쓸 일이 있긴 하다.
- 사용하진 않지만 중요하다. 
- 그래서 더 중요하다


### BeanFactory, ApplicationContext
- (interface)BeanFactory ← (interface)ApplicationContext ← (구현)AnnotationConfig, ApplicationContext
  - 모두를 스프링 컨테이너라 부른다.
  
### 스프링 빈 설정 메타정보 - Bean Definition
- 스프링은 어떻게 다양한 설정 방식을 지원할까 ?
  - by "BeanDefinition" - 추상화 - 역할과 구현의 개념을 잘 나눴다.
  - bean definition = 설정 메타정보
  
- 컨테이너는 위 메타정보를 기반으로 스프링 빈을 생성
- 스프링 컨테이너 - 추상화에만 의존 - 구현체는 따로
- 다양한 형태의 설정 정보를 B/D으로 추상화해서 사용한다.