## Camera
> Intent를 이용하여 Camera 촬영 기능을 사용한다

### Nougat 이전
```
Intent i = new Intent(MediaStore.ACTION_IMAGE_CAPTURE);
startActivityForResult(i, REQ_CAMERA);
```
- onActivityResult 단에서 ImageView src를 변경해주는 로직을 구현하면 완료

### Nougat 이후
```
Uri fileUri = null;

Intent i = new Intent(MediaStore.ACTION_IMAGE_CAPTURE);

if ( Build.VERSION.SDK_INT >= Build.VERSION_CODES.N ) {
    // 저장할 미디어 속성을 정의하는 클래스
    ContentValues values = new ContentValues(1);
    // 속성중에 파일의 종류를 정의
    values.put(MediaStore.Images.Media.MIME_TYPE, "image/jpg");
    // 전역변수로 정의한 fileUri에 외부저장소 컨텐츠가 있는 Uri 를 임시로 생성해서 넣어준다.
    fileUri = getContentResolver().insert(MediaStore.Images.Media.EXTERNAL_CONTENT_URI, values);
    // 위에서 생성한 fileUri를 사진저장공간으로 사용하겠다고 설정
    intent.putExtra(MediaStore.EXTRA_OUTPUT, fileUri);
    // Uri에 읽기와 쓰기 권한을 시스템에 요청
    intent.addFlags(Intent.FLAG_GRANT_READ_URI_PERMISSION 
    			  | Intent.FLAG_GRANT_WRITE_URI_PERMISSION);
}

startActivityForResult(i, REQ_CAMERA);
```
- 안드로이드 누가 버젼 이후로 보안 강화로 인해 임시 Uri을 통해 이미지의 Uri를 받아서 사용해야 한다