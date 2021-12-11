H2DB 생성

이젠 DB와 connection된 상태의 테스트 코트 작성을 해야한다.

```java
@SpringBootTest
@Transactional //rollback을 해준다.
    //beforeeach 과정을 안거쳐도 된다.
class MemberServiceIntegrationTest {
    
    //으로 실행한다.
}
```


- Jdbc Template
    - 반복코드 제거
    - sql은 직접 작성


- JPA사용 
    - JPA lib 추가
    - JPA는 interface → 자바진영 표준기술 → 구현은 여러가지회사가 있다. ex) hibernate
    - JPA를 구현한 Hibernate
    
- JPQL → JPQL 객체지향 쿼리 언어
- JPA를 Spring으로 감싼게 있다 ? → Spring Data JPA
    