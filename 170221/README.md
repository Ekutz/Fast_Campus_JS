## Custom Widget
> 기본 위젯을 상속받은 Class를 이용하여 자신만의 Custom Widget을 만들어 본다

### 기획 순서
1. 상속 받을 기본 Widget을 정하여 상속한 후 생성자를 로드한다
2. attrs xml 파일을 생성한다  
![attrs](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170221/imgs/attrs.png?raw=true)
3. attrs 에 새로운 속성을 만든다
![styleable](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170221/imgs/styleable.png?raw=true)
4. Custom Widget Class에서 새로운 속성을 받아서 이를 처리하는 Logic을 구현한다
5. activity.xml 에서 사용한다

---

### example
```
Custom Widget)
CostomWidget(Context context, AttributeSet attrs) {
	TypedArray typedArray = context.obtainStyledAttributes(attrs, R.styleable.Today);
	int size = typedArray.getIndexCount();
	for(int i=0;i<size;i++) {
	    int current_attr = typedArray.getIndex(i);
	    switch (current_attr) {
	        case R.styleable.Today_delimeter :
	            String delimeter = typedArray.getString(current_attr);
	            setDate(delimeter);
	            break;
	    }
	}
}

setDate(String delimeter) {
	Calendar cal = Calendar.getInstance();
    Date today = cal.getTime();
    SimpleDateFormat sdf = new SimpleDateFormat("yyyy"+delimeter+"MM"+delimeter+"dd");
    setText(sdf.format(today));
}
```

---

## CustomView
> View 자체를 상속받은 Class를 만들어서 FrameLayout에 씌운다

### 기획 순서
1. View를 상속받은 새로운 Class를 만든다
2. 생성자를 만든다
3. onDraw를 Override한다
4. Paint를 정의하고 onDraw에서 canvas로 그려낸다

```
class CustomView extends View {
	
	Paint black = new Paint();
	
    public CustomView(Context context) {
        super(context);
        black.setColor(Color.parseColor("#FFFFFFFF");    
    }
   
    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);
        
        canvas.drawRect(0,0,deviceWidth,deviceWidth,outline);
	
		Paint magenta = new Paint();
		magenta.setColor(Color.MAGENTA);
		canvas.drawCircle(100, 100, 50, magenta);
	}
}
```

### Tip
Bitmap 으로 패턴 draw 하기

```
// Bitmap 변수 선언
Bitmap block;

// BitmapFactory로 이미지 변환
block = BitmapFactory.decodeResource(getResources(), R.drawable.block);

// 형태와 위치 잡기
Rect r = new Rect(unit*j, unit*i, unit*(j+1), unit*(i+1));

// Bitmap 그리기
canvas.drawBitmap(block, null, r, null);
```