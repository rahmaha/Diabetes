# Laporan Proyek Machine Learning - Rahma Hayuning Astuti

## Domain Proyek

Pada proyek predictive analysis ini akan membahas dalam bidang kesehatan yaitu Diabetes. 

Diabetes adalah penyakit dengan ciri meningkatnya kadar gula atau glukosa dalam darah. Glukosa adalah sumber energi dari makanan. Glukosa dapat diserap oleh sel dengan bantuan insulin. Insulin dihasilkan oleh pankreas dalam tubuh. Diabetes merupakan salah satu penyakit yang berbahaya di dunia dan juga banyak penderitanya. Diabetes juga menjadi penyebab kematian terbesar di dunia. Diabetes jika tidak segera ditangani akan dapat mengakibatkan berbagai macam penyakit lainnya seperti stroke, penyakit jantung, gangguan penglihatan dan lainnya. Pencegahan dan pengobatan diabetes hanya dapat dilakukan dengan dengan diet, aktivitas fisik, pengobatan, dan pemeriksaan rutin serta pengobatan untuk komplikasi. Pencegahan dan pemeriksaan dapat dengan berkonsultasi langsung terhadap dokter.

Dalam pemeriksaan pasien oleh dokter dapat dibantu dengan perkembangan teknologi saat ini. Banyak riset yang menunjukkan bahwa machine learning dapat membantu dalam memprediksi suatu penyakit. Hal ini dikarenakan machine learning dapat mengolah data yang banyak seperti data potensi diabetes sehingga dapat membantu dalam memprediksi. Dalam riset prediksi diabetes menggunakan machine learning yang telah dilakukan terdapat beberapa algoritma yang digunakan yaitu seperti SVM, Naïve Bayes, Decision Tree, Random Forest dan masih banyak lainnya. Algoritma tersebut memiliki keunggulan masing-masing. Algoritma yang digunakan dalam penelitian ini adalah decision tree dan random forest. Kedua algoritma tersebut digunakan untuk klasifikasi karena terdapat banyak penelitian yang menunjukan hasil algoritma ini dengan baik. 

Desion tree adalah algoritma supervised learning yang digunakan untuk klasifikasi. Tujuan metode ini adalah untuk memprediksi nilai kelas dari variabel target. Desion tree akan membantu untuk memisahkan kumpulan data dan membangun model untuk memprediksi label kelas yang tidak diketahui (Sneha & Gangil, 2019). Random forest juga merupakan algoritma supervised learning. Algoritma ini biasa digunakan untuk kalsifikasi dan regression. Perbedaan antara random forest dan desion tree adalah proses menemukan simpul akar dan pemisahan simpul fitur akan berjalan secara acak (Sneha & Gangil, 2019).

Dalam sebuah riset prediksi diabetes menunjukan bahwa decision tree menghasilkan akurasi sebesar 86% sedangkan random forest menghasilkan akurasi sebesar 91% (Mujumdar & Vaidehi, 2019). Hasil riset lain menunjukan juga bahwa algoritma decision tree dan random forest memiliki
spesifisitas tertinggi 98,20% dan 98,00%, masing-masing memegang yang terbaik untuk analisis data diabetes (Sneha & Gangil, 2019).
Berdasarkan hasil riset dalam prediksi diabetes menggunakan algoritma random forest dan decision tree, maka akan diimplementasikan dalam proyek ini.

  Referensi:
  [Sneha, N., & Gangil, T. (2019). Analysis of diabetes mellitus for early prediction using optimal features selection. Journal of Big Data, 6(1).](https://doi.org/10.1186/s40537-019-0175-6) 
  [Mujumdar, A., & Vaidehi, V. (2019). Diabetes Prediction using Machine Learning Algorithms. Procedia Computer Science, 165, 292–299.](https://doi.org/10.1016/j.procs.2020.01.047) 


## Business Understanding


### Problem Statements
Berdasarkan literatur pada bagian domain proyek, diketahui bahwa terdapat masalah dalam mendeteksi kemungkinan seseorang mengalami diabetes sehingga memerlukan algoritma yang dapat memprediksi diabetes. Dalam penelitian ini akan di fokuskan pembahasan mengenai:
1. Bagaimana hasil akurasi dari kedua model tersebut?
2. Manakah algoritma model yang mendapatkan akurasi terbaik?

### Goals

Dengan tujuan pembahasan penelitian yang lebih fokus, maka pada proyek ini akan membahas mengenai beberapa hal yaitu
1. Melakukan proses prediksi diabetes menggunakan data dalam format csv.
2. Akan dilakaukan perbandingan hasil dari model prediksi diabetes antara algoritma satu dengan algoritma lain.


## Data Understanding

Dataset yang digunakan merupakan dataset dalam format csv. Dataset dapat diunduh atau di akses melalui Kaggle platform. Dataset berisikan tentang beberapa medical predictor varible seperti pregnancies dan lainnya untuk memprediksi apakah pasien menderita penyakit diabetes atau tidak.
Sumber dataset [Kaggle Pima Indians Diabetes Database](https://www.kaggle.com/datasets/uciml/pima-indians-diabetes-database).


### Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:

- Pregnancies:Number of Pregnancy
- Glucose:2-hour plasma glucose concentration in the oral glucose tolerance test
- Blood Pressure: Blood Pressure (Small Blood Pressure) (mmHg)
- SkinThicknessSkin:Thickness
- Insulin:2-hour serum insulin (mu U/ml)
- DiabetsPedigreeFunction:A function that calculates the probability of having diabetes according to one's descendants
- BMI: Body mass index
- Age : (Type: Year)
- Outcome:1 positive indicates does have diabetes, 0 indicates negative does not have diabetes.


Visualisasi Dataset:
- Visualisasi data akan dilakukan terhadap dataset yang ada untuk mengetahui jenis data dan missing value.
[image3]

## Data Preparation
Dalam pembuatan model perlu dilakuakn data preparation agar model dapat berjalan dengan lebih baik. Data pre-paration yang ada adalah:
1. Mengubah nilai 0 dalam beberapa feature menjadi NaN
    Pengubahan ini dilakukan karena dalam beberapa feature yang ada berisikan nilai 0 yang kemungkinan besar seorang pasien atau manusia tidak akan mendapatkan nilai 0. Pengubahan nilai 0 menjadi NaN juga didasarkan bahwa ada kemungkinan bahwa data tersebut tidak diisi atau data yang hilang sehingga berisakan nilai 0. Feature yang dilakukan perubahan adalah nilai 0 menjadi NaN adalah:
    - Glucose
    - Insulin
    - BMI

2. Check dan Hapus Outlier.
    Dalam datset yang ada biasanya terdapat outlier. Outlier dihapuskan karena outlier mewakili kesalahan pengukuran, entri data atau kesalahan pemrosesan, atau pengambilan sampel yang buruk. 
    [imageeeee]
3. Melakukan pengubahan nilai NaN dengan nilai Median.
    Pengubahan nilai NaN dengan nilai Median dikarenakan jika tidak dilakukan perubahan akan mempengaruhi model dan nilai media dipilih karena median merupakan nilai tengah dari data yang sudah ada.

## Modeling
1. Feature selection 
    dalam pembuatan model feature yang dipakai merupakan semua feature yang ada kecuali feature outcome. Feature yang dipakai  adalah Pregnancies, Glucose, Blood Pressure, SkinThicknessSkin:Thickness, Insulin, DiabetsPedigreeFunction, BMI, Age
2. StandardScaler
    setelah pemilihan feature maka akan dilakukan standard scaler terhadap feature yang dipilih.
3. Pembuatan Model
  a. Random Forest
      Random Forest memiliki beberapa kelebihan dalam penggunaanya yaitu:
      - lebih akurat daripada algoritma decision tree.
      - menyediakan cara yang efektif untuk menangani data yang hilang.
      - dapat menghasilkan prediksi yang masuk akal tanpa penyetelan parameter hiper.
      - memecahkan masalah overfitting di pohon keputusan.
      kekurangan:
      Keterbatasan utama dari random forest adalah bahwa sejumlah besar pohon dapat membuat algoritme terlalu lambat dan tidak efektif untuk prediksi di real time. Secara umum, algoritme ini cepat untuk dilatih, tetapi cukup lambat untuk membuat prediksi setelah dilatih.
  b. Decision Tree
      Decision tree memiliki beberapa keuntungan yaitu:
      - dapat digunakan untuk masalah klasifikasi dan regresi
      - dapat menangkap hubungan nonlinier: Mereka dapat digunakan untuk mengklasifikasikan data yang tidak dapat dipisahkan secara linier.
      - tidak memerlukan transformasi fitur apa pun jika kita berurusan dengan data non-linier karena pohon keputusan tidak memperhitungkan banyak kombinasi berbobot secara bersamaan.
      - Mudah dipahami, diinterpretasikan, divisualisasi
      - dapat menangani semua jenis data apakah itu numerik atau kategorikal, atau boolean.
      beberapa kekurangan:
      - mudah overfitting

    Kedua algoritma tersebut sangat mudah dipelajari dan digunakan. 

4. Hasil Perbandingan
dari pemodelan yang ada random forest memiliki hasil akurasi yang lebih tinggi

## Evaluation

Model yang dibuat akan di evaluasi menggunakan tiga metrik yaitu akurasi, precision dan recall.
a. Random Forest
    Accuracy = 0.7575757575757576
    Recall = 0.6097560975609756
    precision = 0.6097560975609756

b. Decision Tree
    Accuracy = 0.7348484848484849
    Recall = 0.5714285714285714
    precision = 0.5853658536585366

Akurasi adalah salah satu metrik untuk mengevaluasi model klasifikasi. Secara informal, akurasi adalah sebagian kecil dari prediksi model  yang benar. Secara formal, akurasi memiliki definisi sebagai berikut:

Precision digunakan untuk menjawab pertanyaan seperti:
     Berapa proporsi identifikasi positif yang sebenarnya benar?

Recall digunakan untuk menjawab pertanyaan seperti:
      Berapa proporsi positif aktual yang diidentifikasi dengan benar?


**---Ini adalah bagian akhir laporan---**



