# 멀티태스킹 Thread

**들어가기 전에**

**멀티태스킹이란?**
 > 동시에 여러가지 작업을 실행하는것을 말한다.

**운영체제** 에서 멀티태스킹

여러 프로그램을 실행하는것이라 한다.

엑셀로 문서작업을 하며 앱플레이어로 노래를 듣고 포토샵으로 사진을 편집하는것 처럼

각각의 프로세스(실행 중인 프로그램)을 동시에 실행하는 것을 의미한다.

프로세스 기반의 멀티태스킹에서는 병행 처리 단위가 프로세스인 것이다.

![멀티태스킹의 예시](https://t1.daumcdn.net/cfile/tistory/2117883C55C88F680F?original)

그럼 멀티태스킹 = 멀티프로세스 라는 말이 성립이 되는가?
아니다.

![멀티프로세스 예시](https://velog.velcdn.com/images%2Fchy0428%2Fpost%2F64d411b0-0f60-48e0-897e-f535e98ee9d0%2Fimage.png)

프로세스는 `'작업(task)'` 이라는 용어와 같은 의미로 쓰인다.
이말인 즉슨 `1프로세스 = 1작업` 이라는 말과 같다.

예를 들면 똑같은 포토샵 프로그램을 여러게 띄워두고 각각 다른 사진을 작업 한다.
이는 각 프로세스마다 다른 작업을 하는것이라 이해하면 된다.

그렇다면 컴퓨터에서는 어떻게 처리하는가?
프로그램은 하드디스크에 저장되어 있는 실행 코드를 말하는 것이고
프로세스는 프로그램을 구동하여 프로그램 자체와 프로그램의 상태가 메모리 상에서 실행되는 작업의 단위인 것이다.

앞서 말한것 처럼 하나의 포토샵프로그램을 여러 작업하면 하나의 포토샵 프로세스가 작동 되는것이 아니고
각 포토샵 프로세스 마다 메모리를 할당받아 작동됨으로 프로그램에러가 아닌이상 모든 작업이 날라가진 않는다.

![스레드](https://images.velog.io/images/nnnyeong/post/32d38229-c301-46f3-889c-cfaa479d1eea/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-03-07%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.49.40.png)

그렇다면 스레드는?

- 프로세스 내에서 실행되는 흐름의 단위를 말한다.
- 프로세스가 할당받은 메모리를 이용하는 실행단위이다.

멀티스레드는?

- 하나의 응용 프로그램에서 여러 스레드를 구성해 각 스레드가 하나의 작업을 처리하는것

이와 같이 동시에 여러 작업을 하는것을 멀티태스킹 행위를 하는 스레드를 멀티스레드라고 말하는 것이니

용어에 있어서 잠시 내가알던 멀티태스킹이 아닌데? 라는 의문에서 정리하였다.

## Thread

- '실'이라는 뜻을 갖고 있다.
- 한 실행 흐름을 가리킨다.
- 하나의 실은 끊기지 않은 하나의 실행 흐름을 의미한다.

## 스레드생성

- 새 실을 만든다는 것이다.
- 즉 새 실행 흐름을 시작하겠다는 의미다.
- CPU는 스레드를 프로세스와 마찬가지로 동일한 자격을 부여하여
 스케줄링에 참여시킨다.
- 즉 프로세스에 종속된 스레드라고 취급하여
 한 프로세스에 부여된 실행 시간을 다시 쪼개 스레드에 나눠주는 방식이 아니다.
- 그냥 단독적인 프로세스처럼 동일한 실행 시간을 부여한다.

## 스레드 구현하기

```java
public static void main(String[] args){ 
  // 첫째, 스레드를 상속받아 정의 한다.
  class MyThread extends Thread {
     @Override
      public void run() {
      // 별도로 분리해서 병행으로 실행할 코드를 두는 곳!
        for (int i = 0; i < 100; i++) {
          System.out.println("* " + i);
        }
      }
  }
  // 스레드 실행
  // => Thread의 서브 클래스는 그냥 인스턴스를 만들어 start()를 호출한다.
  MyThread t = new MyThread();
  t.start(); // 실행 흐름을 분리한 후 즉시 리턴한다. 비동기로 동작한다.

  // "main" 스레드는 MyThread와 상관없이 병행하여 실행한다.
  for (int i = 0; i < 1000; i++) {
    System.out.println(">>>> " + i);
  }
  
}
```

## Runnable 인터페이스를 사용하여 구현

```java
public static void main(String[] args) {

    // Runnable 인터페이스를 구현하기
    // => 인터페이스를 구현하는 것이기 때문에 다른 클래스를 상속 받을 수 있다.
    // => 직접적으로 스레드가 아니기 때문에 실행할 때는 Thread의 도움을 받아야 한다.
    class MyRunnable implements Runnable {
      @Override
      public void run() {
        // 별도로 분리해서 병행으로 실행할 코드를 두는 곳!
        for (int i = 0; i < 1000; i++) {
          System.out.println("===> " + i);
        }
      }
    }

    // 스레드 실행하기
    // => Runnable 구현체를 Thread 객체에 실어서 실행한다.
    // => start()를 호출하여 기존 스레드에서 분리하여 스레드를 실행시킨다.
    Thread t = new Thread(new MyRunnable());
    t.start(); // 실행 흐름을 분리한 후 즉시 리턴한다.

    // "main" 스레드는 Thread와 상관없이 병행하여 실행한다.
    for (int i = 0; i < 1000; i++) {
      System.out.println(">>>> " + i);
    }

  }

```

## 스레드 메서드

현재 실행중인 흐름의 이름을 찾기

```java
Thread t = Thread.currentThread();
System.out.println("실행 흐름명 = " + t.getName());
```

현재 소속된 그룹 찾기

```java
ThreadGroup group = main.getThreadGroup();
System.out.println("그룹명 = " + group.getName());
```

그룹에 소속된 스레드 찾기

```java
Thread main = Thread.currentThread();
ThreadGroup mainGroup = main.getThreadGroup();
Thread[] arr = new Thread[100];
int count = mainGroup.enumerate(arr, false);
// 두 번째 파라미터 값을 false로 지정하면,
// 하위 그룹에 소속된 스레드들은 제외한다.
// 즉, 현재 그룹에 소속된 스레드 목록만 가져오라는 뜻!

System.out.println("main 그룹에 소속된 스레드들:");
for (int i = 0; i < count; i++)
  System.out.println("   => " + arr[i].getName());
```

출력 :
main 그룹에 소속된 스레드들:
   => main

스레드 그룹에 소속된 하위 그룹 찾기

```java
Thread main = Thread.currentThread();
ThreadGroup mainGroup = main.getThreadGroup();

ThreadGroup[] groups = new ThreadGroup[100];
int count = mainGroup.enumerate(groups, false);
// 두 번째 파라미터 값을 false로 지정하면,
// 하위 그룹에 소속된 그룹들은 제외한다.
// 즉, 현재 그룹에 소속된 하위 그룹의 목록만 가져오라는 뜻!

System.out.println("main 그룹에 소속된 하위 그룹들:");
for (int i = 0; i < count; i++)
  System.out.println("   => " + groups[i].getName());
```

스레드 그룹의 부모 그룹 찾기

```java
Thread main = Thread.currentThread();
ThreadGroup mainGroup = main.getThreadGroup();

ThreadGroup parentGroup = mainGroup.getParent();
System.out.printf("main 스레드 그룹의 부모: %s\n", parentGroup.getName());

// "system" 그룹의 부모 그룹은?
ThreadGroup grandparentGroup = parentGroup.getParent();
if (grandparentGroup != null) {
  System.out.printf("%s 스레드 그룹의 부모: %s\n", 
      parentGroup.getName(), 
      grandparentGroup.getName());
}
```

출력:

main 스레드 그룹의 부모: system

스레드 그룹의 자식그룹 찾기

```java
Thread main = Thread.currentThread();
ThreadGroup mainGroup = main.getThreadGroup();
ThreadGroup systemGroup = mainGroup.getParent();

ThreadGroup[] groups = new ThreadGroup[100];
int count = systemGroup.enumerate(groups, false);

System.out.println("system 스레드 그룹의 자식 그룹들:");
for (int i = 0; i < count; i++) {
  System.out.println("   =>" + groups[i].getName());
}
```

출력 :
system 스레드 그룹의 자식 그룹들:
   =>main
   =>InnocuousThreadGroup

system 스레드 그룹에 소속된 스레드

```java
Thread main = Thread.currentThread();
ThreadGroup mainGroup = main.getThreadGroup();
ThreadGroup systemGroup = mainGroup.getParent();

Thread[] arr = new Thread[100];
int count = systemGroup.enumerate(arr, false);

System.out.println("system 스레드 그룹에 소속된 스레드들:");
for (int i = 0; i < count; i++) {
  System.out.println("   =>" + arr[i].getName());
}
```

JVM 전체 스레드 계층도

```java
public static void main(String[] args) {
    // JVM의 최상위 스레드 그룹인 system의 계층도 출력하기
    Thread mainThread = Thread.currentThread();
    ThreadGroup mainGroup = mainThread.getThreadGroup();
    ThreadGroup systemGroup = mainGroup.getParent();

    printThreads(systemGroup, "");
  }

static void printThreads(ThreadGroup tg, String indent) {
  System.out.println(indent + tg.getName() + "(TG)");

  // 현재 스레드 그룹에 소속된 스레드들 출력하기
  Thread[] threads = new Thread[10];
  int size = tg.enumerate(threads, false);
  for (int i = 0; i < size; i++) {
    System.out.println(indent + "  ==> " + threads[i].getName() + "(T)");
  }

  // 현재 스레드 그룹에 소속된 하위 스레드 그룹들 출력하기
  ThreadGroup[] groups = new ThreadGroup[10];
  size = tg.enumerate(groups, false);
  for (int i = 0; i < size; i++) {
    printThreads(groups[i], indent + "  ");
  }
}
```