### Optional class
 [TCP School](http://www.tcpschool.com/java/intro)

---

#### java.util.Optional<T> 클래스
java.util.Optional<T> 클래스
Optional<T> 클래스는 Integer나 Double 클래스처럼 'T'타입의 객체를 포장해 주는 래퍼 클래스(Wrapper class)입니다.

따라서 Optional 인스턴스는 모든 타입의 참조 변수를 저장할 수 있습니다.



이러한 Optional 객체를 사용하면 예상치 못한 NullPointerException 예외를 제공되는 메소드로 간단히 회피할 수 있습니다.

>즉, 복잡한 조건문 없이도 널(null) 값으로 인해 발생하는 예외를 처리할 수 있게 됩니다.

---

#### 객체 생성
- Optional.of(), Optional.ofNullable() 메소드를 활용하여 Optional객체를 생성할 수 있다.

추후 공부하면서 다시 정리 ㄱㄱ