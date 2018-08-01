리눅스 init.d 스크립트 작성
=========================

# 샘플

```sh
#!/bin/sh

/**
chkconfig 가능하도록 설정
chkconfig: $1 $2 $3
$1 : runlevel
$2 : start priority 부팅시 실행순서
$3 : stop priority 종료시 실행순서

chkconfig --add gabia_mond   등록
chkconfig --del gabia_mond 등록해제.

init script 위 2개의 헤더는 centos 5 사용하기 위한 용도
lsb init script header 는 centos 6 이상부터 사용하기 위한 용도
저레벨 OS 까지 포함하기위해 두개의 header 를사용.
*/

### BEGIN INIT INFO
# Provides: gabia_mond
# Required-Start: $local_fs $remote_fs $network $syslog $time
# Required-Stop: $local_fs $remote_fs $network $syslog $time
# Default-Start:    2 3 4 5
# Default-Stop:    0 1 2 6
# Short-Description: 짧은 설명
# Description: 해당 프로세스의 설명
### END INIT INFO

# chkconfig: 2345 99 10
# probe: true

[ -f $binary_file } ] || exit 0

RETVAL=0

start() {
  # start 정의
}

stop() {
  # stop 정의
}

kill() {
  # kill 정의
}

restart() {
  stop
  sleep 1
  kill
  start
}


case "$1" in
  start)
    start
    ;;
  stop)
    stop
    ;;
  restart)
    restart
    ;;
  *)
    echo "Usage: <프로세스명> {start|stop|restart}"
    exit 1
esac

exit $RETVAL
```