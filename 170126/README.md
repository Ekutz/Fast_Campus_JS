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
![activity_life_cycle](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170126/imgs/activity_life_cycle.jpg?raw=true)

새롭게 호출된 액티비티가 기존의 액티비티를 전부 가린다면 onStop()이 실행된다. 그러나 새롭게 호출된 액티비티가 반투명하거나 액티비티가 아닌 뷰일 경우에는 onPause()까지만 실행된다.

---

##액티비티에 추가 정보 담아 보내기
인텐트에 추가 정보를 HashMap 형태로 담아 붙여 보낼 수 있다

```
MainActivity)

Intent i = new Intent(this, SecondActivity.class);
i.putExtra("extra", "추가 정보");
startActivity(i);
```
```
SecondActivity)

String str = "";

Intent getI = getIntent();
Bundel bundle = getI.getExtras();

str = bundle.getString("extra");
```

---

##액티비티를 통해 실행 값 받기
> "사진 파일 등록"과 같은 기능은 다른 액티비티를 소환한 뒤 소환된 액티비티에서 얻은 정보를 기존에 있는 액티비티에 전달해야 한다  
> 기존에 있는 액티비티는 인텐트 등으로 조작이 불가능하므로 result 기능을 사용한다

```
MainActivity)

public static final int SECOND = 2; // requestCode가 되는 final int 값

Intent i = new Intent(MainActivity.this, SecondActivity.class);
i.putExtra("extra", "추가 정보");
stratActivityForResult(i, SECOND);


@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if(resultCode == 1) {
    	 Bundle bundle = data.getExtras();
        String result = bundle.getString("result");
        switch (requestCode) {
    		case TWO:
                // TODO
                break;
        }
    }
}
```

```
SecondActivity)

Intent getI = new Intent();
int statusCode = 1; // MainActivity.resultcode = statusCode
if (sendData.equals("")) {
    statusCode = 0;
}
intent.putExtra("result", "결과 정보");
setResult(statusCode, getI);
```
---

##Logger
> Log를 사용해서 바로 찍는 방법이 있지만 실제로 App을 Release 했을 때는 Log가 찍히지 않도록 Logger 클래스를 따로 만들어 준다

```
Logger)
public final static boolean DEBUG_MODE = true;
    
public static void print(String str, String className) {
    if(DEBUG_MODE) Log.w(className, str);
}
```
---