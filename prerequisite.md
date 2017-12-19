# Prerequisite

### 

### 시간대 설정

AVS는 UTC 타임에 맞춰져 있어야 설정이 가능한다. Ubuntu에서는 다음으로 처리한다.

```
$ sudo timedatectl set-timezone Etc/UTC
```

### 

### 컴파일러

AVS Device SDK는 C++11 이후 문법을 사용한다. GCC의 경우 5.1 버전 이상이면 C++11, C++14의 대부분 문법을 지원하고 있다\(C++17은 GCC 7 이후 버전에서 지원\). 현재 기준으로 삼는 Ubuntu 16.04.3 에서는 gcc 5.4.0이 제공되므로 이를 그대로 사용한다. 참고로 avs-device-sdk 위키 페이지에서는 GCC 4.8.5 혹은 Clang 3.3을 권장한다.

### 

### Host 유틸리티 설치

처음 우분투를 설치한 경우 다음 유틸리티가 필요하다.

* Git

  ```
  $ sudo apt install git
  ```

* Python 라이브러리 - flask, requests

  ```
  $ sudo apt install python-pip
  $ pip install --upgrade pip
  $ pip install --user flask requests
  ```



