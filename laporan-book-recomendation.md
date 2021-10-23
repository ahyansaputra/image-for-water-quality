# Laporan Proyek Machine Learning Terapan - Muh. Ahyan Saputra (M295R5286)

## Project Overview
### Pendahuluan
> Pada submission ini, saya menggunakan dataset [Book Reviews](https://www.kaggle.com/arashnic/book-recommendation-dataset) sebagai proyek akhir machine learning terapan. Dataset ini berisi tentang kumpulan data buku dan hasil review dari pengguna.

Referensi terkait:
* [Colaborative Filtering](https://www.kaggle.com/rishitarya/collaborative-filtering)
* [Book Recomender System](https://www.kaggle.com/hocohelper/book-recommender-system)
* [Book Recomendation](https://www.kaggle.com/aadarshraj4444/book-recommendation)

## Business Understanding
### Problem Statement
- Pada dasarnya sistem rekomendasi akan menyajikan data yang dibutuhkan oleh pengguna. Terutama pada proyek ini, bagaimana sistem mampu merekomendasikan buku berdasarkan item tertentu pada buku yang diminati pengguna?

### Goals
- Tujuan yang ingin dicapai pada projek kali ini ialah, sistem mampu merekomendasikan buku kepada pengguna berdasarkan kemiripan pada item *penulis buku* atau *author buku*.

### Solution Approach
- *Content Based Filtering*
> Content based filtering merupakan model rekomendasi berdasarkan kemiripan item tertentu yang disukai oleh pengguna. 

> Ilustrasi pemodelan sistem rekomendasi menggunakan content based filtering (Sumber: Modul Machine Learning Terapan oleh Dicoding):

![Content Based Filtering](https://raw.githubusercontent.com/ahyansaputra/image/main/content-base-filtering.jpeg)

## Data Understanding
> Berikut adalah isi konten dataset [Book Recomendation](https://www.kaggle.com/arashnic/book-recommendation-dataset).

![Book Recomendation Dataset](https://raw.githubusercontent.com/ahyansaputra/image/main/book-rec-dataset.png)

1. Book.csv
* ISBN                 : Nomor identitas buku
* Book-Title           : Judul buku
* Book-Author          : Penulis buku
* Year-of-Publication  : Tahun terbit buku
* Publisher            : Penerbit buku
* Image-url-s          : Tautan gambar pendek
* Image-url-m          : Tautan gambar medium
* Image-url-l          : Tautan gambar panjang

2. Rating.csv
* User-Id              : Nomor identitas pengguna
* ISBN                 : Nomor identitas buku
* BookRating           : Rating buku

3. User.csv
* User-Id              : Nomor idenitas pengguna
* Location             : Kota tinggal pengguna
* Age                  : Usia pengguna

## Data Preparation
> Metode data preparation yang saya gunakan adalah mengatasi missing value. Berikut langkah-langkah yang saya lakukan

![Missing-Value1](https://raw.githubusercontent.com/ahyansaputra/image/main/missing-value-1.png)
![Missing-Value2](https://raw.githubusercontent.com/ahyansaputra/image/main/missing-value-2.png)
![Missing-Value3](https://raw.githubusercontent.com/ahyansaputra/image/main/missing-value-3.png)

> Sebelum dimasukkan ke dalam model, perlu dilakukan penghapusan data duplikat pada dataset

![Data-clean](https://raw.githubusercontent.com/ahyansaputra/image/main/data-clean.png)
![Data-clean2](https://raw.githubusercontent.com/ahyansaputra/image/main/data-clean-2.png)

> Selanjutnya mengkonversi dataseries ke dalam list

![Dataseries-to-list](https://raw.githubusercontent.com/ahyansaputra/image/main/dataseries-to-list.png)

> Tahap akhir yakni membuat dictionary untuk pasangan key-value
![Key:Value](https://raw.githubusercontent.com/ahyansaputra/image/main/dict-key-value.png)

## Modelling
> Pada tahap modelling ini, model development yang digunakan yakni *Content Based Filtering*

> Modelling ini perlu dilakukan agar sistem dapat membangun sistem rekomendasi sederhana untuk recomendasi buku.

> Berikut top 5 buku hasil rekomendasi sistem:

![Top-5-Book-Recomendation](https://raw.githubusercontent.com/ahyansaputra/image/main/model-recomendation.png)

> Dari gambar diatas, dapat dilihat terdapat 5 jenis buku karya Fern Michaels. Hal ini sesuai dengan model development yang digunakan. Bahwa sistem akan merekomendasikan buku berdasarkan kontennya saja. Berdasarkan sistem yang dibangun, sistem akan mencari author dari buku terkait, kemudian sistem akan menyajikan buku-buku dengan judul berbeda dari penulis yang sama atau penulis dengan nama yang hampir mirip.

## Evaluation
> Model development *Content Based Filtering* menggunakan 2 metrik untuk membangun sistem rekomendasinya:
1. TF-IDF Vectorizer

![TF-IDF-1](https://raw.githubusercontent.com/ahyansaputra/image/main/tf-idf.png)

![TF-IDF-2](https://raw.githubusercontent.com/ahyansaputra/image/main/tf-idf-2.png)

![TF-IDF-3](https://raw.githubusercontent.com/ahyansaputra/image/main/tf-idf-3.png)

2. Cosine Similarity

![Cosine Similarity](https://raw.githubusercontent.com/ahyansaputra/image/main/cossin-similarity.png)


### Kesimpulan
> Model yang disajikan sudah bisa memberikan rekomendasi buku menggunakan model development *Content Based Filtering*. Adapun metriks yang digunakan ialah TF-IDF Vectorizer dan Cosine Similarity. Tetapi model masih perlu perbaikan dan pengembangan misalnya menambahkan pemodelan *Colaborative Filtering* ke dalam sistem rekomendasi buku ini.
