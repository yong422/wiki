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

# ssh 비대화형 커맨드 환경변수 설정

> linux ssh remote command 실행시 비대화식 커맨드의 경우   
> bashrc or bash_profile 이 실행되지 않는다.   

```bash
$localhost > ssh 10.1.1.1 'command'
#Not found commnad 에러발생
```

> bashrc 파일에   
> if [ "$PS1" ]; then or if [ -z "$PS1" ]; then 행이있을경우   
> 비대화식 ssh 커맨드의 경우 bashrc 설정하지 않음.   
> ssh 명령옵션으로 -t 실행시 TTY 할당이 강제 실행되어   
> 대화형 쉘로 작동하게 한다.   

```bash
$localhost > ssh -t 10.1.1.1 'source ~/.bash_profile; command'
```