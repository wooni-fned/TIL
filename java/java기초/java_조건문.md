# java 조건문

- 조건문
  - if 문과 if ~ else의 사용방법
  - switch의 사용방법

## if 조건문

- 조건식
  - `if (조건) 문장`
  - 만약 (조건이 맞다면) 문장을 출력해라.

```java
int age = 20
if (age > 19)
System.out.println("성인입니다.");

```

- 조건식이 참일 때만 문장을 출력한다.
- **조건은 무조건 참과 거짓 즉 boolean 일때만 가능하다.**
- 가독성을 위해 문장은 다음줄에 놓는다.
- 만약 여러 문장을 쓰고 싶다면 `if (조건) {문장1; 문장2;}` 중괄호를 사용하면 된다.
- 중괄호를 쓰지 않으면 첫번째 문장만 출력된다.
- 중괄호를 사용하면 중괄호에 들어간 문장들만 출력된다
- 이것을 블록(block)이라 한다!

```java
if (age >= 19)  
  System.out.println("성인이다."); // 이 문장만 if에 소속된다.
  System.out.println("군대 가야한다.");
  System.out.println("일해야 한다.");
  System.out.println("세금 납부해야 한다.");

// 여러 문장을 if 문에 종속시키고 싶으면, 블록을 사용하라!
if (age >= 19) {
  System.out.println("성인이다.");
  System.out.println("군대 가야한다.");
  System.out.println("일해야 한다.");
  System.out.println("세금 납부해야 한다.");
}
``` 

- 조건식의 경우 비교연산자를 활용하여 사용할수도 있다.

```java
90 <= x && x <= 100 // x값이 90이상 100보다 작을경우
x < 0 || x > 100 // x값이 0보다 작고 100보다 클때
x%3 == 0 && x%2 != 0 // x가 3의배수 이지만 2의 배수는 아닐때
```

### if ~ else 문

- if 조건이 참일경우에만 출력하고 아닐때에도 출력하고 싶을때 else를 사용 하면 된다.

```java
// if문만 사용할때
if (age < 19)
  System.out.println("미성년입니다.1");
if (age >= 19)
  System.out.println("성년입니다.1");

// 조건이 거짓이면 다음 else 문을 실행한다.
if (age >= 19) 
  System.out.println("성인입니다.2");
else
  System.out.println("미성년입니다.2");


// 한 문장일 때는 블록으로 묶지 않아도 된다.
if (age >= 19) { // OK!
  System.out.println("성인입니다.3");
  System.out.println("--------------------------");
}
else 
  System.out.println("미성년입니다.3");
    
```

- if ~ else 문을 작성할 떄 1줄 2줄 작성에 블록화를 하지 않은경우가 많다.
- 어떤문장에는 1줄이라 사용하지않고 2줄이라 사용하지 않는다고 블록화를 하지 않으면 전달의 오류가 발생할 수 있다
- if문을 사용할땐 **무조건** 블록화를 사용하여 명확하게 구분해 주는것이 좋다.

```java
if (age < 8) {
  System.out.println("아동입니다.");
} else if (age < 14) {
  System.out.println("어린이입니다.");
} else if (age < 19) {
  System.out.println("청소년입니다.");
} else if (age < 65) {
  System.out.println("성인입니다.");
} else {
  System.out.println("노인입니다.");
}
```

- 이처럼 명확하게 구분하여 사용할 것을 추천한다.
- 그리고 else 이후 다른 조건에 맞춰 출력할 경우 if문을 사용하면된다.
- **else if문 같은건 없다.**
- 거짓일 경우 다시 다른조건이 참일경우 출력하는것이다.

## switch 조건문

- 하나의 조건으로 여러가지 경우를 처리할 수 있다.
- 경우의 수가 많을 경우 switch를 사용하는것이 좋다.

```java
Scanner keyScan = new Scanner(System.in);
System.out.println("[지원부서]");
System.out.println("1. S/W개발");
System.out.println("2. 일반관리");
System.out.println("3. 시설경비");
System.out.print("지원 분야의 번호를 입력하세요? ");
int no = keyScan.nextInt();

System.out.println("제출하실 서류는 다음과 같습니다.");
switch (no) {
  case 1:
    System.out.println("정보처리자격증");
    // no의 값이 case에 해당되는 경우
    // break 명령을 만날 때까지 아래로 계속 실행한다.
  case 2:
    System.out.println("졸업증명서");
  case 3:
    System.out.println("이력서");
    break; // 여기까지만 실행한다.
  default:
    System.out.println("올바른 번호를 입력하세요!");
}

```

- switch문의 흐름
  - 조건식을 계산한다.
  - 조건식의 결과가 일치하는 case문으로 이동한다.
  - 이후의 문장들을 수행
  - break문이나 switch문의 끝 default를 만나면 빠져나간다.

### switch문의 제약조건

- `switch (값) {}` 에서 값으로 가능한 데이터타입은?
  - int정수(byte, short,int, char), 문자열, 특별한 상수 Enum타입
  - case 값은 변수로 사용할 수 없다. 리터럴만 가능하다.

```java
int i = 2;
  switch (i) {
    case 1:
    case 2:
    default:
  }

char c = 'A'; // A문자의 유니코드 값(UTF-16) 0x41(65)을 c에 저장한다.
  switch (c) {
    // case 의 값도 int 값이면 무엇이든 된다.
    case 'A': // 0x41 = 65
    case 66:
    case 0x43:
    default:
  }

// String 값을 switch와 case의 값으로 사용할 수 있다.
String str = "hello";
  switch (str) {
    // case 의 값으로 String 가능하다.
    case "hello":
    case "ohora":
    case "hul":
    default:
  }
```

### switch문의 중첩

- switch문도 중첩으로 쓸 수 있다.
- 하지만 `break` 를 빼먹는 경우가 많아 지양한다.

```java
System.out.print("주민번호를 입력하세요 ex)001101-1111222 : ");

Scanner scanner = new Scanner(System.in);
Stirng regNo = scanner.nextLine();
char gender = regNo.charAt(7); //입력받은 8번째 문자를 저장

switch(gender) {
  case '1' : case '3':
    switch(gender) {
      case '1':
      System.out.println("당신은 2000년 이전에 출생한 남자입니다.");
      break;
      case '3':
      System.out.println("당신은 2000년 이후 출생한 남자입니다");
    }
    break; // 누락 없게 주의
  case '2' : case'4':
    switch(gender) {
      case '2':
      System.out.println("당신은 2000년 이전에 출생한 여자입니다.");
      break;
      case '3':
      System.out.println("당신은 2000년 이후 출생한 여자입니다");
      break;
    }
    break;
  default:
    System.out.println("유효하지 않은 주민등록번호 입니다.");
}
```

- 이처럼 여러번의 상황이 올수 있어 누락의 에러가 발생할 경우가 많다.
- 이런경우 되도록 if문을 사용하자.