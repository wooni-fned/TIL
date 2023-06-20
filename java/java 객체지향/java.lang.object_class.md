# 상속

## java.lang.object

- 모든 자바 클래스의 최상위 클래스
- 클래스를 정의할 때 super클래스를 지정하지 않으면 컴파일러가 object를 super클래스로 자동 지정한다.

- class A {...}
- class A extends B {...}

- Object의 메소드들
  - equals()
  - hashcode()
  - toString()

```java
ex) public class A {
  public int plus (int a, int b) {
    return a + b;
  }
}

  public class B extends A {
    public int minus (int a, int b) {
      return a - b;
    }
  }

public class test {
    public static void main(String[] args) {
      B b1 = new B();
      System.out.println(b1.plus(100, 300));
      System.out.println(b1.minus(100, 300));      
    }
  }
```

이처럼 B클래스에 A클래스에 상속을 해주면 A클래스의 래퍼런스 변수를 사용할 수 있다.

- 컴파일러는 실행관점이 아니라 문장의 옳고 그름만 판단한다.
- 실행관점에서는 JVM에서 실행하면서 확인할 수 있다.