## fw
```shell
vim /etc/ssh/sshd.config

38 PubkeyAuthentication yes # 주석 제거
57 PasswordAuthentication no #주석 지우고 수정

AllowUsers cyber@20.20.20.0/23 # 맨 밑
:wq
systemctl restart sshd
```

## mgt-01
```shell
ssh-keygen -t rsa
passphrase: pass1234%%
            pass1234%%
sudo mkdir /root/.ssh
sudo chmod 700 /root/.ssh

sudo ssh-copy-id -i ~/.ssh/id_rsa.pub cyber@201.10.10.1
```