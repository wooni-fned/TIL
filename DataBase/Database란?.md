# DataBase / DB

- 데이터를 저장한 파일
- 데이터 저장소
- 구조화된 데이터 집합
- 통합하여 관리되는 데이터의 집합체

중복된 데이터를 없애고 자료를 구조화 하여 효율적인처리를 할수있도록 관리

## DataBase특징

- 실시간으로 접근이 가능
- 동시에 공유 가능

## DBMS (DataBase Management System)

데이터베이스를 관리하고 운영하는 소프트웨어

### DBMS 특징

- 데이터의 독립성
  - 물리적 독립성
    - 데이터베이스 사이즈를 늘리거나 성능 향상을 위해 데이터 파일을 늘리거나 새롭게 추가하더라도 관련된 응용프로그램을 수정할 필요가 없다.
  - 논리적 독립성
    - 데이터베이스는 다양한 응용프로그램의 논리적 요구를 만족시킨다.

- 데이터의 무결성
  - 여러경로를 통해 잘못된 데이터가 발생하는 경우의 수를 방지하는 기능으로 데이터의 유효성 검사를 통해 데이터의 무결성을 구현
  - 입력 조건에 맞지않는 입력값은 저장할 수 없도록 방지하는 기능이 있다.

- 데이터의 보안성
  - 허가된 사용자들만 데이터베이스 내 자원에 접근할 수 있도록 계정관리, 접근권한을 설정하여 데이터 보안을 구현한다.

- 데이터의 일관성
  - 연관된 정보를 논리적인 구조로 관리함으로써 어떤 하나의 데이터만 변경하였을 경우 발생할 수 있는 데이터의 불일치성을
    배제할 수 있다.
  - 작업 중 일부 데이터만 변경하여 일치하지 않는 경우의 수를 배제할 수 있다.

- 데이터의 중복 최소화
  - 데이터베이스는 데이터를 통합하여 관리함으로써 데이터 중복 문제를 해결할 수 있다.

### DBMS 종류

![계층형 데이터베이스](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdZaBYI%2FbtqvWT3JyZN%2FiI0zGfphdDhGJ0iDcpZjf1%2Fimg.png)

#### 계층형 데이터베이스 (Hierarchical DataBase) : 1960년대

- 데이터 간의 관계가 트리형 구조
- 트리형은 부모 자식간에 1 : N (일 대 다)로 구성될수 있다.
- 데이터를 세그먼트 단위로 관리하며 세그먼트간 계층을 트리구조로 관리한다.
- 구조가 간단하고 구현, 수정, 검색이 쉽다
- 부모자식간의 N : N (다 대 다) 처리가 불가능하고, 구조변경이 어렵다
- DBMS 예 : IMS ( IBM 의 Information Management System )

> 세그먼트 (Segment)란?
> 데이터 저장이 필요한 하나의 객체를 저장하는 단위. ( 테이블, 인덱스 등 )
> 예를 들어, board 테이블을 만들면 하나의 세그먼트가 생성이 되는 것

![네트워크형 데이터베이스](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcNxiAE%2FbtqvWT3JzO2%2FDjPnDemTAg1EG9d1jrF9Z1%2Fimg.png)

#### 네트워크형 데이터베이스 (Network DataBase) : 1960년대

- 계층형 데이터베이스의 단점을 보완하여 데이터 간 N:N (다 대 다) 구성이 가능한 망 형 모델
- 계층 구조에 링크를 추가하여 유연성과 접근성을 높였다
- 구조가 복잡해 유지보수가 어렵다.
- DBMS 예 : IDMS ( Integrated Data Store )

![관계형 데이터베이스](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbA3p5L%2FbtqvUzr3CzF%2F9KUYqtE9Di6DJq1Fqh3cx1%2Fimg.png)

#### 관계형 데이터베이스 (Relational DataBase) : 1970년대

- 관계형 데이터베이스 모델은 키(key)와 값(value)으로 이루어진 데이터들을 행(row)과 열(column)로 구성된 테이블 구조로 단순화 시킨 모델
- SQL (Structured Query Language) 를 사용하여 테이터를 처리
- 데이터 모델링이 간단하지만 CAD/CAM ,GIS 등과 같은 비정형 데이터들을 다루거나 실시간 분석에는 적합하지 않다.
- DBMS 예 : MySQL

![객체지향형 데이터베이스](https://thebook.io/img/006977/022_1.jpg)

#### 객체지향형 (Object-Oriented DataBase) : 1980년대

- 객체지향 프로그래밍 개념에 기반하여 만든 데이터베이스 모델
- 정보를 객체의 형태로 표현
- 객체지향 프로그래밍 개념 ( 클래스, 상속 등 )을 사용할 수 있다.
- CAD/CAM. GIS 등의 비정형 데이터들을 데이터베이스화 할 수 있도록 하기 위해 만들어진 모델
- 멀티미디어 데이터 지원이 가능하지만 SQL 쿼리를 사용할 수 없고
- 검색이나 대규모 트랜잭션 처리에서 성능이 떨어지는 단점이 있어 몇몇 특수한 전문분야 정도에서만 사용

![객체관계형 데이터베이스](https://upload.wikimedia.org/wikipedia/commons/thumb/7/7c/Object-Oriented_Model.svg/1280px-Object-Oriented_Model.svg.png)

#### 객체 관계형 (Object-Relational DataBase) : 1990년대

- 관계형 데이터베이스에 객체 지향 개념을 도입하여 만든 데이터베이스 모델
- 객체지향 개념을 지원하는 표준 SQL을 사용할 수 있고, 데이터 타입도 관계형 데이터베이스 보다 더 다양하게 추가
- DBMS 예 : UniSQL, Object store

![NoSQL](https://media.geeksforgeeks.org/wp-content/uploads/20220405112418/NoSQLDatabases.jpg)

#### NoSQL

- Not Only SQL의 줄임말로 SQL뿐만 아니라 다양한 특성을 지원한다는 의미라고 해석
- 데이터 간에 관계를 정의하지 않는 데이터베이스 모델로 기존의 RDBMS의 복잡도와 용량의 한계를 극복하기 위한 목적으로 만들어졌다.
- 비정형 데이터 처리에 유리하지만 스키마 변경이 불가능해 데이터값에 문제가 발생하면 감지가 어렵다.
- DBMS 예 : redis

> SQL?
> Structured Query Language의 약칭
> 구조화된 조회 언어
> SQL은 데이터베이스 조회 및 프로그래밍 언어
> 데이터의 접근 및 조회, 업데이트 및 관계 데이터베이스 시스템 관리에 사용

![NewSQL](https://editor.analyticsvidhya.com/uploads/60059newsql.JPG)

#### NewSQL

- New 와 SQL 의 합성어이다. RDBMS 의 SQL과 NoSQL의 장점을 결합하여 관계형 모델
- 트랜잭션 지원 및 확장성과 고 가용성을 모두 만족시키려는 목적에서 만들어진 데이터베이스 모델
- DBMS 예 : VoltDB