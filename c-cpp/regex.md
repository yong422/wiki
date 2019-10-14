# regex

## Description

C++ 에서 정규표현식을 사용하기 위한 방법에 대한 문서

## regex

- C++ 에서 주로사용하는 정규표현식 라이브러리는 주로 boost::regex 를 사용.
- c++11 로 넘어오면서 std::regex 가 추가되었으며, GNU libstdc++ 기준으로 4.9.0 에서 릴리즈 되었다.
- 4.9.0 이하 버전에서 테스트성으로 regex 를 사용할 수 있게 되어있으나 릴리즈 버전 이전의 경우 버그가 많아 사용하기가    
용이하지 않다.


## boost regex

### cmake build

- cmake 를 빌드툴로 사용하는 경우 다음의 라인 추가가 필요하다.

  ```cmake
  # static library  사용여부 설정
  SET ( Boost_USE_STATIC_LIBS OFF ) 
  SET ( Boost_USE_MULTITHREADED ON )
  # boo
  FIND_PACKAGE ( Boost 1.53.0 COMPONENTS regex iostreams )
  # 참조 https://cmake.org/cmake/help/v3.0/module/FindBoost.html
  IF ( Boost_FOUND )
    INCLUDE_DIRECTORIES ( ${Boost_ICLUDE_DIRS} )
  ELSE ()
    MESSAGE ( FATAL_ERROR "not found boost")
  ENDIF ()

  # find_package 에서 components 로 추가한 라이브러리에 대해서만 링크한다.
  TARGET_LINK_LIBRARIES ( progname ${Boost_LIBRARIES} )
  ```

### sample code

- 개발기준은 centos 7 기준 boost-1.53.0

  ```cpp
  #include <boost/regex.hpp>
  bool IsMailValid(const std::string& mail) {
    try {
      boost::cmatch what;
      boost::regex pattern(R"regex((\w+)(\.|_)?(\w*)@(\w+)(\.(\w+))+)regex");
      return (!boost::regex_match(mail.c_str(), what, pattern)  ? false : true);
    } catch ( boost::regex_error& e) {
      return false;
    }
    return false;
  }
  ```

## std regex

### cmake build

- 별도의 링크나 FIND_PACKAGE 선행작업은 필요없음.

  ```cmake
  # 단 gcc 기준으로 c++11 을 지원해야 하며 gcc 버전 4.9.0 이상이어야 정상 동작 한다.
  CHECK_CXX_COMPILER_FLAG (-std=c++11 COMPILER_SUPPORT_CXX11 )
  IF ( COMPILER_SUPPORT_CXX11 )
    SET ( CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11" )
  ELSE ()
    MESSAGE ( FATAL_ERROR "The compiler ${CMAKE_CXX_COMPILER} has no C++11 support")
  ENDIF ()
  ```

### sample code

  - gcc 4.9.0 이상에서 정상 동작

  ```cpp
  #include <regex>
    bool IsMailValid(const std::string& mail) {
      try {
        const std::regex pattern(R"regex((\w+)(\.|_)?(\w*)@(\w+)(\.(\w+))+)regex");
        return (!std::regex_match(mail, pattern)  ? false : true);
      } catch ( std::regex_error& e) {
        std::cerr << e.code();
        return false;
      }
      return false;
    }
  ```