# Jarkom-Modul-3-IT27-2024

## IT 27

| No  | Nama Anggota          | NRP        |
| --- | --------------------- | ---------- |
| 1   | Danendra Fidel Khansa | 5027231063 |
| 2   | Farida Qurrotu A'yuna | 5027231015 |

## Topologi Kelompok IT27 Praktikum Modul 3

![Topologi](img/Topologi.png)

## Config

### Paradis (DHCP Relay)

```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 10.77.1.0
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 10.77.2.0
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 10.77.3.0
	netmask 255.255.255.0

auto eth4
iface eth4 inet static
	address 10.77.4.0
	netmask 255.255.255.0

iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.77.0.0/16
```

### Tybur (DHCP Server)

```
auto eth0
iface  eth0 inet static
  address 10.77.4.2
  netmask 255.255.255.0
  gateway 10.77.4.0

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Fritz (DNS Server)

```
auto eth0
iface  eth0 inet static
  address 10.77.4.1
  netmask 255.255.255.0
  gateway 10.77.4.0

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Warhammer (Database)

```
auto eth0
iface  eth0 inet static
  address 10.77.3.3
  netmask 255.255.255.0
  gateway 10.77.3.0

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Beast ( LoadBalancer Laravel)

```
auto eth0
iface  eth0 inet static
  address 10.77.3.1
  netmask 255.255.255.0
  gateway 10.77.3.0

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Colossal (LoadBalancer PHP)

```
auto eth0
iface  eth0 inet static
  address 10.77.3.2
  netmask 255.255.255.0
  gateway 10.77.3.0

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Annie (Laravel Worker)

```
auto eth0
iface  eth0 inet static
  address 10.77.1.1
  netmask 255.255.255.0
  gateway 10.77.1.0

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Bertholdt (Laravel Worker)

```
auto eth0
iface  eth0 inet static
  address 10.77.1.2
  netmask 255.255.255.0
  gateway 10.77.1.0

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Reiner (Laravel Worker)

```
auto eth0
iface  eth0 inet static
  address 10.77.1.3
  netmask 255.255.255.0
  gateway 10.77.1.0

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Armin (PHP Worker)

```
auto eth0
iface  eth0 inet static
  address 10.77.2.1
  netmask 255.255.255.0
  gateway 10.77.2.0

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Eren (PHP Worker)

```
auto eth0
iface  eth0 inet static
  address 10.77.2.2
  netmask 255.255.255.0
  gateway 10.77.2.0

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Mikasa (PHP Worker)

```
auto eth0
iface  eth0 inet static
  address 10.77.2.3
  netmask 255.255.255.0
  gateway 10.77.2.0

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Zeke (Client)

### Erwin (Client)

## Bash Install

- Paradis (DHCP Relay)

```
apt-get update
apt-get install isc-dhcp-relay -y
```

- Tybur (DHCP Server)

```
echo nameserver 192.168.122.1 > /etc/resolv.conf
apt-get update
apt-get install isc-dhcp-server -y
dhcpd --version

echo INTERFACES="eth0" > /etc/default/isc-dhcp-serverm
```

- Fritz (DNS Server)

```
echo nameserver 192.168.122.1 > /etc/resolv.conf
apt-get update
apt-get install bind9 -y
```

- Warhammer (Database)

```
echo nameserver 192.168.122.1 > /etc/resolv.conf

apt-get update
apt-get install mariadb-server -y
service mysql start
```

- Beast (LoadBalancer Laravel)

- Colossal (LoadBalancer PHP)

- Annie , Bertholdt, Reiner (Laravel Worker)

- Armin, Eren, Mikasa (PHP Worker)
