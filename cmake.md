CMake
=====

# Description

> cmake 를 사용하기 위한 간단 사용방식에 대한 설명   
> Centos7 기본빌드를 위하여 cmake 2.8 에서 지원 가능하도록 사용   


## 구조


## 상세 기능

### External

- 참조하는 외부프로젝트를 빌드하기 위한 방법   
- external 프로젝트가 cmake, autoconf  등으로 구성이 다른 경우 별도의 설정이 필요 할 수 있다. 

```cmake
# openssl external project 를 추가 할 경우.
# openssl autoconf 
# 프로젝트명, git repo, tag 순으로 기본 추가
# DEPENDS  는 openssl 이 참조하는 external project 가 있을 경우 추가가 필요하다.
# PREFIX, BINARY_DIR, SOURCE_DIR, INSTALL_DIR 를 설정
# PREFIX 만 설정하면 그에 맞게 binary, source, install dir 이 설정된다.
# source 는 소스가 설치된 디렉토리
# binary 는 빌드된 디렉토리
# install 은 설치된 디렉토리 (install 을 건너뛸 경우 없을 수 있음)

# CONFIGURE_COMMAND 은 configure 실행 커맨드이며 autoconf 로 된 프로젝트 빌드시에만 추가
# BUILD_COMMAND make 또한 cmake 가 아닌 경우 별도의 빌드 커맨드 추가가 필요할 경우 추가

ExternalProject_Add(
    project_openssl
    GIT_REPOSITORY https://github.com/openssl/openssl.git
    GIT_TAG OpenSSL_1_0_2p
    DEPENDS project_zlib
    PREFIX ${CMAKE_CURRENT_BINARY_DIR}/libtemp/openssl
    BINARY_DIR ${CMAKE_CURRENT_BINARY_DIR}/libtemp/openssl/src/openssl
    SOURCE_DIR ${CMAKE_CURRENT_BINARY_DIR}/libtemp/openssl/src/openssl
    INSTALL_DIR ${CMAKE_CURRENT_BINARY_DIR}/libtemp/openssl/build
    CONFIGURE_COMMAND ./config --prefix=<INSTALL_DIR> shared zlib
    BUILD_COMMAND make
  )



```