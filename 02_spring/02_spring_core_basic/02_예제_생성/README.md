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