# Byte Stream

바이트 단위로 출력하기

1. 파일로 데이터를 출력하는 객체를 준비한다.
   - new FileOutputStream(파일경로)
   - 지정된 경로에 해당 파일을 자동으로 생성한다.
   - 기존에 같은 이름의 파일이 있으면 덮어쓴다.
   - 주의! 기존 파일이 삭제된다.
   - 파일 경로가 절대 경로가 아니면
     - 리눅스,유닉스: / 로 시작하지 않으면,
     - 윈도우: c:\, d:\ 등으로 시작하지 않으면, 현재 디렉토리가 기준이 된다.

  `FileOutputStream out = new FileOutputStream("temp/test1.data");`

2. 1바이트를 출력한다.
   - write(int) : 1바이트를 출력하는 메서드이다.
   - 파라미터의 타입이 int라고 해서 4바이트를 출력하는 것이 아니다.
   - 오직 맨 끝 1바이트만 출력한다.

    ```java
      out.write(0x7a6b5c4d); // 출력하는 값은 0x4d 이다.
      out.write(2);     // 0x00000002
      out.write(40);    // 0x00000028
      out.write(100);   // 0x00000064
      out.write(101);   // 0x00000065
      out.write(102);   // 0x00000066
      out.write(127);   // 0x0000007f
      out.write(255);   // 0x000000ff
      out.write('A');   // 0x0041
      out.write('가');  // 0xac00
    ```

3. 출력 도구를 닫는다.
     - OS에서 관리하는 자원 중에서 한정된 개수를 갖는 자원에 대해여러 프로그램이 공유하는 경우, 항상 사용 후 OS에 반납해야 한다.
     - 그래야 다른 프로그램이 해당 자원을 사용할 수 있다.
       - 예) 파일, 메모리, 네트워크 연결 등
     - 이런 자원을 사용하는 클래스는 자원을 해제시키는 close()라는 메서드가 있다.
     - 보통 java.lang.AutoCloseable 인터페이스를 구현하고 있다.
     - 이번 예제에서 다루는 FileOutputStream 클래스에도 close()가 있다.
     - 따라서 FileOutputStream 객체를 사용한 후에는 close()를 호출하여 사용한 자원을 해제시켜야 한다.
     - close()를 호출하면, FileOutputStream이 작업하는 동안 사용했던 버퍼(임시메모리)를 비운다.
     - OS에서 제공한 파일과의 연결을 끊는다.

      `out.close();`

물론, JVM을 종료하면 JVM을 실행하는 동안 사용했던 모든 자원은 자동으로 해제된다.
이런 예제처럼 짧은 시간 동안만  실행되는 경우,
close()를 호출하지 않아도 자원을 해제시키는데 문제가 없다.
문제는 24시간 365일 멈추지 않고 실행하는 서버 프로그램인 경우
사용한 자원을 즉시 해제시키지 않으면
자원 부족 문제가 발생한다.

결론!

- 간단한 코드를 작성하더라도 AutoCloseable 인터페이스를 구현한 클래스를 사용할 때는 사용하고 난 후 자원을 해제시는 close()를 반드시 호출하라.

```java
파일 입출력 API 주요 클래스 (java.io 패키지)
1) 데이터 읽기
InputStream (추상 클래스)
  +-- FileInputStream : 바이트 단위로 읽기 (binary stream)

Reader (추상 클래스)
  +-- FileReader : 문자 단위로 읽기 (character stream)

2) 데이터 쓰기
OutputStream (추상 클래스)
  +-- FileOutputStream : 바이트 단위로 쓰기 (binary stream)

Writer (추상 클래스)
  +-- FileWriter : 문자 단위로 쓰기 (character stream)

## 바이너리 파일 vs 텍스트 파일
1) 바이너리 파일
- character set(문자표) 규칙에 따라 작성한 파일이 아닌 파일.
- 기본 텍스트 편집기(메모장, vi 에디터 등)로 편집할 수 없는 파일을 말한다.
- 만약 텍스트 편집기로 변경한 후 저장하면, 파일 포맷이 깨지기 때문에 무효한 파일이 된다.
- 예) .pdf, .ppt, .xls, .gif, .mp3, .jpg, .hwp, .mov, .avi, .exe, .lib 등
- 바이너리 파일을 편집하려면 해당 파일 포맷을 이해하는 전용 프로그램이 필요하다.

2) 텍스트 파일
- 특정 character set(문자표) 규칙에 따라 작성한 파일.
- 기본 텍스트 편집기(메모장, vi 에디터 등)로 편집할 수 있는 파일을 말한다.
- 예) .txt, .csv, .html, .js, .css, .xml, .bat, .c, .py, .php, .docx, .pptx, .xlsx 등
- 텍스트 파일은 전용 에디터가 필요 없다.
- 텍스트를 편집할 수 있는 에디터라면 편집 후 저장해도 유효하다.

바이너리 데이터 읽고, 쓰기
- 읽고 쓸 때 중간에서 변환하는 것 없이 바이트 단위로 그대로 읽고 써야 한다.
- InputStream/OutputStream 계열의 클래스를 사용하라.

텍스트 데이터 읽고, 쓰기
- 읽고 쓸 때 중간에서 문자 코드표에 따라 변환하는 것이 필요하다.
- Reader/Writer 계열의 클래스를 사용하라.
```

---

## byte 단위로 읽기

 1) 파일 데이터 읽기를 담당할 객체를 준비한다.

- new FileInputStream(파일경로)
- 해당 경로에 파일이 존재하지 않으면 예외가 발생한다.

    `FileInputStream in = new FileInputStream("temp/test1.data");`

2) 1바이트를 읽는다.

- read() 메서드의 리턴 타입이 int 라 하더라도 1바이트를 읽어 리턴한다.
- 이유?
  - 0 ~ 255까지의 값을 읽기 때문이다.
  - byte는 -128 ~ 127까지의 값만 저장한다.

  ```java
      int b = in.read(); // 읽은 값은 0x4d 이다.
      System.out.printf("%02x\n", b);

      System.out.printf("%02x\n", in.read());
      System.out.printf("%02x\n", in.read());
      System.out.printf("%02x\n", in.read());
      // read() 를 호출할 때마다 이전에 읽은 바이트의 다음 바이트를 읽는다.
  ```

3) 읽기 도구를 닫는다.

    `in.close();`

반복문을 사용한 예제

```java
    int b;

    //    while (true) {
    //      b = in.read();
    //      if (b == -1) // 파일의 끝에 도달하면 -1을 리턴한다.
    //        break;
    //      System.out.printf("%02x ", b);
    //    }

    while ((b = in.read()) != -1) { // 리팩토링
      System.out.printf("%02x ", b);
    }
```

### byte 배열 입출력

```java
FileOutputStream out = new FileOutputStream("temp/test1.data");

    byte[] bytes = {0x7a, 0x6b, 0x5c, 0x4d, 0x3e, 0x2f, 0x30};

    // write(byte[]) : 배열의 값 전체를 출력한다.
    // write(byte[], 시작인덱스, 출력개수) : 시작 위치부터 지정된 개수를 출력한다.
    //
    out.write(bytes); // 바이트 배열 전체를 출력한다.


FileInputStream in = new FileInputStream("temp/test1.data");
// 바이트들을 저장할 배열을 넉넉히 준비한다.
// => 이렇게 임시 데이터를 저장하기 위해 만든 바이트 배열을 보통 "버퍼(buffer)"라 한다.
//
byte[] buf = new byte[100];

// read(byte[])
// - 버퍼가 꽉 찰 때까지 읽는다.
// - 물론 버퍼 크기보다 파일의 데이터가 적으면 파일을 모두 읽어 버퍼에 저장한다.
// - 리턴 값은 읽은 바이트의 개수이다.
// read(byte[], 저장할 위치, 저장하기를 희망하는 개수)
// - 읽은 데이터를 "저장할 위치"에 지정된 방부터 개수만큼 저장한다.
// - 리턴 값은 실제 읽은 바이트 개수이다.
int count = in.read(buf);

in.close();

System.out.printf("읽은 바이트 수: %d\n", count);

for (int i = 0; i < count; i++)
  System.out.printf("%02x ", buf[i]);

```

실행결과

읽은 바이트 수: 3

5c 4d 3e 