# DML(Data Manipulation Language)

데이터 등록, 변경, 삭제를 다루는 SQL 문법

## insert

- 데이터를 입력할 때 사용하는 문법이다.
- 전체 컬럼 값 입력하기

컬럼을 지정하지 않으면 테이블을 생성할 때 선언한 컬럼 순서대로 값을 지정해야 한다.

```sql
-- 데이터 입력 문법
insert into 테이블명 values(값,....);
-- 2가지 이상 값을 입력할때
insert into 테이블명(컬럼,컬럼,...) values(값,값,...);

-- 여러개 값 입력 예시
insert into test1(name,tel) values
('aaa', '1111'),
('bbb', '2222'),
('ccc', '3333');
```

### select 결과를 테이블에 insert하기

- select 결과의 컬럼명과 insert 테이블의 컬럼명이 같을 필요는 없다.
- 그러나 결과의 컬럼 개수와 insert 하려는 컬럼 개수가 같아야 한다.
- 결과의 컬럼 타입과 insert 하려는 컬럼의 타입이 같거나 입력 할 수 있는 타입이어야 한다.

```sql
insert into 테이블명(컬럼,컬럼)
  select 컬럼, 컬럼 from 테이블명 where 컬럼 = '값';
```

## update

- 등록된 데이터를 변경할 때 사용하는 명령이다.

```sql
update 테이블명 set 컬럼명=값, 컬럼명=값, ... where 조건...;
```

단 조건을 지정하지 않으면, 모든 데이터에 대해 변경한다.

```sql
update 테이블명 set 컬럼명 ='값';
```

## delete

- 데이터를 삭제할 때 사용하는 명령이다.

```sql
delete from 테이블명 where 조건;
```

조건을 지정하지 않으면 모든 데이터가 삭제된다. **주의!**

```sql
delete from 테이블명;
```

## autocommit

mysql은 autocommit의 기본 값이 true이다.
따라서 명령창에서 SQL을 실행하면 바로 실제 테이블에 적용된다.
수동으로 처리하고 싶다면 autocommit을 false로 설정

```sql
set autocommit=false;
```

insert/update/delete을 수행한 후 승인을 해야만 실제 테이블에 적용된다.

```sql
commmit;
```

마지막 commit 상태로 되돌리고 싶다면,

```sql
rollback;
```