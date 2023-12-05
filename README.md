# Jarkom-Modul-4-D27-2023 (SUBNETTING AND ROUTING)

**SHEET PERHITUNGAN: [Cek disini selengkapnya](https://docs.google.com/spreadsheets/d/1AFVzDLOe8XgPUtKfZ6-JNdbXsctGGFvfrzY1KuioafU/edit?usp=sharing)**

**Anggota Kelompok Jarkom D27:**
* Duevano Fairuz Pandya (5025211052)
* 🤓

**PREFIX 10.35.x.x**

----------------------------------------------------------------------------------------------------------------------------------
## **SOAL**
![Alt text](image.png)<br>
1.	Soal shift dikerjakan pada Cisco Packet Tracer dan GNS3 menggunakan metode perhitungan CLASSLESS yang berbeda.
Keterangan: Bila di CPT menggunakan VLSM, maka di GNS3 menggunakan CIDR atau sebaliknya<br>
2.	Jika tidak ada pemberitahuan revisi soal dari asisten, berarti semua soal BERSIFAT BENAR dan DAPAT DIKERJAKAN.<br>
3.	Untuk di GNS3 CLOUD merupakan NAT1 jangan sampai salah agar bisa terkoneksi internet.<br>
4.	Pembagian IP menggunakan Prefix IP yang telah ditentukan pada modul pengenalan<br>
5.	Pembagian IP dan routing harus SE-EFISIEN MUNGKIN.<br>
Gambar topologi yang lebih jelas dapat diakses pada link berikut<br>


## **PENYELESAIAN**
Untuk menyelesaikan praktikum modul ini saya memilih mengerjakannya dengan membaginya menjadi:
* VLSM : Menggunakan Cisco Packet Tracer (CPT)
* CIDR : Menggunakan GNS3

Sebelumnya saya lakukan pembagian subnet (rute) sebagai berikut:<br>
![Alt text](image-1.png)
![Alt text](image-2.png)

* dari pembagian subnet ini nantinya akan saya temukan pembagian ip yang sesuai menggunakan metode classless VLSM dan CIDR Tree
* pembagian ip digunakan untuk melakukan subnetting pada topologi
* setelah subnetting berhasil langkah terakhir adalah melakukan routing

### 1. VLSM (CPT)
![Alt text](image-5.png)<br><br><br>
Berikut ini adalah VLSM tree yang telah saya buat:
![Alt text](image-3.png)
* karena pada pembagian subnet tercatat total ip adalah 4255 dan netmask cukup menampungnya adalah /19 yang mana mampu menampung ip sebanyak 8190
* root dari tree adalah netmask /19 dengan ip yang dimulai dari 10.35.0.0
* pada pembuatan tree ini saya menggunakan penambahan dari ip terkecil untuk mempermudah
* kaki kiri dari tree akan selalu menunjukkan awal mula dari ip yang tersedia, sedangkan kaki kanan adalah ip setelah ip kaki kiri
* pada kaki kiri juga saya berikan batas atas atau broadcast address dari ip dengan netmask tersebut untuk mempermudah penentuan ip di kaki kanan tree
* iterasi dilakukan terus menerus dari netmask /19 hingga /30
* sedikit catatan, tree yang saya buat tidak sepenuhnya mematuhi aturan binary tree sebagaimana mestinya, namun tetap mengikuti aturan pembagian ip yang sesuai

sehingga diperoleh pembagian ip VLSM: <br>
![Alt text](image-4.png)

Berikut ini adalah isi config pembagian IP VLSM (subnetting) di CPT:
Untuk isi config pembagian ip saya set seperti ini:
* Router memliki `IP NID + 1`
* Host / Client memiliki `IP Rourter + 1` atau `IP Client sesubnet + 1`
* Host / Client memiliki gateway sesuai IP router dalam subnet mereka
* 1 router bisa memiliki beberapa IP karena dalam 1 router dapat menangani beberapa ethernet interface / subnet


Karena config semuanya kurang lebih mirip, jadi akan saya beri contoh assign IP Router dan Client dalam 1 Subnet saja:<br>
Fern:<br>
![Alt text](image-6.png)<br>
![Alt text](image-7.png)<br>

AppetitRegion:<br>
![Alt text](image-8.png)

Laubhills:<br>
![Alt text](image-9.png)<br>

![Alt text](image-10.png)
* Jika sudah maka dalam 1 Subnet ini semuanya pasti bisa saling melakukan ping
* Konfigurasi IP ini dilakukan ke SETIAP Router dan Client nya sebagaimana pembagian IP di sheet perhitungan saya
* Untuk melihat CONFIG LENGKAPNYA silahkan import file .pkt yang ada di repo ke CPT


- isi config routing dan jelasin singkat
- beberapa contoh output ping vlsm di cpt

### 2. CIDR (GNS3)
- pembuatan tree cidr & gambar pembagian ip
- isi config ip cidr
- isi config routing dan jelasin singkat kasih 	[Markdown - Link](#Jarkom-Modul-4-D27-2023)
- beberapa contoh output ping cidr di gns