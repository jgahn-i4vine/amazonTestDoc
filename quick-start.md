# Quick Start Guide

### 개요

 본 문서는 avs-device-sdk를 PC에서 가능한 패키지 설치를 통해 빨리 빌드하는 방법에 대해 기술한다. 이 문서의 작업 환경은 다음과 같다.
 * Intel Core i5-2500 CPU @ 3.3GHz × 4
 * 4GB RAM
 * 500GB HDD
 * Linux Mint 18.3 Cinnamon 64-bit
    * Kernel 4.10.0-42

### 사전 작업
- Git 설치
    ```sh
    sudo apt install git
    ```

### 의존성
#### 핵심 의존성
[avs-device-sdk Linux Quick Start Guide](https://github.com/alexa/avs-device-sdk/wiki/Linux-Quick-Start-Guide)에는 핵심 의존 패키지를 다음과 같이 나열하고 있다.
- C++11 or later
- [GNU Compiler Collection (GCC) 4.8.5](https://gcc.gnu.org/) or later **OR** [Clang 3.3](http://clang.llvm.org/get_started.html) or later
- [CMake 3.1](https://cmake.org/download/) or later
- [libcurl 7.50.2](https://curl.haxx.se/download.html) or later
- [nghttp2 1.0](https://github.com/nghttp2/nghttp2) or later
- [OpenSSL 1.0.2](https://www.openssl.org/source/) or later
- [Doxygen 1.8.13](http://www.stack.nl/%7Edimitri/doxygen/download.html) or later (required to build API documentation)
- [SQLite 3.19.3](https://www.sqlite.org/download.html) or later (required for Alerts)
- For Alerts to work as expected:
    - The device system clock must be set to UTC time. We recommended using `NTP` to do this
    - A file system is required

Linux Mint 18.3에서 2018년 1월 현재 `apt`로 설치할 수 있는 위 패키지들의 버전은 다음과 같다.
- [X] C++11 or later
- [X] GNU Compiler Collection (GCC) 5.4.0 **OR** Clang 3.8.0
- [X] CMake 3.5.1
- [ ] libcurl 7.47.0
- [X] nghttp2 1.7.1-1
- [X] OpenSSL 1.0.2g
- [ ] Doxygen 1.8.11-1
- [ ] SQLite 3.11.0

이들 중 버전이 맞는 것은 gcc, clang, nghttp2, openssl 뿐이다. 이들을 설치한다.
```sh
sudo apt isntall build-essential cmake nghttp2 openssl
```

### MediaPlayer 참조 의존성
미디어 관련 의존성은 다음과 같다.
- GStreamer 1.10.4 (or later)
    **IMPORTANT NOTE FOR LINUX**: GStreamer 1.8 **does not** work.
- GStreamer Base Plugins 1.10.4 or later
- GStreamer Good Plugins 1.10.4 or later
- GStreamer Libav Plugins 1.10.4 or later **OR** GStreamer Ugly Plugins 1.10.4 or later, for decoding MP3 data.

안타깝게도 Linux Mint 18.3에 2018년 1월 현재 자동으로 설치되어 있는 gstreamer의 버전은 1.8.3이다. 따라서 삭제 후 새로 설치해야 한다.
```sh
sudo apt remove gstreamer1.0-x gstreamer1.0-alsa gstreamer1.0-clutter gstreamer1.0-nice gstreamer1.0-plugins-base gstreamer1.0-plugins-base-apps gstreamer1.0-plugins-good gstreamer1.0-pulseaudio gstreamer1.0-tools libgstreamer1.0-0 libgstreamer1.0-0-dbg
sudo apt autoremove
```
### 필요 유틸리티 설치
- [X] 문서화 도구
Doxygen 1.8.13을 설치해야 한다. [avs-device-sdk 문서](https://github.com/alexa/avs-device-sdk/wiki/Linux-Quick-Start-Guide)에는 명시되어 있지 않지만, dot tool 역시 설치해야 한다. 여기서는 dot tool로 graphviz를 설치한다. Linux Mint 18.3에서는 2017년 12월 현재 doxygen 1.8.11-1을 패키지로 제공한다.
    ```sh
    sudo apt install graphviz doxygen
    ```

- [X] pip
    ```sh
    sudo apt install python-pip
    ```

### 필요 라이브러리 설치



