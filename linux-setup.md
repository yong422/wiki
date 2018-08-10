리눅스 설정
==========

# CentOS 특정계정 홈디렉토리 강제 설정 (chroot)

> centos 특정계정 홈디렉토리 강제설정  (chroot)   
> /bin/false, /sbin/nologin 의 차이점   
> /etc/passwd 사용자계정 부분에 /bin/false, /bin/nologin 등으로 설정할 경우가 있는데 그 차이점입니다.    
>   
> /bin/false    
> allows a login, but no shell, no ssh tunnels and no home directory.   
> -> 시스템의 로그인은 불가능, FTP 서버 프로그램같은 프로그램도 불가능하다.   
> 쉘이나 ssh과 같은 터널링(원격접속) 그리고 홈디렉토리를 사용할 수 없다.
>   
> /sbin/nologin    
> disallows logins completely and returns a polite account unavailable message.   
> -> 사용자 계정의 쉘부분에 /bin/nologin 으로 설정을 하면   
> 로긴 불가하고, 메시지들은 반환된다 ssh는 사용불가능하며 ftp의 경우 사용이 가능합니다.   
