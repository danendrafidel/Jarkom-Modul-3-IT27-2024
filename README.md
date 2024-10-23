# Jarkom-Modul-3-IT27-2024

## IT 27

| No  | Nama Anggota          | NRP        |
| --- | --------------------- | ---------- |
| 1   | Danendra Fidel Khansa | 5027231063 |
| 2   | Farida Qurrotu A'yuna | 5027231015 |

## Topologi Kelompok IT27 Praktikum Modul 3

![Topologi](img/Topologi.png)

## SOAL 1 (Config)

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

```
auto eth0
iface  eth0 inet dhcp

up echo nameserver 10.77.4.1 > /etc/resolv.conf
up echo nameserver 192.168.122.1 >> /etc/resolv.conf

```

### Erwin (Client)

```
auto eth0
iface  eth0 inet dhcp

up echo nameserver 10.77.4.1 > /etc/resolv.conf
up echo nameserver 192.168.122.1 >> /etc/resolv.conf

```

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

## SOAL 0

Pulau Paradis telah menjadi tempat yang damai selama 1000 tahun, namun kedamaian tersebut tidak bertahan selamanya. Perang antara kaum Marley dan Eldia telah mencapai puncak. Kaum Marley yang dipimpin oleh Zeke, me-register domain name marley.yyy.com untuk worker Laravel mengarah pada Annie. Namun ternyata tidak hanya kaum Marley saja yang berinisiasi, kaum Eldia ternyata sudah mendaftarkan domain name eldia.yyy.com untuk worker PHP (0) mengarah pada Armin.

- Buat script pada DNS Server Fritz dengan nama `fritz.sh`

```
echo 'zone "marley.it27.com" {
        type master;
        file "/etc/bind/jarkom/marley.it27.com";
};

zone "eldia.it27.com" {
        type master;
        file "/etc/bind/jarkom/eldia.it27.com";
};' > /etc/bind/named.conf.local

mkdir /etc/bind/jarkom

echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     marley.it27.com. root.marley.it27.com. (
                        2024051601      ; Serial
                        604800          ; Refresh
                        86400           ; Retry
                        2419200         ; Expire
                        604800 )        ; Negative Cache TTL
;
@               IN      NS      marley.it27.com.
@               IN      A       10.77.1.1 ; IP Annie Laravel Workerr' > /etc/bind/jarkom/marley.it27.com

echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     eldia.it27.com.  eldia.it27.com.  (
                        2024051601      ; Serial
                        604800          ; Refresh
                        86400           ; Retry
                        2419200         ; Expire
                        604800 )        ; Negative Cache TTL
;
@               IN      NS      eldia.it27.com.
@               IN      A       10.77.2.1 ; IP Armin PHP Worker' > /etc/bind/jarkom/eldia.it27.com

echo 'options {
        directory "/var/cache/bind";

        forwarders {
                192.168.122.1;
        };

        // dnssec-validation auto;
        allow-query{any;};
        auth-nxdomain no;    # conform to RFC1035
        listen-on-v6 { any; };
}; ' >/etc/bind/named.conf.options

service bind9 restart

```

- Kemudian `ping marley.it27.com` pada client `Zeke` dan `ping eldia.it27.com` pada client `Erwin`

![alt text](<img/0 (1).png>)

![alt text](<img/0 (2).png>)

## SOAL 2

Semua Client harus menggunakan konfigurasi ip address dari keluarga Tybur (dhcp).

Client yang melalui bangsa marley mendapatkan range IP dari [prefix IP].1.05 - [prefix IP].1.25 dan [prefix IP].1.50 - [prefix IP].1.100

## SOAL 3

Client yang melalui bangsa eldia mendapatkan range IP dari [prefix IP].2.09 - [prefix IP].2.27 dan [prefix IP].2 .81 - [prefix IP].2.243.

## SOAL 4

Client mendapatkan DNS dari keluarga Fritz dan dapat terhubung dengan internet melalui DNS tersebut.

## SOAL 5

Dikarenakan keluarga Tybur tidak menyukai kaum eldia, maka mereka hanya meminjamkan ip address ke kaum eldia selama 6 menit. Namun untuk kaum marley, keluarga Tybur meminjamkan ip address selama 30 menit. Waktu maksimal dialokasikan untuk peminjaman alamat IP selama 87 menit.
