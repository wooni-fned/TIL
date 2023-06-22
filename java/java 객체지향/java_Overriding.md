# Overriding

- `상속`받은 `클래스에 맞게 재정의`한것
- super클래스의 메소드를 sub클래스에서 자신의 역할과 목적에 맞게 재정의

## Specialization (특수화/ 전문화)

- 가장 많이 사용하는 방법으로 수퍼 클래스를 상속 받아 서브 클래스를 만드는 것이다.
- 수퍼클래스에 새 특징을 추가하거나 새 기능을 추가하여 더 특별한 일을 수행하는 서브클래스를 만든다.
- 이런 상속을 "특수화/전문화(specialization)"이라 부른다.

## Generalization (일반화/표준화)

- 리팩토링 과정에 수행하는 방법이다.
- 서브클래스들의 공통 메소드를 추출하여 수퍼클래스를 정의하는 방법을 말한다.
- 이런 상속을 "일반화/표준화(generalization)"이라 부른다.


### Generalization 예제

Sedan 클래스와 Truck 클래스의 공통 메소드를 추출하여 Car라는 클래스를 정의하고,
두 클래스는 이렇게 새로 만든 Car 클래스를 상속 받도록 한다.

Sedan.java

```java
public class Sedan {
  public void start() {
    System.out.println("시동 건다!");
  }
  public void shutdown() {
    System.out.println("시동 끈다!");
  }
  public void run() {
    System.out.println("쌩쌩 달린다.");
  }
  public void doSunroof(boolean open) {
    if (open) {
      System.out.println("썬루프를 연다.");
    } else {
      System.out.println("썬루프를 닫는다.");
    }
  }
}
```

Truck.java

```java
public class Truck {
  public void launch() {
    System.out.println("시동 건다!");
  }
  public void stop() {
    System.out.println("시동 끈다!");
  }
  public void go() {
    System.out.println("덜컹 덜컹 달린다.");
  }
  public void dump() {
    System.out.println("짐을 내린다.");
  }
}

```

Exam01.java

```java
public class Exam01 {

  public static void main(String[] args) {

    Sedan s = new Sedan();
    Truck t = new Truck();

    s.doSunroof(true);
    t.dump();
  }

}
```

이렇게 Sedan과 Truck 클래스를 만들어 쓰다가 보니 두 클래스 사이에 공통 코드가 발견되었다.
유지보수를 쉽게하기 위해 공통 코드를 추출하여 중복 코드를 없앨 필요가 있다.

다음은 공통코드를 Car 클래스에 추출하고 상속받게 하였다.

```java
public class Car {

  public Car() {
    super();
  }

  public void start() {
    System.out.println("시동 건다!");
  }

  public void shutdown() {
    System.out.println("시동 끈다!");
  }

  public void run() {
    System.out.println("달린다.");
  }

}
```

```java
public class Sedan extends Car {
  public void run() {
    System.out.println("쌩쌩 달린다.");
  }

  public void doSunroof(boolean open) {
    if (open) {
      System.out.println("썬루프를 연다.");
    } else {
      System.out.println("썬루프를 닫는다.");
    }
  }
}

public class Truck extends Car {

  public void run() { // Overriding
    System.out.println("덜컹 덜컹 달린다.");
  }

  public void dump() {
    System.out.println("짐을 내린다.");
  }
}

public class Exam01 {

  public static void main(String[] args) {
    // Sedan과 Truck 두 클래스의 공통점을 추출하여 수퍼 클래스를 정의한 후에
    // 두 클래스의 사용법이 크게 바뀌는 것은 아니다.
    // 단지 유지보수가 좋아질 뿐이다.
    Sedan s = new Sedan();
    s.run();

    Truck t = new Truck();
    t.run();


    // 이렇게 Car 클래스가 존재하면 
    // 어떤 사람은 Car 클래스를 사용하려고 시도할 것이다.
    // 문제는, Car 클래스의 목적이 소스 코드를 보다 쉽게 관리하기 위해 만든 클래스이지,
    // 직접 사용하려고 만든 클래스가 아니다.
    // 그럼에도 불구하고 다른 개발자가 다음과 같이 Car 클래스를 사용한다면
    // 이를 막을 수 없다.
    Car c = new Car();
    // 사실 Car 클래스는 Sedan과 Truck에 공통으로 들어가는 코드를 
    // 좀 더 쉽게 관리하기 위해 추출하여 클래스로 만든 것이다.
    // 이렇게 직접 사용하려고 만든 클래스가 아니다.
    // 그럼에도 불구하고 위의 코드처럼 
    // Car 클래스의 인스턴스를 만드는 것을 막을 수가 없다.
    // 이것을 막는 문법이 "추상클래스" 이다.
  }

}
```

여러 클래스에 공통으로 들어 가는 기능이나 필드가 있다면
유지보수가 쉽도록 별도의 클래스로 추출한다.
그리고 상속 관계를 맺는다.

- Sedan과 Truck 사이에 공통 필드와 메서드가 있다.
- 공통 기능을 추출하여 별도의 클래스를 정의하는 것을 "일반화(generalization)"라 한다.

Sedan과 Truck의 공통 기능인
`start()`, `shutdown()`, `run()` 메서드를 추출하여
Car 클래스를 만들고 Sedan과 Truck은 이 클래스의 서브클래스가 된다.

`start()`와 `shutdown()` 은
`Sedan`이나 `Truck` 모두 같은 작업을 수행하기 때문에 상속 받은 것을 그대로 사용하며 되지만,
`run()`은 `Sedan`과 `Truck`이 서로 다르게 작업하기 때문에 `재정의(오버라이딩)` 해야 한다.

## 메서드 오버로딩 (overloading)

- 파라미터의 타입이나 갯수가 다르면 같은 이름의 메서드를 생성할 수 있는것

```java
 static public void m() {
    System.out.println("m()");
  }

  static public void m(int a) {
    System.out.println("m(int)");
  }

  static public void m(String a) {
    System.out.println("m(String)");
  }

  static public void m(String a, int b) {
    System.out.println("m(String,int)");
  }

  static public void m(int a, String b) {
    System.out.println("m(int,String)");
  }
```

**주의!**

- 변수의 이름만 다른 메서드를 중복해서 만들 수 없다.
- 이유는?
  - 메서드를 찾을 때 파라미터 값의 타입으로 찾기 때문이다.
  - 따라서 다음 메서드는 위의 메서드와 같은 메서드이기 때문에 컴파일 오류이다!

```java
static public void m(int x, String y) {
  System.out.println("m(int,String)");
}
```

리턴 타입만 다른 메서드를 중복해서 만들 수 없다.

- 이유는 ??
  - 메서드를 찾을 때 파라미터 값의 타입으로 찾기 때문이다.
  - 따라서 다음 메서드는 컴파일 오류이다.

```java
static public int m(int a, String b) {
  return 0;
}
```

상속해서 사용할때

```java
public class B extends A {

static void m(int a, int b, int c) {
  System.out.println("m(int,int,int)");
  }
}

```

> 부모 클래스인 `A`에 이미 `m()` 이라는 이름을 가진 메서드가 여러 개 있다.
> 그럼에도 불구하고 파라미터 형식이 다른 메서드를 추가한다면 이것도 마찬가지로 
> `"오버로딩"`이다.
> 즉 한 클래스 안에서 같은 이름의 메서드를 여러 개 만드는 것만 오버로딩이 아니다.
> 수퍼 클래스에 있는 메서드와 같은 이름을 가진 메서드를 추가해도 오버로딩이다.

### Overroding 규칙정리

- 메서드를 찾을 때 이름과 파라미터 타입, 개수로 구분하기 때문에
- 리턴 타입이 다른 것은 구분할 수 없다.
- public int m1() {return 0;} // 컴파일 오류!

1. 파라미터 타입이 달라야 한다.

```java
public void m1(float a) {} // OK
public void m1(byte a) {} // OK
public int m1(short a) {return 0;} // OK
public String m1(long a) {return null;} // OK
```

2. 파라미터 개수가 달라야 한다.

```java
  public float m1(float a, float b) {return 0f;} // OK
  public void m1(short a, String b) {} // OK
```

3. 접근 범위는 상관없다.

```java
void m1(float a, int b) {} // OK
private void m1(float a, int b, int c) {} // OK
protected void m1(float a, int b, int c, String d) {} // OK
```

`!`파라미터 이름이 다른 것으로는 메서드를 구분할 수 없다.

```java
public void m1(float f) {} // 컴파일 오류!
```