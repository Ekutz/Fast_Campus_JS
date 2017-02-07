# 뮤직 플레이어 - 2
> 뮤직 플레이어 - 1의 리스트를 눌러 ViewPager와 연동된 재생기를 완성한다

---
### 기획 순서
1. PlayActivity를 만들고 ViewPager를 위치시킨다
2. PagerAdapter를 Custom 하여 ViewPager에 부착한다
3. 뒤로, 재생, 앞으로 버튼의 리스너를 붙이고 코드를 작성한다
4. Pager의 변화를 감지하는 OnPageChangeListener를 붙인다
5. 1초 마다 SeekBar를 움직이고 초 시계를 담당하는 Thread를 만들고 붙인다
6. 뮤직 플레이어 - 1 의 RecyclerView에서 선택한 item의 position 값을 받아서 로직에 넣는다

```
MusicAdapter)
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
            	//포지션 값을 PlayActivity로 보내준다
                i.putExtra("position", position);
                context.startActivity(i);
            }
        });

    }
}
```
```
public class CustomPagerAdapter extends android.support.v4.view.PagerAdapter {

    ArrayList<Music> music;
    Context context;
    LayoutInflater inflater;

    public CustomPagerAdapter(ArrayList<Music> music, Context context) {
        this.music = music;
        this.context = context;
        inflater = (LayoutInflater)context.getSystemService(Context.LAYOUT_INFLATER_SERVICE);
    }

    @Override
    public int getCount() {
        return music.size();
    }

    // 넘어온 오브젝트가 뷰가 맞는지 확인
    @Override
    public boolean isViewFromObject(View view, Object object) {
        return view==object;
    }


    // 리스트뷰의 getView와 같은 역할
    // view 자체를 만드는 메소드
    @Override
    public Object instantiateItem(ViewGroup container, int position) {
        //return super.instantiateItem(container, position);

        View view = inflater.inflate(R.layout.player_card_item, null);

        ImageView playerImg = (ImageView)view.findViewById(R.id.playerImg);
        TextView playerTit = (TextView)view.findViewById(R.id.playerTitle);
        TextView playerArt = (TextView)view.findViewById(R.id.playerArtist);

        Music data = music.get(position);

        playerTit.setText(data.title);
        playerArt.setText(data.artist);

        Glide.with(context).load(data.album_img).placeholder(android.R.drawable.ic_dialog_alert).into(playerImg);

        container.addView(view);

        return view;
    }

    // 화면에서 사라진 뷰를 메모리에서 제거해 주는 함수
    @Override
    public void destroyItem(ViewGroup container, int position, Object object) {
        container.removeView((View)object);
    }



}
```
```
public class PlayActivity extends AppCompatActivity {

    ArrayList<Music> music;
    ViewPager vp;

    ImageButton btnRew, btnPlay, btnFF;
    int position = 0;
    MediaPlayer audio;
    SeekBar sbar;
    TextView duration, time;

    private static final int PLAY = 0;
    private static final int PAUSE = 1;
    private static final int STOP = 2;

    private static int playStatus = STOP;

    private class OneSec extends Thread {

        @Override
        public void run() {
            while (playStatus < STOP) {
                if(audio!=null) {
                    runOnUiThread(new Runnable() {
                        @Override
                        public void run() {
                            try {
                                sbar.setProgress(audio.getCurrentPosition());
                                time.setText(convertTime(audio.getCurrentPosition()));
                                if (time.getText().toString().equals(duration.getText().toString())) {
                                    next();
                                }
                            } catch (Exception e) {

                            }
                        }
                    });
                }
                try {
                    Thread.sleep(1000);
                } catch(InterruptedException e) {

                }
            }
        }
    }



    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_play);

        setVolumeControlStream(AudioManager.STREAM_MUSIC);

        vp = (ViewPager)findViewById(R.id.viewPager);
        btnRew = (ImageButton)findViewById(R.id.btnRewind);
        btnPlay = (ImageButton)findViewById(R.id.btnPlay);
        btnFF = (ImageButton)findViewById(R.id.btnForwardF);
        sbar = (SeekBar)findViewById(R.id.seekBar);
        duration = (TextView)findViewById(R.id.txtDu);
        time = (TextView)findViewById(R.id.spendTime);

        btnRew.setOnClickListener(clickListener);
        btnPlay.setOnClickListener(clickListener);
        btnFF.setOnClickListener(clickListener);

        music = DataLoader.load(this);

        CustomPagerAdapter adapter = new CustomPagerAdapter(music, PlayActivity.this);

        vp.setAdapter(adapter);

        // ViewPager 페이지가 변하는 것을 감지하는 리스너
        vp.addOnPageChangeListener(pageListener);

        // SeekBar의 변화를 감지하는 리스너
        sbar.setOnSeekBarChangeListener(sbarListener);

        // 특정 페이지 호출
        Intent i = getIntent();
        if(i!=null) {
            Bundle bundle = i.getExtras();
            position = bundle.getInt("position");
            vp.setCurrentItem(position);

            if(position==0) {
                init();
                duration.setText(convertTime(music.get(position).length));
                time.setText("00:00");
                play();
            }
        }
    }

    SeekBar.OnSeekBarChangeListener sbarListener = new SeekBar.OnSeekBarChangeListener() {
        @Override
        public void onProgressChanged(SeekBar seekBar, int i, boolean b) {
            if(audio!=null&&b==true) // b = 사용자가 터치 했는지의 유무
            audio.seekTo(i);
        }

        @Override
        public void onStartTrackingTouch(SeekBar seekBar) {

        }

        @Override
        public void onStopTrackingTouch(SeekBar seekBar) {

        }
    };

    ViewPager.OnPageChangeListener pageListener = new ViewPager.OnPageChangeListener() {
        @Override
        public void onPageScrolled(int position, float positionOffset, int positionOffsetPixels) {

        }

        @Override
        public void onPageSelected(int position) {
            PlayActivity.this.position = position;
            if(audio!=null) {
                audio.release();
            }

            playStatus=STOP;
            init();
            play();
        }

        @Override
        public void onPageScrollStateChanged(int state) {

        }
    };



    View.OnClickListener clickListener = new View.OnClickListener() {
        @Override
        public void onClick(View view) {
            switch (view.getId()) {
                case R.id.btnRewind :
                    preview();
                    break;
                case R.id.btnPlay:
                    play();
                    break;
                case R.id.btnForwardF:
                    next();
                    break;
            }
        }
    };

    private void play() {
        switch(playStatus) {
            case STOP :
                audio.start();
                btnPlay.setImageResource(android.R.drawable.ic_media_pause);
                playStatus=PLAY;

                OneSec one = new OneSec();
                one.start();

                break;
            case PLAY :
                audio.pause();
                playStatus = PAUSE;
                btnPlay.setImageResource(android.R.drawable.ic_media_play);
                break;
            case PAUSE :
                audio.start();
                playStatus = PLAY;
                btnPlay.setImageResource(android.R.drawable.ic_media_pause);
                break;
        }
    }

    private void preview() {
        if(position>0)position -= 1;
        vp.setCurrentItem(position);
    }

    private void next() {
        if(position<music.size())position += 1;
        vp.setCurrentItem(position);
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        if(audio!=null) {
            audio.release();
        }
        playStatus = STOP;
    }

    private void init() {
        if(audio!=null) {
            audio.release(); // 뷰페이저로 이동할 경우 미디어 해제하고 실행한다
        }
        Uri uri = music.get(position).uri;
        audio = MediaPlayer.create(this, uri);
        sbar.setMax(audio.getDuration());
        duration.setText(convertTime(audio.getDuration()));
        audio.setLooping(false);

        Log.w("status", String.valueOf(playStatus));
    }

    private String convertTime(long time) {

        return String.format("%02d", time / 1000 / 60) + ":" + String.format("%02d", (time / 1000 - ((int) time / 1000 / 60) * 60));
    }


}
```