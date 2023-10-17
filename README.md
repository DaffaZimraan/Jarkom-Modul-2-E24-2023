# Jarkom-Modul-2-E24-2023
## Anggota Kelompok
1. Daffa Zimraan Hasan (5025221223)
2. Wardatul Amalia Safitri (5025211006)

## Soal 1
### Pertanyaan
>Yudhistira akan digunakan sebagai DNS Master, Werkudara sebagai DNS Slave, Arjuna merupakan Load Balancer yang terdiri dari beberapa Web Server yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Buatlah topologi dengan pembagian sebagai berikut. Folder topologi dapat diakses pada drive berikut 

### Penyelesaian
Berikut topologi yang kami gunakan:</br>
![ping-topologi](https://github.com/DaffaZimraan/Jarkom-Modul-2-E24-2023/raw/main/image/ping-topologi.jpg)</br>
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
### Penyelesaian

## Soal 3
### Pertanyaan
### Penyelesaian

## Soal 4
### Pertanyaan
### Penyelesaian

## Soal 5
### Pertanyaan
### Penyelesaian

## Soal 6
### Pertanyaan
### Penyelesaian

## Soal 7
### Pertanyaan
### Penyelesaian

## Soal 8
### Pertanyaan
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

