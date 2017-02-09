##Design Pattern

###Singleton(단일체)
- 클래스명 name = new 클래스명(); 을 못하게 하려는 것이 주 목적
- 메모리를 하나로 줄이고 정보를 공유하는 결과를 나타냄

>혼자 개발할 때도 쓰는 이유는 객체지향에서 서로 다른 클래스에서 개체화 할때마다 메모리를 잡아먹을 수 있기 때문이지

##### 디자인 순서
1. 클래스를 담을 변수 생성
2. 생성자 private로 new 클래스명() 제한
3. 생성자를 만들어 넘겨주는 메소드 생성

```
public class Singleton {
	
	private static Singleton instance = null;
	
	private Singleton() {
		
	}
	
	public static Singleton getInstance() {
		// 1. Singleton을 담는 instance가 값을 가지는지 체크한다
		if(instance==null) {
			instance = new Singleton();
		}
		// 2. instance 반환
		return instance;
	}
}
```

Multi-Thread 환경에서는 동기화를 추가해주어야 완벽한 Singleton을 구현할 수 있다

---

###Multiton

##### 디자인 순서
1. 생성자 제한
2. 생성자를 만들어 넘겨주는 메소드 생성

```
public class Multiton {
	
	public String name="";
	
	// 생성자를 private으로 막는다
	private Multiton() {}
	
	// 생성함수를 만든다
	public static Multiton newInstance() {
		return new Multiton();
	}
}
```
---

###Proxy
- 원본데이터는 건드리지 않는 범위에서 데이터를 간접적으로 참조할 수 있도록 만들어준다  
정보 요청의 주체는 연산하지 않고 Proxy가 연산하여 값만을 전달해 주는 데이터의 흐름을 관리

```
class MainProxy {
    public static void main(String[] args) {
        Image image1 = new ProxyImage("Image_Uri_1");
        Image image2 = new ProxyImage("Image_Uri_2");

        image1.displayImage();
        image2.displayImage();
    }
}
```
```
interface Image {
    public void displayImage();
}
```
```
class RealImage extends Image {
	private String fileName;
	
	public RealImage(String fileName) {
		this.fileName = fileName;
		loadImage();
	}
	
	public void loadImage() {
		System.out.println("Loading : " + fileName);
	}

	public void displayImage() {
		System.out.println("Displaying : " + fileName);
	}
}
```
```
class ProxyImage extends Image() {
	private String fileName;
	private Image img = null;
	
	public ProxyImage(String fileName) {
		this.fileName = fileName;
	}
	
	public void displayImage() {
		if(image==null) {
			image = new RealImage(fileName);
		}
		image.displayImage();
	}
}
```
---

###Decorator
- 프록시와는 달리 원본데이터를 가공하는 방식

프록시는 데이터의 흐름을 관리하고 데코레이터는 데이터를 가공하여 관리한다

---

###Template
- 부모의 구현 메소드가 자식이 구현한 부모의 추상 메소드를 호출하는 방식

```
public abstract class Template {
	public void play() {
		System.out.printf("%s\n", "플레이가 시작됩니다");
		jump();
	}
	
	public abstract void jump();
}
```
```
public class Frog extends Template {
	@Override
	public void jump() {
		System.out.println("폴짝폴짝");
	}
}
```
```
public class Rabbit extends Template {
	@Override
	public void jump() {
		System.out.println("깡총깡총");
	}
}
```
```
Console)
플레이가 시작됩니다
폴짝폴짝
플레이가 시작됩니다
깡총깡총
```
---

###Factory

---

###Strategy
- 경우의 수에 따라 개체화시켜 사용하는 방식

##### 디자인 순서
1. 인터페이스 생성
2. 전략을 사용할 Context 객체 생성
3. 클라이언트를 각각 생성하여 Context에 삽입

```
public interface Strategy {
	void runStrategy();
}
```
```
public class Soldier {
	public void useStrategy(Strategy strategy) {
		System.out.println("-----전투 시작-----");
		strategy.runStrategy();
		System.out.println("-----전투 종료-----");
	}
}
```
```
public class StrategySword implements Strategy {
	@Override
	public void runStrategy() {
		System.out.println("찌른다~~~~~");
	}
}

public class StrategyGun implements Strategy {
	@Override
	public void runStrategy() {
		System.out.println("쏜다~~~~~");
	}
}

public class StrategyNuclear implements Strategy {
	@Override
	public void runStrategy() {
		pushButton();
		System.out.println("핵발사~~~~~");
	}
	private void pushButton() {
		System.out.print("핵 버튼을 눌러서 ");
	}
}
```

```
MainActivity)
Strategy strategy = null;
Soldier soldier76 = new Soldier();
	
int distanceBetweenEnemy = new Scanner(System.in).nextInt();
	
if(distanceBetweenEnemy<10) {
	strategy = new StrategySword();
} else if(distanceBetweenEnemy>=10&&distanceBetweenEnemy<50) {
	strategy = new StrategyGun();
} else {
	strategy = new StrategyNuclear();
}
	
soldier76.useStrategy(strategy);
```
---

###Strategy CallBack
- Strategy 와 거의 유사하지만 경우에 따라 매번 Override 해서 Context에 삽입해주는 방식

```
Soldier soldier762 = new Soldier();
	
int distanceBetweenEnemy = new Scanner(System.in).nextInt();
	
if(distanceBetweenEnemy<10) {
	soldier762.useStrategy(new Strategy() {
		@Override
		public void runStrategy() {
			System.out.println("두번 찌른다~~~");
		}
	});
} else if(distanceBetweenEnemy>10&&distanceBetweenEnemy<50) {
	soldier762.useStrategy(new Strategy() {
		@Override
		public void runStrategy() {
			System.out.println("두번 쏜다~~~");
		}
	});
} else if(distanceBetweenEnemy>50) {
	soldier762.useStrategy(new Strategy() {
		@Override
		public void runStrategy() {
			System.out.println("핵쏜다~~~");
			push();
		}
		private void push() {
			System.out.println("두번 쏜다");
		}
	});
}
```
---