##Solid (SRP, OCP, LSP, ISP, DIP)
>객체지향 설계 5대 기본원리

###SRP (Single Responsibility Principle)
>단일책임의 원리

- 하나의 class 는 하나의 책임만 갖는다.
- 하나의 method 는 하나의 책임만 갖는다.

```
class Computer {
	String cpuName;
	int cpuPrice;
	String gpuName;
	int gpuPrice;
	.
	.
	.
}
```
>위와 같은 경우보다는 아래의 코드를 더 지향한다

```
class Computer {
	String cpuName;
	String gpuName;
}

class ComputerPrice {
	int cpuPrice;
	int gpuPrice;
}
```
---

###OCP (Open Closed Principle)
> 개방폐쇄의 원리

- 확장에 대해 열려(Open)야 하고, 수정에 대해서는 닫혀(Close)야 한다.
- 완성된 class 또는 method 는 수정하지 않는다.(error는 제외)
- error 이외에 기능의 추가 또는 수정시 extends를 통해 문제를 해결합니다.

```
class Computer {
	String cpuName;
	String gpuName;
	ComputerSpec spec;
	
	public Computer(String cpuName, String gpuName, ComputerSpec spec) {
		this.cpuName = cpuName;
		this.gpuName = gpuName;
		this.spec = spec;
	}
}

class ComputerSpec {
	.
	.
	.
}

class Cellphone {
	String armName;
	PhoneSpec spec;

	public Cellphone(String armName, PhoneSpec spec) {
		this.armName = armName;
		this.spec = spec;
	}
}

class PhoneSpec {
	.
	.
	.
}
```
> 위와 같이 매번 새로운 클래스를 생성하기 보단 상속으로 확장해서 처리한다

```
class Computer extends Gadget{
	String cpuName;
	String gpuName;
	ComputerSpec spec;
	
	public Computer(String cpuName, String gpuName, ComputerSpec spec) {
		this.cpuName = cpuName;
		this.gpuName = gpuName;
		this.spec = spec;
	}
}

class ComputerSpec extends GadgetSpec {
	.
	.
	.
}

class Cellphone extends Gadget {
	String armName;
	PhoneSpec spec;

	public Cellphone(String armName, PhoneSpec spec) {
		this.armName = armName;
		this.spec = spec;
	}
}

class PhoneSpec extends GadgetSpec {
	.
	.
	.
}
```

---

###LSP (Liskov Substitution Principle)
> 리스코프 치환의 원리

- 파생 class는 상위 class로 대체 가능해야 한다
- 상위 class의 기능을 파생 class가 포함해야 한다
- 상위 class의 기본기능을 파생 class 가 침범해서는 안된다
- 단, 파생 class에서 정의된 변수는 자체적으로 관리할 수 있다.

```
void f(){  
    LinkedList list = new LinkedList();
    // …
    modify(list);
}

void modify(LinkedList list){  
    list.add(…);
    doSomethingWith(list);
}
```
> 위와 같이 만들면 컬렉션을 바꿔야 할 경우 모든 부분을 다 바꿔야 하지만  
> 아래와 같이 만들면 개체화 부분만 바꿔주면 모든게 해결된다!

```
void f(){  
     Collection collection = new HashSet();
     //…
     modify(list);
}

Void modify(Collection collection){  
     collection.add(…);
     doSomethingWith(collection);
}
```

---

###ISP (Interface Segregation Principle)
> 인터페이스 분리의 원리

- 특화된 여러개의 인터페이스가 범용 인터페이스 한개 보다 났다
- ISP 또한 SRP 가 적용되야 한다. 하나의 Interface는 하나의 특성만 관리한다.

---

###DIP (Dependency Inversion Principle)
>의존관계 역전의 원리

- 추상화된것은 구체적인것에 의존하면 안된다.
- 변경될 소지가 있는 구현체라면 인터페이스에 의존해야 한다.
- 인터페이스를 받는 클라이언트 또한 구현체가 아닌 인터페이스에 의존해야한다.