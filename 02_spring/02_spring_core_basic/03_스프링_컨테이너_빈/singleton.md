### 싱글톤
- 객체가 JVM내부에 하나만 존재한다.
1) Web Application에서 싱글톤이 많이 사용되나 ?
2) 싱글톤 패턴에 관하여
3) 싱글톤 컨테이너
4) 주의점
5) @Configuration과 싱글톤

### Web Application과 싱글톤
- 스프링 : 기업용 온라인 서비스 기술 지원을 위해 탄생
- 웹 App은 보통 여러 고객이 ***동시에 요청***을 한다.
- 요청이 올 떄 마다 new를 한다 ? → 문제점
```java
public class SingletonTest {
    @Test
    void 스프링_없는_순수한_DI컨테이너() {
        AppConfig appConfig = new AppConfig();
        //고객의 조회1 : 호출할 떄 마다 객체를 생성
        MemberService memberService1 = appConfig.memberService();

        //고객의 조회2 : 호출할 떄 마다 객체를 생성
        MemberService memberService2 = appConfig.memberService();

        System.out.println("memberService1 = " + memberService1);
        System.out.println("memberService2 = " + memberService2);
        /*
        * memberService1 = hello.core.member.MemberServiceImpl@65d09a04
        * memberService2 = hello.core.member.MemberServiceImpl@33c911a1
        * */
    }
}
```
- 웹 → 요청이 많다 → 요청 만큼의 객체가 생성, 소멸 → 메모리 낭비가 심하다.
- ***해결*** : 객체가 딱 1개만 생성 + 공유가 되도록 설계

### about singleton pattern
- (하나의 JVM, 자바 서버 내부)클래스의 인스턴스가 딱 1개만 생성되는것을 '보장'한다.
- 비유 : 인스턴스 생성 비용 1000, 단순 get의 비용 1
- 스프링 컨테이너는 기본적으로 객체를 싱글톤 패턴으로 관리해준다. 

### 싱글톤의 단점을 커버 한 싱글톤 컨테이너
#### 실글톤 컨테이너 

### 싱글톤 주의점 → 이거 따로 정리 해야함!!
- 상태를 유지하게 설계하면 안된다.
    - 무상태로 설계해야 한다.
    - 예시코드 (멀티스레드 환경에서의)
  
### @Configuration → 싱글톤을 위해 존재한다...?
- @Bean memberService → new MemoryMemberRepository() 호출
- @Bean orderService → new MemoryMemberRepository() 호출
- MemoryMemberRepository 두 번 호출 → 스프링이 용뺴는 재주가 있는것도 아니고 → 싱글톤이 깨지는거 아닌가요 ?

### @Configuration, Byte code
- bean.getClass() = class hello.core.AppConfig$$EnhancerBySpringCGLIB$$721f06a6
- AppConfig@CGLIB 라이브러리를 통한 임의의 클래스
- @Configuration 없이 @Bean만 등록된다면 ?
  - 혼돈의 카오스