git 사용법
==========

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

> git checkout -b 'branch name'    

- 동일한 branch 가 있을 경우 해당 branch 로 전환

> git checkout 'branch name'   

## branch 삭제

> git branch -d 'branch name'   

##


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
