# Stack, Queue

- 자료 구조의 형식
- breadcrumb : 빵부스러기
- 폴더 경로를 부르는 다른말

## Stack

- 구동원리
  - Last in first out (LIFO)
  - 가장 마지막에 들어간것이 먼저 나오는 구조

![stack](https://www.mbaskool.com/2020_images/stories/dec_images/lifo.jpg)

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

## Queue

1. 구동원리
   - First in first out (FIFO)
   - 처음 들어간 것이 처음 나오는 구조
2. 어떤 상황에서 사용하나?
   - 명령어 입력 History 기능에 적용
   - 예약/ 주문 받을때
3. 구현
   - offer()
   - poll()
4. 적용
   - 가장 최근 실행한 메뉴목록 20개 저장
