# ProyekAkhir_MLTerapan - SITI YULIANINGSIH
laporan proyek akhir Machine Learning terapan membuat sistem rekomendasi film. SIB3 Kampus merdeka dicoding

## Domain Proyek
Pertumbuhan penduduk yang terus meningkat mendorong tingginya kebutuhan masyarakat akan tempat tinggal. Tempat tinggal atau rumah merupakan salah satu dari banyaknya kebutuhan primer bagi manusia.  Maka dari itu sangat penting untuk membuat perencanaan agar tiap keluarga dapat memiliki tempat tinggal pribadi.  Dalam perencanaan tersebut dibutuhkan prediksi atau perkiraan harga di masa mendatang.  Tiap manusia membutuhkan rumah untuk tempat berlindung dan sebagai tempat berkumpul dan berlangsungnya aktivitas keluarga, sekaligus sebagai sarana investasi. Fungsi rumah juga telah berubah, dari yang semula hanya sekedar sebagai tempat berlindung. Kini sebuah rumah tak cukup hanya untuk berteduh namun juga dituntut untuk mengakomodir kebutuhan dan keinginan pemiliknya. Seperti luas lahan, luas bangunan  berdiri,  banyaknya  ruangan,  hingga  ketersediaan  tempat  parkir  mobil.

Harga adalah salah satu hal yang dipertimbangkan oleh pembeli rumah oleh masyarakat. menurut penelitian yang dibuat oleh Agustinus Primnanda Alasan masyarakat mempertimbangkan faktor harga karena hal tersebut berkaitan dengan pendapatan mereka. Bagi mereka yang memiliki pendapatan besar mungkin harga tidak akan menjadi masalah, tapi mereka lebih mempertimbangkan luas dan kualitas produk dalam hal ini faktor bangunan.
Dengan melihat kondisi semacam ini mendorong produsen untuk melebarkan sayapnya di bidang perumahan. Maka tidak mengherankan jika akhirakhir ini bisnis di bidang perumahan semakin marak, banyak perusahaan muncul dengan memberikan berbagai macam fasilitas dalam menawarkan produknya. Perkembangan bisnis perumahan semakin marak dewasa ini, tidak hanya terpusat di kota-kota besar akan tetapi sudah meluas di kota-kota kecil.
penelitian agustinus:[FAKTOR-FAKTOR YANG MEMPENGARUHI KONSUMEN DALAM MEMBELI RUMAH)(http://eprints.undip.ac.id/23081/)

## Business Understanding
### Problem Statements
Suatu perusahaan harus selalu survive agar dapat terus bersaing dengan perusahaan-perusahaan sejenis yang sama-sama bergerak dalam bisnis perumahan. Karena banyaknya perusahaan yang bergerak di bidang perumahan, maka perusahaan harus mengenali apa yang mempengaruhi harga jual pada perumahan lain. Jangan sampai kita yang seharusnya mendapat keuntungan karna terdapat kualitas yang bagus pada perumahan kita, kita malah menjualnya dengan harga rendah.
Berdasarkan kondisi yang telah diuraikan sebelumnya, perusahaan akan mengembangkan sebuah sistem prediksi harga rumah untuk menjawab permasalahan berikut:
- Fitur apa yang paling mempengaruhi harga rumah?

### Goals
- Mengetahui fitur yang paling berkorelasi dengan harga rumah.

**Metodologi**
Prediksi harga adalah tujuan yang ingin dicapai. Seperti yang kita tahu, harga merupakan variabel kontinu. Dalam predictive analytics, saat membuat prediksi variabel kontinu artinya Anda sedang menyelesaikan permasalahan regresi. Oleh karena itu, metodologi pada proyek ini adalah: membangun model regresi dengan harga diamonds sebagai target.
**Metrik**
Pengembangan model akan menggunakan beberapa algoritma machine learning yaitu K-Nearest Neighbor, Random Forest, dan Boosting Algorithm. Dari ketiga model ini, akan dipilih satu model yang memiliki nilai kesalahan prediksi terkecil.

## Data Understanding
Data yang akan digunakan pada proyek kali ini adalah housePrice dataset. Dataset ini memiliki 3.474 sampel data dengan berbagai kualitas atau karakteristik dan harga. Karakteristik yang dimaksud di sini adalah fitur non-numerik seperti Parking, Warehouse, Elevator, address, serta fitur numerik seperti address, Room dan  Area. Kesembilan fitur ini adalah fitur yang akan Anda gunakan dalam menemukan pola pada data, sedangkan harga merupakan fitur target.
Adapun uraikanlah seluruh variabel atau fitur pada data, sebagai berikut:

- Parking: adalah keterangan apakah rumah tersebut tersedia tempat parker atau tidak

- Warehouse: berisi informasi apakah rumah terdapat Gudang atau tidak
- Elevator: informasi apakah rumah terdapat tangga  atau tidak
- Room: informasi yang berisi ada berapa ruangan pada rumah tersebut
- Area: informasi mengenai luas bangunan
- Price: informasi harga
- address: berisi informasi tempat rumah tersebut berada
- price(USD): berisi informasi harga dalam USD

Dataset dapat di unduh pada link berikut: [housePrice dataset](https://www.kaggle.com/datasets/mokar2001/house-price-tehran-iran)

- hal pertama yang dilakukan adalah import library yang dibutuhkan
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

