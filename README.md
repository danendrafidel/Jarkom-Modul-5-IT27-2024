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

| **Subnet** | **Jumlah IP** | **Netmask** | **Network ID** | **Broadcast** | **Range IP**              | **Subnet Mask** |
| ---------- | ------------- | ----------- | -------------- | ------------- | ------------------------- | --------------- |
| A1         | 2             | /30         | 10.77.0.0      | 10.77.0.3     | 10.77.0.1 - 10.77.0.2     | 255.255.255.252 |
| A2         | 2             | /30         | 10.77.0.4      | 10.77.0.7     | 10.77.0.5 - 10.77.0.6     | 255.255.255.252 |
| A3         | 3             | /29         | 10.77.0.8      | 10.77.0.15    | 10.77.0.9 - 10.77.0.14    | 255.255.255.248 |
| A4         | 121           | /25         | 10.77.0.128    | 10.77.0.255   | 10.77.0.129 - 10.77.0.254 | 255.255.255.128 |
| A5         | 231           | /24         | 10.77.1.0      | 10.77.1.255   | 10.77.1.1 - 10.77.1.254   | 255.255.255.0   |
| A6         | 3             | /29         | 10.77.1.144    | 10.77.1.151   | 10.77.1.145 - 10.77.1.150 | 255.255.255.248 |
| A7         | 3             | /29         | 10.77.1.152    | 10.77.1.159   | 10.77.1.153 - 10.77.1.158 | 255.255.255.248 |
| A8         | 56            | /26         | 10.77.1.192    | 10.77.1.255   | 10.77.1.193 - 10.77.1.254 | 255.255.255.192 |
| A9         | 2             | /30         | 10.77.1.224    | 10.77.1.227   | 10.77.1.225 - 10.77.1.226 | 255.255.255.252 |

## TOPOLOGI SETELAH PEMBAGIAN SUBNET DAN TREE

![alt text](<img/Topologi Setelah Subnet.png>)
