[기본 구성](../emage/default-setting.md)

## 네트워크 구성

```shell
sudo vim /etc/netplan/00-installer-config.yaml
	network:
		version: 2
	ethernets:
		eth0:
			dhcp4: false
			addresses: [201.10.10.2/24]
		eth1:
			dhcp4: false
			addresses: [201.10.20.1/29]
			nameservers:
				addresses: [201.10.20.2]
		eth2:
			dhcp4: false
			addresses: [10.10.10.1/24]

:wq!
sudo netplan apply
```

## DHCP relay 
```shell
sudo vim /etc/default/isc-dhcp-relay
SERVERS="201.10.20.2"
INTERFACES="eth1 eth2"
:wq!

sudo systemctl enable isc-dhcp-relay
sudo systemctl start isc-dhcp-relay
sudo systemctl status isc-dhcp-relay
```

[DHCP server](ex-ns.md)