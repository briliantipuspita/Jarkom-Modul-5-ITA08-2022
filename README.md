# Jarkom-Modul-5-ITA08-2022

Pengerjaan soal shift jarkom modul 5 oleh ITA08

# Anggota

| Nama                           | NRP          | 
| -------------------------------| -------------| 
| Axellino Anggoro A.              | `5027201040` | 
| Mutiara Nuraisyah Dinda R            | `5027201054` | 
| Brilianti Puspita S.  | `5027201070` |

## A. topologi
membuat topologi dengan ketentuan 
Eden adalah DNS Server
WISE adalah DHCP Server
Garden dan SSS adalah Web Server
Jumlah Host pada Forger adalah 62 host
Jumlah Host pada Desmond adalah 700 host
Jumlah Host pada Blackbell adalah 255 host
Jumlah Host pada Briar adalah 200 host

## B. Perhitungan jumlah subnet

| subnet | jumlah IP    | Netmask   |
| -------| -------------| ----------|
| A3     |     `701`    |   `/22`   |
| A6     |     `256`    |   `/23`   |
| A7     |     `201`    |   `/24`   |
| A2     |     `63`     |   `/25`   |
| A1     |     `3`      |   `/29`   |
| A8     |     `3`      |   `/29`   |
| A4     |     `2`      |   `/30`   |
| A5     |     `2`      |   `/30`   |
|Total   |    `1231`    |   `/21`   |

## Pembagian IP
| No | Subnet | Network ID | Subnet Mask | Wildcard | IP Broadcast | 
| :---: | :---: | :---: | :---: | :---: | :---: |
| 1 | A3 | 192.190.4.0 | 255.255.252.0  | 0.0.3.255 | 192.190.7.255 |
| 2 | A7 | 192.190.2.0 | 255.255.254.0 | 0.0.1.255 | 192.190.3.255 |
| 3 | A6 | 192.190.1.0 | 255.255.255.0 | 0.0.0.255 | 192.190.1.255 |
| 4 | A2 | 192.190.0.128 | 255.255.255.128 | 0.0.0.127 | 192.190.0.255 |
| 5 | A1 | 192.190.0.16 | 255.255.255.248 | 0.0.0.7 | 192.190.0.23 |
| 6 | A8 | 192.190.0.24 | 255.255.255.248 | 0.0.0.7 | 192.190.0.31 |
| 7 | A4 | 192.190.0.0 | 255.255.255.252 | 0.0.0.3 | 192.190.0.3 |
| 8 | A5 | 192.190.0.4 | 255.255.255.252 | 0.0.0.3 | 192.190.0.7 |

## Network Configuration

    - strix
      ```
      auto eth0 
      iface eth0 inet dhcp

      auto eth1 #A4
      iface eth1 inet static
      address 192.213.7.145
      netmask 255.255.255.252

      auto eth2 #A5
      iface eth2 inet static
      address 192.213.7.149
      netmask 255.255.255.

      ```
     - Westalis
      ```
      auto eth0 #A4
      iface eth0 inet static
      address 192.213.7.146
      netmask 255.255.255.252

      auto eth1 #A1
      iface eth1 inet static
      address 192.213.7.129
      netmask 255.255.255.248

      auto eth2 #A3
      iface eth2 inet static
      address 192.213.0.1
      netmask 255.255.252.0

      auto eth3 #A2
      iface eth3 inet static
      address 192.213.7.1
      netmask 255.255.255.128
      ```
    - Ostania
      ```
      auto eth0 #A5
      iface eth0 inet static
      address 192.213.7.150
      netmask 255.255.255.252

      auto eth1 #A6
      iface eth1 inet static
      address  192.213.4.1
      netmask 255.255.254.0

      auto eth2 #A7
      iface eth2 inet static
      address  192.213.6.1
      netmask 255.255.255.0

      auto eth3 #A8
      iface eth3 inet static
      address  192.213.7.137
      netmask 255.255.255.248
      ```
   - Eden (DNS Server)
        ```
       auto eth0 #A1
       iface eth0 inet static
	     address 192.213.7.130
       netmask 255.255.255.248
       gateway 192.213.7.129
        ```
    - WISE (DHCP Server)
        ```
        auto eth0 #A1
        iface eth0 inet static
	      address 192.213.7.131
	      netmask 255.255.255.248
        gateway 192.213.7.129
        ```
   - Garden (WEB server)
        ```
        auto eth0 #A8
        iface eth0 inet static
        address 192.213.7.138
        netmask 255.255.255.248
        gateway 192.213.7.137
        ```
     
   - SSS (WEB server)
        ```
        auto eth0 #A8
        iface eth0 inet static
        address 192.213.7.139
        netmask 255.255.255.248
        gateway 192.213.7.137
        ```
        
        karena SSS dan Garden merupakan WEB server, maka akan diinstall apache2
        ```
        echo nameserver 192.168.122.1 > /etc/resolv.conf
        apt update
        apt install apache2 -y
        service apache2 start
        ```

