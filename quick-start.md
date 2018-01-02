# Quick Start Guide

###

### 개요

 본 문서는 avs-device-sdk를 PC에서 가능한 패키지 설치를 통해 빨리 빌드하는 방법에 대해 기술한다. 이 문서의 작업 환경은 다음과 같다.
 * Intel Core i5-2500 CPU @ 3.3GHz × 4
 * 4GB RAM
 * 500GB HDD
 * Linux Mint 18.3 Cinnamon 64-bit
    * Kernel 4.10.0-42

### 

### 필요 유틸리티 설치
- [X] Git
    ```sh
    sudo apt isntall git
    ```
- [X] Toolchain
컴파일러는 C++11을 지원해야 한다. 아마존 [avs-device-sdk 문서](https://github.com/alexa/avs-device-sdk/wiki/Linux-Quick-Start-Guide)에서는 [GCC 4.8.5](https://gcc.gnu.org)나 [Clang 3.3](http://clang.llvm.org/get_started.html) 버전 이상을 요구한다. 또한 avs-device-sdk 빌드 시 [cmake 3.1](https://cmake.org/download/) 이상을 사용할 것을 요구하고 있다. Linux Mint 18.3에서는 2017년 12월 현재 아래 명령으로 gcc 5.4.0과 cmake 3.5.1을 설치할 수 있다.
    ```sh
    sudo apt install build-essential cmake
    ```
- [X] 문서화 도구
Doxygen 1.8.13을 설치해야 한다. [avs-device-sdk 문서](https://github.com/alexa/avs-device-sdk/wiki/Linux-Quick-Start-Guide)에는 명시되어 있지 않지만, dot tool 역시 설치해야 한다. 여기서는 dot tool로 graphviz를 설치한다. Linux Mint 18.3에서는 2017년 12월 현재 doxygen 1.8.11-1을 패키지로 제공한다.
    ```sh
    sudo apt install graphviz doxygen
    ```

### 필요 라이브러리 설치



