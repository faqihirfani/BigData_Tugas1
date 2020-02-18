# BigData_Tugas1

# Dokumentasi Praktek ETL menggunakan KNIME

* [Business Understanding](https://github.com/faqihirfani/BigData_Tugas1/blob/master/tugas1/README.md#business-understanding)<br/>
* [Data Understanding](https://github.com/faqihirfani/BigData_Tugas1/master/tugas1/README.md#data-understanding)<br/>
* [Data Preparation](https://github.com/faqihirfani/BigData_Tugas1/blob/master/tugas1/README.md#data-preparation)<br/>
* [Modeling](https://github.com/faqihirfani/BigData_Tugas1/blob/master/tugas1/README.md#modeling)<br/>
  - [Proses membaca data dari dua sumber yang berbeda](https://github.com/faqihirfani/BigData_Tugas1/blob/master/tugas1/README.md#proses-membaca-data-dari-dua-sumber-yang-berbeda)<br/>
  - [Proses Modeling](https://github.com/faqihirfani/BigData_Tugas1/blob/master/tugas1/README.md#proses-modeling)<br/>
* [Evaluation](https://github.com/faqihirfani/BigData_Tugas1/blob/master/tugas1/README.md#evaluation)<br/>
* [Deployment](https://github.com/faqihirfani/BigData_Tugas1/blob/master/tugas1/README.md#deployment)<br/>

# Business Understanding
Kemungkinan-kemungkinan yg dapat dilakukan yaitu:
1. Dari data tersebut, dapat dilakukan proses untuk melihat tipe permainan yang sering ditandingkan
2. Dari data tersebut, dapat dilakukan proses untuk melihat persentase kemenangan
3. Dari data tersebut, dapat dilakukan proses untuk melihat persentase negara ikut serta dalam pertandingan

# Data Understanding

- Badminton adalah olahraga yang digemari banyak kalangan, tidak hanya kaum adam, kaum hawa pun menggemari cabang olah raga satu ini
 juga<br/>
- Begitu pula dengan turnamen-nya tidak kalah seru untuk kita mengikutinya.<br/>  
- dataset ini berisi data dari bwf super series 2015-2017.

- dataset ini terdiri dari 11873 baris dan 23 kolom
  -type: jenis permainan yang dimainkan<br/>
  -Year: Tahun penyelenggaraan<br/>
  -Score: skor dari setiap pertandingan<br/>
  -Date: Tanggal pertandingan (hari/bulan)<br/>
  -Peserta: Berisi Negara peserta dari pertandingan <br/>
 
- Source dataset : https://www.kaggle.com/canggih/badminton-game-data-bwf-super-series-20152017

# Data Preparation
- Karena hanya terdiri dari 1 file csv, saya memisahkan isi data dengan node column splitter yang ada di knime.
- Pertama, saya menggunakan node file reader yang tersedia di knime<br/>
![file read](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/fileread.png "fileread")<br/>

- Kedua, klik kanan lalu buka settings dan "browse file .csv yang ingin digunakan, lalu klik ok<br/>
![filereadfind](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/filereadfind.png "filereadfind")<br/>

- Ketiga, Drag node column splitter kedalam workflow, lalu hubungkan dengan node file reader<br/>
![colsplit](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/colsplit.png "colsplit")<br/>

- Keempat, klik kanan pada node column splitter lalu buka settings.<br/>
![colsplitset](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/colsplitset.png "colsplitset")<br/>
  -2 hasil splitter<br/>
      ![colsplit1](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/colsplit1.png "colsplit1")<br/>    
      ![colsplit2](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/colsplit2.png "colsplit2")<br/>
 
-Kelima, simpan salah satu bagian data di database, dan satu bagian lagi di file csv dengan cara:<br/>
 -Database:
  -Gunakan MySQL Connector lalu hubungkan dan setting dengan database yang ingin dipakai<br/>
    ![sqlconn](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/sqlconn.png "sqlconn")<br/>
    ![sqlconnset](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/sqlconnset.png "sqlconnset")<br/>
  -Ambil node DB Writer, lalu hubungkan dengan MySQL Connector dan node Column splitter<br/>
    ![dbwrite](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/dbwrite.png "dbwrite")<br/>
  -Konfigurasi node DB Writer lalu klik ok <br/>
    ![dbwriteset](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/dbwriteset.png "dbwriteset")<br/>
  -Tabel baru sudah ada di phpmyadmin<br/>
    ![phpadmin](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/phpadmin.png "phpadmin")<br/>
 -CSV:
  -Gunakan node CSV Writer<br/>
    ![csvwrite](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/csvwrite.png "csvwrite")<br/>
  -lalu klik kanan untuk melakukan konfigurasi<br/>
    ![csvwriteset](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/csvwriteset.png "csvwriteset")<br/>
  -Pilih output location lalu klik ok, lalu execute<br/>


# Modeling
### Proses membaca data dari dua sumber yang berbeda
#### Proses membaca dari MYSQL
- yang pertama membaca data dari mysql, dengan menggunakan mysql connector nodes dari knime<br/>
 ![sqlconn](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/sqlconn.png "sqlconn")<br/>
- data di mysql seperti dibawah<br/>
 ![phpadmin](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/phpadmin.png "phpadmin")<br/>
- melakukan configurasi disesuaikan dengan mysql yang ada di phpmyadmin, mulai dari database, port dari localhost dan username.<br/>
 ![sqlconnset](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/sqlconnset.png "sqlconnset")<br/>
- db table selector untuk mengambil Koneksi DB sebagai input dan memungkinkan untuk memilih tabel atau tampilan dari dalam database yang terhubung.<br/>
 ![tabsel](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/tabsel.png "tabsel")<br/>
- db reader untuk Mengeksekusi kueri input dalam database dan mengambil hasilnya ke dalam tabel data KNIME.<br/>
 ![dbread](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/dbread.png "dbread")<br/>
- hasil akhir dari pembacaan database yang terhubung dari mysql<br/>
 ![dbreadnew](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/dbreadnew.png "dbreadnew")<br/>

#### Proses membaca dari csv
- memasang csv reader untuk membaca file csv<br/>
 ![fileread](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/fileread.png "fileread")<br/>
- melakukan konfigurasi , menentukan path file dimana csv disimpan<br/>
 ![filereadfind](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/filereadfind.png "filereadfind")<br/>


### Proses Modeling
- menggunakan joiner node, dengan mengsambungkan node dari database yang mengolah mysql dan csv<br/>
 ![joiner](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/joiner.png "joiner")<br/>
- melakukan configure dengan memilih kolom yang urutan nya sama<br/>
  -hasilnya seperti ini<br/>


- menggunakan column filter untuk menentukan column mana yang mau ditampilkan<br/>
 ![alt text](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/colfilt.png "colfilt" ) <br/>
- hasil akhir<br/>
 ![colfiltres](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/colfiltres.png "colfiltres")<br/>


# Evaluation

- dari kedua data yang ada di mysql dan csv telah berhasil di join

- hasil join


- data asli 


- tes berhasil karena hasil join sama dengan data asli sebelum dipisah

# Deployment
### simpan ke csv
- data yang pertama akan disimpan ke csv dengan menggunakan csv writer<br/>
![csvwrite](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/csvwrite.png "csvwrite")<br/>

- memilih penempatan dan konfigurasi lain nya
![csvwritefinale](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/csvwritefinale.png "csvwritefinale")<br/>
 
- data berhasil tersimpan


 ### simpan ke db
- data akan disimpan ke database menggunakan db writer<br/>
![dbwrite](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/dbwrite.png "dbwrite")<br/>

- memilih konfigurasi lain nya, seperti nama dan db yang dituju<br/>
![dbwritefinale](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/dbwritefinale.png "dbwritefinale")<br/>

- berhasil tersimpan<br/>
![phpadmfinale](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/phpadmfinale.png "phpadmfinale")<br/>

 ### gambar knime secara lengkap
-Preparation Phase<br/>
![prep](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/prep.png "prep")<br/>
-Modelling Phase<br/>
![schemefinale](https://github.com/faqihirfani/BigData_Tugas1/blob/master/ssimg/schemefinale.png "schemefinale")<br/>


