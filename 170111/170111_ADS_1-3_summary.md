##1. 운영체제
>붉은별은 빼고 이야기한다

###운영체제란
```
OS: Operating System의 약자
	응용 소프트웨어와 하드웨어 간의 중재자 역할
```
- 공통으로 사용하는 하드웨어와 소프트웨어를 총괄하는 시스템의 필요성으로 인해 탄생했다

---
  
###운영체제의 종류
>어떠한 커널을 사용하는지에 따라 구분되는 것이다

||Unix 계열|Linux 계열|Windows 계열|
|:-:|:-:|:-:|:-:|
|대표작|mac OS|Android / Ubuntu|Windows|

---
  
###운영체제의 역할
#####시스템 하드웨어 관리
- 응용 프로그램의 잘못된 접근을 방지하거나 입출력 장치 등의 연산과 제어를 관리

	>응답없음일 때 강제종료!

#####시스템 서비스 제공
- 프로그램을 쉽고 효율적으로 실행 할 수 있는 환경 제공
	- 실제가 아닌 가상에서 하드웨어와 소프트웨어의 생태계를 조성

#####자원관리
- 시스템 자원을 효율적으로 할당, 관리

	######프로세스 관리
	- 프로세스
		![프로세스](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170111/imgs/process_manage.png?raw=true)
	- 프로세스 주기
		![프로세스 주기](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170111/imgs/process_state.jpg?raw=true)
	- 프로세스 스케쥴링
	
		|방식|특징|장점|단점|  
		|:-:|:-:|:-:|:-:|
		|FCFS|프로세스 생성 순서에 맞추어 처리||앞선 프로세스가 오래 걸리면 뒤쪽은 서비스 불가|
		|SJF|서비스 시간이 짧은 순서대로 처리|빠른 속도|오래 걸리는 프로세스는 계속해서 밀려남|
		|Round Robin Scheduling|일정 시간 안에 처리하지 못하면 순서를 뒤로 미루는 처리법|합리적인 처리 방식으로 부하가 적음|기준 시간이 너무 짧으면 배보다 배꼽이 커짐|
		|Priority Based Scheduling|우선 순위를 정하여 처리|중요한 일부터 처리가 가능|낮은 순위의 프로세스는 서비스 불가|
		|Multi Queue Shceduling|프로세스를 분류하여 각 분류마다 다른 방식 적용|가장 빠르고 정확한 서비스 방식|다른 큐로 이동이 불가능함|
		
	
	######주기억장치 관리
	- 단순 관리
		- 사용하지 않는 메모리 제거
		
	- 가상 메모리
		- 보조기억장치의 일부를 주기억장치처럼 사용하는 방식  

			>다다익**RAM** 이면 쓸 필요 없다

	######파일 관리
	![파일 관리](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170111/imgs/file_manage.png?raw=true)
	>**H/W** vs **S/W** 싸움에 **OS** 등 터진다

---

###커널

---




##2. 자료구조
>데이터를 구조적으로 표현하는 방식  
>자료를 효율적으로 이용할 수 있는 방법론

###원시 구조
- 정수, 실수, 문자와 같이 한 공간에 하나씩 존재하는 데이터

###배열
- 원시 자료들을 일렬로 늘어놓은 것
	- 용량과 주소가 고정적이어서 데이터를 읽고 쓰는게 빠르다
	- 용량과 주소가 고정적이어서 변경이 불가능하다

###연결 리스트
- 단순 연결 리스트
 - 삽입과 삭제가 매우 자유롭다
	- 데이터를 담는 용량 외에도 다음 데이터의 위치를 알려줄 포인터가 필요하다
	- 특정 주소를 찾기 위해선 처음부터 물어봐야한다
	![단순 연결 리스트](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170111/imgs/Single_linked_list.png?raw=true)  

		>눈 감고 기차 놀이
	

- 이중 연결 리스트
 	- 앞 데이터의 위치를 알 수 있어서 데이터 간의 이동이 빠르다
	![이중 연결 리스트](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170111/imgs/Doubly_linked_list.png?raw=true) 

		>장님과 앉은뱅이

- 원형 연결 리스트
	![원형 연결 리스트](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170111/imgs/Circurlar_linked_list.png?raw=true)  
	
	
	
모든 리스트는 상황에 맞추어 가장 알맞은 방법을 선택하여 활용한다

---

###스택
![스택](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170111/imgs/stack.png?raw=true)  
>_First in, Last out!_  
>인터넷 뒤로 가기를 생각하면 빠르다

---

###큐
![스택](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170111/imgs/queue.png?raw=true)  
>_First in, First out!_  
>은행 창구를 생각하면 빠르다

---

###덱큐
![덱큐](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170111/imgs/dequeue.png?raw=true)  
>스택 + 큐

---

###트리
![스택](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170111/imgs/tree.png?raw=true)  
>직박구리 - 국산, 일본, 서양 - 직캠, 몰카...  
>검색이 용이해진다

---

###그래프
![스택](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170111/imgs/graph.png?raw=true)  
>6다리 건너면 오바마랑 페친

---

##3. 알고리즘
>문제해결을 위한 절차 / 방법

###정렬 알고리즘
- 선택정렬
	- 전체를 스캔하여 가장 작은 값을 맨 앞에 가져다두는 방식

- 버블정렬
	- 인접 데이터와 비교를 반복하여 가장 큰 값을 스캔 구역 제일 뒤로 가져다두는 방식

- 삽입정렬
	- 선택한 데이터를 이미 정렬된 데이터의 사이에 삽입하여 정렬하는 방식

- 병합정렬
	- 일정 구간을 나누어 정렬함을 반복하여 최종 정렬을 끝내는 방식

- 퀵정렬
	- 중간값을 기준으로 절반 정렬을 반복

---

###시간 복잡도
- 알고리즘이 실행되는데 소요되는 시간분석
	- 최악만 피하자는 생각으로 각종 표기법 중 O(Big O)표기를 이용하여 표기한다
		- 선형 탐색: O(n)
		- 이진 탐색: O(log n)

---

##4. 자료구조 X 알고리즘은 왜 세트인가
>요즘은 자구알이라고 한다더라

둘의 이해관계 때문에 뗄레야 뗄 수가 없다

###ex)테트리스
**적절한 모양의 블럭**(자료구조)를 이용하여 **요리조리 돌려서**(알고리즘) 게임 클리어!  
![테트리스](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170111/imgs/tetris.png?raw=true)  
>오른쪽은 주커버그 왼쪽은 나다