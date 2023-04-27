# Linux (리눅스)

## Index
- [Linux (리눅스)](#linux-리눅스)
  - [Index](#index)
  - [1. 리눅스(Linux)란?](#1-리눅스linux란)
    - [1.1 리눅스 커널](#11-리눅스-커널)
  - [2. 리눅스의 사용 이유](#2-리눅스의-사용-이유)
  - [3. 리눅스 설치](#3-리눅스-설치)
    - [4.리눅스 기본명령어](#4리눅스-기본명령어)
      - [1) 자주 사용하는 특수문자](#1-자주-사용하는-특수문자)
      - [2) 필수 명령어](#2-필수-명령어)
  - [\<파일의 퍼미션\>](#파일의-퍼미션)
    - [3)](#3)


## 1. 리눅스(Linux)란?

1. 컴퓨터 OS커널의 일종인 리눅스 커널을 사용하는 운영체제
   1. ex : window, macOS
2. 오픈소스 소프트웨어

### 1.1 리눅스 커널

> Linux OS의 주요 구성요소이자 컴퓨터 하드웨어와 프로세스를 잇는 핵심 인터페이스.

1. 메모리 관리 
   - 메모리가 어디에서 무엇을 저장하고, 얼마나 사용되는지 추적
2. 프로세스 관리 
   - 어느 프로세스가 CPU를 언제 얼마나 오랫동안 사용할지 결정
3. 장치드라이버 
   - 하드웨어와 프로세스 사이에서 중재자 역할을 수행
4. 시스템 호출 및 보안 
   - 프로세스의 서비스 요청을 수신

---

## 2. 리눅스의 사용 이유

1. 오픈소스로 무료로 사용 할 수 있다.
2. 보안이 매우 우수
   - 무료배포로 사용자들이 주기적인 버그를 확인하여 취약점을 발견, 개선
3. 메모리를 낭비하지 않으며 성능을 최대한으로 끌어올림
4. 운영체제가 수행해야 하는 핵심 기능만 정의되 있음. 이외의 부분은 사용자의 용도에 맞게 커스터마이징 가능

---

## 3. 리눅스 설치
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
       |  : pipe, 파이프 - 명령어와 명령어를 연결해준다.
       `  : back quote, back tick - 명령어 결과물 저장
       '  : single quote, " : double quote -  문자열을 출력할때 사용
       || : or 연산. 앞 명령어가 참이면 뒤 명령어는 실행하지 않음
       && : and 연산. 앞 명령어가 참일때만 뒤 명령어 실행

         ** 경로 **
        / : 절대위치 기준 경로 (root가 시작점)
       ./ : 현재위치 기준 경로 (현재 디렉토리가 시작점, 생략가능)
      ../ : 현재 위치의 상위 기준 (root/home 이라면 ../는 root임)
       ~/ : Home 위치 기준

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

    2-1) ls (List segments) : 현재 위치의 파일 목록 조회

        ls -l : 파일의 상세정보
        ls -a : 숨김 파일 표시
        ls -t : 파일들을 생성시간순(제일 최신 것부터)으로 표시
        ls -rt : 파일들을 생성시간순(제일 오래된 것부터)으로 표시
        ls -f : 파일 표시 시 마지막 유형에 나타내는 파일명을 끝에 표시
                ('/' : 디렉터리, '*' : 실행파일, '@' : 링크 등등,,,)
    2-2) cd (Change directory) :디렉터리 이동

        cd [디렉터리 경로] : 이동하려는 디렉터리로 이동 
           (경로 입력 시 '[', ']'부분은 빼고 입력!)
        cd ~ : 홈 디렉터리로 이동
        cd / : 최상위 디렉터리로 이동
        cd . : 현재 디렉터리 
        cd .. : 상위 디렉터리로 이동
        cd - : 이전 경로로 이동
    
    2-3) touch : 0바이트 파일 생성, 파일의 날짜와 시간을 수정
         touch filename : filename의 파일을 생성
         touch -c filename : filename의 시간을 현재시간으로 갱신
         touch -t 202110291608 filename : filename의 시간을 날짜 정보(YYYYMMDDhhmm)로 갱신
                  (20211029160 => 2021.10.29.16:08)
         touch -r oldfile newfile  : newfile의 날짜 정보를 oldfile의 날짜 정보와 
                                     동일하게 변경
   
    2-4) mkdir (Make dirctory) : 디렉터리 생성
         mkdir dirname : dirname이라는 디렉터리 생성
         mkdir dir1 dir2: 한 번에 여러 개의 디렉터리 생성
         mkdir -p dirname/sub_dirname : dirname이라는 디렉터리 생성,  
                                        sub_dirname이라는 하위 디렉터리도 생성
         mkdir -m 700 dirname : 특정 퍼미션(권한)을 갖는 디렉터리 생성
         
   ## <파일의 퍼미션>
      8진수	   2진수	   권한	      의미
      0	       000	       ---	   아무 권한 없음
      1         001	       --x	   실행 권한만 있음
      2	       010	       -w-	   쓰기 권한만 있음
      3	       011	       -wx	   쓰기,실행 권한 있음
      4	       100	       r--	   읽기 권한만 있음
      5	       101	       r-x	   쓰기,실행 권한 있음
      6	       110	       rw-	   읽기,쓰기 권한 있음
      7	       111	       rwx	   모든 권한 있음


예를 들어 '777'의 경우 이진수로 111111111이고 rwxrwxrwx라는 의미를 가지므로 파일 소유자, 소유 그룹, 일반 사용자에게 읽기, 쓰기, 실행의 모든 권한을 주는 설정이다.

    2-5). cp (Copy) : 파일 복사
          cp file1 file2 : file1을 file2라는 이름으로 복사
          cp -f file1 file2 : 강제 복사
                  (file2라는 파일이 이미 있을 경우 강제로 기존 file2를 지우고 복사 진행)
          cp -r dir1 dir2 : 디렉터리 복사. 폴더 안의 모든 하위 경로와 파일들을 복사
    
    2-6). mv (Move) : 파일 이동
          mv file1 file2 : file1 파일을 file2 파일로 변경
          mv file1 /dir : file1 파일을 dir 디렉터리로 이동
          mv file1 file2 /dir : 여러 개의 파일을 dir 디렉터리로 이동
          mv /dir1 /dir2 : dir1 디렉터리를 dir2 디렉터리로 이름 변경
 

    2-7) rm (Remove) : 파일 삭제
         rm file1 : file1을 삭제
         rm -f file1 : file1을 강제 삭제
         rm -r dir : dir 디렉터리 삭제 (디렉터리는 -r 옵션 없이 삭제 불가)
 
    2-8). cat (Catenate) : 파일의 내용을 화면에 출력, 리다이렉션 기호('>')를 사용하여
                           새로운 파일 생성
          cat file1 : file1의 내용을 출력
          cat file1 file2 : file1과 file2의 내용을 출력
          cat file1 file2 | more : file1과 file2의 내용을 페이지별로 출력
          cat file1 file2 | head : file1과 file2의 내용을 처음부터 10번째 줄까지만 출력
          cat file1 file2 | tail : file1과 file2의 내용을 끝에서부터 10번째 줄까지만 출력
 

    2-9) redirection ('>', '>>') : 화면의 출력 결과를 파일로 저장
         '>' 기호 : 기존에 있는 파일 내용을 지우고 저장
         '>>' 기호 : 기존 파일 내용 뒤에 덧붙여서 저장
         '<' 기호 : 파일의 데이터를 명령에 입력
         
         cat file1 firle2 > file3 : file1, file2의 명령 결과를 합쳐서 file3라는 파일에 저장
         car file4 >> file3 : file3에 file4의 내용 추가
         cat < file1 : file1의 결과 출력
         cat < file1 > file2 : file1의 출력 결과를 file2에 저장
 

    2-10) alias : 자주 사용하는 명령어들을 별명으로 정의하여 쉽게 사용할 수 있도록 설정
      
          alias 별명 = '명령어 정의'
          ex) alias lsa = 'ls -a' : lsa를 실행하면 -a 옵션을 갖는 ls를 실행합니다.
          unalias lsa
          unalias lsa : lsa라는 alias를 해제
### 3)