Linux OS 의 메타정보 수집방법
===========================

Root partition 의 system uuid

- root 파티션의 파일시스템명을 구한다. (/bin/df)
- ex) /dev/sda1
- /etc/blkid.tab, /etc/blkid/blkid.tab 파일또는 /sbin/blkid 명령어로 uuid 확인

  ```bash
  $localhost > /sbin/blkid

  /dev/sda1: UUID="f121b6db-ea2b-4c00-98b8-e5f34c8aefc2" TYPE="xfs"
  /dev/sda2: UUID="CHGsEQ-hLmT-ZYFH-lcg8-KP6K-xR3x-vtCNTg" TYPE="LVM2_member"
  /dev/mapper/cl-root: UUID="1411022f-fd64-4f0a-9e41-ba91bcea398e" TYPE="xfs"
  /dev/mapper/cl-swap: UUID="bdb589bf-b418-4581-b8d4-e0c0bfb8c8b4" TYPE="swap"

  ```

- 안되는 경우 lsblk 명령어로 확인
  - /bin/lsblk -o mountpoint,uuid

  ```bash
  $localhost > /bin/lsblk -o mountpoint,uuid

  MOUNTPOINT UUID

  /boot      f121b6db-ea2b-4c00-98b8-e5f34c8aefc2
            CHGsEQ-hLmT-ZYFH-lcg8-KP6K-xR3x-vtCNTg
  /          1411022f-fd64-4f0a-9e41-ba91bcea398e
  [SWAP]     bdb589bf-b418-4581-b8d4-e0c0bfb8c8b4
  ```
