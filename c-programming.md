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