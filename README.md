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
- Membaca data-data yang telah di download dengan menggunakan fungsi pandas. terdapat 9742 film dan 951 genre
- lalu melakukan Exploratory Data Analysis, yang bertujuan  untuk mengetahui apakah tipe data pada setiap kolom sudah sesuai atau belum
- Menggabungkan file movie, dan rating ke dalam dataframe movie_info 
- mengecek apakah terdapat missing value atau tidak. setelah di cek tidak ada yang mengalami missing value
- Menggabungkan Data dengan Fitur film Pertama, mendefinisikan variabel all_movie_rate dengan variabel rating yang telah kita ketahui sebelumnya, kemudian definisikan dataframe rating ke dalam variabel all_movie_rate
- Selanjutnya, untuk mengetahui judul film dengan movieId tertentu, dilakukan penggaungan data movies yang berisikan movieId dan judul berdasarkan movieId dan assign ke variabel all_movie_name 
- Menggabungkan Data dengan Fitur gendre film. Langkah selanjutnya adalah menggabungkan variabel all_movie_name diperoleh dari tahapan sebelumnya dengan fitur gendre film. Tujuannya, agar kita mengetahui gendre pada film tersebut

## Data Preparation
- Mengurutkan film berdasarkan movieId kemudian memasukkannya ke dalam variabel fix_movie
- Membuat variabel preparation yang berisi dataframe fix_movie kemudian mengurutkan berdasarkan movieId
- Pada proses pemodelan kali ini hanya mengguakan daya unik, jadi perlu dilakukan penghapusan data yang duplikat dengan fungsi drop_duplicates(). Dalam hal ini, kita membuang data duplikat pada kolom ‘movieId’
- Melakukan konversi data series menjadi list. Dalam hal ini, kita menggunakan fungsi tolist() dari library numpy
- Membuat dictionary untuk data ‘movie_id’, movie_title, dan movie_genre

## Modeling
Pada tahap modeling model Content Based Filtering dnegan tahapan sebagai berikut:
- TF-IDF Vectorizer
  Pada tahap ini, adalah tahap untuk membangun sistem rekomendasi sederhana berdasarkan genre pada film. Teknik ini digunakan pada sistem rekomendasi untuk menemukan representasi fitur penting dari setiap genre. pada proyek ini, kita menggunakan fungsi tfidfvectorizer() dari library sklearn. untuk melihat matriks tf-idf ke beberapa movie (movie_title) dan kategori genre (genre) dibuat dataframe untuk melihat tf-idf matrix dengan ketentuan Kolom diisi dengan genre dan Baris diisi dengan judul film

- Cosine Similarity
  pada tahap ini bertujuan untuk menghitung derajat kesamaan (similarity degree) antar film dengan teknik cosine similarity

## Evaluation

keluaran sistem rekomendasi ini adalah berupa top-N recommendation. Oleh karena itu, kita memberikan sejumlah rekomendasi restoran pada pengguna yang diatur dalam parameter k. Dengan menggunakan argpartition, kita mengambil sejumlah nilai k tertinggi dari similarity data (dalam kasus ini: dataframe cosine_sim_df). Kemudian, mengambil data dari bobot (tingkat kesamaan) tertinggi ke terendah. Data ini dimasukkan ke dalam variabel closest. Berikutnya, kita perlu menghapus movie_title yang yang dicari agar tidak muncul dalam daftar rekomendasi.
Dalam kasus ini, nanti kita akan mencari film yang mirip dengan Toy Story (1995), sehingga kita perlu drop Toy Story (1995) agar tidak muncul dalam daftar rekomendasi yang diberikan nanti. 
setekah dilakukan pencarian film yang mirip dengan Toy Story (1995) didapatkan hasil seperti pada gambar berikut:

![image](https://drive.google.com/uc?export=view&id=1h7cQD0GzURiJwV7BDH0oa5URLJswa4mR)
