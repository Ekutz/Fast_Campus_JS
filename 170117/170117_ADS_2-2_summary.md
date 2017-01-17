##Java 기본 문법

###1. 조건문
>특정한 조건을 만족할 시 조건이 감싸고 있는 블럭을 실행하는 구문  

#####if문
>범위가 나누어져 있는 조건일 때 사용하면 좋다

```
usage)
if(조건1) {
	// TODO 해야할 작동
} else if(조건 2) {
	// TODO 해야할 동작
} else if...
.
.
.
} else if(조건 n) {
	// TODO 해야할 동작
} else {
	// TODO 어느 조건에도 해당되지 않을 때 해야할 동작
}

ex)
if(i > 10) {
	System.out.print("a : " + a);
}

tip)
if(i > 10 || i<=100) {
	System.out.print("a : " + a);
}
와 같이 여러 조건을 동시에 만족시키게 만들 수도 있다
```
---

#####switch - case문
>특정 값과 직접 비교할 때 사용하면 좋다

```
usage)
switch 변수 {
	case 비교값1 :
		// TODO 해야할 동작
		break;
			.
			.
			.
	case 비교값n :
		// TODO 해야할 동작
		break;
	default :
		// TODO 어떤 비교값과도 같지 않을 때 해야할 동작
}

ex)
switch i {
	case 1 :
		System.out.print("i : " + i);
		break;
	case 2 :
		System.out.print("i : " + i);
		break;
	default :
		System.out.print("1도 2도 아니다");
		break;
}

tip)
매 case마다 break;를 써주지 않으면 해당 case 이하의 모든 case를
전부 실행시킨다. 의도한 것이 아니라면 꼭 break;를 써주자
```
---
###2. 반복문
>지정된 조건을 만족할 때 까지 특정 동작을 반복 실행하는 문법

#####for문
>지정된 변수의 증감으로 조건을 만들어서 반복시킬 때 쓰면 좋다

```
usage)
for(초기화;만족조건;증감) {
	// TODO 해야할 동작
}

ex)
int i=0;
for(i=0;i<100;i++) {
	System.out.print("i : " + i);
}

tip)
for(;;;) {
	// TODO 해야할 동작
}
형식으로 만들면 강제로 무한 루프에 빠지게 된다
```

---

#####while문
>for문을 세로로 분리해 놓은 문법 <del>대체 왜...?</del>

```
usage)
while(조건) {
	// TODO 해야할 동작
}

ex)
int i=0;
while(i<100) {
	System.out.print("i : " + i);
	i++;
}

tip)
while(true) {
	// TODO 해야할 동작
}
형식으로 만들면 강제로 무한 루프에 빠지게 된다
```
---