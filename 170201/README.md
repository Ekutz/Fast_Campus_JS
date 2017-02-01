##Permission


##Runtime Permission - Api 23 이상
이전까지 Manifest에 선언만 해주던 방식에서 Runtime 중 권한을 부여할지 설정해주는 다이얼로그를 생성하여 확인받는 방식으로 변경되었다

### 사용 방법
1. Manifest에 사용할 권한에 대한 uses-permission을 등록한다


2. 현재의 안드로이드 버전이 마시멜로우 이상인지 확인한다


3. checkPermission 메소드를 만들어 허가받지 않은 경우 새로 허가를 받는다


4. onRequestPermissionsResult 메소드를 오버라이드해서 권한 수락한 경우와 거절한 경우의 동작을 나눈다


5. 권한을 수락한 경우의 동작 메소드를 만든다

---

###Content Resolver