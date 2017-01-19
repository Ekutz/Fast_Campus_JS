##1. 배열
>특정 자료형의 묶음, 묶음의 크기를 지정할 수 있다.

```
int[] name = new int[]
찾기 쉬움

int name[] = new int[]
자료형 배열이 정돈된다
```
<del>지긋지긋한 편집증</del>

```
usage)
1차원 : 자료형[] 이름 = new 자료형[크기];
2차원 : 자료형[][] 이름 = new 자료형[y크기][x크기];
.
.
.
n차원 : 자료형[][]...[] 이름 = new 자료형 [n크기]...[y크기][x크기];
```
```
ex)
int x = 5, y = 7, z = 10;

int array[][][] = new int[z][y][x];
```
```
tip)
- int 배열은 선언과 동시에 0으로 전부 초기화 됨
```
---
##2. 컬렉션
>객체 자료형의 묶음, 배열의 단점을 보완하기 위해 나왔다. 크기가 동적이다.  
>또한 서로 다른 타입도 같은 컬렉션 내에 삽입 가능하다

###ArrayList
```
usage)
ArrayList<자료형> 이름 = new ArrayList<자료형(생략가능)>();
```
```
ex)
ArrayList<String> nameList = new ArrayList<>();
```
```
tip)
객체를 넣을 수 있기 때문에 추후 안드로이드에서 굉장히 유용하게 쓰일 예정이다.
```
---
##3. 문자열
>참조형 클래스이지만 기본형처럼 사용하는 클래스  
>특별히 비교 시에는 '=='이 아닌 'str1.equals(str2)'형을 사용한다

- 아래 문자열 관련 메소드들은 str1과 str2로 예시를 든다

#####비교
```
usage)
str1.equals(str2)
```
```
return)
boolean : true, false
```
```
ex)
str1 = "Hello";
str2 = "hello";
str1.equals(str2)
```
>false

---
#####인덱스 값으로 문자열에서의 위치 찾기
```
usage)
str1.charAt(index)
```
```
return)
char : str의 index위치의 character
```
```
ex)
String str1 = "Hello";
str1.charAt(1)
```
>'e'

---

#####문자열 합치기
```
usage)
str1 + str2
```
```
return)
String : str1+str2
```
```
ex)
str1 = "000";
str2 = "111";
str1 + str2;
```
>"000111"

---

#####기준과 비교
```
usage)
str1.startsWith(str2)
str1.endsWith(str2)

```
```
return)
boolean : true, false
```
```
ex)
str1 = "12344321";
str2 = "123";
str1.startsWith(str2)
str1.endsWith(str2)
```
>true  
>false

---

#####문자열의 위치
```
usage)
str1.indexOf(str2)
```
```
return)
int : str2가 위치한 str1의 index
```
```
ex)
str1 = "7654321";
str1.indexOf("1")
```
>6

---

#####문자열의 길이
```
usage)
str1.length()
```
```
return)
int : str1의 길이
```
```
ex)
str1 = "12345678";
str1.length()
```
>8

---

#####문자열 수정
```
usage)
str1.replace("str2", "str3")
```
```
return)
String : str1 내부에 str2를 str3로 수정한 String
```
```
ex)
str1 = "123123123";
str1.replace("3", "4")
```
>"124124124"

---

#####문자열 구간 소환
```
usage)
str1.substring(int start)
str1.substring(int start, int range)
```
```
return)
String : str1의 start 부터 끝까지 / start부터 range까지의 String
```
```
ex)
str1 = "012345";
str1.substring(1)
str1.substring(1, 3);
```
>12345  
>12

---

>왜 str1.substring(1,3)인데 1,2,3 이 아닌 1,2가 출력 됐을까?

![index의 위치](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170118/imgs/index.png?raw=true)

---

#####문자열 분리
```
usage)
str1.split(기준)
str1.toCharArray()
```
```
return)
String[] : 기준대로 분리된 각각의 String
char[] : 한글자씩 분리된 각각의 char
```
```
ex)
str1 = "Hello World!";
str2 = "a/b/c/def";
String strResult = str1.split("")
String strResult = str2.split("/")
char charResult[] = str2.toCharArray()
```
>["H"]["e"]["l"]["l"]["o"][" "]["W"]["o"]...  
>["a"]["b"]["c"]["def"]  
>['a']['/']['b']['/']['c']['/']['def']

---
#####문자열 포함 확인
```
usage)
st1.contains(str2)
```
```
return)
boolean : true, false
```
```
ex)
str1 = "12345";
str2 = "34";
str1.contains(str2)
```
>true

---
#####문자를 숫자로 변환
```
usage)
int number = Integer.parseInt(str1)
```
```
return)
int : str1의 숫자형 값
```
```
ex)
str1 = "888";
int number = Integer.parseInt(str1)
```
>888

---