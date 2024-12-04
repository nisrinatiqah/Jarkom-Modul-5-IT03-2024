# Laporan Resmi Praktikum Jarkom Modul 4 2024

---

# Anggota Kelompok
| Nama  | NRP  |
|----------|----------|
| Nisrina Atiqah Dwiputri Ridzki | 5027231075 |
| Nicholas Arya Krisnugroho Rerangin | 5027231058 |

# Daftar Isi
- [Topologi](#topologi)
- [Rute](#rute)
- [Tree](#tree)
- [Pembagian IP VLSM](#pembagian-ip-vlsm)
- [Konfigurasi](#konfigurasi)
- [Misi 1](#misi-1)
  - Soal 4
- [Misi 2](#misi-2)
  - Soal 1
  - Soal 2
  - Soal 3

## Topologi
  ![WhatsApp Image 2024-12-01 at 20 19 44_f8bdf508](https://github.com/user-attachments/assets/42fec390-de12-41b7-a2c8-c35c0aa9c588)

## Rute  
  https://docs.google.com/spreadsheets/d/13zPTL2jgMoY6ygcwE4Qbuzff5Y9avR5I0j0EcIDCU6g/edit?usp=sharing 
  
  ![image](https://github.com/user-attachments/assets/4e8dd6a0-982a-4352-9a1b-078d60330587)

## Tree
  ![Tree Modul 5 drawio](https://github.com/user-attachments/assets/402d97ea-8002-4142-89c3-7b52d3e1e8a8)

## Pembagian IP VLSM
  Pengurutan Kebutuhan
  | Netmask  | Subnet  |
  |--|--|
  |/24 | A2 |
  |/25 | A4 |
  |/26 | A8 |
  |/29 | A3 |
  |/29 | A6 |
  |/29 | A7 |
  |/30 | A1 | 
  |/30 | A5 |
  |/30 | A9 |

  ![image](https://github.com/user-attachments/assets/03fe02a9-c979-4924-8e7e-18f0ea81df66)


  ## Konfigurasi
  ### NewEridu (Router)
  ```
  auto eth0
  iface eth0 inet dhcp

  # A1
  auto eth2
  iface eth2 inet static
	  address 10.65.1.217
	  netmask 255.255.255.252

# A5
auto eth1
iface eth1 inet static
	address 10.65.1.221
	netmask 255.255.255.252

up echo nameserver 192.168.122.1 > /etc/resolv.conf

# RIGHT
post-up route add -net 10.65.0.0 netmask 255.255.255.0 gw 10.65.1.218
post-up route add -net 10.65.1.192 netmask 255.255.255.248 gw 10.65.1.218
post-up route add -net 10.65.1.0 netmask 255.255.255.128 gw 10.65.1.218

# LEFT
post-up route add -net 10.65.1.200 netmask 255.255.255.248 gw 10.65.1.222
post-up route add -net 10.65.1.208 netmask 255.255.255.248 gw 10.65.1.222
post-up route add -net 10.65.1.128 netmask 255.255.255.192 gw 10.65.1.222
post-up route add -net 10.65.1.224 netmask 255.255.255.252 gw 10.65.1.222

```

### LuminaSquare (Router)
```
# A1
auto eth0
iface eth0 inet static
	address 10.65.1.218
	netmask 255.255.255.252
	gateway 10.65.1.217

# A2
auto eth2
iface eth2 inet static
	address 10.65.0.1
	netmask 255.255.255.0

# A3
auto eth1
iface eth1 inet static
	address 10.65.1.193
	netmask 255.255.255.248

up echo nameserver 192.168.122.1 > /etc/resolv.conf

post-up route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.65.1.217
post-up route add -net 10.65.1.0 netmask 255.255.255.128 gw 10.65.1.194 # A4
```

### Jane (Client)
```
auto eth0
iface eth0 inet dhcp
```

### Policeboo (Client)
```
auto eth0
iface eth0 inet dhcp
```

### HIA (Webserver)
```
# A3
auto eth0
iface eth0 inet static
	address 10.65.1.195
	netmask 255.255.255.248
  	gateway 10.65.1.193

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### BalletTwins (Router)
```
# A3
auto eth0
iface eth0 inet static
	address 10.65.1.194
	netmask 255.255.255.248
  	gateway 10.65.1.193

# A4
auto eth1
iface eth1 inet static
  	address 10.65.1.1
	netmask 255.255.255.128

up echo nameserver 192.168.122.1 > /etc/resolv.conf

post-up route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.65.1.192
```

### Ellen (Client)
```
auto eth0
iface eth0 inet dhcp
```

### Lycaon (Client)
```
auto eth0
iface eth0 inet dhcp
```

### SixStreet (Router)
```
# A5
auto eth0
iface eth0 inet static
	address 10.65.1.222
	netmask 255.255.255.252
	gateway 10.65.1.221

# A6
auto eth2
iface eth2 inet static
	address 10.65.1.201
	netmask 255.255.255.248

# A7
auto eth1
iface eth1 inet static
	address 10.65.1.209
	netmask 255.255.255.248

up echo nameserver 192.168.122.1 > /etc/resolv.conf

post-up route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.65.1.221
post-up route add -net 10.65.1.128 netmask 255.255.255.192 gw 10.65.1.210 # A8
post-up route add -net 10.65.1.224 netmask 255.255.255.252 gw 10.65.1.211 # A9
```

### Fairy (DHCP Server)
```
# A6
auto eth0
iface eth0 inet static
	address 10.65.1.202
	netmask 255.255.255.248
	gateway 10.65.1.201

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### HDD (DNS Server)
```
# A6
auto eth0
iface eth0 inet static
	address 10.65.1.203
	netmask 255.255.255.248
	gateway 10.65.1.201

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### OuterRing (Router)
```
# A7
auto eth0
iface eth0 inet static
	address 10.65.1.210
	netmask 255.255.255.248
	gateway 10.65.1.209

# A8
auto eth1
iface eth1 inet static
	address 10.65.1.129
	netmask 255.255.255.192

up echo nameserver 192.168.122.1 > /etc/resolv.conf

post-up route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.65.1.209
post-up route add -net 10.65.1.224 netmask 255.255.255.252 gw 10.65.1.211 # A9
```

### Burnice (Client)
```
auto eth0
iface eth0 inet dhcp
```

### Caesar (Client)
```
auto eth0
iface eth0 inet dhcp
```

### ScootOutpost (Router)
```
# A7
auto eth0
iface eth0 inet static
	address 10.65.1.211
	netmask 255.255.255.248
	gateway 10.65.1.209

# A9
auto eth1
iface eth1 inet static
	address 10.65.1.225
	netmask 255.255.255.252

up echo nameserver 192.168.122.1 > /etc/resolv.conf

post-up route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.65.1.209
post-up route add -net 10.65.1.128 netmask 255.255.255.192 gw 10.65.1.210 # A8
```

### HollowZero (Webserver)
```
# A9
auto eth0
iface eth0 inet static
	address 10.65.1.226
	netmask 255.255.255.252
	gateway 10.65.1.225

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```


## Misi 1
### Soal 4
>Fairy/dhcpsever.sh
  ```
apt-get update && apt-get install isc-dhcp-server -y

echo 'INTERFACESv4="eth0"' > /etc/default/isc-dhcp-server

echo '
# A2 (Jane & Policeboo)
subnet 10.65.0.0 netmask 255.255.255.0 {
  range 10.65.0.2 10.65.0.254;
  option routers 10.65.0.1;
  option broadcast-address 10.65.0.255;
  option domain-name-servers 10.65.1.203;
}
# A4 (Ellen & Lycaon)
subnet 10.65.1.0 netmask 255.255.255.128 {
  range 10.65.1.2 10.65.1.126;
  option routers 10.65.1.1;
  option broadcast-address 10.65.1.127;
  option domain-name-servers 10.65.1.203;
}

# A8 (Caesar & Burnice)
subnet 10.65.1.128 netmask 255.255.255.192 {
  range 10.65.1.130 10.65.1.190;
  option routers 10.65.1.129;
  option broadcast-address 10.65.1.191;
  option domain-name-servers 10.65.1.203;
}

# A6 (Fairy & HDD)
subnet 10.65.1.200 netmask 255.255.255.248{
  range 10.65.1.202 10.65.1.206;
  option routers 10.65.1.201;
  option broadcast-address 10.65.1.207;
  option domain-name-servers 10.65.1.203;
}
' > /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```

>LuminaSquare, BalletTwins, SixStreet, OuterRing/dhcprelay.sh
  ```
apt-get update && apt-get install isc-dhcp-relay -y

echo 'SERVERS="10.65.1.202"
INTERFACES="eth0 eth1 eth2 eth3"
OPTIONS=""
' > /etc/default/isc-dhcp-relay

echo 'net.ipv4.ip_forward=1' >> /etc/sysctl.conf

service isc-dhcp-relay restart
```

>HDD/dnserver.sh
  ```
apt-get update && apt-get install bind9 -y

echo 'options {
        directory "/var/cache/bind";

        forwarders {
                192.168.122.1;
        };

        // dnssec-validation auto;
        allow-query{any;};
        auth-nxdomain no;
        listen-on-v6 { any; };
}; ' >/etc/bind/named.conf.options

service bind9 restart
```

>HIA, HollowZero/webserver.sh
  ```
apt-get update && apt-get install apache2 -y

service apache2 start

echo 'Welcome to {hostname}' > /var/www/html/index.html

service apache2 restart
```


## Misi 2
### Soal 1
  Agar jaringan di New Eridu bisa terhubung ke luar (internet), kalian perlu mengkonfigurasi routing menggunakan iptables. Namun, kalian tidak diperbolehkan menggunakan MASQUERADE.
>NewEridu/eridu1.sh
  ```
  ETH0_IP=$(ip -4 addr show eth0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}')
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source $ETH0_IP
  ```

### Soal 2
  Karena Fairy adalah Al yang sangat berharga, kalian perlu memastikan bahwa tidak ada perangkat lain yang bisa melakukan ping ke Fairy. Tapi Fairy tetap dapat mengakses seluruh perangkat.
>Fairy/fairy2.sh
  ```
iptables -A INPUT -p icmp --icmp-type echo-request -j DROP 
iptables -A OUTPUT -p icmp --icmp-type echo-request -j ACCEPT 
```
- Fairy ke node lain (bisa)

  <img width="461" alt="Screenshot 2024-12-04 063342" src="https://github.com/user-attachments/assets/88ac4603-d495-47c6-8c72-3bae5b91c934">

- Node lain ke fairy (tidak bisa)

  <img width="464" alt="Screenshot 2024-12-04 064120" src="https://github.com/user-attachments/assets/b28e50a5-b7b4-4b01-98c4-adebb469e59b">

### Soal 3
