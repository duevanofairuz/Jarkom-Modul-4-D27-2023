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
* perhitungan ip sudah termasuk ip router
* pembagian ip digunakan untuk melakukan subnetting pada topologi
* setelah subnetting berhasil langkah terakhir adalah melakukan routing

### 1. VLSM (CPT)
![Alt text](image-5.png)<br><br><br>
**Berikut ini adalah VLSM tree yang telah saya buat:**
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

**Berikut ini adalah isi config pembagian IP VLSM (Subnetting) di CPT:**<br>
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
* Konfigurasi IP ini dilakukan ke SETIAP subnet nya sebagaimana pembagian IP di sheet perhitungan saya
* Untuk melihat CONFIG SELENGKAPNYA silahkan import file .pkt yang ada di repo ke CPT atau cek config berikut:

* Rohrroad:<br>
![Alt text](image-11.png)<br>
* Flamme: <br>
![Alt text](image-12.png)<br>
* SchwerMountains: <br>
![Alt text](image-13.png)<br>
* Himmel: <br>
![Alt text](image-14.png)<br>
* Frieren: <br>
![Alt text](image-15.png)<br>
* LakeKoridor: <br>
![Alt text](image-16.png)<br>
* Aura: <br>
![Alt text](image-17.png)<br>
* Denken: <br>
![Alt text](image-18.png)<br>
* RoyalCapital: <br>
![Alt text](image-19.png)<br>
* WilleRegion: <br>
![Alt text](image-20.png)<br>
* Eisen: <br>
![Alt text](image-21.png)<br>
* Richter: <br>
![Alt text](image-22.png)<br>
* Revolte: <br>
![Alt text](image-23.png)<br>
* Stark: <br>
![Alt text](image-24.png)<br>
* Lugner: <br>
![Alt text](image-25.png)<br>
* TurkRegion: <br>
![Alt text](image-26.png)<br>
* GrobeForest: <br>
![Alt text](image-27.png)<br>
* Linie: <br>
![Alt text](image-28.png)<br>
* GranzChannel: <br>
![Alt text](image-29.png)<br>
* Lawine: <br>
![Alt text](image-30.png)<br>
* BredtRegion: <br>
![Alt text](image-31.png)<br>
* Heiter: <br>
![Alt text](image-32.png)<br>
* Sein: <br>
![Alt text](image-33.png)<br>
* RiegelCanyon: <br>
![Alt text](image-34.png)<br>




**Routing**<br>
![Alt text](image-35.png)<br>
Untuk routing dilakukan dengan cara beberapa tahap:
* routing dilakukan dengan cara static dimana next hop dari routing adalah adjacent router terdekat dengan subnet yang ingin dituju, semisal aura ingin berkenalan dengan subnet a1 maka NID dan netmask diisi milik a1 dan next-hop nya adalah frieren
* binding everywhere (0.0.0.0) dilakukan seperti gambar di atas
* kemudian untuk setiap router yang terhubung dengan router lain (nexthop untuk berkenalan lebih dari 1hop) yang memiliki host/client perlu mengenali subnet mereka juga
* contoh:<br> - flamme harus berkenalan dengan subnet a1 dan a4 <br>
          - frieren harus berkenalan dengan subnet a1, a2, a3, a4, a5<br>
          - aura harus berkenalan dengan semua subnet kecuali subnet a8, a10, a11<br>
          - lawine harus berkenalan dengan subnet a21<br>
          - linie harus berkenalan dengan subnet a20, a21<br>
          - eisen harus berkenalan dengan subnet a15, a16, a18, a19, a20, a21<br>
          - dst.<br>
* binding everywhere dari setiap router cukup 1 saja yang mengarah ke router aura / terdekat dengan aura, hal ini dilakukan untuk efisiensi routing (100% success)
* jika aura sudah disetup sebagaimana pengaturan routing di atas maka otomatis semua subnet bisa saling mengenal via aura 
* Untuk melihat CONFIG SELENGKAPNYA silahkan import file .pkt yang ada di repo ke CPT atau cek config berikut:

* Fern:<br>
![Alt text](image-36.png)<br>
* Flamme: <br>
![Alt text](image-37.png)<br>
* Himmel: <br>
![Alt text](image-38.png)<br>
* Frieren:<br>
![Alt text](image-39.png)<br>
* Aura: <br>
SEMUA SUBNET KECUALI SUBNET A8, A10, A11
* Denken: <br>
![Alt text](image-40.png)<br>
* Eisen: <br>
![Alt text](image-41.png)<br>
* Lugner: <br>
![Alt text](image-42.png)<br>
* Linie: <br>
![Alt text](image-43.png)<br>
* Lawine: <br>
![Alt text](image-44.png)<br>
* Heiter: <br>
![Alt text](image-45.png)<br>


**Berikut ini adalah beberapa contoh output ping**<br>
![Alt text](image-46.png)


### 2. CIDR (GNS3)
![Alt text](image-47.png)<br><br>
**Berikut ini adalah proses pembuatan CIDR Tree**<br>
![Alt text](image-48.png)

Proses penggabungan subnet dapat dilihat di Sheet perhitungan di atas atau cek disini:
I.<br>
![Alt text](image-49.png)

II.<br>
![Alt text](image-50.png)

III.<br>
![Alt text](image-51.png)

IV.<br>
![Alt text](image-52.png)

V.<br>
![Alt text](image-53.png)

VI.<br>
![Alt text](image-54.png)

* Penggabungan CIDR disini saya lakukan dengan cara iterasi pertama bertujuan untuk membuat subnet B agar semua jarak subnet adalah minimal 2 Hop ke Aura
* iterasi kedua membuat subnet C agar semua jarak subnet adalah minimal 0 atau 1 Hop
* iterasi ketiga dan seterusnya melakukan penggabungan semua 2 subnet yang bisa digabungkan
* hingga ditemui titik akhir yakni semua subnet tergabung menjadi 1 (G1 /16) 

CIDR IP tree:
![Alt text](image-55.png)
* root dari tree adalah netmask /16 dengan ip yang dimulai dari 10.35.0.0 sebagai subnet G1
* pada pembuatan tree ini saya menggunakan penambahan dari ip terkecil untuk mempermudah
* kaki kiri dari tree akan selalu menunjukkan awal mula dari ip yang tersedia, sedangkan kaki kanan adalah ip setelah ip kaki kiri
* pada kaki kiri juga saya berikan batas atas atau broadcast address dari ip dengan netmask tersebut untuk mempermudah penentuan ip di kaki kanan tree
* kaki kiri tree akan selalu memiliki subnet dengan netmask yang lebih rendah dari kaki kanan untuk mempermudah penentuan ip
* struktur tree mengikuti aturan binary tree, dan setiap parent node merepresentasikan subnet gabungan dari sebelumnya
* jadi tree akan selalu mengikuti alur penggabungan dimana start dari subnet G dan end di subnet A

Sehingga diperoleh rekap pembagian ip tree sebagai berikut:<br>
![Alt text](image-56.png)<br>

**Berikut ini adalah isi config pembagian IP CIDR (Subnetting) di GNS3:**<br>
Untuk isi config pembagian ip saya set seperti ini:
* Router memliki `IP NID + 1`
* Host / Client memiliki `IP Broadcast - 1` atau `IP Client sesubnet - 1`
* Host / Client memiliki gateway sesuai IP router dalam subnet mereka
* 1 router bisa memiliki beberapa IP karena dalam 1 router dapat menangani beberapa ethernet interface / subnet
* Untuk lebih jelasnya:
![Alt text](image-57.png)
![Alt text](image-58.png)
![Alt text](image-59.png)<br>
* jika sudah maka dalam satu subnet pasti bisa saling ping

**Routing (SAMA SEPERTI SEBELUMNYA)**<br>
![Alt text](image-35.png)<br>
Untuk routing dilakukan dengan cara beberapa tahap:
* routing dilakukan dengan cara static dimana next hop dari routing adalah adjacent router terdekat dengan subnet yang ingin dituju, semisal aura ingin berkenalan dengan subnet a1 maka NID dan netmask diisi milik a1 dan next-hop nya adalah frieren
* binding everywhere (0.0.0.0) dilakukan seperti gambar di atas
* kemudian untuk setiap router yang terhubung dengan router lain (nexthop untuk berkenalan lebih dari 1hop) yang memiliki host/client perlu mengenali subnet mereka juga
* contoh:<br> - flamme harus berkenalan dengan subnet a1 dan a4 <br>
          - frieren harus berkenalan dengan subnet a1, a2, a3, a4, a5<br>
          - aura harus berkenalan dengan semua subnet kecuali subnet a8, a10, a11<br>
          - lawine harus berkenalan dengan subnet a21<br>
          - linie harus berkenalan dengan subnet a20, a21<br>
          - eisen harus berkenalan dengan subnet a15, a16, a18, a19, a20, a21<br>
          - dst.<br>
* binding everywhere dari setiap router cukup 1 saja yang mengarah ke router aura / terdekat dengan aura, hal ini dilakukan untuk efisiensi routing (100% success)
* jika aura sudah disetup sebagaimana pengaturan routing di atas maka otomatis semua subnet bisa saling mengenal via aura 
* Untuk melihat CONFIG SELENGKAPNYA silahkan import file .pkt yang ada di repo ke CPT atau cek config berikut:

* Fern: <br>
![Alt text](image-60.png)<br>
* Flamme: <br>
![Alt text](image-61.png)<br>
* Himmel: <br>
![Alt text](image-62.png)<br>
* Frieren: <br>
![Alt text](image-63.png)<br>
* Aura: <br>
![Alt text](image-64.png)<br>
* Denken: <br>
![Alt text](image-65.png)<br>
* Eisen: <br>
![Alt text](image-66.png)<br>
* Lugner: <br>
![Alt text](image-67.png)<br>
* Linie: <br>
![Alt text](image-68.png)<br>
* Lawine: <br>
![Alt text](image-69.png)<br>
* Heiter: <br>
![Alt text](image-70.png)<br>

**Berikut ini adalah beberapa contoh output ping:**<br>
![Alt text](image-71.png)<br>
* ping aura ke subnet a1, a2, a6<br>
![Alt text](image-72.png)<br>
* ping aura ke subnet a3, a4, a5<br>
![Alt text](image-73.png)<br>
* ping aura ke subnet a7, a8, a9, a10<br>
![Alt text](image-74.png)<br>
* ping aura ke subnet a11, a12, a13, a14<br>
![Alt text](image-75.png)<br>
* ping aura ke subnet a15, a16, a17, a18<br>
![Alt text](image-76.png)<br>
* ping aura ke subnet a19, a20, a21 <br>
