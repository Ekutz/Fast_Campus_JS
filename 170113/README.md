##1. 소프트웨어 공학

###공학이란?
>기초된 학문을 응용하여 인간에게 이로운 것을 연구하는 학문

---

###소프트웨어 공학이란?
>소프트웨어의 개발, 운용, 유지보수 및 폐기에 대한 체게적인 접근방법

---

###소프트웨어 개발 생명주기 모델
>소프트웨어를 어떻게 개발할 것인가에 대한 전체적인 흐름

#####폭포수 모델  
![waterfall](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170113/imgs/waterfall.png?raw=true)

- 체계적인 순서를 가진다는 장점이 있다
- 앞 단계가 진행되어야 뒤로 갈 수 있다는 단점이 있다

#####프로토타이핑 모델

![proto](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170113/imgs/proto.jpg?raw=true)

- 데모 버젼을 만들어 지속적으로 수정해 나간다
- 개발 비용이 많이 든다
- 커뮤니케이션으로 인한 일정 소모가 늘어난다

#####나선형 모델
![spiral](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170113/imgs/spiral.png?raw=true)

- 개발 퀄리티가 증가한다
- 전체 개발 시간이 늘어난다
- 의사 소통 과정에서 최종작이 괴랄해 질수도 있다

---

###소프트웨어 개발 방법론
>소프트웨어를 생산하는데 필요한 반복 과정들을 정리한 것

#####Agile(애자일) 개발 프로세스
생명주기 모델 개발 프로세스를 적당하게 버무려서 효율적으로 개발하는 방법론

- 예측하지 않고 일정 주기로 끊임없이 개발하는 적응형 개발 방식  
- 특정한 어떤 방식이 아니라 무조건 빨리 만들기 위한 짬뽕 타입이다

#####UML
>Unified Model Language

- 표준화된 범용 모델링 언어
- 제대로 모델링을 하면 기초적인 부분을 실제 개발을 해서 내준다

#####TDD
>Test Driven Development

- 테스트 주도 개발
	- 애자일과 함께 자주 언급된다
	- 빠르게 변화하는 현실에서 가장 효과적
	- 코드 동작 확인을 위한 코드를 따로 작성하여 테스트 위주의 개발을 한다 <del>테스트 코드에도 버그는 있다</del>
	- 잘 사용하기만 한다면 기술적 부채 탕감에 엄청난 도움이 된다

#####PDD
>Plan Driven Development

- 계획 주도 개발
	- TDD와 반대의 개념

#####형상관리

- 결과물에 대한 형상을 만들고, 이들 형상에 대한 변경을 체계적으로 관리, 제어하는 활동
	- <del>'final_1.ppt'</del> <del>'진짜최종3.ai'</del>

#####버전관리
- 형상관리의 일부
- 소스 코드 형상 관리의 특화된 관리
	- Git

		>누가 왜 이 코드를 짰는지 다 나오기 때문에, 문제 발생 시 총대 매기 딱 좋다

---

##2. 프로그래밍 언어
![언어](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170113/imgs/language.png?raw=true) <del>어우 개 많네...</del>

###언어의 역사
>스압

![history](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170113/imgs/history.jpg?raw=true)

시대에 요구에 따라 과거에 발명된 언어가 뒤늦게 각광받는 경우가 많다.

---

###언어의 종류

#####컴파일 언어: 실행파일을 만든 후, 배포하기 전에, 기계어로 번역되는 언어
- C, C++, Go...
	- 장점 : 기계어로 번역이 완료되어 있어 실행 속도가 빠르다
	- 단점 : 수정을 위해 전체 소스를 재번역해야하는 번거로움이 있다<br/>하드웨어에 대한 의존도가 높아 운영체제에 따라 다르게 제작해야한다

#####바이트코드 언어: 가상머신이 읽을 수 있는 형태로 변환한 뒤 가상머신에 의존하여 실행
- Java, C#...
	- 장점 : 하드웨어 의존도가 낮고, 실행 속도도 빠르다
	- 단점 : 최적화가 어렵다<br/>가상머신도 메모리를 차지한다

#####인터프리터 언어: 실행과 동시에 동시 번역하여 사용하는 언어
- BASIC, JavaScript, Python, Ruby...
	- 장점 : 유지보수가 매우 편리하다
	- 단점 : 실행 속도가 느리다

---

###객체지향 프로그래밍
>프로그래밍을 명령어의 목록으로 보는 시각에서 벗어나 "객체"들의 모임으로 보는 것

#####클래스: 객체를 만들기 위해 공통된 기능을 설명해 놓은 것 <del>붕어빵 틀</del>

#####객체: 실현된 하나의 클래스 <del>붕어빵</del>

>![클래스](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170113/imgs/class.jpg?raw=true)  
>![객체](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170113/imgs/object.jpg?raw=true)

<del>수많은 객체가 죽어나간다</del>

---

###각종 용어 정리
>소프트웨어와 관련된 것들에는 수많은 것들이 추상적이고 가상적이다.  
>그러므로 끊임없이 상상하고 그 관계를 정리하는 연습을 하도록 하자

#####개발자
><del>밤을 세는 자</del>

- 프로젝트를 만드는데 기획부터 제작까지 참여하는 모든 사람

#####Server / Client
- 상대적인 개념으로 정보를 주면 서버, 받으면 클라이언트

#####Front-end / Back-end
>재주는 백이 부리고 돈은 프론트<del>도 못 받는다</del>...

- 상대적인 개념으로 사용자와 직접 상호작용하면 Front-end, 아닐 시 Back-end

#####Thread
![스레드](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170113/imgs/thread.png?raw=true)

- 프로세스 내에서 작업이 실행되는 흐름의 단위

||멀티 스레드|vs|멀티 태스크|
|:-:|:-:|:-:|:-:|
|차이|하나의 프로세스 안에서 여러 개의 작업 흐름을 만듬||한번에 여러가지 프로세스를 처리하는 환경|

#####Library
- 특정 기능을 수행할 수 있는 클래스 또는 함수의 집합체

#####API
>Application Programming Interface

- 소프트웨어 간의 통신을 위해 메시지 전달 방식 등이 결정된 것
- 정보를 가져가는 통로 역할

#####Framework
- 기본 설계의 기반을 모아놓고 구현하고자 하는 기능을 추가, 수정할 수 있도록 담아놓은 집합체

#####디자인 패턴
- 과거 개발 과정에서 발견된 설계의 노하루를 재사용하기 좋은 형태로 묶어서 정리한 것

#####IDE
>Integrated Development Environment

- 통합 개발 환경
	- Android Studio, XCode, Visual Studio...

#####SDK
>Software Development Kit

- 소프트웨어 개발에 필요한 도구의 모음
	- IDE + Framework + Tools...