## Google Map
> Google Map을 Fragment에서 구현한다

### 기획 순서
1. manifest 에 ACCESS_FINE_LOCATION, ACCESS_COARSE_LOCATION 등록
2. 런타임 퍼미션 획득
3. GPS 위치 매니저 정의
4. GPS on/off 확인
5. 리스너 실행
6. 리스너 해제

```
Manifest)
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
```
```
MainActivity)
private LocationManager lM;
final int REQ_CODE = 100;

// 안드로이드 버전에 따라 호출되는 메소드
@TargetApi(Build.VERSION_CODES.M)
public void checkPermission() {
    if(checkSelfPermission(Manifest.permission.ACCESS_FINE_LOCATION) 
    != PackageManager.PERMISSION_GRANTED 
    || checkSelfPermission(Manifest.permission.ACCESS_COARSE_LOCATION) 
    != PackageManager.PERMISSION_GRANTED) {
        String permArr[] = {android.Manifest.permission.ACCESS_FINE_LOCATION, 
        					android.Manifest.permission.ACCESS_COARSE_LOCATION};
        // 새로운 권한 획득을 위한 다이얼로그 요청 메소드
        requestPermissions(permArr, REQ_CODE);
    } else {
        init();
    }
}
@Override
public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
    super.onRequestPermissionsResult(requestCode, permissions, grantResults);
    if(requestCode==REQ_CODE) {
        // 권한을 수락한 경우
        if(grantResults[0]==PackageManager.PERMISSION_GRANTED &&
                grantResults[1]==PackageManager.PERMISSION_GRANTED) {
            init();
        } else { //권한을 수락하지 않은 경우
            Toast.makeText(MainActivity.this, "어플 재시작 후 권한 설정에 동의해 주세요", Toast.LENGTH_SHORT).show();
            finish();
        }
    }
}

private void init() {
    lM = (LocationManager)getSystemService(Context.LOCATION_SERVICE);
    
    // GPS on/off 확인
    if(!gpsCheck()) {
        makeAlertDialog();
    }
}

private void makeAlertDialog() {
    AlertDialog.Builder ad = new AlertDialog.Builder(MainActivity.this);
    ad.setTitle("GPS 설정");
    ad.setMessage("GPS 설정창으로 이동하시겠습니까?");
    ad.setPositiveButton("Yes", new DialogInterface.OnClickListener() {
        @Override
        public void onClick(DialogInterface dialogInterface, int i) {
            Intent intent = new Intent(Settings.ACTION_LOCATION_SOURCE_SETTINGS);
            startActivity(intent);
        }
    });
    ad.setNegativeButton("No", new DialogInterface.OnClickListener() {
        @Override
        public void onClick(DialogInterface dialogInterface, int i) {
            Toast.makeText(MainActivity.this, "GPS 기능을 사용하실 수 없습니다", Toast.LENGTH_SHORT).show();
        }
    });
    ad.show();
}

private boolean gpsCheck() {
    if(Build.VERSION.SDK_INT >= Build.VERSION_CODES.LOLLIPOP) {
        return lM.isProviderEnabled(LocationManager.GPS_PROVIDER);
    } else {
        String gpsEnable = android.provider.Settings.Secure.getString(getContentResolver(), Settings.Secure.LOCATION_PROVIDERS_ALLOWED);
        if(gpsEnable.matches(".*gps.*")) {
            return true;
        } else {
            return false;
        }
    }
}

public LocationManager getLocationManager() {
    return lM;
}
```
```
activity_map)
<fragment
        android:id="@+id/mapView"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:name="com.google.android.gms.maps.SupportMapFragment" />
```
```
MapFragment)
private GoogleMap mMap;
private SupportMapFragment sMF;
MainActivity main;
LocationManager manager;

public FourFragment() {
    // Required empty public constructor
}

@Override
public void onAttach(Context context) {
    super.onAttach(context);
    main = (MainActivity) context;
    manager = main.getLocationManager();
}

@Override
public void onResume() {
    super.onResume();
    
    // 리스너 등록
    if(Build.VERSION.SDK_INT>=Build.VERSION_CODES.M) {
        if (ActivityCompat.checkSelfPermission(getContext(),
         android.Manifest.permission.ACCESS_FINE_LOCATION) 
        != PackageManager.PERMISSION_GRANTED 
        && ActivityCompat.checkSelfPermission(getContext(),
         android.Manifest.permission.ACCESS_COARSE_LOCATION) 
        != PackageManager.PERMISSION_GRANTED) {
            return;
        }
    }
    manager.requestLocationUpdates(LocationManager.GPS_PROVIDER, // 등록할 위치 제공자
            3000, // 업데이트 간격
            1, // 측정 변경 거리
            listener);
    manager.requestLocationUpdates(LocationManager.NETWORK_PROVIDER, // 등록할 위치 제공자
            3000,
            10,
            listener);
}

@Override
public View onCreateView(LayoutInflater inflater, ViewGroup container,
                         Bundle savedInstanceState) {
    View view = inflater.inflate(R.layout.fragment_four, container, false);

    sMF = (SupportMapFragment) getChildFragmentManager().findFragmentById(R.id.mapView);
    sMF.getMapAsync(this);
    return view;
}

@Override
public void onPause() {
    super.onPause();
    if(Build.VERSION.SDK_INT>=Build.VERSION_CODES.M) {
        if (ActivityCompat.checkSelfPermission(getContext(),
         android.Manifest.permission.ACCESS_FINE_LOCATION) 
         != PackageManager.PERMISSION_GRANTED 
         && ActivityCompat.checkSelfPermission(getContext(),
          android.Manifest.permission.ACCESS_COARSE_LOCATION) 
          != PackageManager.PERMISSION_GRANTED) {
            return;
        }
    }
    // 리스너 해제
    manager.removeUpdates(listener);
}

@Override
public void onMapReady(GoogleMap googleMap) {
    mMap = googleMap;
}

LocationListener listener = new LocationListener() {
    @Override
    public void onLocationChanged(Location location) {
        double longitude = location.getLongitude();
        double latitude = location.getLatitude();
        double altitude = location.getAltitude();
        float accuracy = location.getAccuracy();
        String provider = location.getProvider();

        LatLng myPosition = new LatLng(latitude, longitude);
        Log.d("위도", String.valueOf(longitude));
        Log.d("경도", String.valueOf(latitude));
        mMap.addMarker(new MarkerOptions().position(myPosition).title("Marker in my position"));
        mMap.moveCamera(CameraUpdateFactory.newLatLngZoom(myPosition, 18));
    }

    @Override //provider 상태 변경 시 호출
    public void onStatusChanged(String s, int i, Bundle bundle) {

    }

    @Override //GPS 사용이 갑자기 가능해 질 때
    public void onProviderEnabled(String s) {

    }

    @Override //GPS 안될 때
    public void onProviderDisabled(String s) {

    }
};
```