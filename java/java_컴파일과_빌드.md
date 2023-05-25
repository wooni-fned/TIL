# java 컴파일과 빌드

## 자바 컴파일

- 단순 컴파일
  - `$javac` 소스파일명
    - `$javac Hello.java`
- `-d`옵션
  - `$javac -d` 배포디렉토리 소스파일명
    - `$javac -d bin hello.java`
- 소스파일과 클래스 분리
  - $javac -d bin src/Hello.java
    - bin폴더에 src폴더에 있는 Hello.java 소스코드를 컴파일한 클래스파일을 저장
- 예시
- java-study/
  - src/ Hello.java  : 소스파일를 두는 폴더
  - bin/ Hello.class : 컴파일된 파일을 두는 폴더
  
> - 여기서 왜 src 와 bin 파일인가?
    src - source 의 약자 소스코드를 저장하는곳
    bin - binary 의 약자 바이너리로 번역된 코드를 저장하는 곳

## 프로젝트 폴더의 구성

1. 1 저장소 : 1프로젝트 일 경우
   - java_project/
     - src/
     - bin/
   - 실무에서 사용하는 방식
   - 프로젝트의 변경관리 = 저장소 파일에 대해 변경관리
   - 즉, java_project폴더가 저장소겸 프로젝트 폴더

2. 1 저장소 : 다프로젝트 일 경우
   - java_project_server/
     - java-basic/
       - src/
       - bin/
     - java-levelup/
       - src/
       - bin/
   - 각 프로젝트 별 폴더가 저장소가 된다

3. 실제 프로젝트의 폴더 구조
   - 프로젝트폴더/
     - src/
       - main/
         - java/ - `.java` 자바소스파일 위치
         - resources/ - `.xml, .yml, properties` 등 App설정파일
       - test/
         - java/ - `.java` 자바소스파일 위치
         - resources/ - `.xml, .yml, properties` 등 App설정파일
     - pom.xml
     - build.gradle
     - ... (이하 빌드 스크립트 파일)

## 자바 빌드 도구

- 빌드 도구의 종류
  - Ant
    - build.xml
    - 소규모 프로젝트에서 사용
  - Maven
    - pom.xml (project, object, model)
    - 프로젝트의 의존성 관리 기능을 제공
    - 대규모 프로젝트에 사용
  - Gradle
    - build.gradle
    - Groovy 기반의 빌드 도구
    - Ant와 Maven의 장점을 결합한 도구
    - 프로젝트의 의존성 관리 기능을 제공
    - 대규모 포로젝트에 사용
- xml은 프로그래밍 언어가 아니라 빌드과정을 정교하게 기술할 수 없음.

## Gradle 사용법

- `$gradle.init`
  - gradle 관련 폴더와 설정파일을 자동으로 생성한다.

- `.gradle` 폴더
  - gradle을 실행할 때 사용하는 관련 파일들을 모아둔 폴더이다.
- `gradle` 폴더 
  - gradle 실행 파일을 둔 폴더이다.
- `build.gradle`
  - gradle 설정 파일 
- `gradlew`(unix/linux 용), gradlew.bat(windows 용)
  - 사용자 PC에 gradle을 자동으로 다운로드 받아 설치하고 실행한다.
  - 즉 사용자 PC에 gradle이 설치되어 있지 않아도 실행할 수 있다.  
- `settings.gradle`
  - gradle 실행할 때 참조하는 정보가 들어 있다.
- `gradle init --type` [프로젝트타입]
  - 지정한 유형에 맞춰 프로젝트 폴더 및 기본 파일들을 자동으로 생성한다.
- `gradle tasks --all`
  - gradle로 사용할 수 있는 모든 작업을 출력한다.
  - gradle 설정 파일(build.gradle)이 있는 폴더에서 실행해야 한다.
- `plugin`
  - gradle로 실행할 수 있는 작업들을 모아둔 라이브러리이다.

플러그인을 추가하는 방법: build.gradle 파일에 다음 설정을 추가한다. 

```
방법1:
apply plugin: '플러그인명'

방법2:
plugins {
    id '플러그인명'
}
```

- `'java'` 플러그인 
  - `gradle compileJava`
    - build/classes/java/main 폴더를 생성한다.
    - src/main/java 폴더의 모든 자바 소스 파일을 컴파일하여 위에서 생성한 폴더에 넣는다.
  - `gradle clean`
    - build 폴더를 제거한다.
  - `gradle processResources`
    - build/resources/main 폴더를 생성한다.
    - src/main/resources 폴더의 모든 파일을 복사하여 위의 폴더에 넣는다.
  - `gradle classes`
    - compileJava + processResources 작업 수행
  - `gradle compileTestJava`
    - classes 작업을 먼저 수행
    - build/classes/java/test 폴더를 생성한다.
    - src/test/java 폴더의 모든 자바 소스 파일을 컴파일하여 위에서 생성한 폴더에 넣는다.
  - `gradle processTestResources`
    - build/resources/test 폴더를 생성한다.
    - src/test/resources 폴더의 모든 파일을 복사하여 위의 폴더에 넣는다.
  - `gradle testClasses`
    - compileTestJava + processTestResources 작업을 수행 
  - `gradle test`
    - testClasses 작업을 수행
    - build/classes/test 폴더에 있는 테스트 관련 클래스를 모두 실행한다. 
  - `gradle jar`
    - classes 작업 수행
    - build/libs 폴더 생성
    - 자바 클래스 파일과 기타 자원 파일을 .jar 파일에 묶는다. 그리고 위의 폴더로 복사한다.
  - 'application' 플러그인
    - 자바 프로그램을 실행할 수 있는 작업이 들어 있다.
  - `gradle run`
    - classes 작업을 먼저 수행한다.
    - mainClassName에 지정된 자바 클래스를 실행한다.
  - 개별클래스 실행
    - `$java -classpath build/classes/java/main javaclass.App`
    - `-classpath` : `.class`파일이 있는 폴더 경로를 설정
    - 폴더까지만 경로를 명시하고 패키지는 실행파일에 명시해야 한다.