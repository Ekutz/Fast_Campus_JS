##조건문과 반복문을 이용한 패턴 그리기 연습
>다양한 패턴 그리기를 통해 조건문과 반복문을 연습하고 알고리즘 연습을 한다.

###Pattern 1
![pt1](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170119/imgs/pt1.png?raw=true)

- 가장 기본적인  삼각형 그리기

```
int i = 0, j = 0;

for(i=1;i<=count;i++) {
	for(j=1;j<=i;j++) {
		System.out.print(unit);
	}
	System.out.println("");
}
```

---

###Pattern 2
![pt2](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170119/imgs/pt2.png?raw=true)

- 패턴 1을 거울 반전 시킨 형태

```
int i = 0, j = 0, k=0;
		
for(i=1;i<=count;i++) {
	for(k=count;k>i;k--) {
		System.out.print(" ");
	}
	for(j=1;j<=i;j++) {
		System.out.print(unit);
	}
	System.out.println("");
}
```

---

###Pattern 3
![pt3](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170119/imgs/pt3.png?raw=true)

- 각 층(0~)의 2배에 1을 더한 숫자 만큼 글자를 출력하도록 설계하였다

```
int floor=0, j=0, k=0;
int spaces = (2*count-1)/2;
	
for(floor=0;floor<count;floor++) {
	for(k=spaces;k>floor;k--) {
		System.out.print(" ");
	}
	for(j=0;j<(2*floor+1);j++) {
		System.out.print(unit);
	}
	System.out.println("");
}
```

---

###Pattern 4
![pt4](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170119/imgs/pt4.png?raw=true)

- 패턴 3을 만들면서 각 층의 index가 시작과 끝일 때만 문자를 출력하도록 설계

```
int i=0, j=0, k=0;
		
for(i=0;i<count;i++) {
	for(k=(2*count-1)/2;k>i;k--) {
		System.out.print(" ");
	}
	System.out.print(unit);
	for(j=0;j<(2*i-1);j++) {
		System.out.print(" ");
	}
	if(i!=0) System.out.print(unit);
	System.out.println("");
}
```

---

###Pattern 5
![pt5](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170119/imgs/pt5.png?raw=true)

- 전체 층 수가 홀수일 때와 짝수일 때의 출력이 달라야 하므로 중간 층을 산출한 뒤 중간 층 이전과 이후로 방식을 나누어서 출력한다

```
int floor=0, units=0, pre_spaces=0;
int half = 0;
int pre_numberOfPreSpace = 0;
if(count%2==0) {
	pre_numberOfPreSpace = ((2*(count/2)-1))/2;
} else {
	pre_numberOfPreSpace = ((2*((count/2)+1)-1))/2;
}
	
if(count%2==0) {
	half = count/2;
	for(floor=0;floor<half;floor++) {
		for(pre_spaces=pre_numberOfPreSpace;pre_spaces>floor;pre_spaces--) {
			System.out.print(" ");
		}
		int pre_numberOfUnit = (2*floor)+1;
		for(units=0;units<pre_numberOfUnit;units++) {
			System.out.print(unit);
		}
		System.out.println("");
	}
	for(floor=half;floor>0;floor--) {
		for(pre_spaces=pre_numberOfPreSpace+1;pre_spaces>floor;pre_spaces--) {
			System.out.print(" ");
		}
		int pre_numberOfUnit = (2*(floor-1))+1;
		for(units=0;units<pre_numberOfUnit;units++) {
			System.out.print(unit);
		}
		System.out.println("");
	}
} else {
	half = (count/2) +1;
	for(floor=0;floor<half;floor++) {
		for(pre_spaces=pre_numberOfPreSpace;pre_spaces>floor;pre_spaces--) {
			System.out.print(" ");
		}
		int pre_numberOfUnit = (2*floor)+1;
		for(units=0;units<pre_numberOfUnit;units++) {
			System.out.print(unit);
		}
		System.out.println("");
	}
	for(floor=half-1;floor>0;floor--) {
		for(pre_spaces=pre_numberOfPreSpace+1;pre_spaces>floor;pre_spaces--) {
			System.out.print(" ");
		}
		int pre_numberOfUnit = (2*(floor-1))+1;
		for(units=0;units<pre_numberOfUnit;units++) {
			System.out.print(unit);
		}
		System.out.println("");
	}
}
```

---

###Pattern 6
![pt6](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170119/imgs/pt6.png?raw=true)

- 각 층의 공백을 포함한 문자의 총 갯수를 구하고 index가 층수의 인수일 때 문자를 출력하도록 설계

```
int floor=0, units=0, spaces=0;
int pre_space = 0;
	
for(floor=count;floor>0;floor--) {
	for(spaces=pre_space;spaces>0;spaces--) {
		System.out.print(" ");
	}
	pre_space = pre_space + floor - 1;

	for(units=0;units<=(floor*(floor-1));units++) {
		if(units%floor==0) {
			System.out.print(unit);
		} else {
			System.out.print(" ");
		}
	}	
	System.out.println("");
}
```

---

###Pattern 7
![pt7](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170119/imgs/pt7.png?raw=true)

- 가장 아래층의 문자와 공백을 포함한 총 개수를 구하고 각 층은 거울 반전 되어 있으므로 왼쪽은 index에 출력 오른쪽은 (총 개수 - index)일 때 문자를 출력하도록 설계

```
int i=0, j=0;
int pre_spaces = 0;
int mcount=count;
	
for(i=mcount;i>0;i--) {
	pre_spaces = pre_spaces + i;
}
while(pre_spaces>0) {
	for(i=mcount;i>0;i--) {
		int whole = (count*(count+1));
		for(j=0;j<whole;j++) {
			int first = (pre_spaces-i);
			int second = (whole-first-1);
			if(j==first||j==second) {
				System.out.print(unit);
			} else {
				System.out.print(" ");
			}
		}
		System.out.println("");
		pre_spaces = pre_spaces - i;
	}
}
```

---
