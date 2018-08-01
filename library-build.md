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

# 