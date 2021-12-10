### 1. 스프링 빈을 등록하고, 의존관계 설정하기
- View - Controller 연결관계 고려
- Controller - Service 의존관계
    - Service를 통한 1)Data조회, 생성 가능하도록 설계
    - Spring 컨셉에 맞게 설계 
 
- ***정형화된패턴***
    - Controller → 외부요청 받는다
    - Service → 비즈니스 로직 처리
        - Business와 관련된 naming으로 구성해야한다.
    - Repository → Database I/O 담당
        - Database I/O와 관련된 naming으로 구성해야한다.
    
#### 1.1. Dependency Injection이 필요할 때
```java
class MemberServiceTest {
    //MemberService memberService = new MemberService();
    //MemoryMemberRepository memberRepository = new MemoryMemberRepository();
    /*
     * 이미 memberService에는 repo객체가 있다. 
     * repo객체에서 static변수 활용했지만, 근본적으로 다른 인스턴스이다
     * */
    @BeforeEach
    void beforeEach() {
        memberService = new MemberService(new MemoryMemberRepository());
        //service입장에서 보면 직접 new를 하지 않고, 외부에서 D/I가 이루어 졌다. by developer
    }
}
```
- MemberServiceTest에서 MemberService와 Repository 객체가 필요하다
- 문제점 : service 객체 내부 repo객체 != this.repo객체

#### 1.2. Controller - Service - Repository 간의 의존성 설정을 DI로 해줘야 하는 이유
- 공통 기능을 가진 로직이므로 여러 인스턴스를 생성 할 필요가 없다.
- 하나의 인스턴스만 생성하여 공통으로 사용하는게 메모리 효율성이 좋다.

#### 1.3. Dependency Injection 동작원리
- 스프링 실행 → 스프링 컨테이너 생성 → @Controller, @Service, @Repository 인 객체들을 생성 → Container에서 관리 → 스프링 Bean이 된다.
- 생성자 + @Autowired 일때의 동작원리 → 컨테이너가 생성될 때 해당객체의 생성자 호출 → @Autowired는 Target객체를 주입시켜준다
    - Target객체에도 @Component가 있어야 한다.
- Dependency Injection 중 생성자 주입을 구현한 예시 → 스프링이 주체
- @Component → 스프링에게 관리권한을 넘겨준다 → 생성자 호출 시에 자동 주입
- 스프링은 컨테이너에 빈을 등록할 때, ***싱글톤***으로 등록한다. -> 메모리 절약
#### 1.4. 스프링 빈을 등록하는 2가지 방법
##### 1.4.1. Component Scan
- @Component를 갖고있는 @Controller, @Service, @Repository → Component scan

##### 1.4.2. @Configuration 객체 생성 - 자바코드로 등록
- @Configuration 객체 생성 → 이 때 Controller는 예외적으로 우선 Bean등록
- 정형화 되지 않거나, 상황에 따라 구현 클래스를 변경해야 하는 경우 위 방법을 사용

#### 1.5. Dependency Injection의 종류
- DI
    - 필드주입 → 필드에 @autowired 키워드를 달아준다 → 권장하지않는데, 생성자 주입 후 추가 로직 작성이 불가능하다.
    - setter주입 → 치명적인 단점 → 접근제어자로 인해 public하게 노출되어있어 문제가 될 가능성이 있다.
    - 생성자 주입 → 요즘 권장사항 → 초기 app 조립시점에서 견고하게 이루어진다.

#### 1.6 컴포넌스 스캔의 범위(기본값)
- main method → package 하위
- 동일하거나 다른 패키지는 콤포넌트 스캔 대상이 아님
- Service객체의 @Serivce를 제거하고 내부의 @autowired 키워드를 사용한다 ? → ***불가능하다*** 
  → 스프링이 해당객체를 Component Scan을 통해 관리하지 않기 때문에
- autowired 기능이 사용이 되려면 → 스프링 컨테이너에 등록된 빈들만 사용이 가능하다. 

#### 1.7. 구현체가 두 개 이상일 때
- MemberRepository 는 Interface
- Interface를 주입 받을때에 구현체가 두 개 이상일 경우 Component Scan시 오류발생

* keywork : 스프링 컨테이너, 콤포넌트, configure