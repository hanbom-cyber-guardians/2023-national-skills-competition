[기본구성](default-setting)

## 네트워크 구성
```shell
sudo vim /etc/netplan/00-installer-config.yaml
	network:
		version: 2
	ethernets:
		eth0:
			dhcp4: false
			addresses: [10.10.10.1/23]
		eth1:
			dhcp4: false
			addresses: [172.20.200.65]
			nameservers:
				addresses: [172.20.200.102]
		eth2:
			dhcp4: false
			addresses: [201.10.10.1/24]
:wq!
sudo netplan apply
```

## DHCP relay
```shell
sudo vim /etc/default/isc-dhcp-relay
SERVERS="172.20.200.101"
INTERFACES="eth0 eth1"
:wq!

sudo systemctl enable isc-dhcp-relay
sudo systemctl start isc-dhcp-relay
sudo systemctl status isc-dhcp-relay
```

[dhcp server](dlp.md)

