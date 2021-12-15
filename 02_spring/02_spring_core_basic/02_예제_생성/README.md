### 회원 도메인 실행과 테스트
- 클래스 다이어그램
- 객체 다이어 그램

```java
public class MemberServiceImpl implements MemberService {
    private final MemberRepository memberRepository = new MemoryMemberRepository();
    //추상화에 의존 + 구체화에 의존 → DIP위반
}
```

```java
public class OrderServiceImpl implements OrderService {
    private final MemberRepository memberRepository = new MemoryMemberRepository();
    //    private final DiscountPolicy discountPolicy = new FixDiscountPolicy();
    private final DiscountPolicy discountPolicy = new RateDiscountPolicy(); 
    
    // Order service 는 추상화 + 구체화 → 모두 의존 → DIP위반 
    // fix → rate 변경 시 order service의 코드도 변경이 되어야 한다. → OCP위반
}
```

### 관심사의 분리
- 가령 공연의 로미오, 줄리엣 역할을 할당하는건 연기자가 아니다.
- 로미오(배역-인터페이스) 디카프리오(배우-구현)가 줄리엣을 캐스팅한다 ?
    - 책임이 많아진다. → 다양한 책임을 가지고 있다.
- 배우는 대본을 통해 연기만 해야한다 상대 배우가 누구냐에 따라 상관없이
- 각 역할 캐스팅은 ***공연 기획자***가 해야한다 → ***기획자의 책임***

### AppConfig (가명)
- Application의 전체 동작 방식을 구성(config)하기 위해, 구현 객체를 ***생성*** 하고, ***연결***하는 책임을 가지는 별도의 객체 생성
- AppConfig 객체로 Injection 결과
  - DIP : 추상화에 의존하고 구체화는 전혀 모른다.
  - OCP : 확장에는 열려있고, 변경에는 닫혀있다.
  - ***Client코드 변경이 없다.***
  
### 흐름정리
- 새로운 할인정책 개발 적용의 문제
  - 새로개발한 정책 개발 → 클라이언트 코드인 주문 서비스 구현체 코드 변경
  - why ? 주문 서비스가 ***추상화에 의존 + 구체화에도 의존*** → DIP위반
  
- 관심사의 분리 → SRP 지키기
  - 구성자가 구성을 해준다.
  

### IcC, DI, Container
- framework가 호출을 대신 해준다.
- 구현 객체는 자신의 로직을 실행하는 역할만 담당 → 프로그램 제어 프름은 구성영역이 담당
- 의존관계 주입
  - 구현체는 인터페이스에만 의존한다. → 어느 구현체가 사용되는지 모른다.
  - 의존관계를 분리해서 생각해야 한다.  
    - ***정적인 클래스 의존관계***
      - 실행이 없이 분석 가능하다. (import, implements, 선언 등)
    - 실행 시점에 결정되는 ***동적인 객체 의존 관계***
      - 실제 구현체를 선택한다.
    
### IoC 컨테이너, DI컨테이너
- 주로 DI 컨테이너라 많이 쓰인다.

### 컨테이너의 호출 ?
- ApplicationContext → 스프링의 시작점
  - Spring Container
- 구성영역을 직접 작성하고 DI → 스프링 컨테이너를 활용으로 변경
- @Configuration 에 해당하는 구성정보를 사용
  - @Bean에 해당하는 메서드 모두 호출 → 반환된 객체 → 컨테이너 등록 → 등록된 객체 == Spring Bean
  
```java
public class MemberApp {
    ApplicationContext applicationContext = new AnnotationConfigApplicationContext(AppConfig.class);
    //applicationContext.getBean("메서드명", 타입.class);
    MemberService memberService = applicationContext.getBean("memberService", MemberService.class);
}
```
```
22:23:36.904 [main] DEBUG org.springframework.beans.factory.support.DefaultListableBeanFactory - Creating shared instance of singleton bean 'org.springframework.context.annotation.internalConfigurationAnnotationProcessor'
22:23:37.089 [main] DEBUG org.springframework.beans.factory.support.DefaultListableBeanFactory - Creating shared instance of singleton bean 'org.springframework.context.event.internalEventListenerProcessor'
22:23:37.092 [main] DEBUG org.springframework.beans.factory.support.DefaultListableBeanFactory - Creating shared instance of singleton bean 'org.springframework.context.event.internalEventListenerFactory'
22:23:37.094 [main] DEBUG org.springframework.beans.factory.support.DefaultListableBeanFactory - Creating shared instance of singleton bean 'org.springframework.context.annotation.internalAutowiredAnnotationProcessor'
22:23:37.097 [main] DEBUG org.springframework.beans.factory.support.DefaultListableBeanFactory - Creating shared instance of singleton bean 'org.springframework.context.annotation.internalCommonAnnotationProcessor'

//↑스프링 기본 생성 객체 ↓AnnotationContext로 가져온 객체

22:23:37.109 [main] DEBUG org.springframework.beans.factory.support.DefaultListableBeanFactory - Creating shared instance of singleton bean 'appConfig'
22:23:37.120 [main] DEBUG org.springframework.beans.factory.support.DefaultListableBeanFactory - Creating shared instance of singleton bean 'memberService'
22:23:37.142 [main] DEBUG org.springframework.beans.factory.support.DefaultListableBeanFactory - Creating shared instance of singleton bean 'memberRepository'
22:23:37.146 [main] DEBUG org.springframework.beans.factory.support.DefaultListableBeanFactory - Creating shared instance of singleton bean 'orderService'
22:23:37.151 [main] DEBUG org.springframework.beans.factory.support.DefaultListableBeanFactory - Creating shared instance of singleton bean 'discountPolicy'
```

- 코드가 더 복잡해진 것 같은데, 장점이?
  - '어마어마한 장점'에 대해 앞으로 알아가보자 
  
- 객체지향 원리 + 다형성만으로 DIP, OCP를 지킬 수 없는 한계 → AppConfig 생성 후 DI → 이후 DI의 주체를 스프링이 가져간다
  - 그것의 장점이 앞으로 남은시간동안 알아가도 모자라다.