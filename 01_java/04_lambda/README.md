### lambda 관련
- 함수형 interface == interface중 하나의 method를 가지고 있는 interface
    - ex) Runnable 
- 자바는 method만 매게변수로 전달 할 방법이 없다. -> 인스턴스만 전달이 가능하다.
- "method만 전달하기위해" 태어난 개 -> 람다 표현식
```java
public class LamdaExam {
	public static void main(String[] args) {
		new Thread(new Runnable() {
            @Override
            public void run() {
				
            }
        }).start();
    }
}
```
- thread생성자에 존재하는 run이라는 메서드 실행
- run이라는 method를 가지고있는 runnable을 객체로 만든 후 전달 -> 실질적으로 메서드를 전달.

### 표현식 활용
```java
public class LamdaExpress {

  public static void main(String[] args) {
    new Thread(() -> {
      for (int i = 0; i < 10; i++) {
        System.out.println("hello" + i);
      }
    }).start();
  }
}
```
- 객체 자체를 직접 생성할 필요가 없다
  - -> `new Runnable()` -> `()`
  - () -> {} : 람다식
  - 람다식 == 익명 method
  - jvm은 thread 생성자를 보고 해당 람다식을 보고 대상을 추론한다
      - api상 runnable interface를 받는다 
      
### 람다식 문법
(매개변수 목록) -> {실행문}

