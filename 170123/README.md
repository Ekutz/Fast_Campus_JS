## Android Basic

![and_archi](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170123/imgs/Android_architecture.png?raw=true)
- 과거에는 C/C++ 로 되어있는 NDK를 쓰도록 권고했으나 지금은 충분히 빨라져서 NDK 안 쓰도록 권고함

---
## Dalvik vs ART
||Dalvik|ART|
|:-:|:-:|:-:|
|Compile 방식|JIT|AOT + JIT|
|차이점|실행할 때 마다 컴파일|(최초 설치 컴파일 하는 AOT) + JIT|

>사실 Oracle이 고소미를 시전하지 않았으면 아직도 Dalvik 가지고 낑낑댔겠지

---
##Android Compile&Build
###1. Compile
- 리눅스 상에서의 Compile 및 Build 과정
![linux_compile](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170123/imgs/Linux_Compile.png?raw=true)
- 안드로이드 상의 컴파일
![android_compile](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170123/imgs/Android_Compile.png?raw=true)

>리눅스는 컴파일 후 링크를 해주는 것을 포함하여 빌드라고 부르지만 안드로이드는 빌드 과정이 따로 존재한다

---

###2. Build
컴파일이 끝난 파일을 설치파일까지 만들어 주는 것
![android_build](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170123/imgs/Android_Build.png?raw=true)

---

###3. Build Tools
|Make|Maven|Gradle|
|:-:|:-:|:-:|:-:|
|리눅스 빌드(플랫폼 의존성이 있다)|빌드 도구로 시작하였으나 현재는 의존성 관리툴로 사용된다|구글의 전폭적인 지원으로 가장 큰 파이를 차지하게 된 빌드 툴|

---

###4. Gradle
- 비설치형 빌드툴
	- gradlew 명령어로 자동 다운로드 후 실행
- 프로젝트 구조화
	- 구조화된 프로젝트 빌드가 용이하고, 의존관계 정립에 편리하다
- 하위 버전에 대한 호환성 유지
	- 버전 체크를 우선시 하여 호환성을 유지한다

![gradle_config](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170123/imgs/gradle_config.png?raw=true)


---

###Tip
터미널 명령어로 모든 flavor 빌드하기
Terminal Console 에서

윈도우 - $ gradlew build  
맥 OS - $ ./gradlew build

---

###Android Studio with Git
![vcs1](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170123/imgs/vcs1.png?raw=true)
![vcs2](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170123/imgs/vcs2.png?raw=true)

- 프로젝트를 Git으로 관리할 준비를 한다

![vcs3](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170123/imgs/vcs3.png?raw=true)

- add를 하고

![vcs4](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170123/imgs/vcs4.png?raw=true)

- commit & push

>add, commit & push 는 터미널에서 진행하는게 오히려 편하다  
>Remote Repository 만들때 README.md 추가 금지

###travis 연동
root 밑에 .travis.yml 파일 생성

