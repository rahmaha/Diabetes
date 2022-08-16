# Laporan Proyek Machine Learning - Rahma Hayuning Astuti

## Domain Proyek
PIMA Indians Diabetes Dataset merupakan dataset yang berasal dari National Institute of Diabetes and Digestive and Kidney Diseases. Objektif dari dataset ini adalah untuk diagnosa apakah seorang pasien mengalami diabetes atau tidak berdasarkan pengukuran diagnostik tertentu yang disertakan dalam dataset. Dataset ini umumnya dipakai dari data scientist pemula hingga dapat dilakukan sebagai objek penelitian. 

Diabetes adalah penyakit dengan ciri meningkatnya kadar gula atau glukosa dalam darah. Glukosa adalah sumber energi dari makanan. Glukosa dapat diserap oleh sel dengan bantuan insulin. Insulin dihasilkan oleh pankreas dalam tubuh. Diabetes merupakan salah satu penyakit yang berbahaya di dunia dan juga banyak penderitanya.

Dalam perkembangan teknologi saat ini, dokter dapat dibantu dengan kecerdasan buatan untuk mendiagnosa apakah pasien menderita diabetes atau tidak. Untuk mendiagnosa dengan bantuan kecerdasan buatan maka perlu dibuat model. Pembuatan model tersebut akan membutuhkan algoritma. Beberapa penelitian menunjukan bahwa terdapat beberapa algoritma yang dapat digunakan seperti Decision Tree dan Random Forest. 

Di dalam dataset ini, model akan melakukan prediksi apakah pasien menderita dari penyakit diabetes atau tidak. Penyelesaian masalah dalam model akan dilakukan dengan klasifikasi.

## Business Understanding

### Problem Statements
- Apakah pasien menderita penyakit diabetes atau tidak?

### Goals
- Melakukan prediksi apakah pasien menderita penyakit berdasarkan dari *medical predictor variable* yang terdapat dalam dataset.

### Solution Statements:
- Melakukan analisis dan *pre-processing data* yang terdapat dalam dataset.
- Melakukan pembuatan model machine learning untuk mengetahui apakah pasien menderita penyakit diabetes atau tidak. Model yang dibuat adalah model yang dapat mudah dipelajari. Model yang dipakai adalah:
   1. Random Forest
   2. Decision Tree

## Data Understanding

Dataset yang digunakan merupakan dataset dalam format csv. Dataset dapat diunduh atau di akses melalui Kaggle platform. Dataset berisikan tentang beberapa *medical predictor varible* seperti *pregnancies* dan lainnya untuk memprediksi apakah pasien menderita penyakit diabetes atau tidak.
Datset dapat di download di [Kaggle Pima Indians Diabetes Database](https://www.kaggle.com/datasets/uciml/pima-indians-diabetes-database).

### Variabel-variabel pada PIMA Indians Diabetes Dataset adalah sebagai berikut:

- *Pregnancies*: Jumlah kehamilah
- *Glucose*: Konsentrasi glukosa plasma 2 jam dalam tes toleransi glukosa oral
- *Blood Pressure*: Tekanan darah (*Small Blood Pressure*) (mmHg)
- *SkinThickness*: Ketebalan Kulit
- Insulin:2 jam serum insulin (mu U/ml)
- *DiabetsPedigreeFunction*: Sebuah fungsi yang menghitung kemungkinan menderita diabetes menurut keturunannya
- BMI: *Body mass index* berat badan
- *Age* : Umur (tipe: tahun)
- *Outcome*:1 positif menunjukkan memang memiliki diabetes, 0 menunjukkan negatif tidak menderita diabetes.

### Visualisasi Dataset:

Berikut visualisasi data yang digunakan sebelum *pre-processing data* untuk melakukan analisis. 

![Screenshot 2022-08-16 at 21-49-44 ddddddd png (PNG Image 1486 × 1416 pixels) — Scaled (42%)](https://user-images.githubusercontent.com/96067921/184910000-da5e2d20-9299-4c47-87be-82a4e88e0580.png)

Visualisi yang pertama dilakukan untuk melihat pengelompokkan data menggunakan *hue* yang berasal dari Outcome data terhadap feature lainnya.

![Screenshot 2022-08-16 at 15-16-43 Google Colaboratory](https://user-images.githubusercontent.com/96067921/184883659-cce6debe-0893-4fd7-862d-6f81e7206917.png)

Visualisasi displot digunakan untuk visualisasi histogram berdasarkan data yang terdapat dalam tiap feture. Dari visualisi penggunaan displot dapat dilihat bahwa data perlu dilakukan *standard* dikarenakan memiliki rentang yang berbeda.

![Screenshot 2022-08-16 at 21-46-31 Google Colaboratory](https://user-images.githubusercontent.com/96067921/184909567-2359b2f1-7af9-4802-997a-50296d70e054.png)

Visualisasi terakhir menggunakan heatmap menunjukan bahwa semua feature yang ada berpengaruh terhadap outcome.

## Data Preparation

Dalam pembuatan model perlu dilakuakn data preparation agar model dapat berjalan dengan lebih baik. Data pre-paration yang ada adalah:

1. Mengubah nilai 0 dalam beberapa feature menjadi NaN
   Pengubahan ini dilakukan karena dalam beberapa feature yang ada berisikan nilai 0 yang kemungkinan besar seorang pasien tidak akan mendapatkan nilai 0. Pengubahan nilai 0 menjadi NaN juga didasarkan bahwa ada kemungkinan bahwa data tersebut tidak diisi atau data yang hilang sehingga berisikan nilai 0. Feature yang dilakukan perubahan nilai 0 menjadi NaN adalah:

   - Glucose
   - Insulin
   - BMI

2. Check dan Hapus Outlier.
   Dalam datset yang ada biasanya terdapat outlier. Outlier dihapuskan karena outlier mewakili kesalahan pengukuran, entri data atau kesalahan pemrosesan, atau pengambilan sampel yang buruk. Sebelum melakukan penghapusan outlier akan dilakukan visualisasi dulu dalam beberapa feature untuk mengetahui apakah terdapat outlier.
   
   ![Screenshot 2022-08-16 at 21-51-58 blood png (PNG Image 389 × 235 pixels)](https://user-images.githubusercontent.com/96067921/184910447-0f378ea1-9e30-42e8-991f-a12a82207406.png)
   
   Gambar tersebut merupakan plot yang dilakukan dalan feature *BloodPressure* terlihat bahwa terdapat outliers.
   
   ![Screenshot 2022-08-16 at 21-51-34 glucose png (PNG Image 389 × 235 pixels)](https://user-images.githubusercontent.com/96067921/184910556-e854fb99-700d-4315-9ded-c6084369e6fb.png)

    Gambar tersebut merupakan plot yang dilakukan dalan feature *Glucose* tidak terlihat terdapat outliers. Dari kedua gambar tadi dapat disimpulkan bahwa terdapat kemungkinan outliers sehingga perlu dilakukan penghapusan outlier.
    
3. Melakukan pengubahan nilai NaN dengan nilai Median.
   Pengubahan nilai NaN dengan nilai Median dikarenakan jika tidak dilakukan perubahan akan mempengaruhi model dan nilai median dipilih karena median merupakan nilai tengah dari data yang sudah ada.
   
 4. Feature Selection
    Dalam pembuatan model feature yang dipakai merupakan semua feature yang ada kecuali feature outcome. Feature yang dipakai adalah Pregnancies, Glucose, Blood Pressure, SkinThicknessSkin:Thickness, Insulin, DiabetsPedigreeFunction, BMI, Age.
 
 5. Standarisasi Data
    Data yang ada memiliki rentang yang sangat jauh sehingga perlu dilakukan standarisasi dengan StandardScaler() dengan standarisasi data maka akan memudahkan model.
 
 6. Split Dataset
    Dataset yang sudah melalui tahap sebelumnya akan dibagi menjadi training dataset dan test dataset. Hal ini perlu dilakukan untuk memastikan model dapat bekerja dengan baik.
    
## Modeling
1. Random Forest
  Menurut Sneha dan Gangil (Sneha & Gangil, 2019) Random forest adalah supervised learning yang biasa digunakan untuk klasifikasi dan regresi. Logika dari random forest adalah teknik bagging untuk membuat fitur sampel acak.
2. Decision Tree
   Menurut Naz dkk (Naz & Ahuja, 2020) Decision tree adalah graph yang digunakan untuk analisis keputusan dan menunjukkan hasil sebagai aturan pemisahan untuk setiap atribut tertentu.
   
   Berikut Hasil perbandingan kedua model yang telah diterapkan:
   
| Matrik | Random Forest | Decision Tree 
 ----------- | ----------- | ----------- |
| Accuracy | 0.7575757575757576 |  0.7348484848484849 | 
| Precision | 0.6097560975609756 | 0.5714285714285714 |  
| Recall | 0.6097560975609756 |  0.5853658536585366 | 

Dari hasil yang ditunjukan di dalam tabel dapat disimpulkan bahwa random forest menghasilkan model lebih baik dibandingkan dengan decision tree.

## Evaluasi
Dalam pembuatan model ini dilakukan evaluasi dengan confusion matrix. Di dalam confusion matrix terdapat Di dalam confusion matrix terdapat 4 kesimpulan yaitu

- True Positive (TP): Jumlah prediksi positif yang benar terhadap jumlah positif yang sebenarnya.
- False Positive (FP): Jumlah prediksi positif yang salah.
- True Negative (TN): Jumlah prediksi negatif yang benar terhadap jumlah negatif yang sebenarnya.
- False Negative (FN): Jumlah prediksi negatif yang salah.

Confusion Matrix juga memiliki 4 matrik akan tetapi dalam pembuatan model kali ini hanya digunakan 3 saja yaitu accuracy, precision dan recall.
- Accuracy: Ratio dari True Positives dan True Negative terhadap seluruh positif dan negative di seluruh observasi. Rumus Accuracy adalah sebagai berikut

![Screenshot 2022-08-16 at 14-49-18 Classification Accuracy Machine Learning Google Developers](https://user-images.githubusercontent.com/96067921/184913891-3abda482-7316-4959-93f0-630a56e74cbd.png)

- Precision: Kemampuan model untuk memprediksi nilai positif terhadap seluruh jumlah positif yang diprediksi oleh model.

![Screenshot 2022-08-16 at 14-50-18 Classification Precision and Recall Machine Learning Google Developers](https://user-images.githubusercontent.com/96067921/184913989-eb25cb65-c809-40d7-b040-8231431371bb.png)

- Recall: Kemampuan model untuk memprediksi nilai positif terhadap seluruh jumlah positif yang sesungguhnya.

![Screenshot 2022-08-16 at 14-51-32 Classification Precision and Recall Machine Learning Google Developers](https://user-images.githubusercontent.com/96067921/184914044-9497d1a3-d6aa-4b2a-b724-4108e79c490d.png)

Penggunaan hasil evaluasi ditunjukkan dalam tabel sebelumnya.

## Kesimpulan
Dalam melakukan prediksi apakah pasien memiliki diabetes atau tidak dapat menggunakan algoritma random forest atau decision tree. Dari kedua algoritma itu yang menghasilkan terbaik adalah random forest dengan akurasi 75%. Dalam pembuatan model ini masih banyak kekurangan dan juga model yang sudah dibuat dapat dikembangkan lagi.

## Referensi
[Naz, H., & Ahuja, S. (2020). Deep learning approach diabetes prediction using PIMA Indian dataset. Journal of Diabetes and Metabolic Disorders, 19(1), 391–403.](https://doi.org/10.1007/s40200-020-00520-5)

[Sneha, N., & Gangil, T. (2019). Analysis of diabetes mellitus for early prediction using optimal features selection. Journal of Big Data, 6(1).](https://doi.org/10.1186/s40537-019-0175-6)
    
