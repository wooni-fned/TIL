# Linux (리눅스)
   ### 1. 리눅스(Linux)란?
              1)컴퓨터 OS커널의 일종인 리눅스 커널을 사용하는 운영체제
                (ex : window, macOS)
              2)오픈소스 소프트웨어
    
    * 리눅스 커널 - Linux OS의 주요 구성요소이자 컴퓨터 하드웨어와 프로세스를 잇는     
                  핵심인터페이스.
    
    *커널   -  1) 메모리 관리 : 메모리가 어디에서 무엇을 저장하고, 얼마나 사용되는지 추적

               2) 프로세스 관리  :어느 프로세스가 CPU를 언제 얼마나 오랫동안 사용할지 결정

               3) 장치드라이버 : 하드웨어와 프로세스 사이에서 중재자 역할을 수행

               4) 시스템 호출 및 보안 : 프로세스의 서비스 요청을 수신

   ### 2. 왜 리눅스를 쓰는가?
            1) 오픈소스로 무료로 사용 할 수 있음
   
            2) 보안이 매우 우수
               (무료배포로 사용자들이 주기적인 버그를 확인하여 취약점을 발견, 개선)

            3) 메모리를 낭비하지 않으며 성능을 최대한으로 끌어올림
   
            4) 운영체제가 수행해야 하는 핵심 기능만 정의되 있음. 이외의 부분은
               사용자의 용도에 맞게 커스터마이징 가능
   ### 3. 리눅스 설치
RockyLinux image

 https://download.rockylinux.org/pub/rocky/9/isos/x86_64/Rocky-9.1-x86_64-minimal.iso

VirtualBox

https://download.virtualbox.org/virtualbox/7.0.8/VirtualBox-7.0.8-156879-Win.exe

D2coding 글꼴 압축풀고 설치

https://github.com/naver/d2codingfont/blob/master/D2Coding-Ver1.3.2-20180524.zip

putty.exe

https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe


   ### 4.리눅스 기본명령어
#### 1) 자주 사용하는 특수문자
       ~  : tilde, 물결, 출렁이, home - 홈디렉터리로 이동
       |  : pipe, 파이프 - 명려어와 명령어를 연결해준다.
       `  : back quote, back tick - 명령어 결과물 저장
       '  : single quote, " : double quote -  문자열을 출력할때 사용

     ** 경로 **
    /   : 절대위치 기준 경로 (root가 시작점)
    ./  : 현재위치 기준 경로 (현재 디렉토리가 시작점, 생략가능)
    ../ : 현재 위치의 상위 기준 (root/home 이라면 ../는 root임)
    ~/  : Home 위치 기준

#### 2) 필수 명령어
   
    ls - 현재 위치의 파일 목록 조회
    cd - 디렉터리 이동
    touch - 0바이트 파일 생성, 파일의 날짜와 시간을 수정
    mkdir - 디렉터리 생성
    cp - 파일 복사
    mv - 파일 이동
    rm - 파일 삭제
    cat - 파일의 내용을 화면에 출력, 리다이렉션 기호('>')를 사용하여 새로운 파일 생성
    redirection - 화면의 출력 결과를 파일로 저장
    alias - 자주 사용하는 명령어들을 별명으로 정의하여 쉽게 사용할 수 있도록 설정

    1-1) ls (List segments) : 현재 위치의 파일 목록 조회

        ls -l : 파일의 상세정보
        ls -a : 숨김 파일 표시
        ls -t : 파일들을 생성시간순(제일 최신 것부터)으로 표시
        ls -rt : 파일들을 생성시간순(제일 오래된 것부터)으로 표시
        ls -f : 파일 표시 시 마지막 유형에 나타내는 파일명을 끝에 표시
                ('/' : 디렉터리, '*' : 실행파일, '@' : 링크 등등,,,)
    1-2) cd (Change directory) :디렉터리 이동

        cd [디렉터리 경로] : 이동하려는 디렉터리로 이동 
           (경로 입력 시 '[', ']'부분은 빼고 입력!)
        cd ~ : 홈 디렉터리로 이동
        cd / : 최상위 디렉터리로 이동
        cd . : 현재 디렉터리 
        cd .. : 상위 디렉터리로 이동
        cd - : 이전 경로로 이동