라이브러리 빌드
==============

# MySQL

## 버전 참조

  > 현재 MySQL version 은 8 로 넘어간 상태.   
  > client 의 기능은 크게 바뀐게 없으므로 클라이언트 사용시 5 점대 사용   
  > MySQL 5.7 이상부터는 boost 를 사용하는데 boost 포함한 컴파일을 위해서는 CMake 에서 gcc version 을 4.4 이상을 요구한다.   
  > CenOS5 의 기본 gcc version 4.1 대 이므로 CentOS5 에서 사용하려면 MySQL 5.6 사용.   
  > 클라이언트의 기능은 크게 변화가 없어서 호환 가능.   

- https://cdn.mysql.com//Downloads/MySQL-5.7/mysql-5.7.22.tar.gz
- https://cdn.mysql.com//Downloads/MySQL-5.6/mysql-5.6.40.tar.gz

## 빌드 

- [옵션 참고](https://dev.mysql.com/doc/refman/5.6/en/source-configuration-options.html)

- -DDEFAULT_CHARSET=utf8

  > 주로 사용하는 캐릭터셋을 설정   
  > 기본값은 latin1
  > 설정가능한 캐릭터셋은 아래 경로 참조.   
  > mysql-version/cmake/character_sets.cmake

- -DOWNLOAD_BOOST=1

  > 5.7 이상에서 boost 가 미포함된 패키지 인 경우 빌드전 boost 다운로드   

- -DWITH_BOOST=./boost

  > 5.7 이상에서 boost 를 참조할 경로.   
  > 이미 부스트가 설치된 경우 해당 경로를 참조하도록 설정.   

- -DWITH_EXTRA_CHARSETS=all

  > 모든종류의 캐릭터셋을 사용 가능하도록 설정

- -DDEFAULT_COLLATION=utf8_general_ci

  > 기본 collation 설정    
  > 기본값은 latin1_swedish_ci   

# libkrisp

## 참조

  > ip address 로 국가정보와 ISP정보를 검색하는 라이브러리   
  > kisa 에서 제공되는 데이터베이스를 사용하는 국내용과 geoip lite (무료버전 업데이트 늦음) 와 kisa 데이터베이스를 merge   
  > 한 국내, 해외용 데이터베이스를 제공  
  > 라이브러리 사용을 위해서는 libipcalc , sqlite3 필요.   
  > https://github.com/Joungkyun/libkrisp   

## 빌드

  > ./configure --prefix={설치경로} --with-ipcalc={libipcalc 설치경로}/bin/ipcalc-config --with-sqlite={sqlite3 설치경로}

## 주의사항

 - libkrisp configure 실행시 libipcalc 의 설치경로가 기본 경로 (/usr or /usr/local)가 아닌 경우 링크오류.   
 라이브러리파일의 경로를 path에 임시로 추가하여 실행이필요함.   

  > export LIBS='-L{sqlite3설치경로}/lib -L{libipcalc설치경로}/lib   

# libipcalc

## 참조

  > libkrisp 에서 참조하는 ipv4 calculating & subnetting 라이브러리   
  > https://github.com/Joungkyun/libipcalc   

## 빌드

  > ./configure --prefix={설치경로}


# sqlite3

- https://www.sqlite.org/index.html

## 참조

  > 별도의 서버 구축이 필요하지 않고, 응용 프로그램에 넣어 사용하기 편한 가벼운 데이터베이스   
  > 데이터를 저장하는데에 하나의 파일만 사용.

## 빌드

```sh
#sqlite3의 경우 github 에 없으므로 공식홈페이지에서 버전별로 다운로드   
wget https://www.sqlite.org/2018/sqlite-autoconf-3240000.tar.gz

#압축해제
tar xvfzp sqlite-autoconf-3240000.tar.gz

#make 파일 생성
./configure --prefix={설치경로}

#빌드
make;make install
```

# zlib

## 참조

- c 로 작성된 압축 라이브러리   
- 수많은 응용 프로그램에서 직간접적으로 압축을 위해 zlib 사용.   
- 코드가 포팅하기 쉽고 라이선스에서 자유로움.   
- 메모리를 얼마 사용하지 않아 수많은 임베디드 장치에서 쓰인다.   
- http://zlib.net/   
- https://github.com/madler/zlib

## 빌드

```sh
./configure --prefix={설치경로}

#공유라이브러리 빌드를 위한 옵션 추가
export CFLAGS=-fPIC

#빌드
make;make install
```

## windows 빌드

- contrib/vc10  으로 vs2010 에서 빌드 할 경우 ZLIB_WINAPI 전처리기가 정의되어있는 경우 몇몇 함수에서 링크에러 발생
- 해당 전처리기를 제거하고 빌드해야 정상적으로 라이브러리파일이 생성

# openssl

## 참조

- 네트워크를 통한 데이터 통신에 쓰이는 암호화 프로토콜인 TLS 와 SSL의 오픈소스 라이브러리.
- 기본적인 암호화 기능 및 여러 유틸리티 함수를 제공한다.   

## 빌드

```sh
./config --prefix={설치경로} shared zlib
```

# curl

## 참조

- 다양한 통신 프로토콜을 이용하여 데이터를 전송하기 위한 라이브러리와 명령 줄 도구를 제공하는 프로젝트.
- 라이브러리는 libcurl , 도구는 cURL   
- SSH 도 사용가능하나 빌드시 libssh2 가 필요하다   

## 빌드

```sh
export CFLAGS=-fPIC
./configure --prefix={설치경로} --with-ssl={openssl설치경로} --with-zlib={zlib 설치경로}
make;make install
```

## 주의사항

- pkg-config 가 설치되어있어야 curl에서 참조하는 openssl 의 pkgconfig 가 사용 가능   
- CentOS 는 기본적으로 설치 되어있으나 Ubuntu는 기본설치가 안되어 있을 수 있으므로 설치 필요   

