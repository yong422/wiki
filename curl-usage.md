libcurl usage
=============

# Description

## Write callback function

```cpp
CURLcode curl_easy_setopt(CURL *handle, CURLOPT_WRITEFUNCTION, write_callback);

static size_t write_callback(void *ptr, size_t size, size_t nmemb, void *userp);
```

> libcurl 의 write 콜백함수는 수신해야 하는 데이터가 수신되는 즉시 libcurl 에 의해 호출된다.   
> ptr 은 전달된 데이터를 가리키며 해당 데이터의 크기는 nmemb 이다.   
> 크기는 항상 1이다.   
> 쓰기 콜백함수에 전달될 본문의 데이터 최대크기는 curl.h 에 정의되어 있으며   
> CURL_MAX_WRITE_SIZE 기본값은 16kBytes 이다.   
> 전달된 데이터가 비어있을 수 있으므로 0 바이트로 호출될 수 있으며 0으로는 종료되지 않는다.   
> 


# libcurl