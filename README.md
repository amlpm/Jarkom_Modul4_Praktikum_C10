# Jarkom_Modul4_Praktikum_C10

### Kelompok C_10
#### Asisten Dosen Bella Septina 
1. Adrian Danindra 05111840000068
2. Amelia Puji     05111840000147 
#

### Pengerjaan Soal
1. [Pembagian SubNet](#VLSM)
2. [Metode CIDR](#CIDR)
3. [Metode CIDR](#CIDR)
#

# Pembagian Subnet
Untuk server MOJOKERTO dan MALANG, tidak perlu diikutkan dalam subnet pembagian IP, karena mereka menggunakan NID DMZ: 10.151.77.88/29, di mana akan dipecah masing-masing mendapatkan NID 10.151.79.89/30 dan 10.151.79.93/30. 

![Soal Shift Modul 4](https://user-images.githubusercontent.com/57977401/101971748-80ce3980-3c6e-11eb-94c3-a90e6ba771df.png)

Kelompok kami mengerjakan teknik VLSM pada CPT, sedangkan teknik CIDR pada UML.

# VLSM
#### Metode VLSM kami terapkan pada CPT, dengan perhitungan, pohon IP, tabel pembagian IP, dan routing pada CPT sebagai berikut sebagai berikut

Jawab: <br>
- **Perhitungan**

![Metode VLSM](https://user-images.githubusercontent.com/57977401/101971824-25507b80-3c6f-11eb-809e-19f1bf5e4cb6.png)
<br>

- **Pohon IP**

![Pohon IP VLSM](https://user-images.githubusercontent.com/57977401/101971825-2681a880-3c6f-11eb-96ca-48a8ed37002e.png)
<br>

- **Tabel Pembagian IP**

![Tabel IP VLSM](https://user-images.githubusercontent.com/57977401/101971827-284b6c00-3c6f-11eb-8d74-7ba7d9c9248d.png)
<br>

- **Routing pada CPT**<br>

**Surabaya**
```
192.168.27.148/30 via 192.168.27.154
192.168.27.0/25 via 192.168.27.154
192.168.12.0/22 via 192.168.27.154
192.168.0.0/21 via 192.168.27.154
192.168.24.0/23 via 192.168.27.146
192.168.27.128/28 via 192.168.27.146
192.168.16.0/22 via 192.168.27.146
10.151.77.92/30 via 192.168.27.146
192.168.26.0/24 via 192.168.27.146
192.168.20.0/22 via 192.168.27.146
0.0.0.0 via 10.151.76.46
```
<br>

**Pasuruan**
```
192.168.0.0/21 via 192.168.27.150
192.168.27.0/25 via 192.168.27.150
0.0.0.0/0 via 192.168.27.153
```
<br>

**Probolinggo**
```
0.0.0.0/0 via 192.168.27.149
```
<br>

**Batu**
```
192.168.27.128/28 via 192.168.24.2
192.168.26.0/24 via 192.168.27.158
192.168.20.0/22 via 192.168.27.158
10.151.77.92/30 via 192.168.27.158
0.0.0.0/0 via 192.168.27.145
```
<br>

**Kediri**
```
192.168.20.0/22 via 192.168.26.2
0.0.0.0/0 via 192.168.27.157
```
<br>

**Madiun**
```
0.0.0.0/0 via 192.168.24.1
```
<br>

**Blitar**
```
0.0.0.0/0 via 192.168.26.1
```
<br><br><br>

# CIDR
#### Metode CIDR kami terapkan pada UML, dengan perhitungan, pohon IP, tabel pembagian IP, topologi, interfaces, dan routing pada UML sebagai berikut sebagai berikut

Jawab: <br>
- ip tables dengan ```iptables –t nat –A POSTROUTING –o eth0 –j MASQUERADE –s 192.168.0.0/16```

- **Perhitungan**

![Metode CIDR](https://user-images.githubusercontent.com/57977401/101975772-0d322980-3c7a-11eb-94b6-8cc7fbb7d4ee.png)
<br>

- **Pohon IP**

![Pohon IP CIDR](https://user-images.githubusercontent.com/57977401/101975774-0dcac000-3c7a-11eb-9f17-6e30b158dc84.png)
<br>

- **Tabel Pembagian IP**

![Tabel IP CIDR](https://user-images.githubusercontent.com/57977401/101975775-0efbed00-3c7a-11eb-90cc-f3b83f94f117.png)
<br>

- **Topologi.sh**
```
# Switch
uml_switch -unix switch0 > /dev/null < /dev/null &
uml_switch -unix switch1 > /dev/null < /dev/null &
uml_switch -unix switch2 > /dev/null < /dev/null &
uml_switch -unix switch3 > /dev/null < /dev/null &
uml_switch -unix switch4 > /dev/null < /dev/null &
uml_switch -unix switch5 > /dev/null < /dev/null &
uml_switch -unix switch6 > /dev/null < /dev/null &
uml_switch -unix switch7 > /dev/null < /dev/null &
uml_switch -unix switch8 > /dev/null < /dev/null &
uml_switch -unix switch9 > /dev/null < /dev/null &
uml_switch -unix switch10 > /dev/null < /dev/null &
uml_switch -unix switch11 > /dev/null < /dev/null &
uml_switch -unix switch12 > /dev/null < /dev/null &
uml_switch -unix switch13 > /dev/null < /dev/null &
uml_switch -unix switch14 > /dev/null < /dev/null &

# Router
xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,10.151.76.45 eth1=daemon,,,switch1 eth2=daemon,,,switch2 eth3=daemon,,,switch7 eth4=daemon,,,switch0 mem=64M &
xterm -T PASURUAN -e linux ubd0=PASURUAN,jarkom umid=PASURUAN eth0=daemon,,,switch2 eth1=daemon,,,switch3 eth2=daemon,,,switch8 mem=64M &
xterm -T PROBOLINGGO -e linux ubd0=PROBOLINGGO,jarkom umid=PROBOLINGGO eth0=daemon,,,switch3 eth1=daemon,,,switch4 eth2=daemon,,,switch9 mem=64M &
xterm -T MADIUN -e linux ubd0=MADIUN,jarkom umid=MADIUN eth0=daemon,,,switch5 eth1=daemon,,,switch6 mem=64M &
xterm -T BATU -e linux ubd0=BATU,jarkom umid=BATU eth0=daemon,,,switch10 eth1=daemon,,,switch6 eth2=daemon,,,switch7 eth3=daemon,,,switch11 mem=64M &
xterm -T KEDIRI -e linux ubd0=KEDIRI,jarkom umid=KEDIRI eth0=daemon,,,switch12 eth1=daemon,,,switch11 eth2=daemon,,,switch14 mem=64M &
xterm -T BLITAR -e linux ubd0=BLITAR,jarkom umid=BLITAR eth0=daemon,,,switch13 eth1=daemon,,,switch14 mem=64M &

# Server
xterm -T MALANG -e linux ubd0=MALANG,jarkom umid=MALANG eth0=daemon,,,switch12 mem=64M &
xterm -T MOJOKERTO -e linux ubd0=MOJOKERTO,jarkom umid=MOJOKERTO eth0=daemon,,,switch0 mem=64M &

# Klien
xterm -T SAMPANG -e linux ubd0=SAMPANG,jarkom umid=SAMPANG eth0=daemon,,,switch1 mem=64M &
xterm -T BONDOWOSO -e linux ubd0=BONDOWOSO,jarkom umid=BONDOWOSO eth0=daemon,,,switch4 mem=64M &
xterm -T BOJONEGORO -e linux ubd0=BOJONEGORO,jarkom umid=BOJONEGORO eth0=daemon,,,switch5 mem=64M &
xterm -T JOMBANG -e linux ubd0=JOMBANG,jarkom umid=JOMBANG eth0=daemon,,,switch6 mem=64M &
xterm -T JEMBER -e linux ubd0=JEMBER,jarkom umid=JEMBER eth0=daemon,,,switch9 mem=64M &
xterm -T BANYUWANGI -e linux ubd0=BANYUWANGI,jarkom umid=BANYUWANGI eth0=daemon,,,switch9 mem=64M &
xterm -T SIDOARJO -e linux ubd0=SIDOARJO,jarkom umid=SIDOARJO eth0=daemon,,,switch8 mem=64M &
xterm -T NGANJUK -e linux ubd0=NGANJUK,jarkom umid=NGANJUK eth0=daemon,,,switch10 mem=64M &
xterm -T TULUNGAGUNG -e linux ubd0=TULUNGAGUNG,jarkom umid=TULUNGAGUNG eth0=daemon,,,switch13 mem=64M &
xterm -T LUMAJANG -e linux ubd0=LUMAJANG,jarkom umid=LUMAJANG eth0=daemon,,,switch14 mem=64M &
```

![image](https://user-images.githubusercontent.com/57977401/101989803-ce35bf80-3cdd-11eb-8876-ab6d9f6b83d5.png)
<br>

- **Interfaces**<br>

```
Notes = Untuk setiap ROUTER, tidak lupa untuk meng-uncomment di net.ipv4.ip_forward=1 pada file /etc/sysctl.conf
```
<br>

**Surabaya (ROUTER)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.76.46
netmask 255.255.255.252
gateway 10.151.76.45

auto eth1
iface eth1 inet static
address 192.168.64.1
netmask 255.255.252.0

auto eth2
iface eth2 inet static
address 192.168.192.1
netmask 255.255.255.252

auto eth3
iface eth3 inet static
address 192.168.32.1
netmask 255.255.255.252

auto eth4
iface eth4 inet static
address 10.151.77.89
netmask 255.255.255.252
```

![Interfaces SURABAYA](https://user-images.githubusercontent.com/57977401/101990766-42269680-3ce3-11eb-92c3-5d2bd958969e.png)
<br><br>

**Pasuruan (ROUTER)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.192.2
netmask 255.255.255.252
gateway 192.168.192.1

auto eth1
iface eth1 inet static
address 192.168.144.1
netmask 255.255.255.252

auto eth2
iface eth2 inet static
address 192.168.160.1
netmask 255.255.252.0
```

![Interfaces PASURUAN](https://user-images.githubusercontent.com/57977401/101990761-3fc43c80-3ce3-11eb-82d5-f8efe8a32351.png)
<br><br>

**Probolinggo (ROUTER)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.144.2
netmask 255.255.255.252

auto eth1
iface eth1 inet static
address 192.168.136.1
netmask 255.255.255.128

auto eth2
iface eth2 inet static
address 192.168.128.1
netmask 255.255.248.0
```

![Interfaces PROBOLINGGO](https://user-images.githubusercontent.com/57977401/101990762-405cd300-3ce3-11eb-82b0-c350839d8b4f.png)
<br><br>

**Batu (ROUTER)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.32.2
netmask 255.255.255.252
gateway 192.168.32.1

auto eth1
iface eth1 inet static
address 192.168.8.1
netmask 255.255.255.252

auto eth2
iface eth2 inet static
address 192.168.20.1
netmask 255.255.252.0

auto eth3
iface eth3 inet static
address 192.168.16.1
netmask 255.255.254.0
```

![Interfaces BATU](https://user-images.githubusercontent.com/57977401/101990771-43f05a00-3ce3-11eb-8615-282f52eaf26b.png)
<br><br>

**Kediri (ROUTER)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.8.2
netmask 255.255.255.252
gateway 192.168.8.1

auto eth1
iface eth1 inet static
address 192.168.4.1
netmask 255.255.255.0

auto eth2
iface eth2 inet static
address 192.168.92
netmask 255.255.255.252
```

![Interfaces KEDIRI](https://user-images.githubusercontent.com/57977401/101990753-3cc94c00-3ce3-11eb-9d4e-78cd99ebf12c.png)
<br><br>

**Madiun (ROUTER)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.16.2
netmask 255.255.254.0
gateway 192.168.16.1

auto eth1
iface eth1 inet static
address 192.168.18.1
netmask 255.255.255.240
```

![Interfaces MADIUN](https://user-images.githubusercontent.com/57977401/101990755-3dfa7900-3ce3-11eb-92c9-df16a205b6d7.png)
<br><br>

**Blitar (ROUTER)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.4.2
netmask 255.255.255.0

auto eth1
iface eth1 inet static
address 192.168.0.1
netmask 255.255.252.0
```

![Interfaces BLITAR](https://user-images.githubusercontent.com/57977401/101990772-43f05a00-3ce3-11eb-9721-6c4b42ba64a6.png)
<br><br>

**Mojokerto (SERVER)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.77.90
netmask 255.255.255.252
gateway 10.151.77.89
```

![Interfaces MOJOKERTO](https://user-images.githubusercontent.com/57977401/101990758-3f2ba600-3ce3-11eb-8df1-5ce480ddfd25.png)
<br><br>

**Malang (SERVER)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.77.92
netmask 255.255.252.0
gateway 10.151.77.91
```

![Interfaces MALANg](https://user-images.githubusercontent.com/57977401/101990757-3e930f80-3ce3-11eb-9ab3-00ef09c71efe.png)
<br><br>

**Sampang (KLIEN)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.64.2
netmask 255.255.252.0
gateway 192.168.64.1
```

![Interfaces SAMPANG](https://user-images.githubusercontent.com/57977401/101990763-40f56980-3ce3-11eb-951a-1ee5be7ca9b0.png)
<br><br>

**Sidoarjo (KLIEN)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.160.2
netmask 255.255.252.0
gateway 192.168.160.1
```

![Interfaces SIDOARJO](https://user-images.githubusercontent.com/57977401/101990764-418e0000-3ce3-11eb-8e80-78c30643d7f4.png)
<br><br>

**Bondowoso (KLIEN)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.136.2
netmask 255.255.255.128
gateway 192.168.136.1
```

![Interfaces BONDOWOSO](https://user-images.githubusercontent.com/57977401/101990749-3a66f200-3ce3-11eb-9618-f684c23f6334.png)
<br><br>

**Jember (KLIEN)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.128.2
netmask 255.255.248.0
gateway 192.168.128.1
```

![Interfaces JEMBER](https://user-images.githubusercontent.com/57977401/101990751-3b981f00-3ce3-11eb-9855-906ccccd37a8.png)
<br><br>

**Banyuwangi (KLIEN)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.128.3
netmask 255.255.248.0
gateway 192.168.128.1
```

![Interfaces BANYUWANGI](https://user-images.githubusercontent.com/57977401/101990770-4357c380-3ce3-11eb-9039-6110591d0f6f.png)
<br><br>

**Nganjuk (KLIEN)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.20.2
netmask 255.255.252.0
gateway 192.168.20.1
```

![Interfaces NGANJUK](https://user-images.githubusercontent.com/57977401/101990759-3fc43c80-3ce3-11eb-8263-47153bb96e91.png)
<br><br>

**Jombang (KLIEN)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.16.2
netmask 255.255.254.0
gateway 192.168.16.1
```

![Interfaces JOMBANG](https://user-images.githubusercontent.com/57977401/101990752-3c30b580-3ce3-11eb-8477-41f5e062588e.png)
<br><br>

**Lumajang (KLIEN)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.4.2
netmask 255.255.255.0
gateway 192.168.4.1
```

![Interfaces LUMAJANG](https://user-images.githubusercontent.com/57977401/101990754-3d61e280-3ce3-11eb-8bbb-6a02fe404e41.png)
<br><br>

**Bojonegoro (KLIEN)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.18.2
netmask 255.255.255.240
gateway 192.168.18.1
```

![Interfaces BOJONEGORI](https://user-images.githubusercontent.com/57977401/101990773-4488f080-3ce3-11eb-9e99-e5234fde2ec8.png)
<br><br>

**Tulungagung (KLIEN)**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.0.2
netmask 255.255.252.0
gateway 192.168.0.1
```

![Interfaces TULUNGAGUNG](https://user-images.githubusercontent.com/57977401/101990768-42bf2d00-3ce3-11eb-81d6-acdbe4c5a8dc.png)
<br><br>


- **Routing pada UML**<br>

Routing menggunakan CIDR pada UML tentunya lebih sederhana karena pada metode CIDR kita telah mengelompokkan pembagian IP-nya sehingga untuk setiap UML hanya memerlukan routing pada lingkaran besar pengelompokkan yang gambarnya dapat dilihat diatas. Berikut merupakan arah routing dari tiap UML (router) :

Surabaya = D1, D2, Malang<br>
Pasuruan = B2<br>
Batu = B1, A8, Malang<br>
Kediri = A15<br>
<br>
Adapun tambahan route 0.0.0.0 pada seluruh router tergantung pada kebutuhan.<br>

Karena setiap UML perlu di  ```service networking restart``` yang menyebabkan route hilang (untuk mengecek apakah route ada apa tidak, ketikkan command ```route -n```), maka simpanlah routing yang kita lakukan pada suatu file. Kelompok C10 menyimpan dengan nama route.sh. Ketikkan perintah ```nano route.sh``` dan tambahkan route berikut pada setiap UML :

**Surabaya (ROUTER)**
```
route add -net 192.168.128.0 netmask 255.255.192.0 gw 192.168.192.2
route add -net 192.168.0.0 netmask 255.255.224.0 gw 192.168.32.2
route add -net 10.151.77.92 netmask 255.255.255.252 gw 192.168.32.2
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.151.76.45
```
<br>

**Pasuruan (ROUTER)**
```
route add -net 192.168.128.0 netmask 255.255.240.0 gw 192.168.144.2
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.168.192.1
```
<br>

**Probolinggo (ROUTER)**
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.168.144.1
```
<br>

**Batu (ROUTER)**
```
route add -net 192.168.18.0 netmask 255.255.255.240 gw 192.168.16.2
route add -net 192.168.0.0 netmask 255.255.248.0 gw 192.168.8.2
route add -net 10.151.77.92 netmask 255.255.255.252 gw 192.168.8.2
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.168.32.1
```
<br>

**Kediri (ROUTER)**
```
route add -net 192.168.0.0 netmask 255.255.252.0 gw 192.168.4.2
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.168.8.1
```
<br>

**Madiun (ROUTER)**
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.168.16.1
```
<br>

**Blitar (ROUTER)**
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.168.4.1
```
<br>