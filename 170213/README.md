## TabLayout과 ViewPager의 조합

### TabLayout
> Tab 형태를 지니고 현재 선택된 Tab의 하단에 밑줄을 만들어 알려주는 형태

![tablayout](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170213/imgs/tablayout.gif?raw=true)

```
acvitity_main)
<android.support.design.widget.TabLayout
    android:id="@+id/tab"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_centerHorizontal="true">

</android.support.design.widget.TabLayout>
```
```
MainActivity)
final int tabCount = 5;
TabLayout tabL;

tabL = (TabLayout)findViewById(R.id.tab);
tabL.addTab(tabL.newTab().setText("일반 계산기"));
tabL.addTab(tabL.newTab().setText("단위 변환기"));
tabL.addTab(tabL.newTab().setText("검색 엔진"));
tabL.addTab(tabL.newTab().setText("현재 위치"));
tabL.addTab(tabL.newTab().setText("갤러리"));
```

---

### TabLayout & ViewPager
> TabLayout과 ViewPager를 연동하여 유동적인 App을 구성한다

![tabNviewP](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170213/imgs/tabLayoutNviewPager.gif?raw=true)

```
activity_main)
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
```
```
MainActivity)
final int tabCount = 5;

OneFragment one;
TwoFragment two;
ThreeFragment three;
FourFragment four;
FiveFragment five;

FragmentManager fm;

TabLayout tabL;

ViewPager vp;

// 뒤로 가기 stack 관련 변수
private int mPosition=0;
public List<Integer> lastPosition = new ArrayList<>();

<onCreate()>
one = new OneFragment();
two = new TwoFragment();
three = new ThreeFragment();
four = new FourFragment();
// Custom Gallery Fragment 구현을 위한 생성자 제작 후 사용
if(five==null) five = FiveFragment.newInstance(3);

tabL = (TabLayout)findViewById(R.id.tab);
tabL.addTab(tabL.newTab().setText("일반 계산기"));
tabL.addTab(tabL.newTab().setText("단위 변환기"));
tabL.addTab(tabL.newTab().setText("검색 엔진"));
tabL.addTab(tabL.newTab().setText("현재 위치"));
tabL.addTab(tabL.newTab().setText("갤러리"));

vp = (ViewPager)findViewById(R.id.viewPager);

fm = getSupportFragmentManager();
CutomPagerAdapter adapter = new CutomPagerAdapter(fm);
vp.setAdapter(adapter);

lastPosition.add(0);

// ViewPager가 변할 때 TabLayout 변화시키는 리스너
vp.addOnPageChangeListener(new TabLayout.TabLayoutOnPageChangeListener(tabL));

vp.addOnPageChangeListener(new ViewPager.OnPageChangeListener() {
    @Override
    public void onPageScrolled(int position, float positionOffset, int positionOffsetPixels) {
    }
    @Override
    public void onPageSelected(int position) {
        mPosition = position;
        if((!lastPosition.isEmpty())
        	&&lastPosition.get(lastPosition.size()-1)!=mPosition) {
            lastPosition.add(mPosition);
        }
    }
    @Override
    public void onPageScrollStateChanged(int state) {

    }
});

// TabLayout이 변할 때 ViewPager 변화시키는 리스너
tabL.addOnTabSelectedListener(new TabLayout.ViewPagerOnTabSelectedListener(vp));

// Fragment들을 바로 받아 쓰기 위해 내부 Class를 선언
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
            case 4 :
                fragment = five;
                break;
        }
        return fragment;
    }

    @Override
    public int getCount() {
        return tabCount;
    }
}

@Override
public void onBackPressed() {
    //super.onBackPressed();
    if(lastPosition.size()==1) {
        super.onBackPressed();
    } else {
        switch (mPosition) {
            case 2:
                if (three.goBack()) {
                    three.goBack();
                } else {
                    goBackStack();
                }
                break;
            default:
                goBackStack();
                break;
        }
    }
}

private void goBackStack() {
    lastPosition.remove(lastPosition.size() - 1);
    vp.setCurrentItem(lastPosition.get(lastPosition.size() - 1));
}
```