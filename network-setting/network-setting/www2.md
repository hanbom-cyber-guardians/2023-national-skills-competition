[기본 구성](default-setting.md)

## 네트워크 구성

```shell
sudo vim /etc/netplan/00-installer-config.yaml
	network:
		version: 2
	ethernets:
		ens33:
			dhcp4: no
			addresses: [172.20.200.104/26]
			nameservers:
				addresses: [172.20.200.102]
			routes:
			- to: default
			  via: 172.20.200.65
:wq!
sudo netplan apply
		```