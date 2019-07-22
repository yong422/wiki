docker install
==============

# CentOS 7 install

> 최소 커널버전은 2.6.32-431   


- docker repository 추가
https://docs.docker.com/install/linux/docker-ce/centos/#install-using-the-repository

- docker filesystem  
  - docker 실행시 실패
  - /var/log/message 확인 결과 storage driver overlay2 not supported 오류
  - 설치를 해야하나 CentOS 7 에서도 커널버전이 낮으면 설치 불가
    - 3.10.0-514 이상에서 사용가능하며 권장사항은 커널버전 4 이상.
  - https://docs.docker.com/storage/storagedriver/overlayfs-driver/