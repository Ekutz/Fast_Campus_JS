## 1. Git with command
>macOS는 Unix 기반 명령어를 사용한다  
>Terminal을 이용하여 명령어를 입력한다

###기본 Unix 명령어 정리
- `pwd: 현재 경로 표시`  
- `ls: 현재 경로 하위 목록 표시`  
- `clear: 화면 지우기`  
- `cd(change directory) '원하는 경로': 원하는 경로로 이동`  
- `mkdir '폴더명': 폴더 생성`  
- `rmdir '폴더명': 폴더 삭제`  
- `vi '파일명.파일형식': 파일명.파일형식을 vi 편집기로 생성`

---

###Git 명령어
- `git --help: git 명령어 모음집`  
- `git init: 빈 폴더를 Local Repository로 변환`  
- `git status: git이 commit, push 되어야할 상태를 확인`
- `git add '파일명.파일형식': Working Area 의 파일명.파일형식을 Stage Area로 add 시킨다`
- `git add .: 모든 변경된 파일을 Stage Area로 add 시킨다`
- `git commit: 단순 commit 후 메시지 입력창 open <- 맨 윗줄에 commit 메시지 제목을 입력해야한다`  
- `git commit -m "메시지": 간단한 메시지를 포함한 commit`
- `git reset HEAD '파일명.파일형식': 파일명.파일형식 을 Unstage 시킨다`
- `git remote add origin 'http주소': 현재 위치의 Local Repository를 http 주소의 Remote Repository와 연동시킨다`
- `git push -u origin master: 현재 Local Repository와 연동된 Remote Repository로 push하면서 진행 상황을 표시한다`
- `git clone 'http주소': http 주소의 Remote Repository를 현재 위치로 pull 해 온다`

>git 관련 명령어는 모두 git을 어두로 달고 나온다

---

###vi 명령어
#####명령 상태
`:w <- 저장`  
`:q <- 탈출`  
`:q! <- 저장없이 탈출`  
`i <- 입력 상태로 진입`

#####입력 상태
`esc <- 명령 상태로 진입`

---
---

##2. 컴퓨터
>간단한 컴퓨터의 기초에 대해 알아본다

###컴퓨터의 역사
![진공관](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170110/imgs/jingong.jpg?raw=true)
최초의 컴퓨터 구성요소인 진공관, 엄청난 발열과 부피 문제 등으로 인해 곧 사라진다
> TR앰프에 비해 회로가 간단하고 음색이 뛰어나 앰프에서는 진공관이 더 각광받는다

> 발열과 빛 때문에 벌레가 꼬이는걸 방지하고 청소해야 했는데 이 일련의 과정을 Debugging이라고 했다는 썰이있다

![트랜지스터](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170110/imgs/transistor.png?raw=true)  
진공관을 이기고 차세대 컴퓨터 구성요소가 된 트랜지스터, 그러나 이 역시도 부피 문제로 인해 사장된다

![집적회로](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170110/imgs/ic.png?raw=true)  
일반적으로 우리가 아는 컴퓨터에 장착된 IC(Integrated Circuit)이다. 공장 하나의 크기를 지녔던 진공관 컴퓨터가 손가락 한마디의 칩 안에 들어가게 되었다

---

###컴퓨터의 구성
#####하드웨어
- 입력장치
- 출력장치 
- 기억장치
- 연산장치
- 제어장치

> 손으로 만질 수 있으면 죄다 하드웨어다

#####소프트웨어
- 시스템 소프트웨어(OS, Kernel, driver etc...)
- 응용 소프트웨어

---

###컴퓨터의 구조
![컴구조](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170110/imgs/architecture.png?raw=true)  
하버드와 폰 노이만 구조의 차이

#####하버드 구조
메모리의 물리적 분리상태로 빠른 속도를 자랑하지만 복잡한 구조와 비싼 가격이 문제이다

#####폰 노이만 구조
메모리의 단일화로 단순한 구조와 가격이 절충되지만 BUS의 병목현상으로 인한 메모리 속박 현상이 발생하게 된다

#####해결 방법
![컴구조](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170110/imgs/cache.jpg?raw=true)  
L로 시작하는 Cache 메모리들을 CPU에 합류시켜 거시적으로는 폰 노이만 구조를 미시적으로는 하버드 구조를 이용하여 최적의 구조를 만들어 냈다
>우리는 답을 찾을 것이다. 언제나 그랬듯이.

---

###컴퓨터의 표현 방식
>01001001 01101100011011110111011001100101
011110010110111101110101  
= I love you  
이런거 아니다

#####데이터 표현 방식
- 정수
	- 최고차 bit를 부호로 사용하여 양, 음수 구분
- 실수
	- bit를 분할하여 정수부와 실수부를 구분
- 문자
	- ASCII, UTF-8 등 다양한 인코딩 방식에 따라 구분

#####데이터의 연산 방식
- AND(&)
	- 모든 경우가 참이어야 참  
	
	>모 아니면 도
- OR(|)
	- 한 경우라도 참이라면 참

	>좋은게 좋은거 아니겠습니까
- NOT(~ / !)
	- bit의 반전 / bool의 반전
- XOR(^)
	- 모든 경우가 다른 경우에만 참

	>달라야 산다!