# VSCODE

## remote-ssh 설정

- [puttygen 을 이용한 ssh 키 생성](https://extrememanual.net/26803)
- key type RSA (4096 bits) public / priavte key 생성
- private key 는 로컬피시에 복사
- public key 는 ssh 접속될 서버의 ~/.ssh/authorized_keys 에 복사
- chmod 600 ~/.ssh/authorized_keys
- vscode remote-ssh configuration 에 다음의 설정 추가

```
Host my-develop-server
  User myusername
  HostName 10.222.x.x
  # 저장된 개인키
  IdentityFile C:\Users\MyUserID\.ssh\remote_id_rsa
```