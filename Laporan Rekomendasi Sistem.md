# Laporan Proyek Machine Learning - Rahma Hayuning Astuti

## Project Overview
Anime merupakan salah satu hiburan berbentuk tayangan dari 2 dimensi karakter. Anime merupakan animasi yang bersal dari Jepang. 
Anime dapat dinikmati oleh berbagai kalangan usia bahkan penikmat anime tidak hanya orang Jepang melainkan sampai dengan orang yang berada di luar negeri.
Anime sangat bermanfaat untuk memenuhi kebutuhan hiburan manusia. 
Dikarenakan banyaknya peminat anime maka hingga saat ini pembuatan anime sangatlah banyak sehingga user membutuhkan sistem rekomendasi untuk dapat melihat anime lain yang sesuai dengan yang mereka sukai. 
Dalam penyelesaian masalah ini akan menggunakan collaborative filtering untuk dapat memberikan rekomendasi anime dari sesama penyuka anime lain. 

## Business Understanding

### Problem Statements

- Bagaimana cara membuat sistem yang dapat merekomendasikan anime untuk user dengan anime yang disukai oleh user lain?

### Goals
- Mengetahui cara membuat sistem yang dapat merekomendasikan anime untuk user dengan anime yang disukai oleh user lain.

### Solution statements
Dalam penyelesaian masalah ini akan dilakukan dengan Collaborative Based Filtering.
Collaborative Based Filtering Collaborative Based Filtering adalah sistem rekomendasi berdasarkan pendapat suatu komunitas. Pada Collaborative Based Filtering terdapat 2 kategori:
- Metode Berbasis Memori: Metode berbasis memori merupakan metode di mana kita memprediksi prefresensi pengguna dari database atau sample dari pengguna lainnya. Pada model berbasis memori terdapat 2 kategori, yaitu user based dan item based.
- Metode Berbasis Model: Metode berbasis model cukup menarik, karena di metode ini kita mengambil informasi dari kumpulan data yang kemudian diolah untuk menentukan model probabilitas untuk membuat rekomendasi. Pada model berbasis model terdapat 3 kategori, yaitu Cluster-based Algorithm, Matrix factorization, dan Deep Learning

Kelebihan pada Collaborative Based Filtering bila dibandingkan dengan Content Based Filtering adalah pengguna dapat mengeksplorasi item atau konten di luar preferensi pengguna. Pengguna pun juga dapat mendapat rekomendasi sesuai dengan kecenderungan publik yang dianalisa lewat penilaian pengguna - pengguna lainnya.

Kekurangan pada Collaborative Based Filtering adalah pengguna kurang mendapatkan rekomendasi sesuai preferensi pribadi. Konten - konten yang diberikan oleh sistem rekomendasi lebih banyak berasal dari preferensi publik dan bukan preferensi pribadi.

Dalam Pembuatan rekomendasi sistem ini akan menggunakan metode berbasis memori untuk Collaborative Based Filtering.
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

Sebelum memasuki data preparation akan dilakukan EDA dengan cara melihat data di dataset terlebih dahulu.

![Screenshot 2022-08-17 at 09-14-48 Google Colaboratory](https://user-images.githubusercontent.com/96067921/185019765-83364413-2a3b-4a04-b9fc-8700b4b66520.png)

Dari gambar diatas dapat dilihat data yag terdapat di anime.csv

![Screenshot 2022-08-17 at 09-16-20 Google Colaboratory](https://user-images.githubusercontent.com/96067921/185019852-3e34fc63-086b-4a0c-a290-b29c2ad5a0f1.png)

Gambar yang kedua merupakan data yang terdapat dalam rating.csv
Selain melihat data yang terdapat dalam dataset juga diperlukan mencari informasi mengenai dataset.

## Data Preparation
Dalam data preparation saya melakukan beberapa hal yaitu:
1. Mengubah nilai -1 dalam Rating.csv menjadi NaN. 
    Hal ini perlu dilakukan karena -1 mengartikan bahwa user tidak melakukan rating terhadap anime
dan agar mudah nantinya untuk dihapus.
2. Penghapusan nilai NaN 
    Nilai NaN yang ada akan dihapuskan sehingga dapat digunakan dengan lebih baik.
3. Limitasi Data 
    Dataset yang didapat berjumlah besar sehingga perlu dilakukan limitasi data yang dipakai untuk tidak terjadinya komputasi besar.
    dalam hal ini saya menggunakan data sebanyak 1000.
4. Pengelompokan Anime berdasarkan *Type*
    Pengelompokan anime berdasarkan type dilakukan karena dalam sistem rekomendasi ini hanya akan mengambil salah satu tipe anime saja untuk mempermudah. 
    Pengelompokan ini berdasarkan dari rating anime per tipe yang ada.
    
    ![Screenshot 2022-08-17 at 09-27-27 Google Colaboratory](https://user-images.githubusercontent.com/96067921/185021194-d39802c4-8f5f-48b8-966a-f897061e2299.png)
    
    Dalam grafik tersebut ditunjukan perbandingan rating antara tipe anime
    
    ![Screenshot 2022-08-17 at 09-27-41 Google Colaboratory](https://user-images.githubusercontent.com/96067921/185021244-a033bb18-55d4-4c80-9608-9d97bb2dfe6a.png)

    Hasil rata-rata rating anime berdasarkan tipe anime. Dari hasil diatas dapat dilihat bahwa tipe tv memiliki peringkat tertinggi sedangkan tipe music memiliki rating terendah.
    Untuk dalam sistem rekomendasi ini akan menggunakan tipe music dikarenakan memiliki rating yang paling rendah.

## Modeling
Dikarenakan collaborative based filtering menggunakan jenis Metode Berbasis Memori maka dalam pembuatan sistem rekomendasi tidak menggunakan model. 

## Metode Berbasis Memori
Dalam pembuatan collaborative based filtering ini akan menggunakan pivot table untuk mempermudah dalam melakukan penentuan similarity.
Tabel pivot akan membantu dalam menentukan kesamaan antara user dan anime untuk memprediksi lebih baik siapa yang akan menyukai anime apa.
Setelah pembuatan table pivot maka akan diperlukan normalisasi terhadap value yang ada. Tujuan normalisasi adalah untuk mengubah nilai kolom numerik dalam kumpulan data untuk menggunakan skala umum, tanpa mendistorsi perbedaan dalam rentang nilai atau kehilangan informasi.
Kemudian akan dilakukan sparse matrix dan cosine similarity. Sparse matrix dilakukan karena data akan digunakan dengan cosine similarity.

Cosine similarity mengukur kesamaan antara dua vektor dan menentukan apakah kedua vektor tersebut menunjuk ke arah yang sama. 
Ia menghitung sudut cosinus antara dua vektor. Semakin kecil sudut cosinus, semakin besar nilai cosine similarity. 
Cosine similarity digunakan untuk penghitungan antara user similarity dan item similarity. Cosine similarity pada umumnya memiliki rumus.


![dos 784efd3d2ba47d47153b050526150ba920210910171725](https://user-images.githubusercontent.com/96067921/185022912-508d4046-0307-42de-8c60-c1ffa0150161.jpeg)

Kemudian data yang sudah melalui cosine similarity akan dimasukan ke dataframe object.

### Function 

Dikarenakan tidak memakai model maka akan menggunakan function untuk mendapatkan hasil sistem rekomendasi. Beberapa fungsi yang dibuat adalah:
- top_animes(anime_name):Fungsi yang akan mengembalikan anime yang memiliki similarity tertinggi
- top_users(user):Fungsi yang akan mengembalikan sesama user yang memiliki similarity tertinggi.
- similar_user_recs(user): Fungsi yang digunakan untuk membuat daftar yang berisi anime dengan rating tertinggi per user similarity.
- predicted_rating(anime_name, user): Fungsi yang digunakan untuk memprediksi rating yang diberikan user terhadap anime tertentu.

Beberapa contoh dalam penggunaan function 

![Screenshot 2022-08-17 at 09-59-04 Google Colaboratory](https://user-images.githubusercontent.com/96067921/185025116-058da000-f409-48e3-b8b2-6639c09a3c46.png)


![Screenshot 2022-08-17 at 09-59-59 Google Colaboratory](https://user-images.githubusercontent.com/96067921/185025177-50ee335e-261c-4db4-9348-e662f835f80f.png)



Dalam penggunaan metode ini terdapat kelebihan yaitu tidak memerlukan komputasi yang tinggi dan pengolahan data juga cepat. 
Sedangkan untuk kekurangan yang ada adalah tidak dapat mengetahui apakah memiliki hasil yang bagus atau tidak.

## Evaluation
Pada bagian evaluasi dilakukan dengan mean squared error terhadap antara prediksi dan *actual* value. 
Sebelumnya Mean Squared Error (MSE) adalah menghitung jumlah selisih kuadrat rata-rata nilai sebenarnya dengan nilai prediksi. MSE didefinisikan dalam persamaan berikut


![2021071619431112f1106e20559e77c855cea11d1b1479](https://user-images.githubusercontent.com/96067921/185024354-33d8c7c3-7a7a-4f91-90f6-bb2f4dea3457.jpeg)

dengan keterangan:
- N = jumlah dataset
- yi = nilai sebenarnya
- y_pred = nilai prediksi

![Screenshot 2022-08-17 at 09-50-59 Google Colaboratory](https://user-images.githubusercontent.com/96067921/185024021-4cfecb80-6325-4783-a99e-916f66ea1d99.png)

Code dalam melakukan evaluasi.

![Screenshot 2022-08-17 at 09-51-29 Google Colaboratory](https://user-images.githubusercontent.com/96067921/185024670-20923a2f-efff-4b3f-9241-175c80950e84.png)

Hasil Mean Squareed Error dalam prediksi di sistem rekomendasi 




