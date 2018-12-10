GITLAB
======

# gitlab CI 적용

## Gitlab-CI runner 설치

- version 10 이상 기준으로 작성
- gitlab runner 설치

  > curl -L https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.rpm.sh | sudo bash   
  > sudo yum -y install gitlab-runner   

- gitlab-runner 에 gitlab repository 등록

  1. ```[root@localhost] gitlab-runner register ``` 입력   
  2. gitlab URL 입력