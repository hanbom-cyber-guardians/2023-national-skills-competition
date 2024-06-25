## fw
```shell
vim /etc/ufw/before.rules
*nat
:POSTROUTING ACCEPT [0:0]

-A POSTROUTING -s 10.10.10.0/23 -o eth2 -j MASQUERADE
-A POSTROUTING -s 172.20.200.64/26 -o eth2 -j MASQUERADE

COMMIT
:wq

ufw allow ssh
ufw enable
ufw reload
```

## rt
```shell
vim /etc/ufw/before.rules
*nat
:POSTROUTING ACCEPT [0:0]

-A POSTROUTING -s 10.10.10.0/24 -o eth0 -j MASQUERADE

COMMIT
:wq

ufw allow 1194
ufw enable
ufw reload
```