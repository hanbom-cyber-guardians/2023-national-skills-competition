[기본구성](../emage/default-setting)

## 네트워크 구성
```shell
sudo nano /etc/netplan/01-installer-config.yaml
network:
	version: 2
	renderer: NetworkManager
	ethernets:
		ens33:
			dhcp4: no
			addresses: [10.10.11.1/23]
			nameservers:
				addresses: [172.20.200.102]
			routes:
				- to: default
				  via: 10.10.10.1
:wq!
sudo chmod 600 /etc/netplan/01-network-manager-all/yaml
sudo netplan apply
```

