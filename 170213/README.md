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
> TabLayout과 ViewPager를 연도하여