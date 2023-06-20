# 메소드(method)

- 특정 기능을 수행하는 명령문을 관리하기 쉽게 한 단위로 묶는 문법
- 복잡한 코드를 메서드 안에 감춘다 (캡슐화 (encapsulation))

## 메소드 문법

- `[리턴값의 타입] 함수명(파라미터선언, ...) {명령문들}`
- `리턴 값(return value)`의 타입?
  - 함수 블록에 들어있는 명령문을 수행 완료한 후 그 결과로 놓이는 값의 타입.
- `파라미터(parameter)` 선언?
  - 함수 블록을 실행할 때 외부로부터 받은 값을 저장할 변수 선언.
  - 메서드를 실행할 때 사용할 값을 외부로부터 받기 위해 선언한 로컬 변수.
  - 메서드를 실행할 때 생성되고 메서드 실행이 끝나면 제거된다.

- `void` : 리턴값 없음

```java
1)명령문 블록을 실행할 때 값을 받지 않고 결과도 리턴하지 않는다.
void 메서드명() {
  문장1;
  문장2;
}

1) 명령문 블록을 실행할 때 작업에 필요한 값을 받는다. 그러나 결과는 리턴하지 않는다.
void 메서드명(변수선언1, 변수선언2, ...) {
  문장1;
  문장2;
}

1) 명령문 블록을 실행할 때 값을 받지 않는다. 작업 결과는 리턴한다.
리턴타입 메서드명() {
  문장1;
  문장2;
}

1) 명령문 블록을 실행할 때 작업에 필요한 값을 받는다. 그리고 작업 결과를 리턴한다.
리턴타입 메서드명(변수선언1, 변수선언2, ...) {
  문장1;
  문장2;
}
```

- 메서드 : 파라미터(X), 리턴값(O)
  - 메서드 블록을 실행한 후 값을 리턴하는 메서드.
  - 메서드 정의할 때 어떤 값을 리턴하는 지 그 타입을 적어야 한다.
  - 메서드에서도 종료하기 전에 반드시 그 타입의 값을 리턴해야 한다.
  - 리턴 타입은 반드시 한 개만 가능하다.
  - 만약 여러 개의 값을 리턴하고 싶다면, 배열에 담거나 객체에 담아 리턴하라

```java
static String hello() {
  // 값을 리턴하는 문법
  // return 값;
  return "안녕하세요!"; // 리턴 명령을 실행하면 메서드 실행을 종료한다.

  // 메서드를 리턴한 후에 작업을 수행할 수 없다.
  // int a; // 컴파일 오류!
  // System.out.println("NO!"); // 컴파일 오류!
}

public static void main(String[] args) {

  // hello() 메서드를 실행하고, 그 리턴 값을 변수에 담는다.
  // => 리턴 값을 받을 변수를 준비한다.
  // => 변수에 리턴 값을 받는다.
  // => 리턴 값과 변수의 타입이 같아야 한다.
  String r = hello();
  System.out.println(r);

  // 메서드가 리턴한 값을 한 번만 사용할 경우
  // 쓸데없이 로컬 임시 변수를 만들지 않는다.
  // 사용할 곳에 바로 메서드 호출 코드를 둔다.
  // System.out.println(hello());

  // 메서드가 값을 리턴한다고 해서 반드시 그 값을 변수에 받아야 하는 것은 아니다.
  // 변수에 받을 지 여부는 호출하는 쪽의 마음이다.
  hello(); // 값을 받는 변수가 없으면 리턴 값은 버려진다.

  // 리턴 타입과 다른 타입의 변수로 값을 받으려 하면 컴파일 오류!
  // int r2 = hello(); // 컴파일 오류!
}
```

- 메서드 : 리턴값(O), 파라미터(O)

```java
static String hello(String name, int age) {
  String retVal = String.format("%d살 %s님을 환영합니다!", age, name);
  return retVal;
}

public static void main(String[] args) {

  // hello() 메서드를 실행하고, 그 리턴 값을 변수에 담는다.
  String r = hello("홍길동", 20);
  System.out.println(r);

  // 앞의 예제와 마찬가지로 리턴 값을 한 번만 사용한다면,
  // 사용할 곳에 메서드 호출 코드를 둬라!
  // => 리팩토링 기법 중에서 "replace temp with query" 라 부른다.
  System.out.println(hello("홍길동", 20));

  // 리턴 값을 안 받아도 된다.
  hello("임꺽정", 30); // 리턴 값은 버려진다.
}
```

## 메서드 종류?

1) 클래스 메서드
   - 클래스에 소속되어 있다.
   - 모든 인스턴스가 공유한다.
   - static이 붙는다.
2) 인스턴스 메서드
   - 특정 인스턴스에 대해 사용한다.
   - static이 붙지 않는다.

## 메서드를 사용하는 방법

- `[리턴값을 받을 변수]` = `메서드명`(`아규먼트`);
- 아규먼트(argument)?
  - 메서드 블록에 들어 있는 명령을 실행할 때 필요한 값
  - 즉 파라미터 변수에 넘겨주는 값
  - 파라미터 변수의 타입과 개수와 순서에 맞게 값을 넘겨줘야 한다.
    - 만약 변수의 타입과 값의 타입이 다르면 컴파일 오류!
    - 만약 변수의 개수와 값의 개수가 다르면 컴파일 오류!
    - 변수 선언 순서와 값의 순서가 다르면 컴파일 오류!
- 리턴값을 받을 변수
  - 메서드 블록을 실행한 후 리턴되는 값을 받을 변수이다.
  - 메서드가 값을 리턴한다 하더라도 값을 받기 싫으면
    - 변수를 선언하지 않아도 된다.
    - 그러면 리턴 되는 값은 버려진다.
  - 값을 리턴하지 않는 메서드에 대해 변수를 선언하면 컴파일 오류!

```java
리턴데이터타입  메서드명(아규먼트를 받을 변수목록) {
  명령문
  .
  .
  return 작업결과값 ;
}

a 와 b 파라미터에 아규먼트값을 주면 a와 b의 값을 더하고 그 값을 리턴한다
static int plus(int a, int b)  {
  int sum = a + b;
  return sum;
}
```

## 메서드 블록의 명령을 실행하기

- 메서드 실행하기
- 메서드 호출하기
  - 즉 다음은 "hello"라는 이름을 가진 메서드 블록을 찾아가서 실행하라는 의미.
  - `hello();`
- 실행 과정
  1) hello() 메서드의 블록으로 간다.
  2) 메서드 바디를 실행한다.
  3) 다시 원래 위치로 돌아온다.
  4) 다음 줄을 실행한다.

## 메서드(method) = 함수(function)?

- 명령문을 기능 단위로 관리하기 쉽게 별도로 분리하여 묶어 놓은 것.
- 반복적으로 자주 사용하는 명령문을 재사용하기 쉽도록 별도로 분리하여 묶어 놓은 것.
- "코드를 관리하기 쉽고 재사용하기 쉽도록 기능 단위로 묶어 놓는 문법"

## 용어

- 메서드명, 파라미터 변수 선언 : 메서드 시그너처(method signature)
  - 예) hello()
- 메서드 블록 : 메서드 몸체(method body)
  - `{ `System.out.println("안녕하세요")` }`

## 메서드 종류

1) 클래스 메서드
   - 클래스에 소속되어 있다.
   - 모든 인스턴스가 공유한다.
   - static이 붙는다.
2) 인스턴스 메서드
   - 특정 인스턴스에 대해 사용한다.
   - static이 붙지 않는다.

-----

## 가변 파라미터

- `[리턴타입]` `메서드명`(`타입... 변수`) {`...`}
  - 0 개 이상의 값을 받을 때 선언하는 방식.
  - 메서드 내부에서는 배열처럼 사용한다.
  - 가변 파라미터의 메서드를 호출할 때는 낱개의 값을 여러 개 줄 수도 있고 배열에 담아서 전달할 수도 있다.
  - 다음은 hello()를 호출할 때 String 값을 0개 이상 전달할 수 있다.

```java
static void hello(String... names) {
  for (int i = 0; i < names.length; i++) {
    System.out.printf("%s님 반갑습니다.\n", names[i]);
  }
}

public static void main(String[] args) {

  hello(); // 이 경우 names 배열의 개수는 0이다.

  hello("이강인"); // 이 경우 names 배열의 개수는 1이다.

  hello("손흥민", "김민재", "이강인"); // 이 경우 names 배열의 개수는 3이다.

  // 가변 파라미터 자리에 배열을 직접 넣어도 된다.
  String[] arr = {"이강인", "김민재", "조현우", "손흥민"};
  hello(arr);

  hello("홍길동", "임꺽정", "유관순");
  String[] temp = { "홍길동", "임꺽정", "유관순" };
  hello(temp);

  // => 또는 다음과 같이 배열에 담아서 전달할 수도 있다.
  String[] arr = { "김구", "안중근", "윤봉길", "유관순" };
  hello(arr);

  // hello("손흥민", 20, "이강인"); // 다른 타입은 안된다. 컴파일 오류!
}
```

- 가변 파라미터에 배열을 넘길 경우
  - 기존 배열을 그대로 사용할까? 아니면 파라미터로 받은 배열을 복제해서 사용할까?
  - 가변 파라미터에 배열을 넘길 경우 그 배열을 그대로 받아 사용한다.
  - 오직 배열에 담아서 전달해야 한다.

```java
static void hello(String... names) {
  for (int i = 0; i < names.length; i++) {
    names[i] += "^^";
    System.out.printf("%s님 반갑습니다.\n", names[i]);
  }
}

public static void main(String[] args) {

  String[] arr = {"김구", "안중근", "윤봉길", "유관순"};

  // 가변 파라미터에 배열을 넘길 경우
  hello(arr);

  for (String value : arr) {
    System.out.println(value);
  }

  String[] arr2 = { "김구", "안중근", "윤봉길", "유관순" };
  hello2(arr2);
}
```

### 가변 파라미터의 단점

- 가변 파라미터는 여러 개 선언할 수 없다.
  - 아규먼트의 시작과 끝을 구분할 수 없다.
  - 예) m1("aaa", "bbb", "aaa@test.com", "bbb@test.com");
  - 어느 값이 names 배열에 들어가고, 어느 값이 emails 배열에 들어가는가?
  - `static void m1(String... names, String... emails) {} // 컴파일 오류!`
  - `static void m1(String[] names, String[] emails) {} // OK!`
- 중간에 다른 타입이 온다 하더라도 안된다.
  - `static void m1(String... names, int a, String... emails) {}// 컴파일 오류!`
  - `static void m1(String[] names, int a, String[] emails) {} // OK!`

위의 메서드는 값을 구분할 수 있을 것 같은데?
=> 그냥 다음과 같이 호출하면 되는 것 아닌가?

- 예) m1("aaa", "bbb", 100, "ccc", "ddd", "eee");
  - 사람들은 쉽게 구분할 수 있다.
  - 그러나 컴파일러가 이런 상황을 구분하려면 굉장히 복잡해진다.
  - 그래서 가변 파라미터라는 문법의 이점은 사용하되
  - 너무 복잡한 사용법은 지양하기 위해서 사용 방법을 간단히 한 것이다.

- 가변 파라미터는 반드시 맨 끝에 와야 한다.
  - 아규먼트의 시작과 끝을 구분할 수 없다.
예) m2("aaaa");
  - `static void m2(String... names, String a) {} // 컴파일 오류!`
  - `static void m2(boolean b, String... names, int a) {} // 컴파일 오류!`

- 결론!
  - 메서드에 가변 파라미터는 한 개만 사용할 수 있다.
  - 가변 파라미터는 반드시 맨 뒤에 와야 한다.
  - 그 이유는 복잡한 사용을 막기 위해!

-----

## call by value

- 값을 불러와 넘긴다
- 아규먼트가 primitive data type인 경우, 메서드를 호출할 때 값을 넘긴다.
- 자바에서는 primitive data type에 대해서 메모리(변수) 주소를 넘기는 방법이 없다.

```java
public class CallbyValue {

  static void swap(int a, int b) {
    System.out.printf("swap전(): a=%d, b=%d\n", a, b);
    int temp = a;
    a = b;
    b = temp;
    System.out.printf("swap후(): a=%d, b=%d\n", a, b);
  }

  public static void main(String[] args) {
    int a = 100;
    int b = 200;

    // swap() 호출할 때 a 변수의 값과 b 변수의 값을 넘긴다.
    // => 그래서 "call by value"라 부른다.
    // => 비록 swap()에서 a와 b라는 이름의 변수가 있지만,
    //    이 변수는 main()에 있는 변수와 다른 변수이다.
    swap(a, b);
    System.out.printf("main(): a=%d, b=%d\n", a, b);
  }
}

결과 값
swap전(): a=100, b=200
swap후(): a=200, b=100
main(): a=100, b=200
```

### call by reference

- 인스턴스값 즉, 아규먼트 값을 넘기는게 아니라 레퍼런스 변수 주소값을 넘기는 것

```java
public class CallbyReference {

  static void swap(int[] arr) {
    System.out.printf("swap(): arr[0]=%d, arr[1]=%d\n", arr[0], arr[1]);
    int temp = arr[0];
    arr[0] = arr[1];
    arr[1] = temp;
    System.out.printf("swap(): arr[0]=%d, arr[1]=%d\n", arr[0], arr[1]);
  }

  public static void main(String[] args) {
    int[] arr = new int[] {100, 200};
    swap(arr); // 배열 인스턴스(메모리)를 넘기는 것이 아니다. 
    // 주소를 넘기는 것이다.
    // 그래서 "call by reference" 라 부른다.
    System.out.printf("main(): arr[0]=%d, arr[1]=%d\n", arr[0], arr[1]);
  }
}

결과값
swap(): arr[0]=100, arr[1]=200
swap(): arr[0]=200, arr[1]=100
main(): arr[0]=200, arr[1]=100
```
