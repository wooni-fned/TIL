# DDL (Data Definition Language)

DB 객체(테이블, 뷰, 프로시저, 함수, 트리거) 등을 생성, 변경, 삭제하는 SQL 명령

## 데이터베이스

- 생성

```sql
create database 데이터베이스명 옵션들...;
```

- 삭제

```sql
drop database 데이터베이스명 옵션들...;
```

- 변경

```sql
alter database 데이터베이스명 옵션들...;
```

## 테이블

테이블 생성

```sql
create table 테이블명 (
  컬럼명 타입 NULL여부 옵션,
  컬럼명 타입 NULL여부 옵션,
  ...
  컬럼명 타입 NULL여부 옵션
);
```

- 테이블 정보 보기

```sql
describe 테이블명;
desc 테이블명;
```

### 테이블 컬럼 옵션

- null 허용
데이터를 입력하지 않아도 된다.

```sql
create table test1 (
  no int,
  name varchar(20)
);
```

- not null
데이터를 입력하지 않으면 입력/변경 거절!

```sql
create table test1(
  no int not null,
  name varchar(20)
);
```

- 값 입력하기

```sql
insert into test1[테이블명](no, name) values[값](1, 'aaa');
```

- 기본값 지정하기
입력 값을 생략하면 해당 컬럼에 지정된 기본값이 대신 입력된다.

```sql
create table test1(
  no int not null,
  name varchar(20) default 'noname',
  age int default 20
);
```

컬럼에 default 옵션이 있는 경우,

- 컬럼 값을 생략하면 default 옵션으로 지정한 값이 사용된다.
- 컬럼 값을 null로 지정하면 기본 값이 사용되지 않는다.

### 컬럼 타입

#### int

- 4바이트 크기의 정수 값 저장
- 기타 tinyint(1바이트), smallint(2바이트), mediumint(3바이트), bigint(8바이트)

#### float

- 부동소수점 저장

#### numeric = decimal

- 전체 자릿수와 소수점 이하의 자릿수를 정밀하게 지정할 수 있다.
- numeric(n,e) : 전체 n 자릿수 중에서 소수점은 e 자릿수다.
  - 예) numeric(10,2) : 12345678.12
- numeric : numeric(10, 0) 과 같다.

#### char(n)

- 최대 n개의 문자를 저장.
- 0 <= n <= 255
- 고정 크기를 갖는다.
- 한 문자를 저장하더라도 n자를 저장할 크기를 사용한다.
- 메모리 크기가 고정되어서 검색할 때 빠르다.

#### varchar(n)

- 최대 n개의 문자를 저장.
- 0 ~ 65535 바이트 크기를 갖는다.
- n 값은 문자집합에 따라 최대 값이 다르다.
- 한 문자에 1바이트를 사용하는 ISO-8859-n 문자집한인 경우 최대 65535 이다.
- 그러나 UTF-8로 지정된 경우는, n은 최대 21844까지 지정할 수 있다.
- 가변 크기를 갖는다.
- 한 문자를 저장하면 한 문자 만큼 크기의 메모리를 차지한다.
- 메모리 크기가 가변적이라서 데이터 위치를 찾을 때 시간이 오래 걸린다.
  그래서 검색할 때 위치를 계산해야 하기 때문에 검색 시 느리다.

#### text(65535), mediumtext(약 1.6MB), longtext(약 4GB)

- 긴 텍스트를 저장할 때 사용하는 컬럼 타입이다.
- 오라클의 경우 long 타입과 CLOB(character large object) 타입이 있다.

#### date

- 날짜 정보를 저장할 때 사용한다.
- 년,월,일 정보를 저장한다.
- 오라클의 경우 날짜 뿐만 아니라 시간 정보도 저장한다.

#### time

- 시간 정보를 저장할 때 사용한다.
- 시, 분, 초 정보를 저장한다.

#### datetime

- 날짜와 시간 정보를 함께 저장할 때 사용한다.

#### boolean

- 보통 true, false를 의미하는 값을 저장할 때는 정수 1 또는 0으로 표현한다.
- 또는 문자로 Y 또는 N으로 표현하기도 한다.
- 실제 컬럼을 생성할 때 tinyint(1) 로 설정한다.

### 키 컬럼 지정

key column : 데이터를 구분할 때 사용하는 값

테이블:

- name, email, jumin, id, pwd, tel, postno, basic_addr, gender

#### key vs candidate key

- key
  - 데이터를 구분할 때 사용하는 컬럼들의 집합
  - 예)
    - {email}, {jumin}, {id}, {name, tel}, {tel, basic_addr, gender, name}
    - {name, jumin}, {email, id}, {id, name, email} ...
- candidate key (후보키 = 최소키)
  - key 들 중에서 최소 항목으로 줄인 키
  - {jumin}, {email}, {id}, {name, tel}

#### alternate key vs primary key

- primary key (주 키)
  - candidate key 중에서 DBMS 관리자가 사용하기로 결정한 키
  - 예) DBMS 관리자가 id 컬럼의 값을 데이터를 구분하는 키로 사용하기로 결정했다면,
    - 주 키는, {id} 가 된다.
    - 주 키로 선택되지 않은 모든 candidate key는 alternate key가 된다.
- alternate key (대안 키)
  - candidate key 중에서 primary key로 선택된 키를 제외한 나머지 키.
  - 비록 primary key는 아니지만, primary key 처럼 데이터를 구분하는
    용도로 대신 사용할 수 있다고 해서 **대안 키(alternate key)** 라 부른다.

#### artificial key (인공키)

- Primary key로 사용하기에 적절한 컬럼을 찾을 수 없다면,
  - 예) 게시글 : 제목, 내용, 작성자, 등록일, 조회수
- 이런 경우에 key로 사용할 컬럼을 추가한다.
- 보통 일련번호를 저장할 정수 타입의 컬럼을 추가한다.
  - 예) 게시글 : 게시글 번호
- 대부분의 SNS 서비스들은 일련의 번호를 primary key 사용한다.
- 왜?
  - 회원 탈퇴의 경우,
    - 회원 탈퇴할 때 아이디도 제거한다.
    - 아이디를 지우면 그 아이디와 연결된 게시글을 지워야 한다.
    - 그런데 회원 아이디 대신 일련 번호를 사용하면,
    - 그 회원이 쓴 게시글은 일련번호와 묶인다.
    - 따라서 아이디가 삭제되더라도 해당 글은 계속 유효하게 처리할 수 있다.
  - 이메일 변경,
    - primary key 값은 다른 데이터에서 사용하기 때문에,
      - 예) 게시글을 저장할 때 회원 이메일을 저장한다고 가정하자.
    - pk 값을 변경하면 그 값을 사용한 모든 데이터에 영향을 끼친다.
    - 그래서 PK 값을 다른 데이터에서 사용한 경우,
      DBMS는 PK 값을 변경하지 못하도록 통제한다.
    - 이렇게 변경될 수 있는 값인 경우, PK로 사용하지 말라.
    - 대신 회원 번호와 같은 임의의 키(인공 키)를 만들어 사용하는 것이 좋다.

#### primary key

- 테이블의 데이터를 구분할 때 사용하는 컬럼들이다.
- 줄여서 PK라고 표시한다.
- PK 컬럼을 지정하지 않으면 데이터가 중복될 수 있다.
- 두 개 이상의 컬럼을 묶어서 PK로 선언하고 싶다면 각 컬럼에 대해서 개별적으로 PK를 지정해서는 안된다.
- 여러 개의 컬럼을 묶어서 PK로 지정하려면 별도의 문법을 사용해야 한다.
  - constraint 제약조건이름 primary key (컬럼명, 컬럼명, ...)
  - 제약조건이름은 생략 가능.
  - 제약조건이름을 지정하지 않으면 이름이 자동으로 부여된다.
    그래서 나중에 제약조건을 찾기 힘들다.

#### unique = alternate key(대안키)

- PK는 아니지만 PK처럼 중복되어서는 안되는 컬럼을 지정할 때 사용한다.
- 그래서 PK를 대신해서 사용할 수 있는 key라고 해서 "대안키(alternate key)"라고 부른다.
- 즉 대안키는 DBMS에서 unique 컬럼으로 지정한다.

#### index

- 검색 조건으로 사용되는 컬럼인 경우 따로 정렬해 두면 데이터를 찾을 때 빨리 찾을 수 있다.
- 특정 컬럼의 값을 A-Z 또는 Z-A로 정렬시키는 문법이 인덱스이다.
- DBMS는 해당 컬럼의 값으로 정렬한 데이터 정보를 별도의 파일로 생성한다.
- 보통 책 맨 뒤에 붙어있는 색인표와 같다.
- 인덱스로 지정된 컬럼의 값이 추가/변경/삭제 될 때 인덱스 정보도 갱신한다.
- 따라서 입력/변경/삭제가 자주 발생하는 테이블에 대해 인덱스 컬럼을 지정하면,
  입력/변경/삭제 시 인덱스 정보를 갱신해야 하기 때문에
  입력/변경/삭제 속도가 느려지는 문제가 있다.
- 대신 조회 속도는 빠르다.

##### 인덱스 컬럼의 활용

검색할 때 사용한다.

```sql
select * from 테이블명 where 컬럼명 = '값';
```

### 컬럼 값 자동 증가

- 숫자 타입의 PK 컬럼 또는 Unique 컬럼인 경우 값을 1씩 자동 증가시킬 수 있다.
- 즉 데이터를 입력할 때 해당 컬럼의 값을 넣지 않아도 자동으로 증가된다.
- 단 삭제를 통해 중간에 비어있는 번호는 다시 채우지 않는다.
  즉 증가된 번호는 계속 앞으로 증가할 뿐이다.
- 특정 컬럼의 값을 자동으로 증가하게 선언한다.
- 단 반드시 key(primary key 나 unique)여야 한다.

## 뷰(view)

- 조회 결과를 테이블처럼 사용하는 문법
- select 문장이 복잡할 때 뷰로 정의해 놓고 사용하면 편리하다.
- view가 참조하는 테이블에 데이터를 입력한 후 view를 조회하면?
  - 새로 추가된 컬럼이 함께 조회된다.
- 뷰를 조회할 때 마다 매번 select 문장을 실행한다.
  - 미리 결과를 만들어 놓는 것이 아니다.
- 일종의 조회 함수 역할을 한다.
- 목적은 복잡한 조회를 가상의 테이블로 표현할 수 있어 SQL문이 간결해진다.

### 뷰 생성

```sql
create view 뷰테이블명
  as select 가져오고 싶은 컬럼명 from 테이블명 where 조회하고 싶은 컬럼 = '값';
```

### 뷰 삭제

```sql
drop view 뷰테이블명;
```

## 제약 조건 조회

- 테이블의 제약 조건 조회

```sql
select table_name, constraint_name, constraint_type
from table_constraints;
```

- 테이블의 키 컬럼 정보 조회

```sql
select table_name, column_name, constraint_name
from key_column_usage;
```
