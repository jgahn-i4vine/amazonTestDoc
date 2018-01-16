# Quick Start Guide

### 개요

 본 문서는 avs-device-sdk를 PC에서 가능한 패키지 설치를 통해 빨리 빌드하는 방법에 대해 기술한다. 이 문서의 작업 환경은 다음과 같다.
 * Intel Core i5-2500 CPU @ 3.3GHz × 4
 * 4GB RAM
 * 500GB HDD
 * Linux Mint 18.3 Cinnamon 64-bit
    * Kernel 4.10.0-42


### Quickstart Instructions (avs-device-sdk only)
1. 모든 패키지 업데이트
    ```sh
    sudo apt udpate && sudo apt upgrade
    ```
1. 디렉토리 생성
    ```sh
    export WS=$PWD
    mkdir sdk-folder
    cd sdk-folder
    mkdir sdk-build sdk-source third-party application-necessities
    cd application-necessities
    ```
1. 툴체인 업데이트
    ```sh
    sudo apt-get install -y git gcc cmake openssl clang-format
    ```
1. APT로 설치할 수 있는 의존 패키지 설치
    ```sh
    sudo apt-get install -y openssl libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev gstreamer1.0-plugins-good libgstreamer-plugins-good1.0-dev libgstreamer-plugins-bad1.0-dev gstreamer1.0-libav pulseaudio doxygen libsqlite3-dev repo libasound2-dev
    ```
1. nghttp2 빌드
    - nghttp2 의존 패키지 설치
        ```sh
        sudo apt-get install -y g++ make binutils autoconf automake autotools-dev libtool pkg-config zlib1g-dev libcunit1-dev libssl-dev libxml2-dev libev-dev libevent-dev libjansson-dev libjemalloc-dev cython python3-dev python-setuptools  
        ```
    - nghttp2 빌드
        ```sh
        cd $WS/sdk-folder/third-party
        git clone https://github.com/tatsuhiro-t/nghttp2.git
        cd nghttp2
        autoreconf -i
        automake
        autoconf
        ./configure
        make -j4
        sudo make install
        ```
    - 최신 curl을 다운로드 하고 nghttp2와 openssl을 지원하도록 빌드
        ```sh
        cd $WS/sdk-folder/third-party
        wget http://curl.haxx.se/download/curl-7.54.0.tar.bz2
        tar -xvjf curl-7.54.0.tar.bz2
        cd curl-7.54.0
        ./buildconf
        ./configure --with-nghttp2=/usr/local --with-ssl
        make -j4
        sudo make install
        sudo ldconfig     
        ```
    - curl 테스트
        ```sh
        curl -I https://nghttp2.org/
        ```
        결과는 다음과 유사하면 된다.
        ```
        HTTP/2 200 
        date: Mon, 15 Jan 2018 08:25:55 GMT
        content-type: text/html
        last-modified: Tue, 19 Dec 2017 14:35:15 GMT
        etag: "5a3923a3-19d8"
        accept-ranges: bytes
        content-length: 6616
        x-backend-header-rtt: 0.002344
        strict-transport-security: max-age=31536000
        server: nghttpx
        via: 2 nghttpx
        x-frame-options: SAMEORIGIN
        x-xss-protection: 1; mode=block
        x-content-type-options: nosniff
        ```
1. PortAudio 설정 및 설치
    ```sh
    cd $WS/sdk-folder/third-party
    wget -c http://www.portaudio.com/archives/pa_stable_v190600_20161030.tgz
    tar zxf pa_stable_v190600_20161030.tgz
    cd portaudio
    ./configure --without-jack
    make -j4
    sudo make install
    sudo ldconfig
    ```
1. avs-device-sdk 다운로드
    ```sh
    cd $WS/sdk-folder/sdk-source
    git clone git://github.com/alexa/avs-device-sdk.git
    ```
1. 빌드
    아래의 빌드 스크립트는 다음 내용을 포함한다.
    - PortAudio의 헤더와 라이브러리 디렉토리 정의
    - 설치한 gstreamer에 대한 선언과 SampleApp 빌드 여부
    - wake word detector **OFF**
        - Linux도 Sensory와 Kitt.ai를 지원한다. 각각은 license가 필요하므로 일단 끄지만, 같이 빌드하려면 [Build Options](https://github.com/alexa/avs-device-sdk/wiki/Build-Options)를 참조한다.

    **주의**: 아래 명령은 모두 절대 경로로 바꾸어 쓸 것.
    ```sh
    cd $WS/sdk-folder/sdk-build
    cmake $WS/sdk-folder/sdk-source/avs-device-sdk -DSENSORY_KEY_WORD_DETECTOR=OFF -DGSTREAMER_MEDIA_PLAYER=ON -DPORTAUDIO=ON -DPORTAUDIO_LIB_PATH=$WS/sdk-folder/third-party/portaudio/lib/.libs/libportaudio.a -DPORTAUDIO_INCLUDE_DIR=$WS/sdk-folder/third-party/portaudio/include
    make -j4
    ```
1. Python 관련
    - PIP가 설치되어 있는지 확인
        ```sh
        pip --version
        ```
    - PIP가 설치되어 있지 않으면 설치
        ```sh
        sudo easy_install pip
        ```
    - flask, requests, commentjson을 설치
        ```sh
        pip install --user flask requests commentjson
        ```
1. 인증 설정
`$WS/sdk-folder/sdk-build/Integration/AlexaClientSDKConfig.json` 파일을 수정한다. 2가지 수정 사항이 있다.
    - **productId**, **clientId**, **clientSecret**을 Amazon Developer Console에서 참조해 변경한다.
    - 각 **databaseFilePath** 항목들과 **locale**을 아래를 참조해 수정한다. **deviceSerialNumber**는 임의의 유일한 값으로 채워 넣는다.
    ```json
    {
        "authDelegate":{
            "clientSecret":"<실제 clientSecret>",
            "deviceSerialNumber":"<임의의 유일한 값>",
            "refreshToken":"",
            "clientId":"<실제 clientId>",
            "productId":"<실제 productId>"
        },
    "alertsCapabilityAgent":{
            "databaseFilePath":"<$WS/sdk-folder/application-necessities/alerts.db의 절대 경로>"
    },
    "settings":{
            "databaseFilePath":"<$WS/sdk-folder/application-necessities/settings.db의 절대 경로>",
            "defaultAVSClientSettings":{
                "locale":"en-US"
            }
        },
    "certifiedSender":{ 
            "databaseFilePath":"<$WS/sdk-folder/application-necessities/certifiedSender.db의 절대 경로>"
        },
        "notifications":{ 
            "databaseFilePath":"<$WS/sdk-folder/application-necessities/notifications.db의 절대 경로>"
        },
        "sampleApp":{
            "displayCardsSupported":true
        }
    }
    ```
1. 인증 서버 실행
    ```sh
    cd $WS/sdk-folder/sdk-build
    python AuthServer/AuthServer.py
    ```
    그러면 인증시 필요한 웹 서버가 localhost에서 실행이 된다. `http://127.0.0.1:3000`에 접속해 아마존 개발자 계정으로 로그인하면 `AlexaClientSDKConfig.json` 파일에 **refreshToken** 항목이 채워진다. 완성된 `AlexaClientSDKConfig.json` 파일은 미리 백업해 둔다.
1. Integration과 unit test를 진행
    Integratino 과정 중에 `AlexaDirectiveSequencerLibraryTest.oneBlockingDirectiveInTheMiddle`가 fail이 나지만 동작 시 큰 상관은 없는 것 같다.
    ```sh
    cd $WS/sdk-folder/sdk-build
    TZ=UTC make all integration
    make all test
    ```
1. Sample App 실행
    ```sh
    cd $WS/sdk-folder/sdk-build/SampleApp/src
    TZ=UTC ./SampleApp $WS/sdk-folder/sdk-build/Integration/AlexaClientSDKConfig.json
    ```

### Kitt-AI 빌드
1. 디렉토리
    ```sh
    mkdir $WS/sdk-folder/wakeup-words
    ```
1. 소스코드 다운로드
    ```sh
    cd $WS/sdk-folder/wakeup-words
    git clone https://github.com/Kitt-AI/snowboy.git
    ```
1. 의존 패키지 설치
    Kitt-AI를 설치할 때 `swig-3.0.10` 이상을 요구한다. 패키지로 제공되는 swig의 버전은 3.0.8이므로 빌드 시 에러 메시지를 띄운다. Swig 최신 버전을 설치한다. Swig가 정상 동작하기 위해서는 지원 high level language에 대한 development package가 필요하다. 따라서 `python-dev` 패키지가 필요하다. 또한 Swig는 libboost, libatlas가 필요하므로 이를 함께 설치한다.
    - python-dev, libboost, libatlas
        ```sh
        sudo apt install python-dev libboost-all-dev libatlas-base-dev
        ```
    - Swig
        ```sh
        cd $WS/sdk-folder/wakeup-words
        git clone https://github.com/swig/swig.git
        cd swig
        ./autogen.sh
        ./configure
        make -j4
        make check-python-examples
        make check-python-test-suite
        sudo make install
        ```
1. 빌드
    ```sh
    cd $WS/sdk-folder/wakeup-words/snowboy
    python setup.py build
    python setup.py install --user
    ```

### Avs-device-sdk with Kitt-AI
1. 디렉토리
    ```sh
    mkdir $WS/sdk-folder/wakeup-words/avs-build
    cd $WS/sdk-folder/wakeup-words/avs-build
    ```
1. 툴체인
    Kitt-AI를 함께 빌드하기 위해서는 구버전의 gcc, g++이 필요하다.
    ```sh
    sudo apt install gcc-4.8 g++-4.8
    ```
    유닛 테스트 시 google test framework가 필요하다. 
    ```sh
    sudo apt install libgtest-dev google-mock
    ```
1. 빌드
    빌드 전 소스 디렉토리에 Kitt-AI 입력 파일들을 복사해 두어야 한다.
    ```sh
    mkdir $WS/sdk-folder/sdk-source/avs-device-sdk/KWD/inputs/KittAiModels $WS/sdk-folder/sdk-source/avs-device-sdk/Integration/inputs/KittAiModels
    cp $WS/sdk-folder/wakeup-words/snowboy/resources/common.res $WS/sdk-folder/sdk-source/avs-device-sdk/KWD/inputs/KittAiModels/
    cp $WS/sdk-folder/wakeup-words/snowboy/resources/common.res $WS/sdk-folder/sdk-source/avs-device-sdk/Integration/inputs/KittAiModels/
    cp $WS/sdk-folder/wakeup-words/snowboy/resources/alexa/alexa-avs-sample-app/alexa.umdl $WS/sdk-folder/sdk-source/avs-device-sdk/KWD/inputs/KittAiModels/
    cp $WS/sdk-folder/wakeup-words/snowboy/resources/alexa/alexa-avs-sample-app/alexa.umdl $WS/sdk-folder/sdk-source/avs-device-sdk/Integration/inputs/KittAiModels/
    ```
    **주의**: 아래 명령은 모두 절대 경로로 바꾸어 쓸 것.
    ```sh
    cd $WS/sdk-folder/wakeup-words/avs-build
    CC=gcc-4.8 CXX=g++-4.8 cmake $WS/sdk-folder/sdk-source/avs-device-sdk -DKITTAI_KEY_WORD_DETECTOR=ON -DKITTAI_KEY_WORD_DETECTOR_LIB_PATH=$WS/sdk-folder/wakeup-words/snowboy/lib/ubuntu64/libsnowboy-detect.a -DKITTAI_KEY_WORD_DETECTOR_INCLUDE_DIR=$WS/sdk-folder/wakeup-words/snowboy/include -DGSTREAMER_MEDIA_PLAYER=ON -DPORTAUDIO=ON -DPORTAUDIO_LIB_PATH=$WS/sdk-folder/third-party/portaudio/lib/.libs/libportaudio.a -DPORTAUDIO_INCLUDE_DIR=$WS/sdk-folder/third-party/portaudio/include -DCMAKE_BUILD_TYPE=DEBUG
    make -j4
    ```

1. 인증 설정
`$WS/sdk-folder/wakeup-words/avs-build/Integration/AlexaClientSDKConfig.json` 파일을 수정한다. 2가지 수정 사항이 있다.
    - **productId**, **clientId**, **clientSecret**을 Amazon Developer Console에서 참조해 변경한다.
    - 각 **databaseFilePath** 항목들과 **locale**을 아래를 참조해 수정한다. **deviceSerialNumber**는 임의의 유일한 값으로 채워 넣는다.
    ```json
    {
        "authDelegate":{
            "clientSecret":"<실제 clientSecret>",
            "deviceSerialNumber":"<임의의 유일한 값>",
            "refreshToken":"",
            "clientId":"<실제 clientId>",
            "productId":"<실제 productId>"
        },
    "alertsCapabilityAgent":{
            "databaseFilePath":"<$WS/sdk-folder/wakeup-words/db_dir/alerts.db의 절대 경로>"
    },
    "settings":{
            "databaseFilePath":"<$WS/sdk-folder/wakeup-words/db_dir/settings.db의 절대 경로>",
            "defaultAVSClientSettings":{
                "locale":"en-US"
            }
        },
    "certifiedSender":{ 
            "databaseFilePath":"<$WS/sdk-folder/wakeup-words/db_dir/certifiedSender.db의 절대 경로>"
        },
        "notifications":{ 
            "databaseFilePath":"<$WS/sdk-folder/wakeup-words/db_dir/notifications.db의 절대 경로>"
        },
        "sampleApp":{
            "displayCardsSupported":true
        }
    }
    ```
    데이터베이스 디렉토리를 생성해 둔다.
    ```sh
    mkdir $WS/sdk-folder/wakeup-words/db_dir
    ```
1. 인증 서버 실행
    ```sh
    cd $WS/sdk-folder/wakeup-words/avs-build
    python AuthServer/AuthServer.py
    ```
    그러면 인증시 필요한 웹 서버가 localhost에서 실행이 된다. `http://127.0.0.1:3000`에 접속해 아마존 개발자 계정으로 로그인하면 `AlexaClientSDKConfig.json` 파일에 **refreshToken** 항목이 채워진다. 완성된 `AlexaClientSDKConfig.json` 파일은 미리 백업해 둔다.
1. Integration과 unit test를 진행한다.
    역시나 AlexaDirectiveSequencerLibraryTest.oneBlockingDirectiveInTheMiddle 이놈이 뻑난다.
    ```sh
    cd $WS/sdk-folder/wakeup-words/avs-build
    TZ=UTC make all integration
    make all test
    ```
1. Sample App 실행
    ```sh
    cd $WS/sdk-folder/wakeup-words/avs-build/SampleApp/src
    TZ=UTC ./SampleApp $WS/sdk-folder/wakeup-words/avs-build/Integration/AlexaClientSDKConfig.json $WS/sdk-folder/sdk-source/avs-device-sdk/KWD/inputs/KittAiModels
    ```