# final

변경될수 없는 이라는 의미를 가지고 있으며 `상수`의 개념으로 생각하면 된다.

- 사용가능한 곳
  - `클래스`
    - 변경될 수 없는 클래스, 확장될 수 없는 클래스가 된다. 다른클래스의 조상이 될 수 없다.
  - `메서드`
    - 오버라이드를 통해 재정의 될 수 없다.
  - `멤버변수`
  - `지역변수`
    - 변수 앞에 붙으면 값을 변경할 수 없는 상수가 된다.

## 클래스에 붙이는 경우

클래스에 final 을 붙이면 이 클래스의 서브 클래스를 만들 수 없다.

- 서브 클래스의 생성을 방지하여

기존 클래스를 대체하지 못하도록 할 때 사용한다.

- 예)
 java.lang.String

```java
final class A {

}

// final 클래스를 상속 받을 수 없다.
public class Exam0110 // extends A
{

}
```

## 메서드에 붙이는 경우

```java
class B {
  // 메서드에 final 을 붙이면 서브 클래스에서 오버라이딩 할 수 없다.
  // - 서브 클래스에서 변경하면 안되는 메서드인 경우에 사용한다.
  // - 예)
  //   - 보안에 관련된 일을 하는 메서드
  //   - 템플릿 메서드 디자인 패턴에서처럼
  //     전체적인 작업 흐름을 정의한 메서드의 경우
  //     서브 클래스의 오버라이딩을 막는 것이 좋다.
  //
  final void m1() {
    System.out.println("B.m() 호출!");
  }

  void m2() {

  }
}
public class Exam0210 extends B {

  // final 메서드는 오버라이딩 불가!
  //
  //  @Override
  //  void m1() {
  //
  //  }

  // 일반 메서드는 오버라이딩 가능!
  @Override
  void m2() {

  }

}

```

## 변수에 붙이기

### 1. 필드에 붙이기

```java
class C {
  // 필드에 final 을 붙이면 상수 필드가 된다.
  // 생성자에서 초기화시켜야 한다.
  //
  final int v1;

  public C() {
    v1 = 100;
    // v1 = 101; // final 필드는 딱 한 번만 값을 설정할 수 있다.
  }

  public void m1() {
    // 상수 필드는 값을 변경할 수 없다.
    // v1 = 200; // 컴파일 오류!
  }
}


public final class Exam0310 {
  public static void main(String[] args) {
    C c = new C();
    System.out.println(c.v1);
  }
}
```

### 2. 변수에 붙이기

```java
class D {
  // 변수 초기화 문장으로 값을 초기화시킬 수 있다.
  // => 변수 초기화 문장은 컴파일 될 때 생성자로 복사되기 때문이다.
  final int v1 = 100;


  public D() {
    // 초기화 문장에서 값을 설정했으면,
    // 생성자에서 다시 값을 설정할 수 없다.
    // 왜?
    // - 초기화 문장은 결국 컴파일할 때
    //   생성자의 첫 번째 문장으로 옮겨지기 때문이다.
    //    v1 = 200; // 컴파일 오류!
  }
}
public final class Exam0320 {
  public static void main(String[] args) {
    D d = new D();
    System.out.println(d.v1);
  }
}
```

### 3. 인스턴스 초기화

```java
class E {
  // 인스턴스 초기화 블록에서 값을 초기화시켜도 된다.
  final int v1;

  // 초기화 블록의 코드 또한 생성자에 복사된다.
  {
    v1 = 200; // OK!
    //    v1 = 300; // 컴파일 오류!
  }

}

public final class Exam0330 {
  public static void main(String[] args) {
    E e = new E();
    System.out.println(e.v1);
  }
}
```

### 4. 스태틱 상수 필드

```java
class F {
  // 상수 필드는 인스턴스 마다 개별적으로 관리하지 않기 때문에
  // 보통 스태틱 필드(클래스 필드)로 만든다.
  // 공개할 경우 public 으로 선언한다.
  //
  public static final int v1 = 100;

  // 스태틱 상수 필드는 스태틱 블록에서 초기화시킬 수 있다.
  public static final int v2;
  static {
    v2 = 200;
  }

}

public final class Exam0340 {
  public static void main(String[] args) {
    System.out.println(F.v1);
    System.out.println(F.v2);
  }
}
```

### 5. 로컬변수에 붙이기

```java
public final class Exam0410 {

  public void m1() {
    // 로컬 변수에 final을 붙이면 값을 변경할 수 없는 상수로 사용된다.
    final int a = 100;

    // final 로컬 변수는 값을 변경할 수 없다.
    //    a = 200; // 컴파일 오류!

    // 변수를 선언할 때 값을 초기화시키지 않고,
    final int b;

    // 다음에 초기화시킬 수 있다.
    b = 100;

    // 일단 한 번 변수의 값이 초기화되면 변경할 수 없다.
    //    b = 200; // 컴파일 오류!

  }
}
```

### 6. 파라미터에 붙이기

```java
class G {

  public void m1(final int a) {
    // 파라미터는 메서드가 호출될 때 외부의 값을 받는 용도의 변수다.
    // 메서드 안에서 파라미터 값을 임의로 변경하게 되면
    // 처음 받은 파라미터 값을 사용하지 못하는 상황이 발생한다.
    // 그래서 이런 상황을 피하고자,
    // 보통 실무에서 파라미터를 final로 선언한다.
    //
    // a = 200; // 컴파일 오류!

    System.out.println(a);
  }
}


public final class Exam0510 {
  public static void main(String[] args) {
    G g = new G();
    g.m1(100);
    g.m1(200);
    g.m1(300);
  }
}
```