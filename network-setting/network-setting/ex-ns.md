[기본구성](../emage/default-setting)

## 네트워크 구성
```shell
sudo vim /etc/netplan/00-installer-config.yaml
	network:
		version: 2
	ethernets:
		ens33:
			dhcp4: no
			addresses: [201.10.20.2/29]
			nameservers:
				addresses: [201.10.20.2/29]
			routes:
				- to: default
				- via: 201.10.20.1
:wq!
sudo netplan apply
```
