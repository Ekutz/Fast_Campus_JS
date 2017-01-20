##1. Class

```
class Person {	// Class의 첫 글자는 대문자이다

}
```
1. 속성 값을 정해준다
2. 생성자를 만들어 준다
3. 기능(메소드) 정의하기
4. 메소드 오버로드
5. 접근제한자 설정
	- default
	- public
	- protected
	- private

---

Overload vs Override

- Overload
	- 같은 이름의 메소드를 만들되, 파라미터 자료형이나 수가 반드시 달라야 하고 리턴 값이나 접근제한자가 다르게 하는것.  

			public int sum(int a, int b)
			public int sum(int a, int b, int c)
			public double sum(double a, double b)

- Override
	- 상속해준 부모 클래스의 메소드를 자식 클래스에서 수정해야 할 때 권한을 이임받는 것

			in Parent.class
				public void add(int a, int b) {
					a + b;
				}
				
			in Child.class
				@Override
				public void add(int a, int b) {
					System.out.println(a+b);
				}

---

상속  
상속한 class의 모든것을 사용할 때 사용

```
public class 클래스명 extends 부모클래스명 {

}
```

- 부모 클래스의 변수, 메소드 등을 모두 사용할 수 있다.
- 부모 클래스도 상속을 받은 경우 조부모 클래스의 변수, 메소드도 모두 사용 가능하다.

---

POJO
>Plain Old Java Object



---
Getter 와 Setter 만들기

>속성을 선언한 클래스가 아닌 "사용할 클래스의 입장"에서 본 이름이다.  
>주로 getter는 속성값을 반환하고 setter는 속성값을 지정해준다.

```
우클릭 -> source -> Generate Getters and Setters
```
>내가 이거 있는거 미리 알았으면 이렇게 머리 쥐어뜯지도 않았을 텐데

---


##2. BBS 만들기