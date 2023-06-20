# 변수란?

데이터를 임시 보관하는 메모리(RAM)

- 일반적인 경우 Application에서 메모리를 사용
- Java의 경우 JVM에서 메모리를 할당받아 관리하고 Java Application에서 사용한다.

## 그럼 JVM 메모리 구성은 어떻게 되있나?

![](https://b2eprogrammers.com/assets/images/img_Java_memory%20areas%20inside%20jvm_20210830112844.png)

- 작성중

## 변수선언

- 메모리에 값을 담을 수 있도록 메모리의 일정 영역을 확보하는명령
- 값을 저장할 메모리의 종류와 크기를 결정하고 그 메모리에 이름을 부여한다.
- 변수를 선언한 후 바로 그 이름을 사용하여 메모리에 접근하고 값을 넣고 꺼낸다.

```java
int        a;
data type  variables(변수)
메모리용도    메모리 이름

//정수값을 담을 4byte를 확보하고 이름은 a라고 부여한다
```

### 변수의 이름

- 보통 소문자로 시작한다.
- 대소문자를 구분한다.
- 여러 단어로 구성된 경우 두 번째 단어의 시작 알파벳은 대문자로 한다.
- 예) firstName, createdDate, userId
- 상수인 경우 보통 모두 대문자로 이름을 짓는다. 단어와 단어 사이는 _를 사용한다.
- 예) USER_TYPE, USER_MANAGER

### 값 할당 (assignment)

- 변수가 가리키는 메모리에 값을 저장하는 것
- 문법
  - 변수명 = 변수 또는 리터럴;
- 용어
  - 할당 연산자(assignment operator) `=`을 사용
  - l-value : = 왼쪽에 있는 변수를 가리킨다. l-value는 리터럴이 될 수 없다.
  - r-value : = 오른쪽에 있는 변수나 리터럴을 가리킨다.

## 변수의 종류

- 자바 원시 타입의 값을 저장하는 변수와 메모리 주소를 저장하는 변수가 있다.
- 자바 원시 타입 변수(primitive variable)
   정수, 부동소수점, 논리, 문자코드의 값을
- 레퍼런스 변수(referece variable)
   자바 원시 타입의 값을 제외한 모든 값
- 인스턴스 변수(instance variable)
  - new 명령을 사용하여 인스턴스를 생성할 때 준비되는 변수
- 클래스 변수(class variable = static variable)
  - 클래스가 로딩될 때 준비되는 변수
  - 클래스 블록안에 선언된 변수는 종류에 상관없이 중복선언 불가
- 로컬 변수(local variable)
  - 블록을 실행할 때 준비되는 변수
  - 메서드 블록에서는 클래스에 선언된 변수의 이름과 같은 변수를 선언할 수 있다.
- 파라미터(parameter)
  - 메서드의 아규먼트를 받는 로컬 변수이다.
  - 예) 위의 코드에서 main()의 args 로컬 변수

```java
public class variable {

  int a; // 인스턴스 변수

  static int b; // 클래스 변수 == 스태틱 변수


  public static void main(String[] args/*로컬변수=파라미터*/) {

    int c; // 로컬 변수

  }
}
```

### 메모리 크기에 따라 저장할 수 있는 값의 범위

- 1) primitive data type (원시 데이터 타입)
  - 정수
    - byte   : 1byte 메모리 (-128 ~ 127)
    - short  : 2byte 메모리 (-32768 ~ 32767)
    - int    : 4byte 메모리 (약 -21억 ~ 21억)
    - long   : 8byte 메모리 (약 -922경 ~ 922경)
  - 부동소수점
    - float  : 4byte 메모리 (유효자릿수 7자리)
    - double : 8byte 메모리 (유효자릿수 15자리)
  - 문자
    - char   : 2byte 메모리 (0 ~ 65535). UCS-2 코드 값 저장.
  - 논리값
    - boolean : 배열일 경우 1 byte 메모리를 사용한다.
      - JVM에서 4 byte int 메모리를 사용한다.

- 2) reference(레퍼런스)
  - 데이터가 저장된 메모리의 주소를 저장하는 메모리.
  - 문자열(주소)
    - String : 문자열이 저장된 메모리의 주소를 저장한다.
               프로그래밍 입문 단계에서는 그냥 문자열을 저장하는 메모리로만 알고있자
  - 날짜(주소)
    - Date : 날짜 값이 저장된 메모리의 주소를 저장한다.
             프로그래밍 입문 단계에서는 그냥 날짜를 저장하는 메모리로만 알고있자

### 값 저장과 메모리 크기

- 작은 크기의 메모리 값을 큰 크기의 메모리에 저장할 수 있다.

```java
public static void main(String[] args) {

    byte b = 100; // 1byte
    short v1 = b; // 1byte ==> 2byte 

    short s = 100; // 2byte(-32768 ~ 32767)
    int v2 = s; // 2byte ==> 4byte

    int i = 98765678; // 4byte
    long v3 = i; // 4byte ==> 8byte

    long l = 98765678; // 4byte 리터럴 ==> 8byte

    char c = 100; // 2byte(0 ~ 65535)
    //    short x1 = c; // char(0 ~ 65535) ==> short(-32768 ~ 32767),
    // 값의 범위가 맞지 않아 컴파일 오류!
  }
```

- 정수는 부동소수점 메모리에 저장할 수 있다.

```java
public static void main(String[] args) {

    byte b = 100; // 1byte
    short s = 32767; // 2byte(-32768 ~ 32767)
    int i = 98765678; // 4byte(약 -21억 ~ +21억)
    long l = 18_2345_3456_4567_5678L; // 8byte(약 -922경 ~ 922경)

    float f;
    double d;

    // 주의!
    // - float의 자릿수가 넘어가는 정수를 저장하는 경우 값이 짤릴 수 있다.
    // - 그럼에도 불구하고 컴파일 오류가 발생하지 않는다.
    // - 그래서 정수 값을 부동소수점 메모리에 저장할 때 특히 주의해야 한다.

    f = b; // byte(1) ==> float(4). 값을 그대로 저장.
    System.out.println(f);

    f = s; // short(2) ==> float(4). 값을 그대로 저장. 
    System.out.println(f);

    f = i; // int(4) ==> float(4). 
    // 유효자릿수를 넘는 정수는 짤린다.
    System.out.println(f);

    f = l; // long(8) ==> float(4)
    // 유효자릿수를 넘는 정수는 짤린다.
    System.out.println(f);

    d = i; // int(4) ==> double(8)
    // 유효자릿수 범위의 정수 값이므로 int(32비트) 값을 그대로 저장할 수 있다.
    System.out.println(d);       

    d = l; 
    // 유효 범위를 넘어가는 정수인 경우 짤린다.
    // 주의! 컴파일 오류가 발생하지 않는다.
    System.out.println(d);       
  }
```

> 정수 메모리의 값(byte, short, char, int, long)을 
  부동소수점 메모리(float, double)에 저장할 때 주의해서 사용
>> 유효자릿수를 넘어가는 정수 값인 경우 부동소수점 메모리에 저장될 때 짤릴 수 있다.
   그럼에도 컴파일 오류가 발생하지 않기 때문에 놓치는 경우가 많다!


## 형변환(casting)

- 변수나 리터럴의 타입을 다른 타입으로 변환하는것
- 원래 변수의 타입을 바꾸는것이 아니다
- 변수에 들어있는 값을 꺼내 지정된 타입의 임시 메모리를 만들어 저장
- java의 최소 연산 단위는 `int` 가 default값
- 문법
  - 변환하고자 하는 변수나 리터럴 앞에 `(type)변수 or 리터럴`을 붙여주면 된다.
  - `(float)100`, `(long)3.14`
- 큰 메모리의 값이 작은 메모리에 들어갈 경우 앞쪽 바이트의 값이 짤려서 들어감.

```java
l = 400_0000_0000L; 
i = (int)l;
System.out.println(i) // 1345294336
``` 

- 형변환이 가능한 경우
  - 정수 <-> 정수
  - 부동소수점 -> 정수
  - 정수 -> 부동소수점
  - 숫자 -> 문자코드
- 이 외에는 불가함