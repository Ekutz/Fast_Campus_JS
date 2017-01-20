##1. 데이터베이스
>통합 정보가 저장된 공용 데이터의 묶음

###DB의 종류
>담배가 아니다


- 관계형

	>가장 고전적이지만 가장 성능이 좋다  
	>그러나 초기 설계가 까다롭고 수정 역시 까다롭

- 키-값형
- 객체형
- 문서형
- 컬럼형

---

###자료구조 vs DB
- 자료구조: 대부분 주기억장치에서 처리됨
- DB: 대부분 보조기억장치에서 처리됨  
DB에 들어있는 수많은 자료 중 필요한 것들만 메모리에 올려서 정리하는 것이 자료구조

---

###DBMS
>담배멘솔 아니다  
>DataBases Management System

- DB에 접근할 수 있는 기능을 제공하는 소프트웨어, DB계의 OS

즉 DBMS는 달라도 DB는 같을 수도 있는 것이다.

---

###SQL
>Structured Query Language

- DBMS를 통해 데이터를 관리하기 위한 구조화된 질의문을 작성하기 위한 언어
- 관계형 DB에서 사용한다

---

##2. 네트워크
>컴퓨터들이 연결되어 있는 환

###인터넷
>network between network -> Internet

---

###네트워크의 종류
|이름|정식 명칭|범위|
|:--:|:--:|:--:|
|LAN|Local Area Network|근거리|
|MAN|Metropolita Area Network|도시권|
|WAN|Wide Area Network|국가권|

---

###URL
>Uniform Resource Locator

- [Protocol]://[Host]:[Port]/[Path]
	- http://www.daum.net:80/map
	- ftp://id:pw@192.168.1.10:777/mydir

---

###Protocol
>통신 규약

- 장비 사이에서 메시지를 주고 받는 양식과 규칙의 체계

#####HTTP
>Hyper Text Transfer Protocol

HTML(Hyper Text Markup Language)로 된 문서를 주고 받을 수 있다

- HTML 메소드

	|메소드 명|설 명|장 점|단 점|
	|:---:|:---:|:---:|:---:|
	|GET|URL에 직접 노출시켜 정보를 _요청_ 하는 방식|Cache 저장으로 다음 이용 시 빠르게 처리되도록 함|정보가 모두 노출됨|
	|POST|패킷 body에 정보를 숨겨서 서버에 전달하여 값을 _갱신_ 하는 방식|정보의 보안 / 다량의 데이터 전송 가능|서버까지 정보가 왕복하기 때문에 속도가 느릴 수 있다|
	|PUT|서버에 자료를 업데이트 한다|원격지의 정보를 추가 가능하다|변조되기 쉽다|
	|DELETE|서버의 자료를 삭제한다|원격지의 정보를 삭제 가능하다|변조되기 쉽다|

	>이걸 지키지 않으면 요청을 거절당할 수도 있고, 자료가 날아갈 수도 있다

#####FTP
>File Transfer Protocol

- 파일을 전송하기 위한 프로토콜

#####TELNET
>TErminaL NETwork

- 터미널 명령어를 통한 원격 로그인을 위한 프로토콜

#####SSH
>Secure SHell

- 네트워크 상의 다른 컴퓨터에 로그인하거나 명령할 수 있는 프로토콜
- TELNET의 대용 목적으로 설계
- 암호화 되어 있다

#####SSL
>Secure Socket Layer

- 웹서버와 브라우저 사이의 보안을 위한 프로토콜

---

###Host
- 네트워크에 연결된 장치

#####IP
>Internet Protocol

- 장치들이 서로를 인식하고 통신을 하기 위해서 사용하는 번호
- 접속 때마다 유동 IP를 새로 받는다

#####도메인
- 사람이 알기 쉽게 호스트 이름을 문자로 표기한 것

`8.8.8.8 <-> www.google.com`

#####DNS
>Domain Name System

- 도메인 이름을 네트워크 주소로 바꾸거나 반대의 변환을 수행

![dns](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170112/imgs/dns.png?raw=true)  
DNS가 주소를 해석하여 클라이언트에게 보여주는 과정이다

#####MAC 주소
>Media Access Control Address

- 네트워크 어댑터에 부착된 식별자
- 바뀌지 않는 물리적 주소


---

###Port
- 가상의 논리적 통신 연결단
- 서로 다른 목적의 데이터들을 알맞은 프로세스로 보내기 위한 가상 ID
- 프로토콜 마다 지정된 범위의 포트가 있다

---

###OSI 7계층
>잠시 토하고 오겠습니다

![osi](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170112/imgs/osi.png?raw=true)  

![osi2](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170112/imgs/osi2.png?raw=true)  

---

##3. 암호화
>내 개인정보는 중국의 공공재

###대칭키
- 암호화와 복호화에 같은 암호 방식을 쓰는 알고리즘
	- DES, AES, SEED 등

>공인인증서가 SEED 형태의 대칭 암호화 형식을 취하고 있다
>![shit](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170112/imgs/shit.png?raw=true)  
>충격과 공포

###비대칭(=공개)키
- 암호화키는 공개하지만 복호화 키는 따로 존재하는 알고리즘
	- RSA 등

###해쉬키
- 해쉬맵 테이블을 가지고 암호화 하는 방식
	- SHA, MD5
		- 복호화가 안되는 걸로 알려져 있지만 해쉬 테이블을 알면 금새 복구할 수 있다