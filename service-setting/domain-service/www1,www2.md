## Windows Server 도메인에 Linux 서버 가입
```shell
sudo realm discover nicekorea.com
sudo realm join nicekorea.com -U cyber
Cybre2023$$
sudo vim /etc/sssd/sssd.conf

[sssd]
config_file_version = 2
services = nss, pam
domains = nicekorea.com

[domain/nicekorea.com]
ad_domain = nicekorea.com
krb5_realm = NICEKOREA.COM
realmd_tags = manages-system joined-with-adcli
cache_credentials = True
id_provider = ad
fallback_homedir = /home/%u@%d
default_shell = /bin/bash
ldap_id_mapping = True
use_fully_qualified_names = True
access_provider = ad
:wq
 
sudo chmod 600 /etc/sssd/sssd.conf
sudo systemctl restart sssd
sudo systemctl enable sssd
sudo systemctl enable realmd

sudo vim /etc/pam.d/common-session
session required pam_mkhomedir.so skel=/etc/skel/ umask=0022
```