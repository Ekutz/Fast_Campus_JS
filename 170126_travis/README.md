##Constraint Layout의 License를 포함한 .travis.yml

```
language : android

jdk : oraclejdk8

android :
  components :
  - platform-tools #ADB (디바이스 또는 에뮬레이터 통신)
  - tools # 실제 안드로이드 SDK
  - build-tools-25.0.1 # 빌드 툴 버전
  - android-25
  - extra-android-m2repository

before_install :
  - chmod +x gradlew
  - mkdir "$ANDROID_HOME/licenses" || true
  - echo -e "\n8933bad161af4178b1185d1a37fbf41ea5269c55" > "$ANDROID_HOME/licenses/android-sdk-license"
  - echo -e "\n84831b9409646a918e30573bab4c9c91346d8abd" > "$ANDROID_HOME/licenses/android-sdk-preview-license"

script : ./gradlew build
```

- before_install 에서 라이센스를 복사해서 넣어주는 방식으로 라이센스를 취득한다