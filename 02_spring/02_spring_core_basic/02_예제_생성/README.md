### 회원 도메인 실행과 테스트
- 클래스 다이어그램
- 객체 다이어 그램

```java
public class MemberServiceImpl implements MemberService {
    private final MemberRepository memberRepository = new MemoryMemberRepository();
    //추상화에 의존 + 구체화에 의존 → DIP위반
}
```