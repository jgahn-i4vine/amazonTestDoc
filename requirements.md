# Requirements

### 

### CMake

CMake는 3.1 이상을 요구한다. Ubuntu의 apt로 cmake를 설치해도 3.5.1 버전이 설치되므로 그대로 사용해도 무방하지만, 여기에서는 직접 빌드 한다. 본 문서에 사용한 cmake 버전은 3.10.20171218 이다.

```
$ mkdir -p ~/workspaces && cd ~/workspaces
$ git clone https://gitlab.kitware.com/cmake/cmake.git
$ cd cmake
$ ./bootstrap
$ make
$ sudo make install
$ cmake --version
```

### 

### OpenSSL

OpenSSL은 1.0.2 이상을 요구한다. Ubuntu 16.04.3에 이미 1.0.2g 버전이 설치되어 그대로 사용해도 되지만, 여기서는 직접 빌드한다. 본 문서에 사용한 OpenSSL 버전은 1.1.1-dev 이다.

```
$ mkdir -p ~/workspaces && cd ~/workspaces
$ git clone https://github.com/openssl/openssl.git
$ cd openssl
$ ./config
$ make
$ make test
$ sudo make install
```



