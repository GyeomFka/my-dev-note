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
