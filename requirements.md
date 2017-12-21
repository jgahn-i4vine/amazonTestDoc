# Requirements

### 

### Google Test

```
$ cd $WS
$ git clone https://github.com/google/googletest.git
$ mkdir googletest/build && cd googletest/build
$ cmake -Dgtest_build_samples=ON -Dgtest_build_tests=ON ..
$ make
$ make test
$ sudo make install
```

### CMake

CMake는 3.1 이상을 요구한다. Ubuntu의 apt로 cmake를 설치해도 3.5.1 버전이 설치되므로 그대로 사용해도 무방하지만, 여기에서는 직접 빌드 한다. 본 문서에 사용한 cmake 버전은 3.10.20171218 이다.

```
$ cd $WS
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
$ cd $WS
$ git clone https://github.com/openssl/openssl.git
$ cd openssl
$ ./config
$ make
$ make test
$ sudo make install
$ sudo ldconfig
$ openssl version
```

### 

### SQLite

SQLite는 3.19.3 이상을 요구한다. 본 문서에 사용한 SQLite 버전은 3.21.0 이다.

```
$ cd $WS
$ wget https://www.sqlite.org/2017/sqlite-autoconf-3210000.tar.gz
$ tar xvf SQLite-autoconf-3210000.tar.gz
$ cd SQLite-autoconf-3210000
$ ./configure
$ make
$ sudo make install
$ sudo ldconfig
$ sqlite3 -version
```

### 

### nghttp2

nghttp2는 1.0 이상을 요구한다.

nghttp2의 추가 요구 사항은 다음과 같다.

> ##### cunit
>
> ```
> $ cd $WS
> $ wget https://downloads.sourceforge.net/project/cunit/CUnit/2.1-3/CUnit-2.1-3.tar.bz2
> $ tar xvf CUnit-2.1-3.tar.bz2
> $ cd CUnit-2.1-3
> $ ./bootstrap
> $ ./configure
> $ make
> $ sudo make install
> ```
>
> ##### libev
>
> ```
> $ cd $WS
> $ git clone https://github.com/enki/libev.git
> $ cd libev
> $ ./configure
> $ make
> $ sudo make install
> $ sudo ldconfig
> ```
>
> ##### zlib
>
> ```
> $ cd $WS
> $ wget https://downloads.sourceforge.net/project/libpng/zlib/1.2.11/zlib-1.2.11.tar.gz
> $ tar xvf zlib-1.2.11.tar.gz
> $ cd zlib-1.2.11
> $ ./configure
> $ make
> $ sudo make install
> $ sudo ldconfig
> ```
>
> ##### libc-ares
>
> ```
> $ cd $WS
> $ git clone https://github.com/c-ares/c-ares.git
> $ cd c-ares
> $ ./buildconf
> $ ./configure
> $ make
> $ make ahost adig acountry
> $ sudo make install
> $ sudo ldconfig
> ```
>
> ##### libxml2
>
> ```
> $ cd $WS
> $ git clone git://git.gnome.org/libxml2
> $ cd libxml2
> $ ./autogen.sh
> $ make
> $ sudo make install
> $ sudo ldconfig
> ```
>
> ##### jansson
>
> ```
> $ cd $WS
> $ git clone https://github.com/akheron/jansson
> $ cd jansson
> $ autoreconf -i
> $ ./configure
> $ make
> $ sudo make install
> $ sudo ldconfig
> ```
>
> ##### libevent
>
> ```
> $ cd $WS
> $ git clone https://github.com/libevent/libevent.git
> $ mkdir libevent/build && cd libevent/build
> $ cmake ..
> $ make
> $ sudo make install
> $ sudo ldconfig
> ```
>
> ##### jemalloc
>
> ```
> $ cd $WS
> $ git clone https://github.com/jemalloc/jemalloc.git
> $ cd jemalloc
> $ ./autogen.sh
> $ make
> $ sudo make install_bin install_include install_lib
> $ sudo ldconfig
> ```
>
> ##### libboost
>
> ```
> $ cd $WS
> $ git clone --recursive https://github.com/boostorg/boost.git
> $ cd boost
> $ ./bootstrap.sh
> $ ./b2
> $ sudo ./b2 install
> $ sudo ldconfig
> ```

##### 

```
$ cd $WS
$ git clone https://github.com/nghttp2/nghttp2.git
$ cd nghttp2
```

### 

### libcurl

### 

### GStreamer

##### Base Plugins

##### Good Plugins

##### Libav Plugin

##### Ugly Plugins

##### Bad Plugins

### 

### PortAudio

### 

### Libgcrypt

### 

### libsoup

### 

### libfaad-dev

### 

### 



