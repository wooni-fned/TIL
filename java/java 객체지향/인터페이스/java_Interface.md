# Interface

객체의 사용 규칙(호출 규칙)을 정의하는 문법

1. 인터페이스 정의

규칙1) 인터페이스에 선언되는 모든 메서드는 public 이다.

- 인터페이스에 정의하는 메서드는 호출 규칙이다.
- 규칙은 공개되어야 한다.

규칙2) 인터페이스에 선언되는 모든 메서드는 추상 메서드로 선언한다.

- 인터페이스에 선언하는 메서드는 호출 규칙을 정의한 것이다.
- 규칙은 클래스가 따라야 한다.
- 그래서 인터페이스에 선언되는 모든 메서드는 몸체를 구현하지 않는다.

```java
interface MyInterface {

  public abstract void m1();

  // public 을 생략할 수 있다.
  abstract void m2(); // public 이 생략된 것이다. (default) 아니다!

  // abstract 를 생략할 수 있다.
  public void m3();

  // public, abstract 모두 생략할 수 있다.
  void m4();

  // => private, protected, (default)는 없다.
  //  private void m5(); // 컴파일 오류!
  //  protected void m6(); // 컴파일 오류!
  void m7(); // 이건 (default) 아니라, public 이 생략된 것이다.

}
```

2. 인터페이스 구현

```java
abstract class MyInterfaceImpl implements MyInterface {
  @Override
  public void m1() {}

  // public 보다 접근 범위를 좁힐 수는 없다.
  @Override
  //  private void m2() {}  // 컴파일 오류!
  //  protected void m2() {} // 컴파일 오류!
  //  void m2() {} // 컴파일 오류!
  public void m2() {} // OK!

  // 인터페이스의 모든 메서드를 구현해야 한다.
  // 한 개라도 빠뜨린다면 concrete 클래스가 될 수 없다.
  // 추상 클래스로 선언해야 한다.
}

```

3. 인터페이스 사용

```java
public class Exam01 {

  public static void main(String[] args) {
    // 인터페이스 레퍼런스 선언
    MyInterface obj = null;

    // 인터페이스의 구현체 생성
    // - 인터페이스를 구현한 클래스의 객체라면
    // 언제든 해당 인터페이스의 레퍼런스에 담을 수 있다.
    obj = new MyInterfaceImpl();

    // 인터페이스는 규칙이기 때문에
    // 구체적인 구현 내용이 없다.
    // 그래서 인스턴스를 생성할 수 없다.
    //
    // obj = new MyInterface(); // 컴파일 오류!
  }

}
```

## 인터페이스 필드

인터페이스 필드 선언

인터페이스 필드는 public static final 이다.

- 인스턴스를 생성할 수 없기 때문에 인스턴스 필드를 선언할 수 없다.
- 규칙이기 때문에 무조건 public 이다.
- 인스턴스 필드가 아니기 때문에 값을 변경할 수 없다.
- public, static, final 을 생략할 수 있다.
- 인터페이스에 선언한 필드는 public static final 이기 때문에 바로 사용할 수 있다.
- 인터페이스 필드는 상수 필드이기 때문에 값을 변경할 수 없다.

```java
interface MyInterface2 {

  public static final int v1 = 100;

  // public, static, final 을 생략할 수 있다.
  static final int v2 = 200;
  public final int v3 = 300;
  public static int v4 = 400;

  int v5 = 500; // 모두 생략된 상태!
}
```

```java
public class Exam02 {
  public static void main(String[] args) {

    // 인터페이스에 선언한 필드는 public static final 이기 때문에 바로 사용할 수 있다.
    System.out.println(MyInterface2.v1);
    System.out.println(MyInterface2.v2);
    System.out.println(MyInterface2.v3);
    System.out.println(MyInterface2.v4);
    System.out.println(MyInterface2.v5);

    // 인터페이스 필드는 상수 필드이기 때문에 값을 변경할 수 없다.
    // MyInterface2.v1 = 111; // 컴파일 오류!
    // MyInterface2.v2 = 222; // 컴파일 오류!
    // MyInterface2.v3 = 333; // 컴파일 오류!
    // MyInterface2.v4 = 444; // 컴파일 오류!
    // MyInterface2.v5 = 555; // 컴파일 오류!
  }

}

```

## 기본메서드 (default method)

- 기존 프로젝트에 영향을 끼치지 않으면서 기존 규칙에 새 메서드를 추가할 때 유용한다.
- 인터페이스에서 미리 구현한 메서드이기 때문에 클래스에서 구현을 생략할 수 있다.
- 반대로 구현을 강제할 수 없다는 것이 단점이다.

```java
interface MyInterface3 {

  /*public static final*/ int a = 100;

  /*public abstract*/ void m1();

  default void m2() {}
  // 어차피 새 메서드는 새 프로젝트의 구현체가 오버라이딩 할 것이니
  // 여기에서는 자세하게 정의하지 않는다.
  // 다만 이 인터페이스를 구현한 예전 프로젝트에 영향을 끼치지 않으면서
  // 새 메서드를 정의할 때 사용하는 문법이다.

  default void m3() {
    System.out.println("MyInterface3.m3()");
  };
}

```java
class MyInterface3Impl implements MyInterface3 {

  // 추상 메서드는 반드시 구현해야 한다.
  @Override
  public void m1() {
    System.out.println("MyInterfaceImpl.m1()");
  }

  // default 메서드는 오버라이딩 해도 되고 안해도 된다.
  @Override
  public void m2() {
    System.out.println("MyInterfaceImpl.m2()");
  }

  // default 메서드는 오버라이딩 해도 되고 안해도 된다.
  // => m3() 는 이 클래스에서 오버라이딩을 하지 않았다.
}
```

## private 메서드

인터페이스 내부에서 사용할 메서드라면 private 접근 범위를 갖는 구현 메서드를 정의할 수 있다.

언제?

- 해당 기능을 m2()와 m3() 처럼 여러 메서드에서 사용해야 할 경우
  그 공통 코드를 다음과 같이 private 구현 메서드로 정의하면 될 것이다.

```java
interface MyInterface4 {

  void m1();

  default void m2() {
    System.out.println("MyInterface4.m2()");
    x();
  };

  default void m3() {
    System.out.println("MyInterface4.m3()");
    x();
  };

  private void x() {
    System.out.println("MyInterface4.x()");
  }
}
```

인터페이스 구현

```java
class MyInterface4Impl implements MyInterface4 {
  @Override
  public void m1() {

    //    m2(); // 현재 클래스의 m2() 메서드

    // 인터페이스에 선언된 오버라이딩 전의 default 메서드를 호출하고 싶다면,
    super.m2(); 
    // 수퍼 클래스(Object)에서 m2()를 찾아 올라간다. Object에는 m2()가 없기 때문에 컴파일 오류!
    // MyInterface4.m2(); // m2()는 인스턴스(non-static) 메서드이기 때문에 인터페이스 이름으로 직접 호출 불가!
    MyInterface4.super.m2();

    System.out.println("MyInterface4Impl.m1()");
  }

  @Override
  public void m2() {
    System.out.println("MyInterface4Impl.m2()");
  }
}
```

## static 메서드

인터페이스도 클래스처럼 static 메서드를 정의할 수 있다.

- 접근 범위는 기본이 public 이다. 다른 접근 범위를 가질 수 없다.
- public 을 생략할 수 있다.

```java
interface MyInterface5 {
  // 다음 메서드는 public 이 생략된거지, (package-private) 접근 범위가 아니다.
  static void m1() {
    System.out.println("MyInterface5.m1()");
  }
}

class Parent {
  static void m2() {
    System.out.println("Parent.m2()");
  }
}

class MyInterface5Impl extends Parent implements MyInterface5 {

}
```

```java
public class Exam05 {
  public static void main(String[] args) {
    // 인터페이스의 스태틱 메서드 호출하기
    MyInterface5.m1();

    // 클래스의 스태틱 메서드 호출하기
    Parent.m2();

    MyInterface5Impl obj = new MyInterface5Impl();

    // 수퍼 클래스에 정의된 static 메서드는,    
    // => 다음과 같이 서브 클래스를 통해 호출할 수 있다.
    MyInterface5Impl.m2();

    // => 또는 다음과 같이 인스턴스 레퍼런스를 통해 호출할 수 있다.
    // => 물론 스태틱 메서드는 가능한 그 메서드가 선언된 클래스 이름으로 호출하는 것이 좋다.
    obj.m2(); 

    // 그러나, 인터페이스에 정의된 static 메서드는,
    // => 인터페이스를 구현한 클래스를 통해 호출할 수 없다.
    //    MyInterface5Impl.m1(); // 컴파일 오류!

    // => 또한 구현체의 레퍼런스를 통해서도 호출할 수 없다.
    //    obj.m1(); // 컴파일 오류!
  }

}
```