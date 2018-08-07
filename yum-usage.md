yum 사용법
==========

# 제공하는 binary 로 패키지 검색하는법.

- 예를 들어 whois 커맨드가 설치되어있지 않은 경우

```sh
[root@dev ~]# whois
-bash: whois: command not found
```

- yum whatprovides 사용

```sh
[root@dev ~]# yum whatprovides *bin/whois*
Loaded plugins: auto-update-debuginfo, fastestmirror, security
Loading mirror speeds from cached hostfile
 * base: mirror.navercorp.com
 * epel: mirror.premi.st
 * epel-debuginfo: mirror.premi.st
 * extras: mirror.navercorp.com
 * updates: mirror.navercorp.com
base/filelists_db                                                                            | 6.4 MB     00:00
base-debuginfo/filelists_db                                                                  |  67 MB     00:13
epel/filelists                                                                               | 7.3 MB     00:00
epel-debuginfo/filelists                                                                     | 4.9 MB     00:00
extras/filelists_db                                                                          |  24 kB     00:00
updates/filelists_db                                                                         | 484 kB     00:00
jwhois-4.0-19.el6.x86_64 : Internet whois/nicname client
```