##달팽이 그리기
>정보 처리 기사의 마지막 관문  
><del>그다지 큰 쓸모는 없구나</del>

![snail](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170119/imgs/snail.png?raw=true)

- size를 입력 받고 size X size 의 2차원 배열에 달팽이 모양으로 숫자를 입력하는 알고리

```
if(size==5)
 1  2  3  4  5
 6  7  8  9

10 11 12 13
14 15 16

17 18 19
20 21

22 23
24

25
```
```
if(size==7)
 1  2  3  4  5  6  7
 8  9 10 11 12 13

14 15 16 17 18 19
20 21 22 23 24

25 26 27 28 29
30 31 32 33

34 35 36 37
38 39 40

41 42 43
44 45

46 47
48

49
```

>위 두 예시와 같은 방식으로 돌아가는 알고리즘을 구현해 보았다

```
public void snail(int size) {
	
	int snail[][] = new int[size][size];
	
	// xpos는 0부터 시작해야 하는데 최초 진입 부터 1을 더해야 해서 -1로 시작시켰다
	int xpos=-1, ypos=0;
	int count = 0;
	
	// 한 방향을 돌때 마다 증감은 바뀌지만 절대값은 1로 고정이다
	int direction = 1;
	int times = size;
	int i = 0;
	while(times>0) {
		for(i=0;i<times;i++) {
			xpos+=direction;
			count++;
			snail[ypos][xpos]=count;
		}
		times--;
		for(i=0;i<times;i++) {
			ypos+=direction;
			count++;
			snail[ypos][xpos]=count;
		}
		//증감 부호 변환
		direction *= -1;
	}
	
	int check1=0,check2=0;
	for(check1=0;check1<size;check1++) {
		for(check2=0;check2<size;check2++) {
		//출력값이 10 미만이면 안 이쁘니까 경우의 수를 나눠준다
			if(snail[check1][check2]<10) {
				System.out.print("[0"+snail[check1][check2] + "] ");
				if(check2!=0&&check2%(size-1)==0) {
					System.out.println("");
				}
			} else {
				System.out.print("["+snail[check1][check2] + "] ");
				if(check2!=0&&check2%(size-1)==0) {
					System.out.println("");
				}
			}
		}
	}
}
```