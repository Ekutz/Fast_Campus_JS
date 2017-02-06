##뮤직 플레이어
>스마트폰 저장 공간에 있는 음악을 가져와서 실행하는 로컬 뮤직 플레이어

### 기획 순서
1. 스마트폰 내부 저장 공간을 이용하는 권한에 대한 권한 획득을 한다
2. 곡의 정보를 받을 Music 클래스를 만든다
3. 곡 정보를 받아오는 DataLoader 클래스를 만든다
4. DataLoader로 부터 받은 정보를 받을 MusicAdapter를 만들어 RecyclerView에 붙인다

---

## 1. 권한 획득

```
AndroidManifest)
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />

추가

```
```
MainActivity)
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

	// 현재 스마트폰의 안드로이드 버젼과 마시멜로우의 버젼의 숫자를 비교하여  
		마시멜로우 이상일 경우 런타임 권한 획득 방시으로 권한을 획득한다
    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
        checkPermission();
    } else {
        init();
    }
}



private final int REQ_CODE = 100;

@TargetApi(Build.VERSION_CODES.M)
private void checkPermission() {
    if (checkSelfPermission(Manifest.permission.READ_EXTERNAL_STORAGE) !=
		PackageManager.PERMISSION_GRANTED) {
        
        String permArr[] = {Manifest.permission.READ_EXTERNAL_STORAGE};

        requestPermissions(permArr, REQ_CODE);
    } else {
        init();
    }
}

@Override
public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
    super.onRequestPermissionsResult(requestCode, permissions, grantResults);

    if (requestCode == REQ_CODE) {
        if (grantResults[0] == PackageManager.PERMISSION_GRANTED) {
            init();
        } else {
            Toast.makeText(this, "권한 없으면 프로그램 못씀", Toast.LENGTH_LONG).show();
            finish();
        }
    }
}

public void init() {

}

```
---

## 2. Music.class
```
Music.class)
public class Music {
    String id; // 음원 고유 id
    Uri uri; // id를 이용해 음원의 uri를 담을 uri
    int album_id; // 음원의 album id(같은 앨범 수록곡일 시 같은 값을 가진다)
    Uri album_img; // album_id를 이용해 앨범 자켓의 uri를 담을 uri
    String title; // 음원의 제목
    String artist; // 음원의 아티스트
    int length; // 음원의 재생 길이(단위 : ms)
}
```
---

## 3. DataLoader.class
```


```