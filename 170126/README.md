##Intent

###명시적
- 클래스 이름을 호출, 값 전달

###암시적
- Action과 관련된 액티비티 실행

```
ACTION_DIAL
ACTION_SENDTO  
ACTION_VIEW
```

- 주요액션


---

## 액티비티 생명주기
새로 호출된 액티비티가 완전히 기존 액티비티를 가리면 onStop()까지 호출  
반투명이나 다이얼로그 등은 onPause()