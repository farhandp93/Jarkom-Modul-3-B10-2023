# Jarkom-Modul-3-B10-2023

**Praktikum Jaringan Komputer Modul 3 Tahun 2023**

Anggota :

Farhan Dwi Putra (5025211093)

Yusuf Hasan Nazila (5025211225)

# Laporan Resmi

## Topologi
![Screenshot (115)](https://github.com/farhandp93/Jarkom-Modul-3-B10-2023/assets/128909158/a7d8f028-c409-48f0-9cbd-4fc14dc25df5)

Aura Router (DHCP Relay)
```
auto eth0
iface eth0 inet dhcp
auto eth1
iface eth1 inet static
address 192.183.1.0
netmask 255.255.255.0
auto eth2
iface eth2 inet static
address 192.183.2.0
netmask 255.255.255.0
auto eth3
iface eth3 inet static
address 192.183.3.0
netmask 255.255.255.0
auto eth4
iface eth4 inet static
address 192.183.4.0
netmask 255.255.255.0
```
Himmel DHCP Server
```
auto eth0
iface eth0 inet static
address 192.183.1.1
netmask 255.255.255.0
gateway 192.183.1.0
```
Heiter DNS Server
```
auto eth0
iface eth0 inet static
address 192.183.1.2
netmask 255.255.255.0
gateway 192.183.1.0

```
Denken Database Server
```
auto eth0
iface eth0 inet static
address 192.183.2.1
netmask 255.255.255.0
gateway 192.183.2.0
```
Eisen Load Balancer
```
auto eth0
iface eth0 inet static
address 192.183.2.2
netmask 255.255.255.0
gateway 192.183.2.0
```
Frieren Laravel Worker
```
auto eth0
iface eth0 inet static
address 192.183.4.1
netmask 255.255.255.0
gateway 192.183.4.0
```
Flamme Laravel Worker
```
auto eth0
iface eth0 inet static
address 192.183.4.2
netmask 255.255.255.0
gateway 192.183.4.0
```
Fern Laravel Worker
```
auto eth0
iface eth0 inet static
address 192.183.4.3
netmask 255.255.255.0
gateway 192.183.4.0
```
Lawine PHP Worker
```

auto eth0
iface eth0 inet static
address 192.183.3.1
netmask 255.255.255.0
gateway 192.183.3.0
```
Linie PHP Worker
```
auto eth0
iface eth0 inet static
address 192.183.3.2
netmask 255.255.255.0
gateway 192.183.3.0
```
Lugner PHP Worker
```
auto eth0
iface eth0 inet static
address 192.183.3.3
netmask 255.255.255.0
gateway 192.183.3.0
```
Revolte Client
```
auto eth0
iface eth0 inet dhcp
```
Richter Client
```
auto eth0
iface eth0 inet dhcp
```
Sein Client
```
auto eth0
iface eth0 inet dhcp
```
Stark Client
```
auto eth0
iface eth0 inet dhcp
```

## Soal 1
```
auto eth0
iface eth0 inet static
	address 192.183.3.1
	netmask 255.255.255.0
	gateway 192.183.3.0
```
- **Fern (Laravel Worker)**
```
auto eth0
iface eth0 inet static
	address 192.183.4.1
	netmask 255.255.255.0
	gateway 192.183.4.0
```
### Script
```sh
echo 'zone "riegel.canyon.b10.com" {
    type master;
    file "/etc/bind/sites/riegel.canyon.b10.com";
};

zone "granz.channel.b10.com" {
    type master;
    file "/etc/bind/sites/granz.channel.b10.com";
};

zone "1.183.192.in-addr.arpa" {
    type master;
    file "/etc/bind/sites/1.183.192.in-addr.arpa";
};' > /etc/bind/named.conf.local

mkdir -p /etc/bind/sites
cp /etc/bind/db.local /etc/bind/sites/riegel.canyon.b10.com
cp /etc/bind/db.local /etc/bind/sites/granz.channel.b10.com
cp /etc/bind/db.local /etc/bind/sites/1.183.192.in-addr.arpa

echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     riegel.canyon.b10.com. root.riegel.canyon.b10.com. (
                        2023111401      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      riegel.canyon.b10.com.
@       IN      A       192.183.4.1     ; IP Fern
www     IN      CNAME   riegel.canyon.b10.com.' > /etc/bind/sites/riegel.canyon.b10.com

echo '
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     granz.channel.b10.com. root.granz.channel.b10.com. (
                        2023111401      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      granz.channel.b10.com.
@       IN      A       192.183.3.1     ; IP Lugner
www     IN      CNAME   granz.channel.b10.com.' > /etc/bind/sites/granz.channel.b10.com

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

service bind9 start
```
## Result
![WhatsApp Image 2023-11-19 at 1 01 58 PM](https://github.com/farhandp93/Jarkom-Modul-3-B10-2023/assets/128909158/e2e44c36-90ad-4402-bf63-64193a7c0fed)
![WhatsApp Image 2023-11-19 at 1 02 10 PM](https://github.com/farhandp93/Jarkom-Modul-3-B10-2023/assets/128909158/377111e8-4fa0-4e56-a012-6afc37830beb)

## Soal 2
### Script 
```sh
echo 'subnet 192.183.1.0 netmask 255.255.255.0 {
}

subnet 192.183.2.0 netmask 255.255.255.0 {
}

subnet 192.183.3.0 netmask 255.255.255.0 {
    range 192.183.3.16 192.183.3.32;
    range 192.183.3.64 192.183.3.80;
    option routers 192.183.3.0;
}' > /etc/dhcp/dhcpd.conf
```

## Soal 3
### Script 
```sh
echo 'subnet 192.183.1.0 netmask 255.255.255.0 {
}

subnet 192.183.2.0 netmask 255.255.255.0 {
}

subnet 192.183.3.0 netmask 255.255.255.0 {
    range 192.183.3.16 192.183.3.32;
    range 192.183.3.64 192.183.3.80;
    option routers 192.183.3.0;
}

subnet 192.183.4.0 netmask 255.255.255.0 {
    range 192.183.4.12 192.183.4.20;
    range 192.183.4.160 192.183.4.168;
    option routers 192.183.4.0;
} ' > /etc/dhcp/dhcpd.conf
```

## Soal 4
### Script
```sh 
subnet 192.183.3.0 netmask 255.255.255.0 {
    ...
    option broadcast-address 192.183.3.255;
    option domain-name-servers 192.183.1.2;
    ...
}

subnet 192.183.4.0 netmask 255.255.255.0 {
    option broadcast-address 192.183.4.255;
    option domain-name-servers 192.183.1.2;
} 
```

Gunakan ``shell`` script

```sh
echo 'subnet 192.183.1.0 netmask 255.255.255.0 {
}

subnet 192.183.2.0 netmask 255.255.255.0 {
}

subnet 192.183.3.0 netmask 255.255.255.0 {
    range 192.183.3.16 192.183.3.32;
    range 192.183.3.64 192.183.3.80;
    option routers 192.183.3.0;
    option broadcast-address 192.183.3.255;
    option domain-name-servers 192.183.1.2;
}

subnet 192.183.4.0 netmask 255.255.255.0 {
    range 192.183.4.12 192.183.4.20;
    range 192.183.4.160 192.183.4.168;
    option routers 192.183.4.0;
    option broadcast-address 192.183.4.255;
    option domain-name-servers 192.183.1.2;
} ' > /etc/dhcp/dhcpd.conf

service isc-dhcp-server start
```

Lakukan setup untuk DHCP Relay, jalankan command dibawah ini di DHCP Relay
```sh
echo '
SERVERS="192.183.1.1"
INTERFACES="eth1 eth2 eth3 eth4"
OPTIONS=""' > /etc/default/isc-dhcp-relay

service isc-dhcp-relay start 
```
![WhatsApp Image 2023-11-19 at 13 27 54_7c930469](https://github.com/farhandp93/Jarkom-Modul-3-B10-2023/assets/114125438/08f52319-3ec3-4c4b-8e4e-0f4a1e12843b)

Lalu pada file ``/etc/sysctl.conf`` lakukan uncommented pada ``net.ipv4.ip_forward=1``

Restart seluruh client untuk dapat melakukan leasing IP dari DHCP Server
### Result

## Soal 5
### Script
```sh
echo 'subnet 192.183.1.0 netmask 255.255.255.0 {
}

subnet 192.183.2.0 netmask 255.255.255.0 {
}

subnet 192.183.3.0 netmask 255.255.255.0 {
    range 192.183.3.16 192.183.3.32;
    range 192.183.3.64 192.183.3.80;
    option routers 192.183.3.0;
    option broadcast-address 192.183.3.255;
    option domain-name-servers 192.183.1.2;
    default-lease-time 180;
    max-lease-time 5760;
}

subnet 192.183.4.0 netmask 255.255.255.0 {
    range 192.183.4.12 192.183.4.20;
    range 192.183.4.160 192.183.4.168;
    option routers 192.183.4.0;
    option broadcast-address 192.183.4.255;
    option domain-name-servers 192.183.1.2;
    default-lease-time 720;
    max-lease-time 5760;
}

service isc-dhcp-server restart
```
### Result
![image](https://github.com/farhandp93/Jarkom-Modul-3-B10-2023/assets/114125438/c14090e5-069b-4816-999a-9b9180b20145)
![image](https://github.com/farhandp93/Jarkom-Modul-3-B10-2023/assets/114125438/916e1286-a62f-4d50-a995-8ec3c04ba110)


## Soal 6
```sh
wget -O '/var/www/granz.channel.b10.com' 'https://drive.google.com/u/0/uc?id=1ViSkRq7SmwZgdK64eRbr5Fm1EGCTPrU1&export=download'
unzip -o /var/www/granz.channel.b10.com -d /var/www/
rm /var/www/granz.channel.b10.com
mv /var/www/modul-3 /var/www/granz.channel.b1o.com 
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/granz.channel.b10.com
ln -s /etc/nginx/sites-available/granz.channel.b10.com /etc/nginx/sites-enabled/
rm /etc/nginx/sites-enabled/default

echo 'server {
    listen 80;
    server_name _;

    root /var/www/granz.channel.b10.com;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.3-fpm.sock; 
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}' > /etc/nginx/sites-available/granz.channel.b10.com

service nginx restart
```

### Result 
![image](https://github.com/farhandp93/Jarkom-Modul-3-B10-2023/assets/114125438/77160555-4c1c-44e2-b256-e862c4297a1d)

## Soal 7
### Script
```sh
echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     riegel.canyon.b10.com. root.riegel.canyon.b10.com. (
                        2023111401      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      riegel.canyon.b10.com.
@       IN      A       192.183.2.2     ; IP LB Eisen
www     IN      CNAME   riegel.canyon.b10.com.' > /etc/bind/sites/riegel.canyon.b10.com

echo '
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     granz.channel.b10.com. root.granz.channel.b10.com. (
                        2023111401      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      granz.channel.b10.com.
@       IN      A       192.183.2.2     ; IP LB Eisen
www     IN      CNAME   granz.channel.b10.com.' > /etc/bind/sites/granz.channel.b10.com
```
```sh 
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/lb_php

echo ' upstream worker {
    server 192.183.3.1;
    server 192.183.3.2;
    server 192.183.3.3;
}

server {
    listen 80;
    server_name granz.channel.b10.com www.granz.channel.b10.com;

    root /var/www/html;

    index index.html index.htm index.nginx-debian.html;

    server_name _;

    location / {
        proxy_pass http://worker;
    }
} ' > /etc/nginx/sites-available/lb_php

ln -s /etc/nginx/sites-available/lb_php /etc/nginx/sites-enabled/
rm /etc/nginx/sites-enabled/default

service nginx restart
```

### Result
Jalankan perintah berikut pada client ``Revolte``
```sh
ab -n 1000 -c 100 http://www.granz.channel.b10.com/ 
```
![image](https://github.com/farhandp93/Jarkom-Modul-3-B10-2023/assets/114125438/1bdf8076-c899-45c8-914c-80a5e0bc4b23)

Requests per second:     2019.86 [#/sec] (mean)


## Soal 8
### Script
Jalankan perintah berikut pada client ``Revolte``
```sh
ab -n 200 -c 10 http://www.granz.channel.b10.com/ 
```
#### Round Robin
![image](https://github.com/farhandp93/Jarkom-Modul-3-B10-2023/assets/114125438/08483f71-950d-42fa-81b3-95be6800893d)
![image](https://github.com/farhandp93/Jarkom-Modul-3-B10-2023/assets/114125438/cd3ed56d-74b7-4a2f-a2b2-d9235b842baa)

#### Least Connection
![image](https://github.com/farhandp93/Jarkom-Modul-3-B10-2023/assets/114125438/9dead566-e369-441a-a81a-f1da0f717233)
![image](https://github.com/farhandp93/Jarkom-Modul-3-B10-2023/assets/114125438/a02ae385-9ba9-42a2-bb3e-75577678098f)

#### IP Hash
![image](https://github.com/farhandp93/Jarkom-Modul-3-B10-2023/assets/114125438/737e466c-9413-4bd5-8ba7-681a1fec2ff1)
![image](https://github.com/farhandp93/Jarkom-Modul-3-B10-2023/assets/114125438/58107d7d-e0f0-4d07-875a-313f0c61e3e0)

#### Generic Hash
![image](https://github.com/farhandp93/Jarkom-Modul-3-B10-2023/assets/114125438/56eb2549-302e-4f80-9480-af1a3d1894df)
![image](https://github.com/farhandp93/Jarkom-Modul-3-B10-2023/assets/114125438/24cb6a76-bf54-4ec8-9941-3149824a9d66)

#### Grafik
![image](https://github.com/farhandp93/Jarkom-Modul-3-B10-2023/assets/114125438/fedf7bab-ebe0-4444-bf85-04d64190c26f)


## Soal 9
### Script
Jalankan perintah berikut pada client ``Revolte``
```sh
ab -n 100 -c 10 http://www.granz.channel.b10.com/ 
```

### Result

## Soal 10
### Script
```sh 
mkdir /etc/nginx/rahasisakita
htpasswd -c /etc/nginx/rahasisakita/htpasswd netics
```
![image](https://github.com/farhandp93/Jarkom-Modul-3-B10-2023/assets/114125438/e21431b8-3f4a-4ce6-83fc-d431e5bb5ab7)

Masukkan password ``ajkb10``


```sh
auth_basic "Restricted Content";
auth_basic_user_file /etc/nginx/rahasisakita/htpasswd;
```

### Result
Saat mengakses url ``http://www.granz.channel.b10.com/`` terdapat unauthorized sebagai berikut



## Soal 11
Script /etc/nginx/sites-available/lb_php pada Eisen
![image](https://github.com/farhandp93/Jarkom-Modul-3-B10-2023/assets/114125438/8f586369-148b-4bae-bd05-fca1317ada09)

Tes dengan ``lynx www.granz.channel.b10.com/its`` di Client
![image](https://github.com/farhandp93/Jarkom-Modul-3-B10-2023/assets/114125438/59f3514c-3e6f-47c7-a2ed-f0926ed5b2b9)

## Soal 12
![image](https://github.com/farhandp93/Jarkom-Modul-3-B10-2023/assets/114125438/1007c538-d171-4dfe-96df-e8df8f3ca2bd)
IP (tidak allow) Deny
![image](https://github.com/farhandp93/Jarkom-Modul-3-B10-2023/assets/114125438/560f9bb1-722f-47e9-bd78-b97545f131cc)
FIXED address pada Himmel
![image](https://github.com/farhandp93/Jarkom-Modul-3-B10-2023/assets/114125438/b1e6dc91-e4e1-4a35-a530-6d6fe2d183cd)





