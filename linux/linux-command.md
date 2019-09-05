# linux command

## rpm

- install or erase 실행시 패키지 내부 스크립트의 실행오류로 실패하는 경우

  ```bash
  # 내부 스크립트를 실행하지 않고 삭제
  $ rpm -e --noscripts {패키지명}
  ```