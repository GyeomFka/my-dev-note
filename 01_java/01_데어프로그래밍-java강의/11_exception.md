### 1.Exception
- 컴파일 시점 exception → Exception을 상속한다.
    - java가 catch가 가능하다.
    - 컴파일 자체가 안된다.
- 런타임 시점 excpetion → RuntimeException을 상속한다.
    - java는 모르지만, 개발자가 알아야 한다.
    - 컴파일은 되지만, 프로그램 실행 도중 오류가 발생한다. → 프로그램이 강제로 종료된다.
    - catch의 역할은 try(시도)를 하다가 예외가 발생하면 어떻게 처리할지 정의하는 영역

- ex) thread.sleep(1000) → InterruptedException 컴파일 시점에 잡아줘야 한다.
    - InterruptedException 예시 : 강의중 화재가 발생 → 화재를 제압한다(***예외처리***)
    - cpu가 1000ms off상태 → 방해 가능성 (os에 오류) → 오류를 해결해야한다.

- [코드보기](https://github.com/GyeomFka/java-dare/blob/master/src/main/java/ch07/ExceptionEx01.java)
