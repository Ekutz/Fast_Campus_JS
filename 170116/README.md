##1. Java란
>James Gosling 개발 / 객체지향을 더 완벽하게 하기 위한 C++의 확장 언어

###Java의 특징
- 객체지향
- 캡슐화
- 상속
- 다형성
- Garbage Collector
	- JVM(Java Virutal Machine)이 스스로 메모리 관리를 해준다
- OS 독립성
	- 모든 OS에서 동일한 코드로 동일하게 작동

---

##2.자바 코딩 및 실행법(with Terminal.app)

1. 서브라임으로 코딩
2. 파일명(Camel Case로 생성).java 형태로 저장
3. 터미널에서 디렉토리 이동
4. _$_ javac 파일명.java
5. 파일명.class 생성된 것 확인
6. _$_ java 파일명 -> 실행

---
##### Tips
	다른 함수는 몰라도 main 함수는 꼭 정해진 형태에 맞춰져야 한다  
	- public static void main(String[] 파라미터 이름)
	
	파일명과 클래스명이 반드시 같아야 한다
	
	들여쓰기 할 땐 공백 4개
	
	함수 내부 logic은 함수 내부에서 작성할 것

---

##3. Java 파일의 Runtime 컴파일

JIT
>Just In Time

- 실행 시 최초 한번 기계어로 컴파일 한다. 속도 저하 발생 가능

AOT
>Ahead Of Time

- 설치 시 최초 한번 기계어로 컴파일 한다. 안드로이드와 같이 명확한 구조에서만 가능하다.

안드로이드 Nougat 부터는 두가지를 안드로이드 OS가 알아서 판단해서 한다
<del>나보다 약한자의 명령을 따르지 않는다</del>

---

##4. Java 함수 만들기

    [접근 제어자] [리턴형] [함수명] ([파라미터])

```
ex) public void print(String value)
    private int add(int a, int b)
```

##5. JavaDoc 주석 방식
		/** + 엔터
>자동으로 JavaDoc 주석이 생성된다

```
/** [바로 아래에 나오는 method 설명]
  *
  *
  */
```

###JavaDoc 생성 방법

	File - Export - 'javadoc' 검색 - 설정 - finish
	workspace에 가면 doc 폴더가 생성되고 index.html을 열면 JavaDoc을 열람할 수 있다

---