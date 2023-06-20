# java 반복문

- 반복문
  - while문
  - for문
    - 반복횟수를 알고있을때 사용

## for문

- for문의 구조
  - `for (초기화; 조건식; 증감식) {문장}`
    - 초기화
      - 반복문에 사용될 변수를 초기화 하는 부분 처음에 한번만 수행
      - 변수 하나로 for문을 제어하지만 두가지의 변수가 필요할 경우 `,`를 사용해 쓸수있다.
      - `for (int i = 0, j =1; i < 10; i++)`
      - 단, 두변수의 타입은 같아야 한다.
    - 조건식
      - 조건식의 값이 참이면 계속 반복하고 거짓이면 중단한다.
    - 증감식
      - 반복문을 제어하는 변수의 값을 증가 또는 감소시키는 식이다.
      - 반복마다 변수의 값이 증감식에 의해서 변하다 조긴식이 거짓이 되어 for문을 벗어난다.
      - 주로 값을 1씩 증가시키는 `++` 증감연산자가 많이 사용된다.
      - 다영한 연산자를 통해 증감식사용도 가능하다.
      - ex) `i--`, `i += 2`, `i *=3`
      - 쉼표를 이용해 2가지의 증감식 작성도 가능하다
      - `for (int i = 0, j = 10; i < 10; i++, j--)`
- 이 3가지 요소는 필요하지 않을 경우 생략도 가능하다.
  - `for(;;)` 단 조건식의 기본값은 참이된다.
  - 조건식이 생략된 경우 무한반복문이 된다.

```java
// for문 기본 예시
for (int i = 1; i <= 5; ++i)
  System.out.println(i);

// 모든 요소를 밖으로 뺀 경우
int i = 1;
for (  ;  ;  ) {
  if (i > 5)
    break;
  System.out.println(i);
  i++;

// 반복문 종료한 뒤에도 변수의 값을 사용하고 싶다면
// 반복문 밖에 변수를 선언하여 사용하면 된다.
int x;
  for (x = 1; x <= 5; x++) {
    System.out.println(x);\
  }
  System.out.printf("x = %d\n", x);
}
```

### for문과 배열 

- for (:)
  - 배열 전체를 반복하거나 컬렉션 객체 전체를 반복할 때 유용하다.
  - 배열의 일부만 반복할 수 없다.
  - 배열의 값을 다룰 때 인덱스를 사용할 필요가 없어 편리하다.
- 문법:
  - for (변수 선언 : 배열, Iterable 구현체) 문장1;
  - for (변수 선언 : 배열, Iterable 구현체) { 문장1; 문장2; ...}
  - 변수의 타입은 배열이나 Iterable 구현체의 항목 타입과 같아야 한다.
  - 반복문을 돌 때 마다 항목을 값을 꺼내 변수에 담는다.

```java
String[] names = { "홍길동", "임꺽정", "유관순", "윤봉길", "안중근" };
// for (배열에서 꺼낸 값을 저장할 변수 선언 : 배열주소) 문장;
for (String name : names)
  System.out.printf("%-1s\t ", name);


// 아래처럼 배열의 값을 계산할때 유용하다.
String name = "";
for (String item : names)
  name += item;
System.out.println(name);
```

## while문

- 조건이 참인경우 거짓이 될때 까지 문장을 계속 반복한다.
- 조건식이 거짓이 될경우 벗어난다
- 조건은 생략이 불가하고 조건식은 항상 참이다.

```java
//      while (조건)
//          문장;
// => 조건이 참인 동안 문장을 계속 실행한다.
count = 0;
while (count < 5)
  System.out.println(count++);


//      while (조건) {}
// => 여러 개의 문장을 반복 실행하려면 블록으로 묶어라!
count = 0;
while (count < 5) {
  System.out.println(count);
  count++;
}
```

- while문의 경우 조건식이 상수는 아니지만 변수가 고정된 값을 유지함므로 무한반복문과 다름없다.
- 특정조건을 만족할 때 반복문을 멈추게 하는 if문이 반복문 안에 꼭 필요하다.

### do ~ while

- while문의 변형으로 기본구조는 while문과 같으나 조건식과 블럭의 순서를 바꿔 놓은것
- while문과 반대로 블럭`{}`을 먼저 수행 후 조건식을 평가한다.
- while문은 조건식의 결과에따라 블럭이 한번도 수행되지 않을 수 있지만 do~while문은 최소 한번은 수행하는것을 보장한다.
- 기본문법

```java
do {
  //조건식의 연산결과가 참일 떄 수행될 문장을 적는다.
} while (조건식);  // 끝에 ; 을 누락하지 않게 주의

// 입력값이 369 일때 박수를 치는 예제
for(int i = 0; i <= 100 ; i++) {
    System.out.printf("i = %d ", i);
    
    int tmp = i;
    
    do {
      if (tmp % 3 == 0 && tmp % 10 !=0) {
        System.out.print("짝");
      } 
      
    } while ((tmp/=10) !=0);
    System.out.println();
  }
```

## break

- 자신이 포함된 가장 가꾸운 반복문을 벗어난다.
- 주로 if문과 함꼐 사용되어 특정 조건을 만족하면 반복문을 벗어나도록 한다.

```java
// break
for (int i = 1; i <= 10; i++) {
      for (int j = 1; j <= i; j++) {
        System.out.print(j + " ");
        if (j == 5)
          break; // break 소속된 현재 반복문을 멈춘다.
      }
      System.out.println();
      if (i == 5)
        break;
    }

// for문에 break라벨링을 통해 지정한 문장에서 나갈 수 있다.
loop1: {
      for (int i = 1; i <= 10; i++) {
        for (int j = 1; j <= i; j++) {
          System.out.print(j + " ");
          if (j == 5)
            break loop1; // 라벨로 지정한 문장을 나간다.
        }
        System.out.println();
      }
      System.out.println("-------------------------");
    }
    System.out.println("loop1 밖!");
```

## continue

- 반복문 내에서만 사용이 가능하다.
- 반복이 진행되는 도중 continue문을 만나면 반복문의 끝으로 이동하여 다음반복으로 넘어간다.
- for문의 경우 증감식으로 이동
- while문과 do ~ while문의 경우 조건식으로 이동한다.
- 주로 if문과 함께 사용되며 특정조건을 만족하는 경우 continue문의 이후의 문장들을 수행하지 않고 다음 반복으로 넘어가서 계속 진행하게 된다.
- 전체 반복중에 특정조건을 만족하는 경우를 제외하고자 할때 유용하다.

```java
// continue
for (int i = 1; i <= 10; i++) {
  if (i % 2 == 0)
    continue;
  for (int j = 1; j <= i; j++) {
    if (j % 2 == 0) {
      continue;
    } // 다음 줄로 가지 않고 '변수증가문'으로 이동한다.
    System.out.print(j + " ");
  }
  System.out.println();
}
```