# 상속 (inheritance)

- 기존 클래스를 재사용하여 새로운 클래스를 작성하는 것
- 상속을 통해서 적은양의 코드로 새로운 클래스를 작성 할 수 있고 코드를 공통적으로 관리할 수 있다.

상속을 사용하기 전에 코드 예제를 통해 알아보자.

``` java
public class Calculator {

  public int result;

  public void plus(int value) {
    this.result += value;
  }

  public void minus(int value) {
    this.result -= value;
  }
}

public class Exam02 {
  public static void main(String[] args) {
    Calculator c1 = new Calculator();
    c1.plus(5);
    c1.minus(2);
    System.out.println(c1.result);
  }
}
```

Calculator 클래스를 활용하여 계산기능을 더하기 빼기를 사용하는 프로그램을 만들었다.

만약에 이코드만 사용하는 회사말고 다른회사에서는 곱하기와 나누기도 필요한 프로그램이 필요하다고 요구사항이 들어왔다

그렇다면 어떻게 할것인가?
보통은 복사 붙여넣기를 하여 메소드의 이름만 바꾸면 된다고 생각한다.

```java
public class Calculator {

  public int result;

  public void plus(int value) {
    this.result += value;
  }

  public void minus(int value) {
    this.result -= value;
  }

  // 새 기능을 기존 클래스에 추가한다.
  //
  public void multiple(int value) {
    this.result *= value;
  }

  public void divide(int value) {
    this.result /= value;
  }
}

public class Exam02 {
  public static void main(String[] args) {

    Calculator c1 = new Calculator();
    c1.plus(5);
    c1.multiple(2);
    c1.minus(2);
    c1.divide(4);
    System.out.println(c1.result);
  }
}
```

이렇게 기존코드에 새기능을 기존 클래스에 추가하여 사용한다.
하지만 여기서 문제점이 발생한다.

1) 기존 클래스에 코드를 추가하였을때 문제점

- 기존 코드를 변경하게 되면 원래 되던 기능도 오류가 발생할 수 있는 위험이 있다.
- 그래서 원래 코드를 손대는 것은 매우 위험한 일이다.
- 기존에 잘 되던 기능까지 동작이 안되는 문제가 발생할 수 있기 때문이다.

그렇다면 클래스를 새로 복사하여 사용하면 가능하지 않을까?

다음 예제를 확인해보자
```java
public class Calculator {

  public int result;

  public void plus(int value) {
    this.result += value;
  }

  public void minus(int value) {
    this.result -= value;
  }
}
```

```java
public class Calculator2 {

  public int result;

  public void plus(int value) {
    this.result += value;
  }

  public void minus(int value) {
    this.result -= value;
  }

  // 새 기능을 기존 클래스에 추가한다.
  //
  public void multiple(int value) {
    this.result *= value;
  }

  public void divide(int value) {
    this.result /= value;
  }
}
```

이렇게 하면 장점은 있다. 기존코드를 손대지 않아서 문제가 발생할 가능성은 낮다.

하지만 단점이 너무 많다.

2) 기존 코드를 복사하여 새 클래스를 만들었을때 문제점

- 장점
  - 기존 코드를 손대지 않기 때문에 문제가 발생할 가능성은 줄인다.
- 단점
  - 기존 코드의 크기가 큰 경우에는 복사 붙여넣기가 어렵다.
  - 기존 클래스의 소스가 없는 경우에는 이 방법이 불가능하다.
      엥? 다른 개발자가 배포한 라이브러리만 있는 경우를 말한다.
      소스가 없는 다른 개발자가 만든 클래스에 기능을 덧 붙일 때는 이 방법이 불가능하다.
  - 기존 코드에 버그가 있을 때 복사 붙여넣기 해서 만든 클래스도 영향을 받는다.
  - 기존 코드를 변경했을 때 복사 붙여넣기 한 모든 클래스를 찾아 변경해야 한다.

그렇다면 어떻게 수정해야 안전한가?

이때 바로 상속을 사용한다.

``` java
public class Calculator2 extends Calculator {

  // 상속은 기존 코드를 자동으로 복사해오는 것이 아니다! 아니다! 아니다!
  // 아니다! 아니다! 아니다! 아니다! 아니다! 아니다! 아니다!

  // 새 기능을 추가한다.
  public void multiple(int value) {
    this.result *= value;
  }

  public void divide(int value) {
    this.result /= value;
  }
}
```

기존의 코드를 손대지 않고 기존 기능을 상속받아 손대지 않고 추가할 기능만 작성하면 된다.

단! 상속은 기존 코드를 복사해오는것이 `절대 아니다!`

3) 기존 코드를 상속 받아 기능을 추가하는 방법

- 장점
  - 기존 클래스의 소스 코드가 필요 없다.
  - 간단한 선언으로 상속 받겠다고 표시한 후 새 기능만 추가하면 된다.
- 단점
  - 일부 기능만 상속 받을 수 없다.
  - 쓰든 안쓰든 모든 기능을 상속 받는다.


다음은 자동차를 만드는 예제이다.

한번더 복기한다는 생각으로 확인해보자

```java
public class Car {

  public String model;
  public String maker;
  public int capacity;

  public Car() {

  }

  public Car(String model, String maker, int capacity) {
    this.model = model;
    this.maker = maker;
    this.capacity = capacity;
  }

  public void run() {
    System.out.println("달린다!");
  }
}

public class Exam01 {
  public static void main(String[] args) {
    Car c1 = new Car();
    c1.maker = "현대자동차";
    c1.model = "아반때";
    c1.capacity = 5;

    Car c2 = new Car("소나타", "비트자동차",  5);
  }
}
```

자동차 제조사와 모델, 수용인원의 클래스에 이외에 옵션을 추가하고 싶다
세단에 선루프 장착여부와, 자동변속기 장착여부

상속을 사용하여 작성해보자

```java
// "Sedan클래스를 통해서 Car의 기능을 사용할 수 있다" 
public class Sedan extends Car { 

  // 인스턴스 변수 추가
  public boolean sunroof;
  public boolean auto;

  public Sedan(String model, String maker, int capacity,
      boolean sunroof, boolean auto) {
    this.model = model;
    this.maker = maker;
    this.capacity = capacity;
    this.sunroof = sunroof;
    this.auto = auto;
  }
}

public class Exam01 {
  public static void main(String[] args) {

    Sedan c = new Sedan("티코", "비트자동차", 5, true, true);

/*
상속을 이용하여 기능을 추가한 클래스를 사용한다.
  장점:
  => 기존 코드에 문제가 있으면 그 코드를 수정하는 순간 
      그 코드를 상속 받아 만든 모든 클래스에 자동으로 적용된다.
  => 기존 코드를 손대지 않기 때문에 새 기능을 추가하더라도
      기존 기능에 문제가 발생할 가능성이 거의 없다.
  => 소스 코드의 유지보수가 쉽다.
*/
```

이것이 상속이라는 문법이 등장한 이유이다.

> 즉 기존 코드의 수정을 최소화하면서 새 기능을 추가하는 방법! 
> 기존 기능을 재작성하지 않고 다시 사용할 수 있게 만드는 문법이다.
> 코드 재사용성을 높인다. 

그럼 상속받는 클래스의 이름을 클래스 명으로 불러야 하나?

이름은 정해져있다.

상속을 받을때 클래스의 이름을 바로 super클래스 라고한다.

다음 예제를 보자

각기 다른 파일로 되있으나 설명을 위해 한곳에 작성한다.

```java
A.java

public class A { // super클래스
  void m1() {
    System.out.println("A.m1()");
  }
}

B.java
public class B extends A {
  // 상속이란? super클래스의 사용권을 획득하는 것이다.
  // 그래서 내 것처럼 사용하는 것이다.

  public void m2() {
    System.out.println("B.m2()");
  }
}

C.java
public class C extends B {
  // 상속이란? super클래스의 사용권을 획득하는 것이다.
  // 그래서 내 것처럼 사용하는 것이다.

  public void m3() {
    System.out.println("C.m3()");
  }
}

D.java
public class D extends C {
  // 상속이란? super클래스의 사용권을 획득하는 것이다.
  // 그래서 내 것처럼 사용하는 것이다.

  public void m4() {
    System.out.println("D.m4()");
  }
}
```

각 클래스별로 상속을 받아온다

A 클래스 파일을 super클래스로 지정하고

B 클래스 파일은 A 에서 상속받고

C 클래스 파일은 B 에서 상속받고

D 클래스 파일은 C 에서 상속받는다.

그럼 D클래스에서도 super클래스의 상속받은 내용을 사용할수 있는것이다.

다음 예제를 확인해보자.



Exam 01 예제파일

```java
public class Exam01 {

  public static void main(String[] args) {
    B obj = new B();

    // B 인스턴스를 이용하여 B가 사용권을 획득한 A 클래스의 메서드를 호출할 수 있다.
    obj.m1(); // A 클래스의 m1() 호출

    obj.m2(); // B 클래스의 m2() 호출

  // 실험:
  // bin/main/.../A.class 파일을 제거한 후 다시 실행하라!
  // => 결과는?
  //    A 클래스가 없다고 예외가 발생한다.
  // => 의미?
  //    상속 받는다는 것은 수퍼 클래스의 코드를 그대로 복제해 온다는 것이 아니다.
  //    그냥 수퍼 클래스의 코드를 사용할 수 있는 권한을 획득한다는 것이다.
  //    그래서 서브 클래스를 사용하려면
  //    반드시 서브 클래스가 상속 받는 모든 조상 클래스가 있어야 한다.
  //

  }

}
```

Exam02 예제파일

```java
public class Exam02 {

  public static void main(String[] args) {
    D obj = new D();

    obj.m4(); // obj 레퍼런스의 클래스에서 m4()를 찾아 호출한다.
    obj.m3(); // obj 레퍼런스의 클래스(D)에서 m3()를 찾아보고 없다면 수퍼 클래스에서 찾는다.
    obj.m2(); // 만약 D의 수퍼 클래스에서도 못찾는다면 그 위의 클래스에서 찾아본다.
    obj.m1(); // 그 위에 클래스에서도 없다면 더 위에 클래스에서 찾아본다.
    //    obj.m0(); // 더 위에 있는 클래스에서도 찾을 수 없다면 컴파일 오류이다!
  }

}

```

즉 메서드를 호출할 때는 클래스 상속 관계에 따라 레퍼런스의 클래스에서 시작하여 상위 클래스로 찾아간다.

그래서 클래스를 사용하려면 그 클래스가 상속 받는 상위 클래스들이 모두 있어야 한다.

Exam03 예제파일

```java
public class Exam03 {

  public static void main(String[] args) {
    B obj = new D();

    //    obj.m4(); // obj 레퍼런스의 클래스(B)에서 m4()를 찾아보고 없다면 수퍼 클래스에서 찾는다.
    //    obj.m3(); // obj 레퍼런스의 클래스(B)에서 m3()를 찾아보고 없다면 수퍼 클래스에서 찾는다.
    obj.m2();
    obj.m1();

  }

}

```

---

## 클래스 로딩과 인스턴스 생성과정

클래스에 선언되있는 인스턴스가 JVM 메모리 영역에 어떻게 생성되는지 알아보자

아래 예제를 확인 해 보자.

```java
public class A {
  int v1;

  static { 
    System.out.println("A클래스의 static{} 실행!");
  }
}

public class B extends A {
  int v2;

  static {
    System.out.println("B클래스의 static{} 실행!");
  }
}
```


```java
public class Exam01 {
  public static void main(String[] args) {

    B obj = new B();
    // B 클래스의 설계도에 따라 Heap 영역에 변수를 준비한다.
    // - B 클래스는 A 클래스에 기능을 덧붙인 것이라 선언했기 때문에
    //   A 클래스의 설계도에 따라 A 클래스에 선언된 인스턴스 변수도 함께 생성된다.

    obj.v2 = 200; // B 클래스 설계도에 따라 만든 변수
    obj.v1 = 100; // A 클래스 설계도에 따라 만든 변수

    System.out.printf("v2=%d, v1=%d\n", obj.v2, obj.v1);
    System.out.println("---------------------------------");

    // 클래스는 오직 한 번만 로딩된다.
    // - 그래서 static 블록도 위에서 한 번 실행되면 다시 실행하지 않는다.
    B obj2 = new B();
    obj2.v2 = 2000;
    obj2.v1 = 1000;
    System.out.printf("v2=%d, v1=%d\n", obj2.v2, obj2.v1);

    // B 클래스의 인스턴스 생성 과정
    // 1) B의 수퍼 클래스가 로딩되어 있지 않다면, 수퍼 클래스(A 클래스)를 먼저 로딩한다.
    //    - 스태틱 필드 생성한 후
    //    - 스태틱 블록 실행한다.
    // 2) 그런 후 B 클래스를 로딩한다.
    //    - 스태틱 필드 생성한 후
    //    - 스태틱 블록 실행한다.
    // 3) 인스턴스 필드 생성
    //    - 수퍼 클래스의 인스턴스 필드부터 생성한다.
    //    v1   |    v2    : A의 v1 필드 생성, B의 v2 필드 생성
    //    0    |    0     : 각 필드를 기본 값으로 설정한다.
    //    100  |    0     : A 클래스의 생성자 수행
    //    100  |    200   : B 클래스의 생성자 수행
    //
    // - B 클래스의 인스턴스는 수퍼 클래스의 인스턴스 필드도 포함한다.
  }
}
```

- 인스턴스 생성 절차 정리!

1) 상속 받은 수퍼 클래스를 먼저 메모리에 로딩한다.
    이미 로딩되어 있다면 다시 로딩하지는 않는다.
2) 그런 후 해당 클래스를 메모리에 로딩한다.
    마찬가지로 이미 로딩되어 있다면 다시 로딩하지는 않는다.
3) 수퍼 클래스에 선언된 대로 인스턴스 변수를 Heap에 만든다.
4) 해당 클래스에 선언된 대로 인스턴스 변수를 Heap에 만든다.
5) 수퍼 클래스부터 생성자를 실행하며 해당 클래스까지 내려온다.

그래서 인스턴스를 생성할 때는 항상 상속 받아야 하는 클래스 파일이 모두 있어야 한다.

- 용어 정리!
  - 상속(inheritance)
    - 기존에 만든 클래스를 자신의 코드처럼 사용하는 기법이다.
    - 보통 기존 코드를 손대지 않고 새 코드를 덧붙일 때 많이 사용한다.
  - 수퍼클래스(super class) = 부모클래스(parents class)
    - B 클래스 입장에서, B 클래스에게 상속 해주는 A 클래스를 말한다.
  - 서브클래스(sub class) = 자식클래스(child class)
    - A 클래스 입장에서, A 클래스가 상속해주는 B 클래스를 말한다.

즉 수퍼 클래스나 서브 클래스는 상대적인 개념이다.
