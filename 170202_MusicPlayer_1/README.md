# 뮤직 플레이어 - 1
> 음원의 정보를 받아와서 RecyclerView에 붙여 진열한다

---

##뮤직 플레이어
>스마트폰 저장 공간에 있는 음악을 가져와서 실행하는 로컬 뮤직 플레이어

### 기획 순서
1. 스마트폰 내부 저장 공간을 이용하는 권한에 대한 권한 획득을 한다
2. 곡의 정보를 받을 Music 클래스를 만든다
3. 곡 정보를 받아오는 DataLoader 클래스를 만든다
4. MusicAdapter 클래스를 만든다
5. MainActivity의 init()에서 데이터를 받고 adapter를 붙인다

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
	//TODO 기획 순서 5에서 제작
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
public class DataLoader {

    private static ArrayList<Music> datas = new ArrayList<>();
    Context context;

    public static ArrayList<Music> load(Context context) {
        if(datas==null|| datas.size()==0) {
            getContacts(context);
        }
        return datas;
    }

    public static void getContacts(Context context) {

        Uri uri = MediaStore.Audio.Media.EXTERNAL_CONTENT_URI;

        String projections[] = new String[] {
                MediaStore.Audio.Media._ID,
                MediaStore.Audio.Media.ALBUM_ID,
                MediaStore.Audio.Media.TITLE,
                MediaStore.Audio.Media.ARTIST,
                MediaStore.Audio.Media.DURATION
        };

        ContentResolver resolver = context.getContentResolver();

        String sortOrder =  MediaStore.Audio.Media.ALBUM_ID+ " ASC";

        Cursor cursor = resolver.query(uri, projections, null, null, sortOrder);

        if(cursor.moveToFirst()) {
            while(cursor.moveToNext()) {
                Music mMusic = new Music();

                int idx = cursor.getColumnIndex(projections[0]);
                mMusic.id = (cursor.getString(idx));
                idx = cursor.getColumnIndex(projections[1]);
                mMusic.album_id = (cursor.getInt(idx));
                idx = cursor.getColumnIndex(projections[2]);
                mMusic.title = (cursor.getString(idx));
                idx = cursor.getColumnIndex(projections[3]);
                mMusic.artist = (cursor.getString(idx));
                idx = cursor.getColumnIndex(projections[4]);
                mMusic.length = (cursor.getInt(idx));

                mMusic.album_img = getAlbumImgSimple(""+mMusic.album_id);

                mMusic.uri = getMusicUri(mMusic.id);

                datas.add(mMusic);
            }
            cursor.close();
        }
    }

	// 음원 저장소의 uri + muisc_id 로 각 음원의 uri를 반환
    private static Uri getMusicUri(String music_id) {
        Uri contentUri = MediaStore.Audio.Media.EXTERNAL_CONTENT_URI;
        return Uri.withAppendedPath(contentUri, music_id);
    }
}

```
---

## 4. Adapter 제작
```
public class MusicAdapter extends RecyclerView.Adapter<MusicAdapter.Holder> {

    ArrayList<Music> data;
    Context context;
    Intent i = null;

    public MusicAdapter(ArrayList<Music> data, Context context) {
        this.data = data;
        this.context = context;
        i = new Intent(context, PlayActivity.class);
    }

    @Override
    public Holder onCreateViewHolder(ViewGroup parent, int viewType) {
        View view = LayoutInflater.from(parent.getContext()).inflate(R.layout.card_item, parent, false);
        Holder holder = new Holder(view);
        return holder;
    }

    @Override
    public void onBindViewHolder(Holder holder, int position) {
        final Music music = this.data.get(position);

        int dur_min = music.length/1000/60;
        int dur_sec = music.length/1000 - (dur_min)*60;

        // Glide를 활용하여 이미지 삽입해주기
        Glide.with(context).load(music.album_img).placeholder(android.R.drawable.ic_dialog_alert).into(holder.img);
        //글라이드.활용(context).load(uri).placeholder(공석일 경우 대체 이미지).into(위젯);

        holder.album_id.setText(""+music.album_id);
        holder.title.setText(music.title);
        holder.artist.setText(music.artist);
        holder.length.setText("0"+dur_min+":"+dur_sec);
        holder.position = position;

        Animation anime = AnimationUtils.loadAnimation(context, android.R.anim.slide_in_left);
        holder.card.setAnimation(anime);
    }

    @Override
    public int getItemCount() {
        return data.size();
    }

    public class Holder extends RecyclerView.ViewHolder {

        ImageView img;
        TextView album_id, title, artist, length;
        CardView card;

        int position;

        public Holder(View itemView) {
            super(itemView);

            img = (ImageView)itemView.findViewById(R.id.imgView);
            album_id = (TextView)itemView.findViewById(R.id.txtAlbumId);
            title = (TextView)itemView.findViewById(R.id.txtTitle);
            artist = (TextView)itemView.findViewById(R.id.txtArtist);
            length = (TextView)itemView.findViewById(R.id.txtLength);
            card = (CardView)itemView.findViewById(R.id.cardView);

            card.setOnClickListener(new View.OnClickListener() {
                @Override
                public void onClick(View view) {
                }
            });

        }
    }
}
```
## 5. init() 완성
```
MainActivity)
public void init() {
	// Dataloader에서 데이터 받아오기
	ArrayList<Music> data = Dataloader.load(this);
	lv = (RecyclerView)findViewById(R.id.recyView);
	// Adapter에 data, context 전달
	MusicAdapter adapter = new MusicAdapter(data, MainActivity.this);
	lv.setAdapter(adapter);
	lv.setLayoutManager(new LinearLayoutManager(this));
}
```
---

##Glide
> 이미지를 가져오다보면 딜레마에 빠지기 마련이다.  
> 1. App 내부에 이미지를 저장하고 불러오기  
> 2. URL 등을 사용하여 로드해서 불러오기  
> 
> 1의 경우에는 매우 단순한 코드 작성과 안정성의 장점이 있지만 App 자체의  
> 용량이 크다는 단점이 있다. 2의 경우에는 App의 용량을 비약적으로 줄일 수  
> 있지만 통신의 안정성이 요구되고 Bitmap으로 처리할 경우 메모리를 걱정해야  
> 한다는 단점이 있다. 그래서 이미지 로딩 라이브러리를 사용한다.

### 1. Gradle 추가
```
compile 'com.github.bumptech.glide:glide:3.6.0'
```

### 2. 클래스 내 사용법
```
Glide.with(context).load(uri).placeholder(공석일 경우 대체 이미지).into(위젯);
```

### 3. 다른 메소드
```
error(uri)
로딩에 실패했을 경우 실패 이미지를 지정한다

thumbnail(float percent)
: 지정한 %비율 만큼 이미지를 Blur 처리 후 가져와서 보여준다

asGif()
: gif을 가져온다
```