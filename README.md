# ProyekAkhir_MLTerapan - SITI YULIANINGSIH

## Domain Proyek
Film merupakan salah satu dunia hiburan yang sangat digemari oleh masyarakat. Dikarenakan dengan semakin ramainya penggemar film, baik film Asia maupun film Barat. Maka timbul pemikiran untuk mengembangkan informasi seputar dunia industri perfilman. Dengan cara memberikan informasi film – film kepada konsumen, dengan maksud agar konsumen tertarik dan berminat untuk menonton film – film yang ditawarkan dan masyarakat mengetahui gambaran film yang akan ditonton.

Genre dalam film dapat menunjukkan kepada penonton poin utama referensi untuk sebuah film  dan dapat  berfungsi sebagai  quasi-search karakteristik  yang menyebabkan penonton dapat mengetahui gambaran besar tentang film tersebut tanpa harus melihat film tersebut. Dengan adanya genre, industri perfilman dapat memberitahu kepada penonton terdapat kesenangan  yang mirip  seperti film  sebelumnya dan  genre merupakan sebuah faktor yang penting untuk penonton dalam membuat keputusan tentang film apa yang ingin dilihat.  

penelitian Muhammad Fadhiil Rachman:[Sistem Rekomendasi Film Berdasarkan Pengalaman Pengguna Menggunakan Algoritma Simple Additive Weighting Dan Content-Based Filtering](https://www.researchgate.net/publication/325260942_Sistem_Rekomendasi_Film_Berdasarkan_Pengalaman_Pengguna_Menggunakan_Algoritma_Simple_Additive_Weighting_Dan_Content-Based_Filtering)

## Business Understanding
### Problem Statements
produksi membuat calon penonton kesulitan dalam menentukan film yang akan ditontonnya. Untuk mencari film tentunya akan memakan waktu, selain itu film yang sudah ditentukan untuk ditonton belum tentu sesuai dengan keinginan calon penonton setelah menontonnya, sehingga akan menghabiskan waktu lebih banyak lagi. Menonton film melalui bioskop, platform penyedia layanan streaming, maupun penyewaan dan pembelian kaset DVD juga diperlukan biaya, akan terbuang sia-sia apabila film yang ditonton tidak sesuai keinginan.
Berdasarkan kondisi yang telah diuraikan sebelumnya, perusahaan akan mengembangkan sebuah sistem rekomendasi film untuk menjawab permasalahan berikut:
- Film apa yang memiliki genre sama dengan film yang telah ditonton sebelumnya?
- Berdasarkan data mengenai pengguna, bagaimana membuat sistem rekomendasi yang dipersonalisasi dengan teknik content-based filtering?

### Goals
- Mengetahui film yang paling mirip dengan film yang diinginkan penonton.
- Menghasilkan sejumlah rekomendasi film yang dipersonalisasi untuk pengguna dengan teknik content-based filtering

## Data Understanding
Data yang akan digunakan pada proyek kali ini adalah movie-lens-dataset. Dataset ini memiliki empat file CSV. yaitu links.csv, movies.csv, ratings.csv, dan tags.csv.   
Adapun uraikanlah seluruh file dan fitur pada data, sebagai berikut:

- links.csv = Pengidentifikasian yang dapat digunakan untuk menautkan ke sumber data film lainnya. di dalam file tersebut terdapat fitur:
 
  -movieId: pengenal untuk film yang digunakan oleh [Movie Lens](https://movielens.org)
 
  -imdbId: pengenal untuk film yang digunakan oleh [IMDb](http://www.imdb.com)
 
  -tmdbId: pengenal untuk film yang digunakan oleh [TMDB](https://www.themoviedb.org)
  
- movies.csv =  Informasi mengenai film. Setiap baris pada file ini mewakili satu film, dan memiliki fitur berikut:
  
  -movieId: Id Unik untuk setiap Film
  
  -title: Nama film dengan Tahun dalam tanda kurung
 
  -genres: Jenis kategori film
  
- ratings.csv =  Berisi informasi penilaian/peringkat oleh penonton, pada file ini berisi fitur:

  -userId: Id Unik yang disediakan untuk setiap Pengguna

  -movieId: Id Unik untuk setiap Film

  -rating: Peringkat yang dibuat dalam skala bintang 5

  -timestamp: menunjukkan detik Coordinated Universal Time(UTC)
  
- tags.csv = Tag yang diterapkan ke satu film oleh satu pengguna, berisi fitur: userId, movieId, timestamp, dan tag yaitu metadata yang dibuat pengguna tentang film

pada proyek sistem rekomendasi ini hanya memerlukan 2 file yaitu file movies.csv dan file rating.csv. 
Dataset dapat di unduh pada link berikut: [Movie-lens-dataset](https://www.kaggle.com/datasets/aigamer/movie-lens-dataset?select=links.csv)

- hal pertama yang dilakukan adalah menginstall kaggle agar dapat mendownload dataset
- Membaca data-data yang telah di download dengan menggunakan fungsi pandas

===========YG DULU==========
- lalu melakukan Exploratory Data Analysis, yang bertujuan  untuk mengetahui apakah tipe data pada setiap kolom sudah sesuai atau belum
- setelah itu menangani missing value jika ada. Pada dataset kali ini terdapat 10  sampel missing value pada fitur room. Karena 10 data tersebut bernilai 0. untuk mengatasi missing value dilakukan penghapusan sampe pada fitur room yang bernilai 0. mengapa demikian? karena 10 merupakan jumlah yang kecil dibandingkan dengan seluruh sampel yaitu 3.474 jadi kita tidak akan kehilangan banyak informasi
-	Selanjutnya membagi fitur menjadi dua bagian dengan proses Univariate Analysis. Dengan code :
numerical_features = [ 'Area', 'Room', 'Price']
categorical_features = ['Parking', 'Warehouse', 'Elevator']
-	Melakukan Exploratory Data Analysis, untuk menunjukkan hubungan antara dua atau lebih variabel pada data. Pada kasus kali ini kita melakukan nya pada fitur katagori yaitu parking, warehouse, elevator, dan pada fitur numerik yaitu harga.

## Data Preparation
- Untuk mengubah fitur agar menjadi variable numerik, dilakukan proses encoding dengan teknik one-hot-encoding pada data parking, warehouse, dan elevator. 

- Selanjutnya membagi dataset menjadi data train dan data test agar dapat mempertahankan data yang ada menguji seberapa baik generalisasi model terhadap data baru. pada proyek kali ini menggunakan pembagian proporsi sebesar 90:10 dengan fungsi train_test_split dari sklearn

- Kemudia kita perlu melakukan standarisasi pada data train untuk menghindari kebocoran informasi pada data test

## Modeling
Pada tahap modeling menggunaka tiga model yaitu: K-Nearest Neighbor (KNN), Random Forest (RF), dan  Boosting Algorithm.
-	KKN

      Untuk menentukan titik mana dalam data yang paling mirip dengan input baru KNN menggunakan perhitungan ukuran jarak. pada kasus ini menggunakan nilai k= 10 tetangga dan metric Euclidean untuk mengukur jarak antara titik. Padatahap dilakukan untuk melatih data training dan menyimpan data testing untuk tahap evaluasi yang akan dibahas di Modul Evaluasi Model       
      
      Pemodelan KKN adalah algoritma yang relatif sederhana dibandingkan dengan algoritma lain sehingga sangat mudah dipahami, namun ia memiliki kekurangan jika dihadapkan pada jumlah fitur atau dimensi yang besar. permasalahan ini muncul ketika jumlah sampel meningkat secara eksponensial seiring dengan jumlah dimensi (fitur) pada data
      
-    Random Forest

     Pada algoritma Random Fores menggunakan parameter:
     - n_estimator yaitu jumlah trees (pohon) di forest dengan nilai n_estimator=50
     - max_depth yaitukedalaman atau panjang pohon dengan nilai max_depth=16. 
     - random_state=55 yang digunakan untuk mengontrol random number generator. 
     - n_jobs yaitu jumlah job (pekerjaan) yang digunakan secara paralel. pada kasus ini n_jobs di set  dengan -1 yang artinya semua proses berjalan secara paralel

     Random forest adalah salah satu algoritma supervised learning yang dapat digunakan untuk menyelesaikan masalah klasifikasi dan regresi. Random forest juga cukup sederhana tetapi memiliki stabilitas yang mumpuni. Namun random forest  tidak akan memberikan hasil maksimal ketika data yang kita pakai sangat jarang.
      
-    Boosting Algorithm
     Pada algoritma ini parameter yang digunakan adalah learning_rate yaitu bobot yang diterapkan pada setiap regressor, dan random_state yang digunakan untuk mengontrol number generator.
     
     Boosting algorithm dapat meningkatkan performa atau akurasi prediksi. Namun hal ini tetap bergantung pada kasus per kasus, ruang lingkup masalah, dan dataset yang digunakan. 
     
Dari ketiga model yang digunakan, setelah diterapkan pada kasus ini yang terbaik adalah model Boosting Algorithm, karena meiliki nilai error yang kecil

## Evaluation
Pada evaluasi model kali ini menggunakan metrik MSE. sebelum menghitung model MSE pada model kita perlu melakukan proses scalling fitur nuerik pada model selesai dilatih dengan 3 algoritma, yaitu KNN, Random Forest, dan Boosting algorithm agar skala antara data latih dan data uji sama dan kita bisa melakukan evaluasi.
      
Jika proses scalling selesai, maka selanjutnya dilakukan evaluasi model dengan metrik MSE, yang di dapatkan hasi evaluasi yaitu:

![image](https://drive.google.com/uc?export=view&id=1PmhjESKzgWM4wl1b7WYxbEd4MoCAfwNW)

- Pada model KKN nilai data latih mencapai 1,64 dengan nilai data uji 2,49
- Pada model RF nilai data latih mencapai 8.0 dengan nilai data uji 2,15
- Pada model Boosting nilai data latih mencapai 1,81 dengan nilai data uji 2,53

untuk mengujinya, mari dibuat prediksi menggunakan beberapa harga dari data test dengan hasil berikut:

![image](https://drive.google.com/uc?export=view&id=1Lmb_WGcGlkyVtLFQPFrqr3crzUzNp93u)

<b>Sehingga dapat disimpulkan bahwa model algoritma Boosting memberikan nilai eror yang paling kecil. Model inilah yang akan kita pilih sebagai model terbaik untuk melakukan prediksi harga rumah.</b>

