# json (JavaScript Object Natation)

- 자바스크립트 객체리터럴 문법을 모방하여 만든 텍스트 포맷 

## 객체 --> JSON 문자열 : 객체의 필드 값을 json 형식의 문자열로 만들기

JSON 객체 형식 - { 객체 정보 }
 => { "프로퍼티명" : 값, "프로퍼티명": 값, ...}

- 값:
  - 문자열 => "값"
  - 숫자 => 값
  - 논리 => true, false

프로퍼티명은 반드시 문자열로 표현해야 한다.

```java
public class ExamJson {
  public static void main(String[] args) {

    // 1) 객체 준비
    Member m = new Member();
    m.setNo(100);
    m.setName("홍길동");
    m.setEmail("hong@test.com");
    m.setPassword("1111");
    m.setPhoto("hong.gif");
    m.setTel("010-2222-1111");
    m.setRegisteredDate(new Date(System.currentTimeMillis()));

    // 2) JSON 처리 객체 준비
    Gson gson = new Gson();

    // 3) 객체의 값을 JSON 문자열로 얻기
    String jsonStr = gson.toJson(m);

    System.out.println(jsonStr);
  }
}
```

### Gson vs Jackson 출력시 프로퍼티명 차이점

property (setter/getter)

```java
class Member {
  Stirng nm; //  필드명 nm

  void setName(...) { // porperty명 = name
    ...
  }
  void getName(...) {
    ...
  }
}
```

 property명과 필드명이 다를경우

 Gson은 필드명 사용
 Jackson은 property명 사용

필드명과 property명은 무조건 똑같이 사용하자!

## 객체 -> JSON 문자열 : 객체의 필드 값을 json 형식의 문자열로 만들기

```java
public class ExamJson2 {
  public static void main(String[] args) {

    // 1) JSON 문자열 준비
    String jsonStr =
        "{\"no\":100,\"name\":\"홍길동\",\"email\":\"hong@test.com\",\"password\":\"1111\",\"photo\":\"hong.gif\",\"tel\":\"010-2222-1111\",\"registeredDate\":\"7월 03, 2023\"}";

    // 2) JSON 처리 객체 준비
    Gson gson = new Gson();

    // 3) JSON 문자열을 가지고 객체 만들기
    Member m = gson.fromJson(jsonStr, Member.class);

    System.out.println(m);
  }
}
```

출력 : Member [no=100, name=홍길동, email=hong@test.com, password=1111, photo=hong.gif, tel=010-2222-1111, registeredDate=2023-07-03]

만약 property 이름이 다르다면 null값을 출력한다.

`name -> nm`으로 변경할 경우 `name = null`

### 날짜 형식을 yyyy-MM-dd 형식으로 출력하기

위 코드에서 날짜형식을 dd-MM-yyyy 대신 yyyy-MM-dd 형식으로 출력해보자

2가지 방식중 첫번째

1. Gson 객체생성

```java
GsonBuilder builder = new GsonBuilder();
builder.setDateFormat("yyyy-MM-dd");
Gson gson = builder.create();
```

위 코드를 한줄로 작성하면 아래와 같다.

```java
Gson gson = new GsonBuilder().setDateFormat("yyyy-MM-dd").create();
```

기존 Gson 객체 생성을 GsonBuilder으로 생성하여 Format을 재설정 해준다.

Date타입의 프로퍼티 값을 JSON 문자열로 바꿔준다.

2. JsonSerializer (직렬화로 처리하는방법)

```java
public class JsonSerializer {
  public static void main(String[] args) {

    // 1) 객체 준비
    Member m = new Member();
    m.setNo(100);
    m.setName("홍길동");
    m.setEmail("hong@test.com");
    m.setPassword("1111");
    m.setPhoto("hong.gif");
    m.setTel("010-2222-1111");
    m.setRegisteredDate(new Date(System.currentTimeMillis()));

    // 2) JSON 처리 객체 준비
    // Date타입의 값을 내보내고 가져올 때 사용할 변환 도구를 준비
    class GsonDateFormatAdepter implements JsonSerializer<Date> {

      private DateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd");

      @Override
      public JsonElement serialize(Date src, Type typeOfSrc, JsonSerializationContext context) {
        // 객체를 JSON문자로 변환할 때 호출한다.
        // 그 중 Date 타입의 프로퍼티 값을 JSON 문자열로 바꿀 때 호출된다.
        // JsonElement에 담아서 리턴
        return new JsonPrimitive(dateFormat.format(src));
      }
    }

    GsonBuilder builder = new GsonBuilder();

    // Date 타입의 프로퍼티 값을 JSON형식의 문자열로 바꿔줄 변환기를 등록.
    builder.registerTypeAdapter(Date.class, // 원래의 데이터타입
        new GsonDateFormatAdepter()/* Date 형식의 데이터 출력을 도와줄 객체 */
    );

    Gson gson = builder.create();
    // 3) 객체의 값을 JSON 문자열로 얻기
    String jsonStr = gson.toJson(m);

    System.out.println(jsonStr);
  }
}
```

3. JsonDeserializer

```java
public class JsonDeserializer {
  public static void main(String[] args) {

    // 1) JSON 문자열 준비
    String jsonStr =
        "{\"no\":100,\"name\":\"홍길동\",\"email\":\"hong@test.com\",\"password\":\"1111\",\"photo\":\"hong.gif\",\"tel\":\"010-2222-1111\",\"registeredDate\":\"2023-07-03\"}";

    // 2) JSON 처리 객체 준비
    class GsonDateFormat implements JsonDeserializer<Date> {
      @Override
      public Date deserialize(JsonElement json, Type typeOfT, JsonDeserializationContext context)
          throws JsonParseException {
        // JSON 문자열을 자바 타입의 값으로 바꿀 떄 호출된다.
        // 특히 Date타입의 값으로 바꿀 떄 호출된다.
        String strValue = json.getAsString();
        return Date.valueOf(strValue); // yyyy-MM-dd -> Date
      }
    }

    GsonBuilder builder = new GsonBuilder();
    builder.registerTypeAdapter(Date.class, new GsonDateFormat());
    Gson gson = builder.create();

    // 3) JSON 문자열을 가지고 객체 만들기
    Member m = gson.fromJson(jsonStr, Member.class);

    System.out.println(m);
  }
}
```

## JSON 배열 다루기

```java
JSON 배열 형식 - [{ 객체 정보 },{ 객체 정보}, ...]

 => [
      {"프로퍼티명":값,"프로퍼티명":값, ...}, 
      {"프로퍼티명":값,"프로퍼티명":값, ...},
      {"프로퍼티명":값,"프로퍼티명":값, ...},
      ...
    ]
```

```java
public class JsonArray {
  public static void main(String[] args) {

    // 1) 배열 준비
    Member m1 = new Member();
    m1.setNo(101);
    m1.setName("홍길동");
    m1.setEmail("hong@test.com");
    m1.setRegisteredDate(new Date(System.currentTimeMillis()));

    Member m2 = new Member();
    m2.setNo(102);
    m2.setName("임꺽정");
    m2.setEmail("leem@test.com");
    m2.setRegisteredDate(new Date(System.currentTimeMillis()));

    Member m3 = new Member();
    m3.setNo(103);
    m3.setName("안창호");
    m3.setEmail("ahn@test.com");
    m3.setRegisteredDate(new Date(System.currentTimeMillis()));

    Member[] members = {m1, m2, m3};

    String jsonStr = new Gson().toJson(members);

    System.out.println(jsonStr);
  }
}

```

 출력 : [{"no":101,"name":"홍길동","email":"hong@test.com","registeredDate":"7월 3, 2023"},
 {"no":102,"name":"임꺽정","email":"leem@test.com","registeredDate":"7월 3, 2023"},
 {"no":103,"name":"안창호","email":"ahn@test.com","registeredDate":"7월 3, 2023"}]

객채마다 {} 로 구분된다.

```java
public class JsonArrays {
  public static void main(String[] args) {

    String jsonStr = "[{\"no\":101,\"name\":\"홍길동\"},{\"no\":102,\"name\":\"임꺽정\"},{\"no\":103,\"name\":\"안창호\"}]";

    Member[] members = new Gson().fromJson(jsonStr, Member[].class);

    for (Member m : members) {
      System.out.println(m);
    }
  }
}
```

출력 :
Member [no=101, name=홍길동, email=null, password=null, photo=null, tel=null, registeredDate=null]
Member [no=102, name=임꺽정, email=null, password=null, photo=null, tel=null, registeredDate=null]
Member [no=103, name=안창호, email=null, password=null, photo=null, tel=null, registeredDate=null]
