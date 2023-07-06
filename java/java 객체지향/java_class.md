# class와 객체(Object)

## 클래스(Class)란?

클래스의 정의

- `객체를 정의해놓은 것` 또는 `객체의 설계도 또는 틀` 이라고 정의할 수 있다.

클래스의 용도

- 객체를 생성하는데 사용되며 객체는 클래스에 정의된 대로 생성된다.

---

## 객체 (Object)

객채의 정의

- 사전적 정의는, 실제로 존재하는 것이다.
- 사물 또는 개념

객체의 용도

- 객체가 가지고 있는 기능과 속성에 따라 다르다.

유형의 객체

- 우리가 볼 수 있는 사물 자동차, 책상, 의자 가 곧 객체이다.

무형의 객체

- 수학공식, 프로그램 에러와 같은 논리나 개념

객체는 클래스에 정의 된 내용대로 메모리에 생성되는것을 뜻한다.

>실생활에서의 예를 들면 자동차설계도(클래스)는 자동차라는 제품(객체)를 정의한것이며,
자동차(객체)를 만들때 사용된다.
또한 클래스는 객체를 생성하는데 사용될 뿐, 객체 그 자체는 아니다. 우리가 원하는 기능의 객체를 사용하기 위해서는 먼저 클래스로 부터 객체를 생성하는 과정이 선행 되어야 한다!
우리가 자동차를 타기 위해서 자동차(객체)가 필요한것이지 자동차설계도(클래스)가 필요한것이 아니며
자동차설계도(클래스)는 단지 자동차(객체)를 만드는 데만 사용한다.
이처럼 프로그래밍에서는 먼저 클래스를 작성한 다음 클래스로 부터 객체를 생성하여 사용한다.

java 코드의 예시이다.

```java
class Car { // 자동차 설계도
  String model; // 자동차 이름
  String color; // 자동차 색상
}
```

이렇게 클래스를 정의 하고 객체를 생성하는 이유는 설계도를 통해서 제품을 만드는 이유와 같다.

하나의 설계도만 잘 만들어 놓으면 나중에 다른 제품을 생산하는 일이 쉬워진다.

제품을 만들때 마다 매번 고민할 필요 없이 설계도 대로만 만들면 되기 때문이다.

이런 객체지향프로그래밍을 위해 JDK(Java Development Kit)에서는 많은 수의 유용한 클래스 (JavaAPI)
를 기본적으로 제공하고 있으며, 이를 클래스들을 이용해 원하는 기능의 프로그램을 보다 쉽게 작성할 수 있다.

---

## 인스턴스 (instance)

클래스는 자동차설계도 이고 객체는 자동차 라고 정의한다면 인스턴스는 객체의 구체적인 상태(변수)와 행위(기능)의 집합 이라 생각하면 된다.

자동차를 만들어도 종류가 다양하다 경차, 승용차, SUV, 트럭 등 다양한 종류들이 있다.

이처럼 자동차를 만들 때 자동차설계도(클래스)는 같은 이름이지만 자동차(객체)의 종류에 따라

차종, 색상, 자동차 문, 엔진, 트렁크 등등 종류마다 가지고 있어야할 정보들이 각기 다를것이다.

이렇게 만들어낸 자동차는 각기 다른 `상태와 행위`를 갖는다 즉 이것을 인스턴스라 한다.

코드로 작성하면 아래와 같다.

```java
Car sonata = new Car();
Car k5 = new Car();
Car santafe = new Car();
Car benzGLC = new Car();
Car bmwX5 = new Car();
```

인스턴스의 존재 이유는 `서로 다른상태를 가지기 위해서` 또는 `서로 다른개성을 존중하자` 라고 생각하면 이해가 쉽다.

- 클래스로 부터 객체를 만드는 과정을 `클래스의 인스턴스화 (instantiate)`
- 어떤 클래스로 부터 만들어진 객체를 해당 `클래스의 인스턴스(instance)` 라고 한다

## 객체의 구성요소

- 속성 (property) : 멤버변수, 특성, 필드, 상태
- 기능 (function) : 메서드, 행위, 함수

```bash
자동차가 "달리고" 있다면 "기능"에 해당
자동차의 "이름이 아반떼" 라고 한다면 "속성"에 해당한다.
```

`속성`과 `기능`의 집합을 `객체` 라고 한다.

## 객체의 생성과 사용

자동차에는 아래와 같은 속성(변수) 와 기능(메서드)가 있다.

- 속성 : 엑셀레이터, 브레이크패달
- 기능 : 속도를 올린다, 속도를 줄이거나 멈춘다.

이처럼 개념을 적용하여 코드를 작성해본다.

```java
클래스명 변수명; // 클래스의 객체를 참조하기 위한 참조변수를 선언
변수명 = new 클래스명(); // 클래스의 객체를 생성 후 객체의 주소를 참조변수에 저장

Car suv; // Car클래스 의 참조변수 suv를 선언
suv = new Car(); // Car인스턴스를 생성한 후 생성된 Car 인스턴스 주소를 suv에 저장

Car suv = new Car(); // 이처럼 한줄로 표현할 수 있다.
```

---
 > 여기서 용어의 정리!
인스턴스 변수값을 담는 참조변수를 다른말로 레퍼런스 변수라고도 한다.
참조변수 = 레퍼런스변수 이다.
그래서 아래부터는 레퍼런스 변수라고 선언하겠다.
---

조금더 정확하게 해석하면
`Car클래스설계도`에 따라 인스턴스 `주소값` 을 같는 레퍼런스 변수`suv`를 생성한다.

주의하자! `인스턴스 값`이 아니고 `인스턴스 주소값`이다!

```java
class Car {
  String carName;
  String color;
  boolean power;
  int radioVolume;

  void power() {
    power = !power;
  }
  void radioVolumeUp() {
    ++radioVolume;
  }
  void radioVolumeDown() {
    --radiovolume;
  }
}

class Car Test {
  public static void main(String[] args) {
    Car suv = new Car(); // Car설계도에 따라 인스턴스 주소값을 갖는 래퍼런스변수 suv를 생성한다.
    suv.radioVolume = 10; // 라디오볼륨의 값을 10으로 한다.
    suv.radioVolumeDown(); // 볼륨을 1 줄인다.
    System.out.println("자동차의 라디오 볼륨은" + suv.radioVolume+ "입니다");
  }
}

결과 : 자동차의 라디오 볼륨은 9 입니다.
```

여기서 생성되는 인스턴스 주소값은 몇개일까?

총 1가지 이다.

```bash
suv
```

JVM Stack에 suv 변수가 생성되고 Car클래스의 인스턴스가 suv변수의 주소값을 갖는 메모리가 생성된다.

- `suv` 주소값  0x001
  - 0x001의 주소값을 갖는 인스턴스 carName, color, power, radioVolume, power(), radioVolumeUp(), radioVolumDown() 그리고 메소드를 제외한 각 인스턴스는 초기값을 가진다.

> 인스턴스는 레퍼런스변수를 통해서만 다룰수 있으며, 레퍼런스 변수의 타입은 인스턴스의 타입과 일치해야 한다.

## 래퍼런스 배열

많은수의 객체를 다뤄야 할때 배열로 다루면 편리할 것이다.
객체 역시 배열로 다루는것이 가능하며 이를 레퍼런스 배열이라 한다.

- 문법:
  - `클래스명[]` `배열명` = `new 클래스명`[`레퍼런스개수`];
- 주의!
  - 레퍼런스 배열이다. 인스턴스 배열이 아니다!
  - 배열안에 인스턴스값이 저장되는것이 아니고 인스턴스 주소값이 저장된다.

다음은 길이가 3인 배열을 생성하는 코드이다.

```java
Score[] arr = new Score[3];

arr[0] = new Score();
arr[1] = new Score();
arr[2] = new Score();
```

배열의 인덱스는 0부터 시작한다.

다뤄야할 객체수가 많다면 for문을 사용하면 된다.

```java
Score[] arr = new Score[100];

for (int i = 0; i < arr.length; i++) {
  arr[i] = new Score();
}
```

간단 예제를 통해 살펴보자

```java
public class Exam0240 {

// 여러 메서드에서 공유하려면 클래스를 메서드 밖에 선언해야 한다.
// => static 메서드들이 사용할 수 있게 클래스도 static으로 선언한다.
// => static에 대한 의미는 나중에 설명한다.

  static class Score {
    String name;
    int kor;
    int eng;
    int math;
    int sum;
    float aver;
  }

  public static void main(String[] args) {

    Score[] arr = new Score[3];

    // 메서드에서 생성한 Score 객체를 레퍼런스 배열의 각 항목에 저장한다.
    arr[0] = createScore("홍길동", 100, 100, 100);
    arr[1] = createScore("임꺽정", 90, 90, 90);
    arr[2] = createScore("유관순", 80, 80, 80);

    // 메서드에 배열을 통째로 넘길 수 있다.
    // => 정확하게 표현하면, arr 변수에 저장된 레퍼런스 배열의 주소를 넘긴다.
    printScoreList(arr);

  }

  // 클래스를 이용하면 성적 정보를 하나로 묶어 리턴할 수 있다.
  // 참고!
  // - 다음과 같이 메서드를 통해 인스턴스를 생성하는 코딩 기법을 
  //   "팩토리 메서드(factory method)" 패턴이라 부른다.
  static Score createScore(String name, int kor, int eng, int math) {
    Score s = new Score();

    s.name = name;
    s.kor = kor;
    s.eng = eng;
    s.math = math;
    s.sum = s.kor + s.eng + s.math;
    s.aver = s.sum / 3f;

    return s;
  }

  static void printScoreList(Score[] arr) {
    // main()에서 넘겨준 레퍼런스 배열의 주소를 arr 변수에 받는다.
    // 결국 main()에서 만든 레퍼런스 배열을 사용하는 것이다.
    //
    for (int i = 0; i < arr.length; i++) {
      System.out.printf("%s: %d, %d, %d, %d, %.1f\n",
          arr[i].name, arr[i].kor, arr[i].eng, arr[i].math, arr[i].sum, arr[i].aver);
    }
  }
}
```
