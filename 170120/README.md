#try catch

- JDK 1.7 이상 버전에서의 예외처리

```
usage)
try {
	// TODO
} catch(Error e) {
	// Print Error
} finally {
	// .Close()
}

try(IO) {
	// TODO
} catch(Error e) {
	// Print Error
}
```
>IO 선언을 try에 인자로 넘겨주면 자동으로 close 기능을 생성해준다.

---
#String 연산
- 반복문 안에서의 String + String 은 일반 + 연산으로 인식되므로 가급적 StringBuilder를 사용하자

```
StringBuilder str1 = new StringBuilder();
str1.append("aaa").append("bbb");
```

---

#Wrapper Class

- java는 데이터를 클래스나 객체 외에 (int, double, char 및 boolean과 같은) 기초 타입을 가진다. 따라서 Java에서는 기본형 타입과 객체 참조 같은 두가지 타입의 관리 데이터를 가지게 된다.

 > 데이터를 저장할 때, 기본형 타입의 변수에 저장할 수 있고, 다양한 객체들을 저장할 수 있는 컨테이너 역할을 하는 객체를 생성할 수도 있다. 그러나 어떤 상황에서는 기본형 타입을 객체로 사용해야 하는 경우가 있다. 이러한 경우에 기본형 타입 값을 객체로 포장할 필요가 있다. 

 > 포장 클래스(wrapper class)는 특정 기본형 타입을 나타낸다. 예를 들어 Integer 클래스는 간단한 정수 값을 나타낸다. Integer 클래스로부터 생성된 객체는 하나의 int 값을 저장할 수 있다. Wrapper class의 구성자는 저장할 기본형 타입 값을 받는다.

#Boxing&UnBoxing

- Wrapper 클래스는 산술연산을 위해 정의된 클래스가 아니기 때문에, 이 클래스의 인스턴스에 저장된 값은 변경이 불가능하며, 값을 저장하는 새로운 객체의 생성 및 참조만 가능하다.


#java NIO package

- New I/O는 JDK1.4에서 새로 추가된 패키지이다. JDK1.4의 정식 명칭은 Java 2 Standard Edition JDK1.4이다.

> - 기본 데이터형용 버퍼를 클래스로 제공해 준다.
> - Character-set 인코더들과 디코더.
> - 패턴과 어울린 기능은 Perl-style 정규식들로 설정.
> - 채널, 새로운 I/O 추상화.
> - 메모리 매핑과 파일의 lock(잡금장치)를 지원해주는 인터페이스.
> - non-blocking 입출력이 가능.

#java IO Stream Package
 - Java에서 데이터는 Stream을 통해 입출력된다. 
 
- 프로그램이 데이터를 입력받을 때에는 InputStream 이라 부르고, 프로그램이 데이터를 보낼 때에는 OutputStream 이라고 부른다.

 - Stream은 단방향이므로 프로그램이 다른 프로그램과 데이터를 교환하려면 양쪽 모두 InputStream과 OutputStream이 필요하다.


#java IO Stream 구성
 - 스트림은 크게 입력, 출력 두가지 형태로 구분할 수 있는데 바이트 기반 스트림은 이미지, 동영상 ,문자 등 모든 종류의 미디어를 주고받을 수 있는데 반해, 캐릭터 기반 스트림은 문자만 주고 받도록 설계되어 있다.

#IO vs NIO

- IO와 NIO는 데이터를 입출력한다는 목적은 동이랗지만, 방식에 있어서는 차이점이 있다.

> - Stream vs Channel
채널은 입출력시 하나만 생성하는 반면, 스트림은 입력과 출력 두개 필요

> - non-Buffer vs Buffer
버퍼는 HW/SW 간의 속도차이를 줄여준다. 빠르다. 채널은 기본적으로 버퍼를 사용한다.

> - Blocking vs non-Blocking
스트림은 파일 읽기시 해당 스레드가 블로킹되고 ‌interrupe로 빠져나오는 것도 불가능하다, stream.close()로만 블로킹을 해제할 수 있다.

#NIO Pate처리 (jdk 7 이상)

 - 1. 파이렃리의 간소화를 위해 NIO2 도입 (NIO = new I/O)
 - 2, 경로에 대한 처리를 위해 Path가 추가되었다.
 - 3. 파일의 읽기와 쓰기를 위한 method가 추가되었다.


# NIO File 처리

- 파일과 디렉토리 생성

- 파일 복사, 이동, 삭제


#NIO장점
- 불특정 다수의 클라이언트 연결 또는 멀티 파일들을 넌 블로킹이나 비동기로 처리할 수 있기 때문에 과도한 스레드 생성을 피하고 스레드를 효과적으로 재사용한다는 점에서 큰 장점이 있다.

#IO
- 대용량 데이터를 처리할 경우에는 IO가 더 유리한데, NIO는 버퍼의 할당 크기도 문제가 되고, 모든 입출력 작업에 버퍼를 무조건 사용해야 하므로 받은 즉시 처리하는 IO보다는 좀 더 복잡하다.