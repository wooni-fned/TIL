# Stack, Queue

- 자료 구조의 형식
- breadcrumb : 빵부스러기
- 폴더 경로를 부르는 다른말

## Stack

- Last in first out (LIFO)
- 가장 마지막에 들어간것이 먼저 나오는 구조

### Stack 인스턴스

```java
public class Member {
  String name;
  String email;
  String password;
}

public class Stack extends Member {
  String school;
  String major;
  boolean working; 
}
```