# 보금자리
나만의 펜트하우스 : 보금자리

## 개요
보금자리는 거주지 정보 제공 및 사용자 맞춤 추천 서비스입니다.
대학생, 사회초년생 등 원룸, 오피스텔, 빌라 위주의 집을 구하려는 사람을 주 타겟으로 하며, 사용자가 등록한 집의 일조량, 공과금, 편의시설 정보 등의 제공을 통해 집 선택 단계에서 사용자가 효율적인 선택을 하도록 도와줍니다.

## 서비스 설치 및 실행
1. Android Studio가 설치되어 있어야 합니다.
2. Python이 설치되어 있어야 합니다.
3. https://github.com/Capstone-Penthouse/bogmjary.git에서 bogmjary 프로젝트를 clone합니다
4. 카카오 지도 API를 활용하기 위해 추가적인 설정이 필요합니다.
5. 편의시설 지도를 확인하기 위해서 안드로이드 기기의 연결이 필요합니다. 편의시설 부분을 제외하고는 에뮬레이터
상에서도 확인할 수 있습니다.
6. https://github.com/Capstone-Penthouse/calculate.git에서 calculate 프로젝트를 clone합니다
7. Python 서버를 활용하기 위해 추가적인 설정이 필요합니다 

## penthouse_bogmjary
1.Project clone
 git clone https://github.com/Capstone-Penthouse/bogmjary.git
2.Kakao Developers에 로그인 한 후, 내 애플리케이션 - 애플리케이션 추가하기를 통해 앱을 등록해줍니다.
3.내 애플리케이션 > 앱 설정 > 플랫폼에서 앱의 패키지 명을 등록합니다. 
4. 패키지 명을 입력하는 플랫폼 창의 아래에, 키 해시를 입력합니다.
  이때, 키 해시를 받는 방법은 다음과 같습니다.
  1. 먼저 openssl을 다운받아줍니다.
  2. 이후 openssl 폴더 내 bin 폴더가 있는 경로를 환경 변수에 등록해줍니다.
  3. cmd 창을 열어 openssl이 있는 곳으로 cd 명령어를 통해 이동한 후, 다음을 입력해줍니다.
    keytool -exportcert -alias androiddebugkey -keystore %HOMEPATH%/.android/
    debug.keystore | openssl sha1 -binary | openssl base64
  4. 이후 비밀번호를 입력하라고 나오는데, android를 입력해주면 키 해시가 발급됩니다.
5. 내 애플리케이션 > 앱 설정 > 앱 키에서 네이티브 앱 키와 REST API 키를 복사합니다..
6. 안드로이드 스튜디오에서 프로젝트를 연 후, 상단의 AndroidManifest.xml의 아래에 다음과 같은 내용이 있습니다.
  - android:value=“(발급받은 네이티브 앱 키)”를 붙여넣기 합니다.
7. values > strings.xml로 가서, 맨 위의 부분에 두 가지 키를 붙여넣기 해줍니다.
  - daummap_key에는 네이티브 앱 키를, restapi_key에는 발급받은 REST API 앱 키를 넣어줍니다
8. 왼쪽 상단에서 Android를 Project로 바꿔준 후, google-services.json에서 다음과 같이 바꿔줍니다.
  -oauth_clien의 certificate_hash에 cmd 창에서 발급받은 키 해시 값을 붙여넣기 합니다.


## calculate 서버
1.프로젝트 clone
  git clone https://github.com/Capstone-Penthouse/calculate.git
  cd Calculate
2.가상환경 설치 및 활성화
  pip install virtualenv
  virtualenv venv -python=python3.8(본인의 python version)
  venv\Scripts\activate
3.모듈 설치
  pip install pandas
4.Host ip 변경
  - calculate\server_elec.py, server_gas.py 에서 host=‘’ 부분 본인의 ip로 설정
  - penthouse_bogmjary\app\src\main\java\com\penthouse_bogmjary\FeeActivity.java에서
  private String ip= “”; 부분 본인의 ip로 설정
5.calculate\server_elec.py, server_gas.py 실행
