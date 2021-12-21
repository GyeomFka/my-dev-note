#### 다양한 의존관계 주입 방법
- 생성자 주입
    - 호출시점에 딱 1번만 호출 ***보장***
    - 불변, 필수 → final → 필수적으로 값이 있어야 함!
    - 생성자가 딱 1개만 있을 때 @Autowired생략이 가능하다.
- setter 주입
    - setMethod + @Autowired → 의존관계 주입
    - 선택적, 변경 가능
    - setMethod를 public하게 두어야 한다 : 문제점
- 필드 주입
- 일반 메서드 주입

#### 생성자 주입 권장
- why ? 
  - 순수 자바 언어의 특징을 잘 살리는 방법이기도 함
  - 불변 : Application 시작 ↔ 종료까지 바뀌지 않는다.
  - final 키워드로 실수 방지 : 초기화 강제성 부여
  
#### 롬복
- 불변성이 개발에 중요하다.
- 필드 주입처럼 편리하게 사용하는 방법
- 롬복 추가 build.gradle 생성
- intellij plugin설치 → intellij annotation processing 체크
- @RequiredArgsConstructor //final -> 키워드로 생성자를 만들어준다.

#### 조회 빈이 2 개 
```java
class Sample{
    @Autowired //생성자 하나일 때, 생략가능
    public OrderServiceImpl(MemberRepository memberRepository, DiscountPolicy discountPolicy) {
        this.memberRepository = memberRepository;
        this.discountPolicy = discountPolicy;
    }
}
```
- DiscoungPolicy의 타입
  - fix
  - rate
  - 둘 다 빈 등록이 될 때 : 오류 메시지
- 하위 타입을 지정하면, DIP위배
