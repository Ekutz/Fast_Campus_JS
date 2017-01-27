##Intent
> 다른 액티비티나 서비스 등으로 구성된 컴포넌트를 호출할 때 사용되는 객체

###명시적
호출하는 클래스의 이름을 명시하여 호출하는 인텐트

```
usage)
Intent 이름 = new Intent(호출하는 액티비티, 호출되는 액티비티);
startActivity(이름);
```
```
ex)
Intent i = new Intent(MainActivity.this, SecondActivity.class);
startActivity(i);
```


###암시적
호출하는 클래스의 이름은 없지만 해당 기능을 가진 클래스를 호출하는 인텐트

```
usage)
Intent 이름 = new Intent(Intent.ACTION_기능, Uri.parse(기능에 맞는 프토토콜 + 추가 path);
startActivity(이름);
```
```
ex)
Intent iDial = new Intent(Intent.Action_DIAL, Uri.parse("tel : " + "01012345678");
startActivity(iDial);
```
#####암시적 액션
|액션|대상 컴포넌트|기능|
|:-:|:-:|:-:|
|ACTION_CALL|액티비티|path 번호로 전화 걸기|
|ACTION_SENDTO|액티비티|path 번호로 문자 보내기|
|ACTION_BATTERY_LOW|브로드캐스트 리시버|배터리 저전압 경보|

---

##액티비티
어플리케이션의 "화면" 단위

---

##액티비티 생명주기



새로 호출된 액티비티가 완전히 기존 액티비티를 가리면 onStop()까지 호출  
반투명이나 다이얼로그 등은 onPause()

> 안드로이드 버전에 따라 생각해야 할게 많다...

---
