## Lambda
> 기존의 불필요한 코드를 줄이고 가독성을 향상시키는데 목적을 둔 표현식 <del>버카충, 갈비, 넌씨눈</del>

### 기본 사용법
```
( parameters ) -> expression body
( parameters ) -> { expression body }
() -> { expression body }
() -> expression body
```
```
ex)
btn.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        System.out.println("Clicked");
    }
});

==

btn.setOnClickListener((View v) -> {
	System.out.println("Clicked")
	});
	
==

btn.setOnClickListener((v) -> {
	System.out.println("Clicked")
	});
	
==

btn1.setOnClickListener((v)-> System.out.println("Clicked"));

==

btn.setOnClickListener(System.out::println);
```
> 왜 이러는지 진짜 도통 모르겠다

### 단일 메소드 interface를 통한 Lambda 사용
```
main() {
	LambdaFunction arg = calc();
	int result = arg.squareParameter(50, 20);
}

public LambdaFunction calc() {
    return (value, value2) -> value+value2;

    /* 위는 아래와 같음
    * 인터페이스 내의 유일한 메소드를 구현(num) {
    *   return num * num;
    * }
    * */
}

interface LambdaFunction {
    public abstract int squareParameter(int num, int num2);
}
```

### stream을 이용한 대용량 반복문 성능 향상
```
btn2.setOnClickListener((v)->{
    for(String str:arr) {
        if(str.length()==1) {
            try {
                Toast.makeText(MainActivity.this, "I am "+str, Toast.LENGTH_SHORT).show();
                sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
});

btn3.setOnClickListener((v) -> {
    Stream<String> stream = Arrays.stream(arr);
    stream.filter(a->a.length()==1).forEach(System.out::println);
});
```
> 위 두 버튼의 기능은 완전히 같다. 그러나 데이터의 양이 매우 많아지면 두 기능의 성능 차이는 확연하게 차이가 나게 된다.<del>고 한다.</del>