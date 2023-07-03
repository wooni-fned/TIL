# GoF패턴

## Command 패턴

- 

## Observer 패턴

- 객체의 상태가 변경 되었을때 보고받아서 처리하는 경우
- 옵저버들의 목록을 객체에 등록하여 상태 변화가 있을때 마다 메서드 등을 통해 객체가 직접 목록의 옵저버에게 통지하도록 하는 디자인 패턴
- 주로 분산 이벤트 핸들링 시스템을 구현하는데 사용
- 발행 / 구독 모델로 알려져있다.
- 간단히 어떤 객체의 상태가 변할 때 그와 연관된 객체 들에게 알림을 보내는 디자인 패턴

### Observer 패턴의 동작원리

## Interator 패턴

- 무언가 많이 모여있는 것을 하나씩 지정해서 순서대로 처리하는 패턴
- 무언가를 반복한다는 의미

```java
​for (int i = 0; i < n; i++) {
    System.out.println(array[i]);
}
```

for문 초기호화문에서 사용되는 i 변수의 역할을 추상화 한것이다.

- interface 문법
- Nested 클래스 문법
- Interator 사용법

## Factory Method 패턴


## Builder패턴

```java
GsonBuilder builder = new GsonBuilder();
builder.setDateFormat("yyyy-MM-dd");
Gson gson = builder.create();
```

```java
Gson gson = new GsonBuilder().setDateFormat("yyyy-MM-dd").create();
```