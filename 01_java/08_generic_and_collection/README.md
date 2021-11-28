### 1.generic 
- A라는 클래스를 만든다고 가정
    - 상황에 따라, 문자열을 저장 혹은 숫자를 저장
    
```java
class A {
    Object data;
}

public class GenericEx {
    public static void main(String[] args) {
        A a = new A();
        a.data = 1;
        System.out.println(a.data);
        
        A a2 = new A();
        a2.data = "string";
        System.out.println(a2.data);
    }
}
```

- 왜 사용하나?
  - 클래스를 생성할 때, 타입이 정해져 있지 않아 Object를 활용하지 않기 위해 타입을 강제하도록 도와준다.
  - [코드보기](https://github.com/GyeomFka/java-dare/blob/master/src/main/java/ch06/GenericEx01.java)
  
#### 1.1. 와일드 카드 → 제네릭 고급
- 메서드의 리턴을 '몰라' ?
  - <? extends Object> : 오브젝트를 상속하고 있는 모든 클래스 들 중 하나
  - ? → 모든 클래스
  - 예제 확실하게 이해 해야함
  - [코드보기](https://github.com/GyeomFka/java-dare/blob/master/src/main/java/ch06/GenericEx03.java)
  
### 2. collection
- 단점 : data reading이 비효율 적이다.
- ArrayList <int> c1 = new ArrayList<>();
  - int, double, char, boolean → 기본자료형(값)
  - String, 클래스 → 래퍼런스 자료형(주소)
  - ***래핑클래스*** : Integer, Double, Character, Boolean
- 호출할때 주의점
  - for(int i=0; i<c1.size(); i++) {}
  - c1.size() 를 계속호출하게 된다
  - size = c1.size(); → c1.size를 한번만 호출하게 한다.