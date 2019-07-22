GITLAB
======

# gitlab CI 적용

## yml 파일 작성 팁

- cache

> 이전 작업의 동일한 내용을 다시 사용하여 작업이 실행되는 속도를 빠르게 할 수 있다.   
> 외부에서 가져오는 라이브러리를 사용할때 유용하다.   
> 파이프라인 작업간에 공유가 가능하다.   

- cache:key

> 작업간의 캐쉬를 공유하기 위한 키값을 설정 할 수 있다.   
> 동일한 분기내에서 캐쉬를 공유할 경우  ${CI_COMMIT_REF_SLUG} 키값으로 사용한다.   
> 

- cache:policy

> gitlab-ci cache 에 paths 를 명시한 경우 각 job 마다 pull push 를 진행한다.   
> 실제 cache 하는 파일의 변경작업에서만 push 가 필요하고 나머지 job 에서는 사용만 필요한 경우,   
> 정책에 pull 추가   

```yml
prepare:
  stage: setup
  cache:
    key: gems
    paths:
      - vendor/bundle
  script:
    - bundle install --deployment

rspec:
  stage: test
  cache:
    key: gems
    paths:
      - vendor/bundle
    policy: pull
```

- cache 저장공간

> gitlab runner 의 실행자가 shell 인 경우 로컬 스토어에 저장된다.   
> Locally, stored under the gitlab-runner user’s home    
> directory: /home/gitlab-runner/cache/\<user\>/\<project\>/\<cache-key\>/cache.zip.

## Gitlab-CI runner 설치

- version 10 이상 기준으로 작성
- gitlab runner 설치

  > curl -L https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.rpm.sh | sudo bash   
  > sudo yum -y install gitlab-runner   

- gitlab-runner 에 gitlab repository 등록

  1. ```[root@localhost] gitlab-runner register ``` 입력   
  2. gitlab URL 입력
  3. token 입력 (프로젝트 CI/CD 참조)
  4. 태그명 입력



## Gitlab-CI Configuration parameters



### environment

- [참조](https://docs.gitlab.com/ee/ci/environments.html#configuring-manual-deployments)
- job 이 특정 environment 에서 배포되도록 정의 할 수 있다.
- environment 값을 미리 설정 할 수 있으나 dynamic 으로 설정 할 수도 있으며, gitlab UI 에 자동으로 생성된다.

  ```yaml
  # test environment 에서의 배포정의
  environment:
    name: test
    url: https://test.xms.gabia.com
  when: manual
  allow_failure: false
  ```

### when

- 해당 job 을 언제 동작시킬지에 대한 옵션
- manual 로 활성화 할 경우 job 을 실행 할 수 있는 버튼이 생성되며, 실행시에만 job 이 실행되도록 설정 할 수 있다.

  - 상세옵션으로 allow_failure: true or false 가 있으며 다음의 manual job 이 파이프라인에 영향을 주지않도록 하는 옵션이며 true(영향없음), false(파이프라인 실패)
  
- delayed 로 활성화 할 경우 일정 시간 대기후 job 이 실행되도록 설정 할 수 있다.
- gitlab-ci pipeline 에서 environment 옵션과 manual