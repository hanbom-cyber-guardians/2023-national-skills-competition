[기본구성](default-setting)

## 네트워크 구성
```shell
sudo vim /etc/netplan/00-installer-config.yaml
	network:
		version: 2
	ethernets:
		ens33:
			dhcp4: no
			addresses: [172.20.200.101/26]
			nameservers:
				addresses: [172.20.200.102]
			routes:
			- to: default
			  via: 172.20.200.65
:wq!
sudo netplan apply
```

## DHCP server
```shell
sudo vim /etc/dhcp/dhcpd.conf
subnet 10.10.10.0 netmask 255.255.254.0 { 
	range 10.10.10.2 10.10.10.255; 
	option routers 10.10.10.1;
	option domain-name-servers 172.20.200.102;
}

subnet 172.20.200.64 netmask 255.255.255.192 { 
	option routers 172.20.200.65;
}
:wq!

sudo vim /etc/default/isc-dhcp-server
INTERFACEv4="ens33"
:wq!

sudo systemctl enable isc-dhcp-server
sudo systemctl start isc-dhcp-server
sudo systemctl status isc-dhcp-server

```

[dhcp relay](fw.md)


