# Laporan Proyek Machine Learning - Rahma Hayuning Astuti

## Project Overview
Anime merupakan salah satu hiburan berbentuk tayangan dari 2 dimensi karakter. Anime merupakan animasi yang bersal dari Jepang. 
Anime dapat dinikmati oleh berbagai kalangan usia bahkan penikmat anime tidak hanya orang Jepang melainkan sampai dengan orang yang berada di luar negeri.
Anime sangat bermanfaat untuk memenuhi kebutuhan hiburan manusia. 
Dikarenakan banyaknya peminat anime maka hingga saat ini pembuatan anime sangatlah banyak sehingga user membutuhkan sistem rekomendasi untuk dapat melihat anime lain yang sesuai dengan yang mereka sukai. Rekomendasi sistem adalah algoritma yang memprediksi suka dan tidak suka pengguna berdasarkan pada aktivitas konsumen sebelumnya (online) dan merekomendasikan item yang relevan untuk menyelesaikan krisis tersebut. Sistem rekomendasi adalah salah satu prinsip teknologi perangkat lunak yang mendasari sebagian besar layanan online di berbagai bidang seperti bidang *online shop* dan lainnya (Nitu et al., 2021).

Dalam penyelesaian masalah ini akan menggunakan  Content Based Filtering dan Collaborative Based Filtering untuk dapat memberikan rekomendasi anime dari sesama penyuka anime lain. 

## Business Understanding

### Problem Statements

- Bagaimana cara membuat sistem yang dapat merekomendasikan anime untuk user dengan anime yang disukai oleh user lain?

### Goals
- Mengetahui cara membuat sistem yang dapat merekomendasikan anime untuk user dengan anime yang disukai oleh user lain.

### Solution statements
Dalam penyelesaian masalah ini akan dilakukan dengan Content Based Filtering dan Collaborative Based Filtering

Content Based Filtering adalah sistem rekomendasi yang merekomendasikan item sesuai dengan item yang dulu disukai oleh user.

Content Based mempelajari profil dan perilaku dari pengguna yang kemudian dari informasi tersebut dianalisa dan diproses sehingga menghasilkan sistem rekomendasi yang baik. Semakin banyak informasi yang diberikan ke sistem ini, maka sistem rekomendasi berbasis content based akan memiliki akurasi yang lebih baik.

Ada 2 informasi yang penting dalam sistem rekomendasi berbasis Content Based Filtering:

- Model preferensi pengguna
- Riwayat interaksi pengguna

Kelebihan pada Content Based Filtering dibandingkan dengan Collaborative Filtering: 
- Sistem rekomendasi dapat merekomendasikan item - item berdasarkan *history* dari pengguna. Setiap pengguna memiliki preferensinya masing - masing, sehingga Content Based Filtering dapat memberikan rekomendasi item yang subjektif dan tepat dengan pengguna.

Kekurangan pada Content Based Filtering dibandingkan dengan Collaborative Filtering: 
- Sistem rekomendasi tidak dapat merekomendasikan item - item secara objektif, karena sistem rekomendasi Content Based Filtering memiliki bias terhadap riwayat profil dan perilaku pengguna.

Pada Content Based Filtering, akan membuat sistem rekomendasi yang berpusat pada tipe anime (*type*), sehingga pengguna akan mendapatkan hasil rekomendasi berdasarkan tipe anime yang telah dibaca oleh pengguna.

Collaborative Based Filtering Collaborative Based Filtering adalah sistem rekomendasi berdasarkan dari user lain. Pada Collaborative Based Filtering terdapat 2 kategori:
- Metode Berbasis Memori
     Metode berbasis memori merupakan metode di mana kita memprediksi prefresensi pengguna dari database atau sample dari pengguna lainnya. Pada model berbasis memori terdapat 2 kategori, yaitu user based dan item based.
- Metode Berbasis Model
    Metode berbasis model cukup menarik, karena di metode ini kita mengambil informasi dari kumpulan data yang kemudian diolah untuk menentukan model probabilitas untuk membuat rekomendasi. Pada model berbasis model terdapat 3 kategori, yaitu Cluster-based Algorithm, Matrix factorization, dan Deep Learning

Kelebihan pada Collaborative Based Filtering bila dibandingkan dengan Content Based Filtering:
- Pengguna dapat mengeksplorasi item atau konten di luar preferensi pengguna. 
- Pengguna pun juga dapat mendapat rekomendasi sesuai dengan kecenderungan publik yang dianalisa lewat penilaian pengguna - pengguna lainnya.

Kekurangan pada Collaborative Based Filtering:
- pengguna kurang mendapatkan rekomendasi sesuai preferensi pribadi. 
- Konten - konten yang diberikan oleh sistem rekomendasi lebih banyak berasal dari preferensi publik dan bukan preferensi pribadi.

Dalam Pembuatan rekomendasi sistem ini akan menggunakan rating dari user lain sebagai rekomendasi anime.

## Data Understanding
Dataset yang digunakan untuk proyek ini berada di Kaggle platform yang dapat diakses melalui [tautan](https://www.kaggle.com/datasets/CooperUnion/anime-recommendations-database) ini.
Dataset berisikan 2 dataframe yaitu **anime.csv** dan **rating.csv***.

Dalam anime.csv terdapat beberapa variable yaitu:

- anime_id:  Unique Id anime di myanimelist.net.
- name: Nama dari anime
- genre: List genre dalam anime yang dipisahkan dengan tanda baca koma.
- type: Tipe Anime (movie, TV, OVA, dll).
- episodes: Banyaknya episode dalam anime.
- rating: Rata-rata rating dalam skala 10 untuk per anime.
- members: Komunity member yang berada di "grup" anime tersebut.

Rating.csv terdapat variabel yaitu:
- user_id: Id user
- anime_id: anime yang user sudah nilai.
- rating: user rating dalam skala 10 (-1 tidak melakukan penilaian).

### Data Preprocessing
Sebelum memasuki data preparation akan dilakukan beberapa data preprocessing yaitu seperti:
1. Mengubah nama kolom dalam datset anime dan rating
Pengubahan nama kolom ini didasarkan agar tidak terjadi kebingungan dalam penggunaan dataset.  Perubahan yang dilakukan adalah
- kolom rating di dalam anime.csv akan diubah menjadi AverageRating menyesuaikan variabel yang sebelumnya dijelaskan.
- kolom rating di dalam rating.csv akan diubah menjadi user_rating menyesuaikan variabel yang sebelumnya dijelaskan.
2. Pembatasan Dataset dikarenakan dataset yang banyak
Dataset yang didapat berjumlah sangat besar dengan anime.csv sebesar 12294 data sedangkan rating.csv sebesar 7813737. Jumlah yang sangat besar ini akan memengaruhi dalam komputasi sehingga data yang dipakai dibatasi dalam jumlah 1000.
3. Mengubah Unknown menjadi 0 
Dalam beberapa data pada bagian kolom episodes di anime.csv dapat dilihat bahwa berisikan kalimat unknown. Pengisian unknown dalam data akan mempengaruhi dalam pembuatan sistem rekomendasi sehingga untuk memudahkan akan diubah dengan nilai 0.

### Data analysis
 Setelah melalui proses preprocessing maka akan dilihat data untuk memudahkan dalam memahami data. Visualisasi data berdasarkan univariate data analysis. Dalam visualisai ini dilakukan 2 bar plot yaitu visualiasi *type* anime dan juga *user_rating* dalam anime.
 
![Screenshot 2022-08-17 at 18-36-39 Google Colaboratory](https://user-images.githubusercontent.com/96067921/185109096-7b6b1f74-6528-411e-b895-81e7991c7e6e.png)

Dalam visualisasi diatas dapat dilihat jumlah anime berdasarkan *type anime* di dalam anime.csv

![Screenshot 2022-08-17 at 18-36-52 Google Colaboratory](https://user-images.githubusercontent.com/96067921/185109247-920077e3-e7c5-4592-8ae0-0375a7a64383.png)

Dalam visualisasi diatas dapat dilihat jumlah anime berdasarkan *user_rating anime* di dalam rating.csv

## Data Preparation
Dalam data preparation dilakukan beberapa hal sebelum memasuki pembuatan modelling Content Based Filtering dan Collaborative Based Filtering yaitu:
- Penghapusan nilai NaN 
 penghapusan nilai NaN digunakan dalam proses data preparation untuk membuang seluruh row yang memiliki NaN values. Model tidak dapat melakukan training jika terdapat nilai NaN pada *training data*.
- Pengubahan nilai -1 menjadi NaN 
pengubahan nilai -1 menjadi NaN dikarenakan -1 mengindisikan bahwa user tidak melakukan penilaian dalam anime yang mereka tonton sehingga pengubahan ini diperlukan agar mempermudah dalam persiapan data yang selanjutnya akan dihapuskan nilai NaN tersebut.

### Data Preparation di Content Based Filtering
Dalam pembuatan model Content Based Filtering terdapat tambahan untuk data preparation yaitu,

- Mengubah Dataframe dari anime menjadi sebuah list.
 Perubahan dari dataframe menjadi list menggunakan .tolist() method. Proses ini dilakukan karena list ini akan digunakan pada tahap selanjutnya menjadi dictionary baru yg akan menjadi landasan pada sistem rekomendasi.
- Memasukkan List ke Dictionary.
Setelah pembuatan list, maka perlu membuat dictionary yang digunakan untuk memnentukan pasangan key-value pada:
    - anime_id,
    - anime_name,
    - anime_genre,
    - anime_type,
    - anime_episodes,
    - anime_AveRat (average rating),
    - anime_members,
### Data Preparation di Collaborative Based Filtering
Dalam pembuatan model Collaborative Based Filtering terdapat tambahan untuk data preparation yaitu,
- mengubah user_id pada rating_data dan anime_id pada anime_dataset menjadi integer.
    Setelah dilakukan pengubahan, jumlah dari user_id dan anime_id tersebut akan disimpan pada num_users dan num_anime.
- Pembagian Data Train dan Data Valid 
Pembagian dilakukan ketika data telah semua sudah terkumpul, data yang ada harus dibagi menjadi data latih dan data validasi, akan tetapi sebelum itu kita perlu menarik sample dari dataset yang sudah ada.

## Modeling
### Modeling Content Based Filtering
dalam metode Content Based Filtering akan menggunakan TF-IDF Vectorizer untuk membangun sistem rekomendasi berdasarkan type anime.TF-IDF yang merupakan kepanjangan dari Term Frequency-Inverse Document Frequency memiliki fungsi untuk mengukur seberapa pentingnya suatu kata terhadap kata - kata lain dalam dokumen. Berikut code yang digunakan dalam pembuatan modeling dengan TF-IDF Vectorizer,

![Screenshot 2022-08-17 at 18-59-48 Google Colaboratory](https://user-images.githubusercontent.com/96067921/185113231-55c80fc8-4073-4891-b38f-a4e75578c970.png)

Code diatas akan menghasilkan kata - kata penting dalam kolom anime_type yang berasal dari attribut .get_feature_names() dari tf.
Kemudian dari string yang didapat akan dimasukkan ke dalam matriks yaitu tfidf_matrix.

Dalam sistem rekomendasi, diperlukan mencari cara agar item yang direkomendasikan tidak terlalu jauh dari data pusat atau item, oleh karena itu dibutuhkan derajat kesamaan pada item, dalam proyek ini, akan menggunakan cosine similarity untuk antar anime.
Kemudian membutuhkan fungsi anime_type_recommendation yang terdapat atribut argpartition untuk mengambil sejumlah nilai k. Fungsi tersebut akan mengembalikan 5 anime type tertinggi dari tingkat kesamaan yang berasal dari dataframe cosine_sim_df.

```
anime[anime.anime_name.eq(anime_ditonton)]
```
kode tersebut akan digunakan dalam pencarian rekomendasi tipe anime.
```
recommendations = anime_type_recommendation(anime_ditonton, cosine_sim_df, anime[['anime_name', 'anime_type']])
```
Untuk mendapatkan rekomendasi anime berdasarkan tipe dapat menggunakan code diatas. Hasil yang didapat ditampilkan dalam gambar table selanjutnya.

![Screenshot 2022-08-17 at 19-09-15 Google Colaboratory](https://user-images.githubusercontent.com/96067921/185115092-a5654601-fd2f-49cb-bfb7-9887278779d2.png)

### Modeling Collaborative Based Filtering
Dalam Modeling Collaborative Based Filtering akan menggunakan RecommenderNet. Proses compile pada model dilakukan dengan binary crossentropy sebagai loss function, adam sebagai optimizer, dan RMSE sebagai metrik dari model. Model juga dilatih dengan 20 epoch.

Sebelum pembuatan rekomendasi, akan dilakukan code untuk mengambil user_id secara acak dari rating_data. Hal ini dilakukan untuk mengetahui anime yang pernah ditonton oleh user sehingga dapat dilakukan pembuatan rekomendasi.

![Screenshot 2022-08-17 at 19-15-15 Google Colaboratory](https://user-images.githubusercontent.com/96067921/185116092-ea4dc976-585a-463a-aa77-6262a6b54417.png)

Gambar diatas merupakan hasil rekomendasi menggunakan Collaborative Based Filtering untuk user 3.
## Evaluation

### Evaluation Content Based Filtering
Dalam evaluasi model Collaborative Based Filtering digunakan Akurasi. Rumus akurasi yang digunakan adalah: Jumlah anime yang direkomendasikan sesuai dengan tipe anime / Jumlah anime yang direkomendasikan. Akurasi secara umum adalah Ratio dari True Positives dan True Negative terhadap seluruh positif dan negative di seluruh observasi. Rumus Accuracy adalah sebagai berikut

![Screenshot 2022-08-16 at 14-49-18 Classification Accuracy Machine Learning Google Developers](https://user-images.githubusercontent.com/96067921/184913891-3abda482-7316-4959-93f0-630a56e74cbd.png)

Sebelum memasuki code akurasi akan dilakukan penambahan code untuk proses pengecekan setiap type dari anime yang direkomendasikan, jika sama maka variabel type_asli akan bertambah 1. Kemudian setelah proses pengecekan akan dapat dilakukan penghitungan akurasi. 

![Screenshot 2022-08-17 at 19-29-13 Google Colaboratory](https://user-images.githubusercontent.com/96067921/185121938-c52f199f-ec23-4629-920b-370a13cd4f36.png)

Gambar diatas merupakan code dan hasil dari akurasi model yang telah dibuat.

### Evaluation Collaborative Based Filtering
Dalam evaluasi model Collaborative Based Filtering digunakan RMSE. RMSE adalah hasil dari akar MSE membuat RMSE memiliki nilai yang lebih kecil dibandingkan dengan MSE. RMSE sering digunakan untuk perbedaan antara nilai (nilai sampel atau populasi) yang diprediksi oleh model atau penduga dan nilai yang diamati.
Rumus RMSE:

![22](https://user-images.githubusercontent.com/96067921/185116677-e75af030-ab14-42a3-831e-ba65480218e1.JPG)

- At = Nilai data Aktual 
- Ft = Nilai hasil peramalan 
- N = banyaknya data 
- ∑ = Summation (Jumlahkan keseluruhan nilai)

RMSE memiliki nilai yang lebih kecil daripada MSE sehingga error yang dihasilkan akan sedikit.
Berikut grafik RMSE dari model yang telah dibuat.

![Screenshot 2022-08-17 at 19-21-07 Google Colaboratory](https://user-images.githubusercontent.com/96067921/185117142-eb968b62-2b9d-41cb-a063-9e92b35e9ceb.png)


## Kesimpulan
Dalam pembuatan rekomendasi sistem dapat dilakukan dengan 2 cara yaitu Content Based Filtering dan juga Collaborative Based Filtering. Kedua cara tersebut memiliki kelebihan dan kekurangan masing-masing yang dapat dikembangkan labih baik lagi. 

## Referensi
[Nitu, P., Coelho, J., & Madiraju, P. (2021). Improvising personalized travel recommendation system with recency effects. Big Data Mining and Analytics, 4(3), 139–154.](https://doi.org/10.26599/BDMA.2020.9020026)

