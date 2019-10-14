C programming
=============

# 동적파라미터 함수 만들기

> printf, fprintf, snprintf 등의 ... 을 va_list 를 사용할 수 있도록 만들어진 함수를 사용   
> vprintf, vfprintf, vsprintf, vsnprintf 사용.   

```cpp
#include <stdarg.h>
int vprintf(const char* format, va_list ap);
int vsnprintf(char *str, size_t size, const char* size, va_list ap);
```

# 정규표현식

- GNU libstdc++ 에서 공식적으로 std::regex 가 릴리즈 된 건 v4.9.0
- v4.8 (CentOS 7 개발기준 4.8.6) 부터도 사용가능하나 버그가 많음