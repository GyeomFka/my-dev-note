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