# 메소드(method)

- 특정 기능을 수행하는 명령문을 관리하기 쉽게 한 단위로 묶는 문법
- 복잡한 코드를 메서드 안에 감춘다 (캡슐화 (encapsulation))

```java
리턴데이터타입  메서드명(아규먼트를 받을 변수목록) {
  명령문
  .
  .
  return 작업결과값 ;
}

static int plus(int a, int b)  {
  int sum = a + b;
  return sum;
}

```

## 메소드명과 클래스명 관례

- 메소드명
  - 동사 : print(), copy()
  - 동사구 : printMember, addMember()
  - 전치사구 : toString(), fromJson()
  - 명사/명사구 : name(), email()
- 