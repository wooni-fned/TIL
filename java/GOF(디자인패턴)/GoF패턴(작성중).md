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

## Template Method

여러 클래스에서 공통으로 사용하는 메서드를 템플릿화 하여 상위 클래스에서 정의하고, 하위 클래스마다 세부 동작 사항을 다르게 구현하는 패턴

변하지 않는 기능(템플릿)은 상위 클래스에 만들어두고 자주 변경되며 확장할 기능은 하위 클래스에서 만들도록 하여, 상위의 메소드 실행 동작 순서는 고정하면서 세부 실행 내용은 다양화 될 수 있는 경우에 사용된다.

템플릿 메소드 패턴은 상속이라는 기술을 극대화하여, 알고리즘의 뼈대를 맞추는 것에 초점을 둔다.

![](https://s3.ap-northeast-2.amazonaws.com/yaboong-blog-static-resources/diagram/template-method-pattern.png)

위와 같은 구조의 템플릿 메소드 패턴 적용에 대한 코드이다.

**AbstractClass.java**

```java
public abstract class AbstractClass {
    
    protected abstract void hook1();
    
    protected abstract void hook2();
    
    public void templateMethod() {
        hook1();
        hook2();
    }
    
}
```

**ConcreteClass**

```java
public class ConcreteClass extends AbstractClass {

    @Override
    protected void hook1() {
        System.out.println("ABSTRACT hook1 implementation");
    }

    @Override
    protected void hook2() {
        System.out.println("ABSTRACT hook2 implementation");
    }

}
```

**TemplateMethodPatternClient.java**

```java
public class TemplateMethodPatternClient {
    public static void main(String[] args) {
        AbstractClass abstractClass = new ConcreteClass();
        abstractClass.templateMethod();
    }
}
```

추상클래스인 AbstractClass 에는 실제로 실행을 위해 호출 될 public 메소드인 templateMethod 가 정의되어 있고,
templateMethod 내부에는 hook1 -> hook2 의 단계를 가지는 추상메소드가 호출된다.
이 추상메소드들은 AbstractClass 를 상속받아 구현한 ConcreteClass 에서 구체적인 구현이 정의된다.

## DAO 와 Proxy 패턴

## Flyweight 패턴 (스레드 풀)