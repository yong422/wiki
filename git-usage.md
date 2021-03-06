git 사용법
==========

# git 설치 예외처리

* curl-config 에러 발생할 경우 아래 패키지 설치
```bash
$localhost> sudo apt-get install libcurl4-gnutls-dev
$localhost> sudo apt-get install libcurl4-openssl-dev

#* /bin/sh: autoconf: not found 에러 발생할 경우 아래 패키지 설치
$localhost> sudo apt-get install autoconf autoconf2.13 

#* tclsh failed; using unoptimized loading 에러 발생할 경우 아래 패키지 설치
$localhost> sudo apt-get install gettext

#* /bin/sh: asciidoc: not found 에러 발생할 경우 아래 패키지 설치
$localhost> sudo apt-get install asciidoc
```


# 인증정보 캐쉬

- 인증정보가 설정된 git remote repository 사용시 submodule 하나하나 인증정보를 입력해야 하는 이슈   
- 인증정보 캐쉬설정으로 일정 시간내에는 한번의 인증정보로 사용하도록 설정

> git config --global credential.helper cache   

# submodule 삭제

- git 의 경우 submodule 을 삭제하는 별도의 명령어가 없음   
- 다음의 작업을 순차적으로  진행해야함.

  1. .gitmodule 파일의 삭제할 submodule 의 라인 전체를 삭제.
  2. .git/config 파일의 삭제할 submodule 삭제.
  3. 실제 submodule 의 위치 삭제.

# branch

## branch 전환

- 해당 branch 가 없을 경우 생성하며 branch 전환
- 동일한 branch 가 있을 경우 실패

  ```bash 
  $ git checkout -b 'branch name' 
  ```

- 동일한 branch 가 있을 경우 해당 branch 로 전환

  ```bash 
  $ git checkout 'branch name'   
  ```

- remote branch 를 따라가도록 전환

  ```bash 
  $ git branch -b newbranch origin/newbranch   
  ```

## branch 삭제

```bash 
git branch -d 'branch name'   
```


# remote

## remote 추가

- git remote add 단축이름 url
```sh
> git remote
# origin 이라는 이름으로 리모트 추가
$ git remote add origin git://github.com/yong422/wiki.git
$ git remote -v
origin git://github.com/yong422/wiki.git (fetch)
origin git://github.com/yong422/wiki.git (push)

```


# CentOS5 git 설치

- CentOS 5 의 경우 기본 제공되는 git 의 버전이 1.8x
- 최신버전을 git-scm.com 에서 설치
- https://www.kernel.org/pub/software/scm/git/git-2.9.5.tar.gz

```sh
./configure --prefix=/usr
make
make install

# 기존 git 을 덮어쓰기위해 usr 에 설치
```

# reset

## commit reset

- 커밋이 잘못되었거나 할 경우 기존의 특정 리비전으로 변경하고 싶을때

```sh
commit 47d1eaf0de28ba692705b0cdc3f5a01ee6aaa82a (HEAD -> develop_tms-10, origin/develop_tms-10)
Merge: 2189341 092f499
Author: Yongkyu Jo <ykjo@gabia.com>
Date:   Fri Aug 10 14:57:44 2018 +0900

    TMS-10 syslog module 추가 및 테스트 추가

commit 218934126b148524fa0905b3569989f32a638283
Author: Yongkyu Jo <ykjo@gabia.com>
Date:   Fri Aug 10 14:55:26 2018 +0900

    TMS-10 syslog module 추가 및 테스트 추가

commit 092f4991bceeece26fb996c83fa11213f0e8856c
Author: KimMineCheol <kmc@gabia.com>
Date:   Thu Aug 9 16:49:53 2018 +0900

    TMS-10 일부 불필요 코드삭제 및 띄어쓰기 수정

commit 46f2a151be1e1247395f736d20e55747bd3f2dda
Author: KimMineCheol <kmc@gabia.com>
Date:   Thu Aug 9 16:45:31 2018 +0900

    TMS-10 syslog module 추가 및 테스트코드 추가

commit 48050ec1a3d87c8c50b473940e251f4e5c879eec (origin/develop_tms-5, develop_tms-5)
Author: ykjo <ykjo2gabia.com>
Date:   Thu Aug 9 15:26:25 2018 +0900

    TMS-5 띄어쓰기 오류수정
```

- 돌아가고 싶은 리비전 확인.
  - 48050ec1a3d87c8c50b473940e251f4e5c879eec

```sh
git reset --soft 48050ec1a3d87c8c50b473940e251f4e5c879eec

# 해당 리비전으로 되돌리며 현재까지 작업한 내용은 그대로 유지한다.
# --hard 옵션인 경우 해당 리비전의 소스로 원복한다.
```

# setup

## windows git config 에디터 수정

- [참조](https://stackoverflow.com/questions/10564/how-can-i-set-up-an-editor-to-work-with-git-on-windows)

# rebase

## git squash

- 여러 commit 을 하나의 commit 으로 변경 하고자 할때 

```bash
# git commit hash 를 한라인으로 확인.
$ git log --pretty=oneline

5143680e54e893adcfe9223cd712b99e97e03ca7 Merge branch 'develop_xms-541' into 'master'
9dcc0d395fbb4b7ee59548f7d9bf43cafff29c2d XMS-541 v1.3.1 readme 추가
d9acffea4dae12d77fe45deb36f5a016dabaf126 XMS-541 dictionary 를 이용한 string 의 파라미터 변환을 위한 기능 추가
b5a0806f94e860d529a613de7d9466f784ffb7e0 Merge branch 'develop_xms-489' into 'master'
5d953126ddfd2096b7f3186dc986afd8cdc0a148 XMS-489 timestamp 를 변수로 사용가능한 외부함수에 대해 static 으로 정의
e920dd8565e5fa1d7eee41f4f7d926f49b60b6ca XMS-489 README 내용 추가
bc97cf2e2a412b232112b5112f509d3bfd3ce9c2 Merge branch 'develop_xms-489' of https://gitlab.gabia.com/monitoring/common/cpp/reference into develop_xms-489
c410d24cd7532385af7e6af6bd15d2baada09703 XMS-489 xms datetime string 공통 사용을 위한 DateTime 모듈 추가
43d791968c9063aec0380b0080ec197e29c83a78 Merge branch 'develop_xms-530' into 'master

# 최상단 HEAD 를 포함한 3개의 commit rebase

$ git rebase -i HEAD~3


# editor 출력

pick 5143680 XMS-633 Merge branch 'develop_xms-541' into 'master'
pick 9dcc0d3 XMS-633 XMS-541 v1.3.1 readme 추가
pick d9acffe XMS-541 dictionary 를 이용한 string 의 파라미터 변환을 위한 기능 추가

# Rebase b5a0806..5143680 onto b5a0806 (3 command(s))
#
# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
# d, drop = remove commit


# 다음과 같은 출력
# squash 하려는 commit 을 squash 로 수정.
# 하나의 커밋을 pick 으로 남겨둔다.

pick 5143680 XMS-633 Merge branch 'develop_xms-541' into 'master'
squash 9dcc0d3 XMS-633 XMS-541 v1.3.1 readme 추가
squash d9acffe XMS-541 dictionary 를 이용한 string 의 파라미터 변환을 위한 기능 추가

# 저장시 새로운 commit 에 대한 commit message 에 대해 수정 후 커밋을 완료.
```

