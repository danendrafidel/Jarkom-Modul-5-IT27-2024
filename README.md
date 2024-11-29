# Jarkom-Modul-5-IT27-2024

## IT 27

| No  | Nama Anggota          | NRP        |
| --- | --------------------- | ---------- |
| 1   | Danendra Fidel Khansa | 5027231063 |
| 2   | Farida Qurrotu A'yuna | 5027231015 |

## IP PREFIX

`10.77`

## TOPOLOGI GNS | VLSM |

![alt text](img/Topologi.png)

## RUTE SUBNET

| **Nama Subnet** | **Rute**                                      | **Jumlah IP** | **Netmask** |
| --------------- | --------------------------------------------- | ------------- | ----------- |
| A1              | NewEridu > SixStreet                          | 2             | /30         |
| A2              | NewEridu > LuminaSquare                       | 2             | /30         |
| A3              | LuminaSquare > Ofc.Mewmew > HIA > BalletTwins | 3             | /29         |
| A4              | BalletTwins > Victoria > Lycaon > Ellen       | 121           | /25         |
| A5              | LuminaSquare > Pubsec > Policeboo > Jane      | 231           | /24         |
| A6              | SixStreet > Metro1 > ScootOutpost > OuterRing | 3             | /29         |
| A7              | SixStreet > RandomPlay > Fairy > HDD          | 3             | /29         |
| A8              | OuterRing > SoC > Caesar > Burnice            | 56            | /26         |
| A9              | ScootOutpost > HollowZero                     | 2             | /30         |
| **Total**       |                                               | **423**       | **/23**     |

## TREE VLSM

![alt text](<img/VLSM Tree.png>)

## PEMBAGIAN IP | VLSM |

| Subnet | Jumlah IP | Netmask | Network ID  | Broadcast   | Range IP                  | Subnet Mask     |
| ------ | --------- | ------- | ----------- | ----------- | ------------------------- | --------------- |
| A1     | 2         | /30     | 10.72.0.0   | 10.72.0.3   | 10.72.0.1 - 10.72.0.2     | 255.255.255.252 |
| A2     | 2         | /30     | 10.72.0.4   | 10.72.0.7   | 10.72.0.5 - 10.72.0.6     | 255.255.255.252 |
| A3     | 3         | /29     | 10.72.0.8   | 10.72.0.15  | 10.72.0.9 - 10.72.0.14    | 255.255.255.248 |
| A4     | 121       | /25     | 10.72.0.128 | 10.72.0.255 | 10.72.0.129 - 10.72.0.254 | 255.255.255.128 |
| A5     | 231       | /24     | 10.72.1.0   | 10.72.1.255 | 10.72.1.1 - 10.72.1.254   | 255.255.255.0   |
| A6     | 3         | /29     | 10.72.2.0   | 10.72.2.7   | 10.72.2.1 - 10.72.2.6     | 255.255.255.248 |
| A7     | 3         | /29     | 10.72.2.8   | 10.72.2.15  | 10.72.2.9 - 10.72.2.14    | 255.255.255.248 |
| A8     | 56        | /26     | 10.72.2.64  | 10.72.2.127 | 10.72.2.65 - 10.72.2.126  | 255.255.255.192 |
| A9     | 2         | /30     | 10.72.2.128 | 10.72.2.131 | 10.72.2.129 - 10.72.2.130 | 255.255.255.252 |

## TOPOLOGI SETELAH PEMBAGIAN SUBNET DAN TREE

![alt text](<img/Topologi Setelah Subnet.png>)

## KONFIGURASI

### NEW ERIDU (ROUTER)

```
auto eth0
iface eth0 inet dhcp

#A1
auto eth1
iface eth1 inet static
  address 10.77.0.1
  netmask 255.255.255.252

#A2
auto eth2
iface eth2 inet static
  address 10.77.0.5
  netmask 255.255.255.252

iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.77.0.0/16

#A6
post-up route add -net 10.77.2.0 netmask 255.255.255.248 gw 10.77.0.2

#A3
post-up route add -net 10.77.0.8 netmask 255.255.255.248 gw 10.77.06

#A8
post-up route add -net 10.77.2.64 netmask 255.255.255.192 gw 10.77.0.2

#A7
post-up route add -net 10.77.2.8 netmask 255.255.255.248 gw 10.77.0.2

#A4
post-up route add -net 10.77.0.128 netmask 255.255.255.128 gw 10.77.0.6

#A5
post-up route add -net 10.77.1.0 netmask 255.255.255.0 gw 10.77.0.6

#A9
post-up route add -net 10.77.2.128 netmask 255.255.255.252 gw 10.77.0.2
```

### SixStreet (ROUTER DHCP RELAY)

```
#A1
auto eth0
iface eth0 inet static
  address 10.77.0.2
  netmask 255.255.255.252
  gateway 10.77.0.1

#A6
auto eth1
iface eth1 inet static
  address 10.77.2.1
  netmask 255.255.255.248

#A7
auto eth2
iface eth2 inet static
  address 10.77.2.9
  netmask 255.255.255.248

up echo nameserver 192.168.122.1 > /etc/resolv.conf

#A8
post-up route add -net 10.77.2.64 netmask 255.255.255.192 gw 10.77.2.3

#A9
post-up route add -net 10.77.2.128 netmask 255.255.255.252 gw 10.77.2.2

#A4
post-up route add -net 10.77.0.128 netmask 255.255.255.128 gw 10.77.0.1
```

### LuminaSquare (ROUTER DHCP RELAY)

```
#A2
auto eth0
iface eth0 inet static
  address 10.77.0.6
  netmask 255.255.255.252
  gateway 10.77.0.5

#A3
auto eth1
iface eth1 inet static
  address 10.77.0.9
  netmask 255.255.255.248

#A5
auto eth2
iface eth2 inet static
  address 10.77.1.1
  netmask 255.255.255.0

up echo nameserver 192.168.122.1 > /etc/resolv.conf

#A1
post-up route add -net 10.77.0.0 netmask 255.255.255.252 gw 10.77.0.5

#A4
post-up route add -net 10.77.0.128 netmask 255.255.255.128 gw 10.77.0.11

#A7
post-up route add -net 10.77.2.8 netmask 255.255.255.248 gw 10.77.0.5

```

### BalletTwins (ROUTER DHCP RELAY)

```
#A3
auto eth0
iface eth0 inet static
  address 10.77.0.11
  netmask 255.255.255.248
  gateway 10.77.0.9

#A4
auto eth1
iface eth1 inet static
  address 10.77.0.129
  netmask 255.255.255.128

up echo nameserver 192.168.122.1 > /etc/resolv.conf

#A2
post-up route add -net 10.77.0.4 netmask 255.255.255.252 gw 10.77.0.9

#A1
post-up route add -net 10.77.0.0 netmask 255.255.255.252 gw 10.77.0.9

#A7
post-up  route add -net 10.77.2.8 netmask 255.255.255.248 gw 10.77.0.9
```

### OuterRing (ROUTER DHCP RELAY)

```
#A6
auto eth0
iface eth0 inet static
  address 10.77.2.3
  netmask 255.255.255.248
  gateway 10.77.2.1

#A8
auto eth1
iface eth1 inet static
  address 10.77.2.65
  netmask 255.255.255.192

up echo nameserver 192.168.122.1 > /etc/resolv.conf

#A9
post-up route add -net 10.77.2.128 netmask 255.255.255.252 gw 10.77.2.2

#A1
post-up route add -net 10.77.0.0 netmask 255.255.255.252 gw 10.77.2.1

#A7
post-up route add -net 10.77.2.8 netmask 255.255.255.248 gw 10.77.2.1

```

### ScootOutpost (ROUTER)

```
#A6
auto eth0
iface eth0 inet static
  address 10.77.2.2
  netmask 255.255.255.248
  gateway 10.77.2.1

#A9
auto eth1
iface eth1 inet static
  address 10.77.2.65
  netmask 255.255.255.252

up echo nameserver 192.168.122.1 > /etc/resolv.conf

#A2
post-up route add -net 10.77.0.4 netmask 255.255.255.252 gw 10.77.2.1

#A8
post-up route add -net 10.77.2.16 netmask 255.255.255.192 gw 10.77.2.3

#A1
post-up  route add -net 10.77.0.0 netmask 255.255.255.252 gw 10.77.2.1

```

### Fairy (DHCP SERVER)

```
auto eth0
iface eth0 inet static
  address 10.77.2.11
  netmask 255.255.255.248
  gateway 10.77.2.9

up echo nameserver 192.168.122.1 > /etc/resolv.conf

#A8
post-up route add -net 10.77.2.16 netmask 255.255.255.192 gw 10.77.2.9

#POJOK KANAN BAWAH LYCAON
post-up route add -net 10.77.0.128 netmask 255.255.255.128 gw 10.77.2.9
```

### HDD (DNS SERVER)

```
auto eth0
iface eth0 inet static
  address 10.77.2.10
  netmask 255.255.255.248
  gateway 10.77.2.9

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### HollowZero (WEB SERVER)

```
auto eth0
iface eth0 inet static
  address 10.77.2.130
  netmask 255.255.255.252
  gateway 10.77.2.129

up echo nameserver 192.168.122.1 > /etc/resolv.conf

#A1
post-up route add -net 10.77.0.0 netmask 255.255.255.252 gw 10.77.2.129
```

### HIA (WEB SERVER)

```
auto eth0
iface eth0 inet static
  address 10.77.0.10
  netmask 255.255.255.248
  gateway 10.77.0.9

up echo nameserver 192.168.122.1 > /etc/resolv.conf

```

### Caesar (CLIENT)

```
auto eth0
iface eth0 inet dhcp

#Hollowzero
post-up route add -net 10.77.2.64 netmask 255.255.255.252 gw 10.77.2.65

#A1
post-up route add -net 10.77.0.0 netmask 255.255.255.252 gw 10.77.2.65
```

### Burnice (CLIENT)

```
auto eth0
iface eth0 inet dhcp

#Hollowzero
post-up route add -net 10.77.2.128 netmask 255.255.255.252 gw 10.77.2.65
```

### Jane, Policeboo, Ellen, Lycaon (CLIENT)

```
auto eth0
iface eth0 inet dhcp
```

## SETUP
