# Laporan Proyek Machine Learning Terapan - Muh. Ahyan Saputra (M295R5286)

## Domain Proyek
Domain yang saya pilih untuk proyek ini adalah Kesehatan

Berikut tautan untuk dataset yang saya gunakan untuk proyek ini: 
[Kaggle: Water Quality](https://www.kaggle.com/mssmartypants/water-quality).

- Latar belakang
> Air merupakan kebutuhan pokok setiap makhluk hidup, terutama manusia. Kualitas air diperlukan sebagai tolak ukur layaknya air untuk dikonsumsi. Kualitas air dapat diketahui dengan melakukan pengujian tertentu terhadap air tersebut. Pengujian yang dilakukan adalah uji unsur senyawa yang dikandung didalam air.

- Masalah
> Masalah utama yang dihadapi berkaitan dengan sumber daya air adalah kuantitas air yang sudah tidak mampu memenuhi kebutuhan yang terus meningkat dan kualitas air untuk keperluan domestik yang semakin menurun. Pengujian kualitas air masih menggunakan cara manual yakni dengan uji kimia, fisik, biologi, dan uji penampakan(warna, bau). Metode ini memiliki kekurangan yakni hasil pengamatan yang tidak akurat karena adanya faktor-faktor penghambat, baik faktor internal ataupun faktor eksternal.
   Dengan adanya proyek ini, diharapkan pengujian kualitas air dapat dilakukan menggunakan machine learning.

- Referensi Pendukung
  * [Jurnal Ilmu Lingkungan: KAJIAN KUALITAS AIR DAN PENGGUNAAN SUMUR GALI OLEH MASYARAKAT DI SEKITAR SUNGAI KALIYASA KABUPATEN CILACAP](http://repository.unpkediri.ac.id/1853/).
  * [Kualitas Air](http://repository.umy.ac.id/bitstream/handle/123456789/4624/7.%20BAB%20III%20Landasan%20Teori.pdf?sequence=7&isAllowed=y)


## Business Understanding
### Problem Statement
- Kandungan apa saja yang menentukan aman atau tidaknya air untuk dikonsumsi?

### Goals
- Menciptakan model machine learning untuk mengetahui kualitas air berdasarkan kandungannya.

### Solution Statements
Disini saya menggunakan 2 model development machine learning:
- K-Nearest Neighbour
> KNN bekerja dengan membandingkan jarak satu sampel ke sampel pelatihan lain dengan memilih sejumlah k-tetangga terdekat. Algoritma KNN menggunakan ‘kesamaan fitur’ untuk memprediksi nilai dari setiap data yang baru. Dengan kata lain, setiap data baru diberi nilai berdasarkan seberapa mirip titik tersebut dalam set pelatihan.

- Random Forest
> Algoritma random forest adalah salah satu algoritma supervised learning. Ia dapat digunakan untuk menyelesaikan masalah klasifikasi dan regresi. Random forest termasuk ke dalam kelompok model ensemble (group) yakni setiap model harus membuat prediksi secara independen. Kemudian, prediksi dari setiap model ensemble ini digabungkan untuk membuat prediksi akhir.

### Data Understanding
Berikut adalah isi konten dari dataset [Water Quality](https://www.kaggle.com/mssmartypants/water-quality):

![Water-quality-dataset](https://raw.githubusercontent.com/ahyansaputra/image-for-water-quality/main/water-quality-download.png)

- aluminium - berbahaya jika kandungannya lebih besar dari 2.8
- ammonia - berbahaya jika kandungannya lebih besar dari 32.5
- arsenic - berbahaya jika kandungannya lebih besar dari 0.01
- barium - berbahaya jika kandungannya lebih besar dari 2
- cadmium - berbahaya jika kandungannya lebih besar dari 0.005
- chloramine - berbahaya jika kandungannya lebih besar dari 4
- chromium - berbahaya jika kandungannya lebih besar dari 0.1
- copper - berbahaya jika kandungannya lebih besar dari 1.3
- flouride - berbahaya jika kandungannya lebih besar dari 1.5
- bacteria - berbahaya jika kandungannya lebih besar dari 0
- viruses - berbahaya jika kandungannya lebih besar dari 0
- lead - berbahaya jika kandungannya lebih besar dari 0.015
- nitrates - berbahaya jika kandungannya lebih besar dari 10
- nitrites - berbahaya jika kandungannya lebih besar dari 1
- mercury - berbahaya jika kandungannya lebih besar dari 0.002
- perchlorate - berbahaya jika kandungannya lebih besar dari 56
- radium - berbahaya jika kandungannya lebih besar dari 5
- selenium - berbahaya jika kandungannya lebih besar dari 0.5
- silver - berbahaya jika kandungannya lebih besar dari 0.1
- uranium - berbahaya jika kandungannya lebih besar dari 0.3
- is_safe - class attribute {0 - not safe, 1 - safe}

### Data Preparation
- Data preparation yang saya gunakan yakni Train-test-split
> Saya menggunakan itu karena saya perlu mempertahankan sebagian data yang ada untuk menguji seberapa baik generalisasi model terhadap data baru.  Saya menggunakan proporsi 90:10.
> Berikut kode yang saya gunakan:

  ```
  X = water.drop(["is_safe"],axis =1)
  y = water["is_safe"]
  X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.1, random_state = 123)
  ```

### Modelling
> Saya menggunakan 2 algoritma penyelesaian masalah untuk mengetahui akurasi dataset dengan menggunakan pendekatan K-Nearest Neighbour (KNN) dan Random Forest (RF).

> Berdasarkan pemodelan dengan dua algoritma tersebut saya mendapatkan nilai akurasi dari masing masing prediksi dua model.
First Header | Second Header
------------ | -------------
Content from cell 1 | Content from cell 2
Content in the first column | Content in the second column
 **KNN**|**RF**
 -------|------
 92%|94%

> Berikut hasil imlementasinya di dalam notebook:

-KNN
> ![Implementasi KNN Prediction](https://raw.githubusercontent.com/ahyansaputra/image-for-water-quality/main/KNN-Classification-acc.png)

-RF
> ![Implementasi RF Prediction](https://raw.githubusercontent.com/ahyansaputra/image-for-water-quality/main/RF-Classification-acc.png)

## Evaluation
> Pada kasus ini, saya menggunakan kasus klasifikasi dengan menggunakan metriks precision, recall, dan f1-score.

- KNN
is_safe|Precission|Recall|F1-Score
-------|----------|------|--------
0|94%|98%|96%
1|23%|9%|13%

- RF
is_safe|Precission|Recall|F1-Score
-------|----------|------|--------
0|100%|95%|97%
1|18%|86%|29%


1. Kelebihan Klasifikasi Metriks(precision, recall, dan f1-score)
* Penggunaan metrik precission, recall dan f1-score dapat menjadi solusi terbaik dalam proses klasifikasi karena ada beberapa momen tertentu penggunaan metrik akurasi kurang tepat untuk permasalahan data yang tidak seimbang.

2. Kekurangan Klasifikasi Metriks(precision, recall, dan f1-score)
* Orang- orang cenderung lebih tertarik dengan akurasi walaupun ada metrik yang lebih sesuai

Cara mengaplikasikan metriks ke dalam kode:
1. KNN
> ![Water-Quality: KNN](https://raw.githubusercontent.com/ahyansaputra/image-for-water-quality/main/KNN-Water.png).
2. Random Forest
> ![Water-Quality: RF](https://raw.githubusercontent.com/ahyansaputra/image-for-water-quality/main/RF-Water.png). 


### Kesimpulan
> Model untuk memprediksi data air yang layak di konsumsi oleh manusia telah selesai dibuat dan model ini dapat digunakan untuk memprediksi data sebenarnya. Namun demikian beberapa pengembangan lain masih dapat dilakukan agar membuat model yang memiliki akurasi lebih tinggi lagi seperti dengan mencoba penggunaan algoritma lainnya dalam membuat model seperti Random Forest, Decision Tree, Gradient Boosting dan masih banyak lagi.