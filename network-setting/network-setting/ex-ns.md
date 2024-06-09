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

## DHCP server
```shell
sudo vim /etc/dhcp/dhcpd.conf
subnet 10.10.10.0 netmask 255.255.255.0 { 
	range 10.10.10.2 10.10.10.255; 
	option routers 10.10.10.1;
	option domain-name-servers 201.10.20.2;
}

subnet 201.10.20.0 netmask 255.255.255.248 { 
	option routers 201.10.20.1;
}
:wq!

sudo vim /etc/default/isc-dhcp-server
INTERFACEv4="ens33"
:wq!

sudo systemctl enable isc-dhcp-server
sudo systemctl start isc-dhcp-server
sudo systemctl status isc-dhcp-server
```

[DHCP relay](rt.md)