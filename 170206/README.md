##프래그먼트
> 뷰 100개가 먹는 리소스 == 액티비티 1개가 먹는 리소스

### 기획 순서
1. activity_main에 FrameLayout을 배치한다
2. New -> Fragment -> Fragment(Blank)
3. activity_fragment를 커스터마이징한다
4. MainActivity에서 FragmentManager, FragmentTransaction을 선언하고 add, commit하여 FrameLayout에 Fragment를 붙인다

```
activity_main)
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.jspark.android.maps.MainActivity">
    <FrameLayout
        android:id="@+id/frame"
        android:layout_width="match_parent"
        android:layout_height="match_parent">
    </FrameLayout>
</RelativeLayout>
```
```
MainActivity)
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        BlankFragment b = new BlankFragment();

        FragmentManager fm = getSupportFragmentManager();
        FragmentTransaction ft = fm.beginTransaction();

        ft.add(R.id.frame, b);
        ft.commit();
    }
}
```