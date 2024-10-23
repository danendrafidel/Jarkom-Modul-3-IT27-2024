# Jarkom-Modul-3-IT27-2024

## IT 27

| No  | Nama Anggota          | NRP        |
| --- | --------------------- | ---------- |
| 1   | Danendra Fidel Khansa | 5027231063 |
| 2   | Farida Qurrotu A'yuna | 5027231015 |

## Daftar Isi

- [Topologi](#topologi)

- [Soal 1](#SOAL1)

- [Soal 2](#Soal-2)

- [Soal 3](#Soal-3)

- [Soal 4](#Soal-4)

- [Soal 5](#Soal-5)

- [Soal 6](#Soal-6)

- [Soal 7](#Soal-7)

- [Soal 8](#Soal-8)

- [Soal 9](#Soal-9)

- [Soal 10](#Soal-10)

- [Soal 11](#Soal-11)

- [Soal 12](#Soal-12)

- [Soal 13](#Soal-13)

- [Soal 14](#Soal-14)

- [Soal 15](#Soal-15)

- [Soal 16](#Soal-16)

- [Soal 17](#Soal-17)

- [Soal 18](#Soal-18)

- [Soal 19](#Soal-19)

- [Soal 20](#Soal-20)

## Topologi Kelompok IT27 Praktikum Modul 3

![Topologi](img/Topologi.png)

## SOAL 0 (Config)

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

## SOAL 1

Pulau Paradis telah menjadi tempat yang damai selama 1000 tahun, namun kedamaian tersebut tidak bertahan selamanya. Perang antara kaum Marley dan Eldia telah mencapai puncak. Kaum Marley yang dipimpin oleh Zeke, me-register domain name **marley.yyy.com** untuk worker Laravel mengarah pada **Annie**. Namun ternyata tidak hanya kaum Marley saja yang berinisiasi, kaum Eldia ternyata sudah mendaftarkan domain name **eldia.yyy.com** untuk worker PHP (0) mengarah pada **Armin**.

- Buat script pada DNS Server Fritz dengan nama `1.sh`

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

Semua Client harus menggunakan konfigurasi ip address dari keluarga **Tybur (dhcp)**.

**Client** yang melalui bangsa marley mendapatkan range IP dari [prefix IP].1.05 - [prefix IP].1.25 dan [prefix IP].1.50 - [prefix IP].1.100

- Pada Paradis (DHCP Relay) buat script `nano paradis.sh` untuk dairahkan ke Tybur (DHCP Server)

```
apt-get update
apt-get install isc-dhcp-relay -y
service isc-dhcp-relay start

relay="SERVERS=\"10.77.4.2\"
INTERFACES=\"eth1 eth2 eth3 eth4\"
OPTIONS=\"\"
"
echo "$relay" > /etc/default/isc-dhcp-relay

echo net.ipv4.ip_forward=1 > /etc/sysctl.conf

service isc-dhcp-relay restart
```

- Setelah di run script diatas dengan `bash paradis.sh` lalu pindah ke Tybur (DHCP Server) dan buat script `nano 2.sh` untuk setup subnet yang marley dahulu

```
echo 'subnet 10.77.3.0 netmask 255.255.255.0 {
    option routers 10.77.3.0;
}

subnet 10.77.4.0 netmask 255.255.255.0 {
    option routers 10.77.4.0;
}

subnet 10.77.1.0 netmask 255.255.255.0 {
    range 10.77.1.5 10.77.1.25;
    range 10.77.1.50 10.77.1.100;
    option routers 10.77.1.1;
}' > /etc/dhcp/dhcpd.conf
```

## SOAL 3

**Client** yang melalui bangsa eldia mendapatkan range IP dari [prefix IP].2.09 - [prefix IP].2.27 dan [prefix IP].2 .81 - [prefix IP].2.243.

- Kemudian tambahkan setup subnet yang eldia dengan bikin script baru yaitu `nano 3.sh`

```
echo 'subnet 10.77.3.0 netmask 255.255.255.0 {
    option routers 10.77.3.0;
}

subnet 10.77.4.0 netmask 255.255.255.0 {
    option routers 10.77.4.0;
}

subnet 10.77.1.0 netmask 255.255.255.0 {
    range 10.77.1.5 10.77.1.25;
    range 10.77.1.50 10.77.1.100;
    option routers 10.77.1.1;
}

subnet 10.77.2.0 netmask 255.255.255.0 {
    range 10.77.2.09 10.77.2.27;
    range 10.77.2.81 10.77.2.243;
    option routers 10.77.2.1;
} ' > /etc/dhcp/dhcpd.conf
```

## SOAL 4

**Client** mendapatkan DNS dari keluarga Fritz dan dapat terhubung dengan internet melalui DNS tersebut.

- Kemudian buat script baru lagi dengan `nano 4.sh` untuk nambahin `option-domain-name-servers`

```
echo 'subnet 10.77.3.0 netmask 255.255.255.0 {
    option routers 10.77.3.0;
    option broadcast-address 10.77.3.255;
}

subnet 10.77.4.0 netmask 255.255.255.0 {
    option routers 10.77.4.0;
    option broadcast-address 10.77.4.255;
}

subnet 10.77.1.0 netmask 255.255.255.0 {
    range 10.77.1.5 10.77.1.25;
    range 10.77.1.50 10.77.1.100;
    option routers 10.77.1.1;
    option broadcast-address 10.77.1.255;
    option domain-name-servers 10.77.4.1;
}

subnet 10.77.2.0 netmask 255.255.255.0 {
    range 10.77.2.9 10.77.2.27;
    range 10.77.2.81 10.77.2.243;
    option routers 10.77.2.1;
    option broadcast-address 10.77.2.255;
    option domain-name-servers 10.77.4.1;
} ' > /etc/dhcp/dhcpd.conf
```

- Jangan lupa untuk setup di Fritz (DNS Server) pake `nano fritz.sh`

```
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
```

## SOAL 5

Dikarenakan keluarga **Tybur** tidak menyukai kaum **eldia**, maka mereka hanya meminjamkan ip address ke kaum **eldia** selama 6 menit. Namun untuk kaum **marley**, keluarga **Tybur** meminjamkan ip address selama 30 menit. Waktu maksimal dialokasikan untuk peminjaman alamat IP selama 87 menit.

- Untuk nambahin limit waktu buat script baru lagi yaitu `nano 5.sh` seperti berikut, tambahkan authoritative; di awal konfigurasi agar DHCP server menjadi sumber otoritatif untuk jaringan tersebut.

```

echo INTERFACESv4="eth0" > /etc/default/isc-dhcp-server

echo 'authoritative;

subnet 10.77.3.0 netmask 255.255.255.0 {
    option routers 10.77.3.0;
    option broadcast-address 10.77.3.255;
}

subnet 10.77.4.0 netmask 255.255.255.0 {
    option routers 10.77.4.0;
    option broadcast-address 10.77.4.255;
}

subnet 10.77.1.0 netmask 255.255.255.0 {
    range 10.77.1.5 10.77.1.25;
    range 10.77.1.50 10.77.1.100;
    option routers 10.77.1.1;
    option broadcast-address 10.77.1.255;
    option domain-name-servers 10.77.4.1;
    default-lease-time 1800;
    max-lease-time 5220;
}

subnet 10.77.2.0 netmask 255.255.255.0 {
    range 10.77.2.9 10.77.2.27;
    range 10.77.2.81 10.77.2.243;
    option routers 10.77.2.1;
    option broadcast-address 10.77.2.255;
    option domain-name-servers 10.77.4.1;
    default-lease-time 360;
    max-lease-time 5220;
} ' > /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```

- Lakukan `bash 5.sh` untuk menjalankan Tybur (DHCP Server)

- Kemudian coba tes telnet ke client `zeke` untuk marley dan `erwin` untuk eldia, namun sebelum itu tolong matikan dulu kedua client lalu nyalakan kembali dan hasilnya berikut, coba ping

- Client `Zeke` (ditandai dengan udhcpc saat masuk)
  ![alt text](<img/5 (1).png>)

-Client `Erwin` (ditandai dengan udhcpc saat masuk)
![alt text](<img/5 (2).png>)

## SOAL 6

**Armin** berinisiasi untuk memerintahkan setiap worker PHP untuk melakukan konfigurasi virtual host untuk website berikut https://intip.in/BangsaEldia dengan menggunakan php 7.3

## SOAL 7

Dikarenakan Armin sudah mendapatkan kekuatan titan colossal, maka bantulah kaum **eldia** menggunakan **colossal** agar dapat bekerja sama dengan baik. Kemudian lakukan testing dengan 6000 request dan 200 request/second.

## SOAL 8

Karena Erwin meminta “laporan kerja Armin”, maka dari itu buatlah analisis hasil testing dengan 1000 request dan 75 request/second untuk masing-masing algoritma Load Balancer dengan ketentuan sebagai berikut:

- Nama Algoritma Load Balancer
- Report hasil testing pada Apache Benchmark
- Grafik request per second untuk masing masing algoritma.
- Analisis

## SOAL 9

Dengan menggunakan algoritma Least-Connection, lakukan testing dengan menggunakan 3 worker, 2 worker, dan 1 worker sebanyak 1000 request dengan 10 request/second, kemudian tambahkan grafiknya pada “laporan kerja Armin”.

## SOAL 10

Selanjutnya coba tambahkan keamanan dengan konfigurasi autentikasi di **Colossal** dengan dengan kombinasi username: “arminannie” dan password: “jrkmyyy”, dengan yyy merupakan kode kelompok. Terakhir simpan file “htpasswd” nya di /etc/nginx/supersecret/

## SOAL 11

Lalu buat untuk setiap request yang mengandung /titan akan di proxy passing menuju halaman https://attackontitan.fandom.com/wiki/Attack_on_Titan_Wiki

**hint: (proxy_pass)**

## SOAL 12

Selanjutnya **Colossal** ini hanya boleh diakses oleh client dengan IP [Prefix IP].1.77, [Prefix IP].1.88, [Prefix IP].2.144, dan [Prefix IP].2.156.

**hint: (fixed in dulu clientnya)**
