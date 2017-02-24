## Thread
> 동시에 일을 진행할 때 만들어 쓴다

### 기획 순서
1. Thread를 상속받은 Class를 만든다
2. run을 Override한다
3. Logic을 구현한다

```
public Class extends Thread {
	@Override
	public void run() {
		// Logic 구현
	}
}
```

---

## Handler
> 서브 스레드의 메시지를 받아 메인 스레드에서 처리해 준다

###1. 단순 case를 나눈 Message
```
Handler h = new Handler() {
    @Override
    public void handleMessage(Message msg) {
        switch (msg.what) {
            case SET_TEXT :
            	switch 'msg에 담긴 int 값' :
            	// Logic 구현
            break;
        }
    }
};

public Class extends Thread {
	@Override
	public void run() {
		Message msg = new Message();
		msg.what = 'int 값'
		msg.sendEmptyMessage(msg);
	}
}
```
###2. 인자를 가진 Message
```
Handler h = new Handler() {
    @Override
    public void handleMessage(Message msg) {
        switch (msg.what) {
            case SET_TEXT :
            	switch 'msg에 담긴 int 값' :
            	// msg.arg1 이용한 Logic 구현
            break;
        }
    }
};

public Class extends Thread {
	@Override
	public void run() {
		Message msg = new Message();
		msg.what = 'int 값'
		msg.arg1 = '보내고자 하는 값'
		msg.sendMessage(msg);
	}
}
```

---

## AsyncTask
> 메인 스레드를 거치지 않고도 순차적으로 스레드 동작이 일어나도록 해주는 스레드

```
public class TestAsync extends AsyncTask<String, Integer, Boolean> {
	// AsyncTask의 파라미터
	// 1. doInBackground 의 파라미터
    // 2. onProgressUpdate 의 파라미터
    // 3. onPostExecute 의 파라미터
    
    // 최초 실행 시 init() 작업
	@Override
    protected void onPreExecute() {
        super.onPreExecute();
    }
    
    // 서브 스레드에서 실행
    @Override
    protected Boolean doInBackground(String... params) {
    
    }
    
    // doInBackgroudn 가 끝난 후 return 값을 받는 메소드
    @Override
    protected void onPostExecute(Boolean aBoolean) {
    
    }
    
    // 메인 스레드에서 실행
    @Override
    protected void onProgressUpdate(Integer... values) {
    
    }
}
```