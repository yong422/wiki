OpenSSL library 사용
====================

# 라이브러리 초기화


# OpenSSL static lock

- openssl 을 사용하는 멀티스레드 프로그램인 경우 static lock 을 설치(등록)해야 한다.
- libcrypto 난수생성기에서 static lock 을 사용.
- openssl 초기화에 사용하는 함수들

  ```cpp
  SSL_library_init();
  OpenSSL_add_ssl_algorithms();
  OpenSSL_add_all_digests();
  SSL_load_error_strings();
  ERR_load_BIO_strings();
  ```

- 이상은 openssl static lock 사용을위한 콜백등록전 호출하여 초기화 해야 한다.
- [참조 url](https://wiki.openssl.org/index.php/Library_Initialization)