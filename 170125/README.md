##ConstraintLayout
>희소행렬 이론으로 만들어진 관계형 레이아웃  
>전체적으로는 RelativeLayout과 비슷하게 동작하지만 성능이 우월하다고 한다

###Handles
![handles](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170125/imgs/handles.png?raw=true)  
핸들을 통해 위젯의 크기와 정렬 기준을 지정할 수 있다.

###Resize
![resize](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170125/imgs/resize_handle.gif?raw=true)  
각 꼭지점에 있는 점을 사각형 점을 통해 위젯의 크기를 조절할 수 있다.

###Constraint
핸들의 축에 있는 원형 점을 통해 레이아웃, 다른 위젯과의 관계를 제한할 수 있다.
#####세로축
![vertical](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170125/imgs/constraint_handle_vertical.gif?raw=true)
#####가로축
![horizontal](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170125/imgs/constraint_handle_horizontal.gif?raw=true)
#####중앙축
![center](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170125/imgs/constraint_handle_center.gif?raw=true)

---

###layout_size
#####wrap_Content
![wrap_content](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170125/imgs/size_wrap_content.png?raw=true)
- 위젯 내부의 컨텐츠를 감쌀 만큼만 공간을 차지한다

#####fixed
![wrap_content](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170125/imgs/size_fixed.png?raw=true)
- 고정된 값으로 공간을 차지한다

#####any size
![wrap_content](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170125/imgs/size_any_size.png?raw=true)
- constraint를 만족시키는 선에서 최대한 공간을 차지한다

---

##OnCheckedChangeListener
> Compound.OnCheckedChangeListener

- 뷰의 상태가 boolean으로 표현 가능할 때 사용하는 리스너
	- ToggleButton
	- CheckBox
	- RadioButton

```
CompoundButton.OnCheckedChangeListener toggleListener = new CompoundButton.OnCheckedChangeListener() {
    @Override
    public void onCheckedChanged(CompoundButton compoundButton, boolean b) {
        Toast.makeText(WidgetActivity.this, "토글 상태 : "+b, Toast.LENGTH_SHORT).show();
    }
};
```
```
implements CompoundButton.OnCheckedChangeListener


checkBox1.setOnCheckedChangeListener(this);
checkBox2.setOnCheckedChangeListener(this);
checkBox3.setOnCheckedChangeListener(this);


@Override
public void onCheckedChanged(CompoundButton compoundButton, boolean b) {
    if(b==true) {
        String fruit = "";
        switch (compoundButton.getId()) {
            case R.id.cBox1:
                fruit = "Apple";
                break;
            case R.id.cBox2:
                fruit = "Banana";
                break;
            case R.id.cBox3:
                fruit = "Cherry";
                break;
        }
        Toast.makeText(WidgetActivity.this, "I Like " + fruit, Toast.LENGTH_SHORT).show();
    }
}


```
```
radioG.setOnCheckedChangeListener(new RadioGroup.OnCheckedChangeListener() {
    @Override
    public void onCheckedChanged(RadioGroup radioGroup, int id) {
        String name = "";
        switch(id) {
            case R.id.rdBtn1 :
                name = "Anaconda";
                break;
            case R.id.rdBtn2 :
                name = "Bear";
                break;
            case R.id.rdBtn3 :
                name = "Cat";
                break;
        }
        Toast.makeText(WidgetActivity.this, name+" 버튼 선택됨", Toast.LENGTH_SHORT).show();
    }
});
```
---

##Widgets
> 다양한 위젯과 그 사용 예를 알아보자

###ToggleButton
![toggleButton](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170125/imgs/toggleBtn.png?raw=true)  
버튼의 On/Off를 판단하고 보여주는 위젯

###CheckBox
![checkBox](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170125/imgs/checkBox.png?raw=true)  
체크 여부를 판단하고 보여주는 위젯

###RadioGroup
- 1개 세트의 라디오 버튼을 감싸는 컨테이너
#####RadioButton
![radioButton](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170125/imgs/radio.png?raw=true)  
다중택일이며 선택 여부를 판단하고 보여주는 위젯

###Spinner
![spinnner](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170125/imgs/spinner.png?raw=true)  
한 카테고리의 데이터 묶음을 고를 수 있도록 제공해 주는 위젯

```
ArrayAdapter<String> adapter = new ArrayAdapter<String>(this, android.R.layout.simple_spinner_dropdown_item, data); // Context, 스피너에서 쓸 레이아웃, 데이터
sp.setAdapter(adapter);
sp.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {
    @Override
    public void onItemSelected(AdapterView<?> adapterView, View view, int i, long l) {
        Toast.makeText(WidgetActivity.this, "선택된 년도 : "+ data.get(i), Toast.LENGTH_SHORT).show();
    }

    @Override
    public void onNothingSelected(AdapterView<?> adapterView) {

    }
});
```

###SeekBar
- 데이터 값을 0~100으로 조절할 수 있게 해주는 위젯

#####SeekBar
![seekBar](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170125/imgs/seekbar.png?raw=true) 

#####SeekBar(Discrete)
![seekBarD](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170125/imgs/seekbarD.png?raw=true) 

```
seekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() {
    @Override
    public void onProgressChanged(SeekBar seekBar, int i, boolean b) {
        seekBar_TextView.setText(i+"%");
    }
}
```

---

##setVisibility()
액티비티나 위젯의 보여지는 것과 존재의 여부를 조절하는 함수

###visible
공간을 차지하고 보여지는 방식 / 기본값이다  
![visibel](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170125/imgs/visible.png?raw=true) 

###invisible
공간은 차지하지만 보이지 않는 방식  
![invisible](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170125/imgs/invisible.png?raw=true) 

###gone
보이지도 않고 공간도 차지하지 않는 방식  
![gone](https://github.com/Ekutz/Fast_Campus_JS/blob/master/170125/imgs/gone.png?raw=true) 

---

사진 출처  
[커니의 안드로이드 이야기](http://kunny.github.io/)