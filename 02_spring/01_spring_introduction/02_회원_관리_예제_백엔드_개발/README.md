### 1. 회원관리 예제 - 백엔드 개발
- Controller
- Domain → Database에 저장되는 객체
  - ex) 회원객체 
- Service → Domain을 활용한 Business logic이 동작하도록 구현 한 계층
  - ex) 회원은 중복가입이 허용되지 않는다.
- Repository → Database에 접근 + Domain객체를 database에 저장하고 관리  

#### 1.1. JUnit test framework 활용
- 테스트 코드는 메소드 순서가 보장되어있지 않다
- 순서에 의존하여 작성하면 안된다.
- 순서에 상관없이 설계를 해야한다.  
- 매 테스트마다 객체를 초기화 해줘야 한다.

#### 1.2. 회원 Domain과 Repository만들기
- [Code link](https://github.com/GyeomFka/spring-I)

```java
public class MemoryMemberRepository implements MemberRepository{
    private static Map<Long, Member> store = new HashMap<>();
    private static long sequence = 0L;
}
```
> 공유변수 Type관련 추가 학습자료
> - 동시성 문제가 일어날 가능성이 높음
> - HashMap → ConcurrentcyMap 사용 권장
> - long → AtomicLong 사용 권장

#### 1.3. 회원 Service 개발
- 회원 Repo와 Domain을 활용해서 Business 로직을 작성한다.
- Optional 사용 문법 간소화 코드 사용법 → 메소드 추출 
- 서비스 method명을 통해 repo 와 비교점
  - repository : 단순 DB조회 ㄴ느낌
  - service : 비즈니스 냄새가 남
  
- service 영역은 business용어의 냄새가 많이 나야한다 → 누구든 알아볼 수 있도록
  - 비즈니스에 의존적인 설계
- repo는 db i/o 에 가깝도록 설계  

- MemberServiceTest class에서 바라본 
  - MemberService의 MemeberRepo 객체
  - MemberServiceTest의 MemberRepo 객체
  - 생성자 주입 → Dependency Injection
  
