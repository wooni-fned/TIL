# Network

## IP 주소와 Port

- IP : 컴퓨터를 구분하는 주소
- Port : 컴퓨터안에 있는 `서버`들을 구분하는 값

확인방법

- window
  - 명령어 창에서 ipconfig
- mac
  - iTerm 에서 ifconfig

- Well Known Port번호
  - 0 ~ 1023
  - 국제인터넷 주소관리 기구 (ICANN)에서 미리 예약해둔 포트
- Registered Port 번호
  - 1024~49151
  - 개인 또는 회사에서 사용하는 포트
- Dynamic 또는 Private Port번호
  - 49152~65535
  - 운영체제가 부여하는 동적 포트 또는 개인적인 목적으로 사용 할 수 있는 포트

### 127.0.0.1

- 내컴퓨터 IP = root IP
- localhost : 내 컴퓨터 도메인 주소

## 도메인(Domain)주소

- www.google.com, www.xxx.com 등을 도메인 주소라 한다.

### 도메인 네임 서버 (Domain Name Server : DNS)

- 도메인 주소를 ip주소로 변환한다.
- `nslookup 도메인주소`
  - 명령어로 도메인 주소를 확인 할 수 있다.

## java 에서 IP주소 알아내기

- InetAddress

- 사용자 컴퓨터의 IP주소 찾기

```java
InetAddress ia = InetAdress.getLocalHost();
System.out.println(ia.getHost.Address());
```

- google의 IP주소 알아내기

```java
InetAddress[] iaArr = InetAdress.getAllByName("www.google.com");
for (InetAddress ia : iaArr) {
  System.out.println(ia.getHost.Address());
}
```

## Client & Server 프로그래밍

- socket : Server에 접속하는 역할
- ServerSocket : Client가 접속 요청을 기다리는 역할
  - Client 요청을 기다리다가 접속을 하면 Socket을 반환한다.
- Socket과 Socket 간에는 IO객체를 이용하여 통신할 수 있다.

## 브라우저 요청 결과를 출렷하는 Server프로그램 작성하기

- `http://ip:port` 주소로 브라우저는 요청을 보낼 수 있다.
- ServerSocket은 특정 Port로 접속 요청을 기다릴 수 있다.
- 브라우저는 서버와 연결이 되면 요청 정보를 전송한다.
- 서버는 브라우저가 보내는 요청정보를 읽어들인 후, 그 결과를 출력할 수 있다.

