## Android Basic

![and_archi](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170123/imgs/Android_architecture.png?raw=true)
- 과거에는 C/C++ 로 되어있는 NDK를 쓰도록 권고했으나 지금은 충분히 빨라져서 NDK 안 쓰도록 권고함

---
- Dalvk vs ART

---
###1. Compile
- 리눅스 상에서의 Compile 및 Build 과정

- 안드로이드 상의 컴파일

###2. Build
컴파일이 끝난 파일을 설치파일까지 만들어 주는 것

###3. Build Tools
Maven <-> Gradle
이 둘만 알아도 됨

###4. Gradle
#####1. Gradle의 특징
#####2. Gradle의 장점



###호오라
findViewByID()는 View 를 리턴 하므로

(타입)find... 로 써서 캐스팅 해준다.


###호오라
터미널 명령어로 모든 flavor 빌드하기

윈 - gradlew build
맥 - ./gradlew build

### Lint
Android Code Scanning Tool


##### lint Severity(심각도)

#####lint 모든 flavor 실행
./gradlew lint

###Android Studio with Git
Remote Repository 만들때 README.md 추가 금지

###travis 연동
root 밑에 .travis.yml 파일 생성