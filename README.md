# coffeeshop-analysis
## Project Overview
Membuat analisa dari data penjualan coffeeshop selama sebulan yang dibuat secara generatif. Project ini bertujuan untuk membuat dashboard yang mudah di mengerti menggunakan Metabase agar bisa membuat keputusan yang lebih baik. 
## Masalah Utama
* Total Transaksi Penjualan
* Total Barang terjual
* Total Nilai Penjualan
* Total Keuntungan
* Komposisi dari Transaksi per Kategori
* Trend Keuntungan
* Kota Dengan Keuntungan Terbesar
* Kota Dengan Nilai Penjualan Terbesar
## Tools Yang Digunakan
* MiniO : Storage
* Iceberg : Open Table Format
* SparkSQL : Query Engine
* Apache Spark : Processing Engine
* Jupyter-Lab : Analytics Tools
* Apache Airflow : Orchectrator
* Metaabse : Visualization
## Pemebersihan dan Analisa Data
Data akan diproses menggunakan aritektur Medallion :
### Lapisan Bronze
Data mentah (Raw data) dimuat ke dalam datalake. Data disimpan dalam miniO dan akan dengan format Apache Parquet dan dikelola sebagai tabel iceberg. Ditahapan ini data harus disimpan tanpa perubahan apapun dan dalam kondisi apapun.
### Lapisan Silver
Data yang sudah tersimpan di lapisan Bronze harus dibersihkan dan dirapihkan sebelum bisa dimasukan ke Silver layer. Pembersihan bisa mencangkup beberapa hal diantaranya :
* Merapihkan tipe data
* Menghapus data duplikat
* Menangani nilai NULL
* Menambahkan Tabel yang mungkin dibutuhan oleh data tertentu
Setelah sekiranya sudah bersih, data baru bisa dimasukkan ke dalam Lapisan Silver. Jika terdapat lebih dari satu tabel, maka proses ini dilakukan untuk setiap tabel yang ada.
### Lapisan Gold
Data yang sudah dimasukkan kedalam lapisan Silver diagregasi dan distruktur menjadi tabel fakta dan tabel dimensi.
* Tabel Fakta : tabel fakta menyimpan kolom yang bisa dihitung atau diagragasi dan kolom ID untuk penghubung ke tabel dimensi.
* Tabel Dimensi : Tugas tabel dimensi adalah memberikan atribut deskriptif untuk tabel fakta. Oleh karena itu isi dari tabel dimensi adalah Primary Key untuk setiap entitas dan atributnya seperti nama_produk, kategori, dll.
Tujuan membuat tabel fakta dan dimensi :
* Menghemat ruang & Menghindari rendundansi
* Performa Lebih Cepat
* Analisis yang lebih Fleksibel dan Intuituf (Slicing & Dicing)
Tabel ini akan menjadi tabel utama kita ketika membuat visualisasi didalam Metabase.
## Metabase
Jika sudah berhasil menjalankan Metabase, kita bisa menambahkan database dengan cara menghubungkanya dengan minilake dengan menggunakan query SparkSQL, port 10000, dan nama database. jika berhasil seharusnya database akan muncul bersama dengan semua tabel nya.
### Dashboard
Berikut adalah dashboard yang sudah saya buat secara langsung di Metabase
![Pratinjau Dashboard Power BI](assets/dashboard.png)
