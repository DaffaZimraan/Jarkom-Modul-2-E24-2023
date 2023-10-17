# Jarkom-Modul-2-E24-2023
## Anggota Kelompok
1. Daffa Zimraan Hasan (5025221223)
2. Wardatul Amalia Safitri (5025211006)

## Soal 1
### Pertanyaan
>Yudhistira akan digunakan sebagai DNS Master, Werkudara sebagai DNS Slave, Arjuna merupakan Load Balancer yang terdiri dari beberapa Web Server yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Buatlah topologi dengan pembagian sebagai berikut. Folder topologi dapat diakses pada drive berikut 

### Penyelesaian
Berikut topologi yang kami gunakan:</br>
![topologi](https://github.com/DaffaZimraan/Jarkom-Modul-2-E24-2023/raw/main/image/topologi.jpg)</br>

Konfigurasi Pandudewanata:
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.218.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 192.218.2.1
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 192.218.3.1
	netmask 255.255.255.0
```
Konfigurasi Nakula:
```
auto eth0
iface eth0 inet static
	address 192.218.1.2
	netmask 255.255.255.0
	gateway 192.218.1.1
```
Konfigurasi Sadewa:
```
auto eth0
iface eth0 inet static
	address 192.218.1.3
	netmask 255.255.255.0
	gateway 192.218.1.1
```
Konfigurasi Yudhistira:
```
auto eth0
iface eth0 inet static
	address 192.218.1.4
	netmask 255.255.255.0
	gateway 192.218.1.1
```
Konfigurasi Werkudara:
```
auto eth0
iface eth0 inet static
	address 192.218.1.5
	netmask 255.255.255.0
	gateway 192.218.1.1
```
Konfigurasi Arjuna:
```
auto eth0
iface eth0 inet static
	address 192.218.2.2
	netmask 255.255.255.0
	gateway 192.218.2.1
```
Konfigurasi Prabakusuma:
```
auto eth0
iface eth0 inet static
	address 192.218.3.2
	netmask 255.255.255.0
	gateway 192.218.3.1
```
Konfigurasi Abimanyu:
```
auto eth0
iface eth0 inet static
	address 192.218.3.3
	netmask 255.255.255.0
	gateway 192.218.3.1
```
Konfigurasi Wisanggeni:
```
auto eth0
iface eth0 inet static
	address 192.218.3.4
	netmask 255.255.255.0
	gateway 192.218.3.1
```

## Soal 2
### Pertanyaan
>Buatlah website utama pada node arjuna dengan akses ke arjuna.yyy.com dengan alias www.arjuna.yyy.com dengan yyy merupakan kode kelompok.

### Penyelesaian
Tambahkan config sebagai berikut di **/etc/bind/named.conf.local** yudhistira:
```
echo 'zone "arjuna.e24.com" {
	type master;
	file "/etc/bind/jarkom/arjuna.e24.com";
};' > /etc/bind/named.conf.local
```
Kemudian tambahkan config berikut pada file **/etc/bind/jarkom/arjuna.e24.com** di node Yudhistira:
```
mkdir -p /etc/bind/jarkom
cp /etc/bind/db.local /etc/bind/jarkom/arjuna.e24.com
sed -i 's/localhost/arjuna.e24.com/g' /etc/bind/jarkom/arjuna.e24.com
sed -i 's/127.0.0.1/192.218.2.2/g' /etc/bind/jarkom/arjuna.e24.com
echo 'www.arjuna.e24.com.	IN CNAME arjuna.e24.com.' >> /etc/bind/jarkom/arjuna.e24.com
```
Berikut hasil ping **arjuna.yyy.com**:</br>
![ping-arjuna](https://github.com/DaffaZimraan/Jarkom-Modul-2-E24-2023/raw/main/image/ping-arjuna.jpg)</br>

## Soal 3
### Pertanyaan
>Dengan cara yang sama seperti soal nomor 2, buatlah website utama dengan akses ke abimanyu.yyy.com dan alias www.abimanyu.yyy.com.

### Penyelesaian
Tambahkan config sebagai berikut di **/etc/bind/named.conf.local** yudhistira:
```
echo 'zone "abimanyu.e24.com" { 
	type master;
	file "/etc/bind/jarkom/abimanyu.e24.com";
};' >> /etc/bind/named.conf.local
```
Kemudian tambahkan config berikut pada file **/etc/bind/jarkom/abimanyu.e24.com** di node Yudhistira:
```
mkdir -p /etc/bind/jarkom
cp /etc/bind/db.local /etc/bind/jarkom/abimanyu.e24.com
sed -i 's/localhost/abimanyu.e24.com/g' /etc/bind/jarkom/abimanyu.e24.com
sed -i 's/127.0.0.1/192.218.3.3/g' /etc/bind/jarkom/abimanyu.e24.com
echo 'www.abimanyu.e24.com.	IN CNAME abimanyu.e24.com.' >> /etc/bind/jarkom/abimanyu.e24.com
```
Berikut hasil ping **abimanyu.yyy.com:**</br>
![ping-abimanyu](https://github.com/DaffaZimraan/Jarkom-Modul-2-E24-2023/raw/main/image/ping-abimanyu.jpg)</br>

## Soal 4
### Pertanyaan
>Kemudian, karena terdapat beberapa web yang harus di-deploy, buatlah subdomain parikesit.abimanyu.yyy.com yang diatur DNS-nya di Yudhistira dan mengarah ke Abimanyu.
### Penyelesaian
Tambahkan config berikut pada file **/etc/bind/jarkom/abimanyu.e24.com**:
```
echo 'parikesit       IN      A       192.218.3.3' >> /etc/bind/jarkom/abimanyu.e24.com
echo 'www.parikesit       IN      CNAME       abimanyu.e24.com.' >> /etc/bind/jarkom/abimanyu.e24.com
```
Berikut hasil ping **parikesit.abimanyu.yyy.com**:
![ping-parikesit](https://github.com/DaffaZimraan/Jarkom-Modul-2-E24-2023/raw/main/image/ping-parikesit.jpg)</br>

## Soal 5
### Pertanyaan
>Buat juga reverse domain untuk domain utama. (Abimanyu saja yang direverse)
### Penyelesaian
Tambahkan config sebagai berikut di **/etc/bind/named.conf.local** yudhistira
```
echo 'zone "3.218.192.in-addr.arpa" {
	type master;
	file "/etc/bind/jarkom/3.218.192.in-addr.arpa";
};' >> /etc/bind/named.conf.local
```
Kemudian tambahkan config berikut pada file **/etc/bind/jarkom/3.218.192.in-addr.arpa** di node Yudhistira
```
cp /etc/bind/db.local /etc/bind/jarkom/3.218.192.in-addr.arpa
sed -i 's/localhost/abimanyu.e24.com/g' /etc/bind/jarkom/3.218.192.in-addr.arpa
sed -i 's/127.0.0.1/192.218.3.3/g' /etc/bind/jarkom/3.218.192.in-addr.arpa
echo '3.218.192.in-addr.arpa.	IN NS abimanyu.e24.com.' >> /etc/bind/jarkom/3.218.192.in-addr.arpa
echo '3				IN PTR abimanyu.e24.com.' >> /etc/bind/jarkom/3.218.192.in-addr.arpa
```
Berikut hasil reverse domain abimanyu:</br>
![reverse-abimanyu](https://github.com/DaffaZimraan/Jarkom-Modul-2-E24-2023/raw/main/image/reverse-abimanyu.jpg)</br>


## Soal 6
### Pertanyaan
>Agar dapat tetap dihubungi ketika DNS Server Yudhistira bermasalah, buat juga Werkudara sebagai DNS Slave untuk domain utama.
### Penyelesaian
Tambahkan config sebagai berikut di **/etc/bind/named.conf.local** yudhistira
```
echo '        notify yes;' >> /etc/bind/named.conf.local
echo '        also-notify { 192.218.1.5; };' >> /etc/bind/named.conf.local
echo '        allow-transfer { 192.218.1.5; };' >> /etc/bind/named.conf.local
```
Kemudian tambahkan config sebagai berikut di **/etc/bind/named.conf.local** Werkudara
```
echo 'zone "arjuna.e24.com" {
	type slave;
	masters { 192.218.1.4; };
	file "/var/lib/bind/arjuna.e24.com";
};' >> /etc/bind/named.conf.local

echo 'zone "abimanyu.e24.com" {
	type slave;
	masters { 192.218.1.4; };
	file "/var/lib/bind/abimanyu.e24.com";
};' >> /etc/bind/named.conf.local
```

Berikut hasil ping abimanyu.yyy.com dengan service bind9 pada DNS Master dimatikan:
![bind9-stop](https://github.com/DaffaZimraan/Jarkom-Modul-2-E24-2023/raw/main/image/bind9-stop.jpg)</br>
![ping-dnsslave](https://github.com/DaffaZimraan/Jarkom-Modul-2-E24-2023/raw/main/image/ping-dnsslave.jpg)</br>


## Soal 7
### Pertanyaan
>Seperti yang kita tahu karena banyak sekali informasi yang harus diterima, buatlah subdomain khusus untuk perang yaitu baratayuda.abimanyu.yyy.com dengan alias www.baratayuda.abimanyu.yyy.com yang didelegasikan dari Yudhistira ke Werkudara dengan IP menuju ke Abimanyu dalam folder Baratayuda.

### Penyelesaian
Tambahkan nameserver baru `ns1` pada file /etc/bind/jarkom/abimanyu.e24.com melalui yudhistira
```
echo 'ns1     IN      A       192.218.3.3' >> /etc/bind/jarkom/abimanyu.e24.com
echo 'baratayuda        IN      NS      ns1' >> /etc/bind/jarkom/abimanyu.e24.com
```
Setelah menambahkan nameserver, kita akan menambahkan potongan kode yaitu `allow-query{any;};` di Yudhistira maupun Werkudara pada file **/etc/bind/named.conf.options**
```
echo 'options {
	directory "/var/cache/bind";
allow-query{any;};
auth-nxdomain no;   
listen-on-v6 { any; };
};' > /etc/bind/named.conf.options
```


## Soal 8
### Pertanyaan
>Untuk informasi yang lebih spesifik mengenai Ranjapan Baratayuda, buatlah subdomain melalui Werkudara dengan akses rjp.baratayuda.abimanyu.yyy.com dengan alias www.rjp.baratayuda.abimanyu.yyy.com yang mengarah ke Abimanyu.
### Penyelesaian

## Soal 9
### Pertanyaan
### Penyelesaian

## Soal 10
### Pertanyaan
### Penyelesaian

## Soal 11
### Pertanyaan
### Penyelesaian

## Soal 12
### Pertanyaan
### Penyelesaian

## Soal 13
### Pertanyaan
### Penyelesaian

## Soal 14
### Pertanyaan
### Penyelesaian

## Soal 15
### Pertanyaan
### Penyelesaian

## Soal 16
### Pertanyaan
### Penyelesaian

## Soal 17
### Pertanyaan
### Penyelesaian

## Soal 18
### Pertanyaan
### Penyelesaian

## Soal 19
### Pertanyaan
### Penyelesaian

## Soal 20
### Pertanyaan
### Penyelesaian

