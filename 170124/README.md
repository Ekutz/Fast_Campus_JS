##다른 액티비티 불러오기

```
public class MainActivity extends AppCompatActivity implements View.OnClickListener {
	// 위젯을 선언한다
    Button btn;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

		// 선언한 위젯을 id와 연동해준다
        btn = (Button)findViewById(R.id.btnClick);

        // 위젯에 onClickListener를 달아준다
        btn.setOnClickListener(this);
    }


    @Override
    public void onClick(View view) {

    	// view 의 id를 기준으로 경우의 수를 나눈다
        switch (view.getId()) {

        	// id가 btnClick일 때
            case R.id.btnClick :

            	// MainActivity 에서 SecondActivity 컴포넌트를 소환하는 Intent 선언
                Intent i = new Intent(MainActivity.this, SecondActivity.class);
                
                // Intent 시작
                startActivity(i);
        }
    }
}
```

##그리드 레이아웃
> Grid 좌표 값을 지정할 수 있는 레이아웃

- 레이아웃 속성
	- rowCount : row 최대값 고정
	- columnCount : column 최대값 고정
- 자식 속성
	- layout_row : row 좌표값 고정
	- layout_rowSpan : row 방향 차지하는 칸 수 지정
	- layout_rowWeight : row 방향으로 자식 채우기
	- layout_column : column 좌표값 고정
	- layout_columnspan : column 방향 차지하는 칸 수 지정
	- layout_columnWeight : column 방향으로 자식 채우기

###Mission <-GridLayout 연습->
![grid](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170124/imgs/grid.png?raw=true)

```
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_grid"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="com.jspark.android.widgets.GridActivity">

    <GridLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:columnCount="3"
        android:layout_alignParentTop="true"
        android:layout_alignParentLeft="true"
        android:layout_alignParentStart="true">
        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Button"
            android:layout_columnSpan="2"
            android:layout_columnWeight="1"/>
        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Button"
            android:layout_rowSpan="2"
            android:layout_rowWeight="1"/>
        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Button"/>
        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Button"
            android:layout_rowSpan="2"
            android:layout_rowWeight="1"/>
        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Button"
            android:layout_columnSpan="2"
            android:layout_columnWeight="1"/>
        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Button"
            android:visibility="invisible"/>
        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Button"

            android:layout_rowSpan="2"
            android:layout_rowWeight="1"
            android:layout_columnSpan="2"
            android:layout_columnWeight="1"/>
        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Button"/>
        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Button"/>
        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Button"/>
        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Button"/>
    </GridLayout>

</RelativeLayout>
```

