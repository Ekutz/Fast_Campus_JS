##프래그먼트
> 뷰 100개가 먹는 리소스 == 액티비티 1개가 먹는 리소스


---

##프래그먼트와 뷰페이저의 연동

### 기획 순서
1. activity_main에 TabLayout과 Fragment를 배치한다
2. MainActivity에서 tabCount를 정해주고 각 Fragment들을 개체화 해준다
3. ViewPager에 Adapter extends FragmentStatePagerAdapter 를 세팅해준다
4. ViewPager와 TabLayout이 연동 되도록 각자 Listener를 세팅해준다

```
activity_main)
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.jspark.android.myutility.MainActivity">


    <android.support.design.widget.TabLayout
        android:id="@+id/tab"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_centerHorizontal="true">

    </android.support.design.widget.TabLayout>
    <android.support.v4.view.ViewPager
        android:id="@+id/viewPager"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_below="@id/tab">

    </android.support.v4.view.ViewPager>
</RelativeLayout>
```

```
public class MainActivity extends AppCompatActivity {

final int tabCount = 4;

OneFragment one;
TwoFragment two;
ThreeFragment three;
FourFragment four;

FragmentManager fm;

TabLayout tabL;

ViewPager vp;


@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    one = new OneFragment();
    two = new TwoFragment();
    three = new ThreeFragment();
    four = new FourFragment();

    fm = getSupportFragmentManager();

    tabL = (TabLayout)findViewById(R.id.tab);
    tabL.addTab(tabL.newTab().setText("일반 계산기"));
    tabL.addTab(tabL.newTab().setText("단위 변환기"));
    tabL.addTab(tabL.newTab().setText("검색 엔진"));
    tabL.addTab(tabL.newTab().setText("현재 위치"));

    vp = (ViewPager)findViewById(R.id.viewPager);

    fm = getSupportFragmentManager();
    CutomPagerAdapter adapter = new CutomPagerAdapter(fm);
    vp.setAdapter(adapter);

    // ViewPager가 변할 때 TabLayout 변화시키는 리스너
    vp.addOnPageChangeListener(new TabLayout.TabLayoutOnPageChangeListener(tabL));

    // TabLayout이 변할 때 ViewPager 변화시키는 리스너
    tabL.addOnTabSelectedListener(new TabLayout.ViewPagerOnTabSelectedListener(vp));

}

class CutomPagerAdapter extends FragmentStatePagerAdapter {

    public CutomPagerAdapter(FragmentManager fm) {
        super(fm);
    }

    @Override
    public Fragment getItem(int position) {
        Fragment fragment = null;
        switch (position) {
            case 0 :
                fragment = one;
                break;
            case 1 :
                fragment = two;
                break;
            case 2 :
                fragment = three;
                break;
            case 3 :
                fragment = four;
                break;
        }
        return fragment;
    }

    @Override
    public int getCount() {
        return tabCount;
    }
}
```
- CustomAdapter를 내부 Class로 만든 이유는 각각의 Fragment를 매번 개체화 시켜서 뿌려주는 것보다 Class 내에서 바로 사용하는 것이 훨씬 효율적이기 때문이다

---

##구글 맵

### 기획 순서
1. activity_fragment에 fragment 를 넣는다
2. id를 할당하고 android:name = "com.google.android.gms.maps.SupportMapFragment"을 삽입한다
3. Fragment.java에 GoogleMap과 SupportMapFragment를 선언한다
4. New -> Google -> Google Map Activity 를 만든다
5. google_maps_api 에서 주소를 복사하여 KEY를 얻는다
6. Fragment에 OnMapReadyCallBack을 implements 시키고 MapsActivity의 onMapReady 함수를 가져와서 사용한다
7. MainActivity 에서 Fragment를 붙인다

```

```

---