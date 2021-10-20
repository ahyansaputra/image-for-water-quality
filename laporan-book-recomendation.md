# Laporan Proyek Machine Learning Terapan - Muh. Ahyan Saputra (M295R5286)

## Project Overview
### Pendahuluan
> Pada submission ini, saya menggunakan dataset [Book Reviews](https://www.kaggle.com/arashnic/book-recommendation-dataset) sebagai proyek akhir machine learning terapan. Dataset ini berisi tentang kumpulan data buku dan hasil review dari pengguna.

- Referensi terkait:
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

> Contoh pemodelan sistem rekomendasi menggunakan content based filtering (Sumber: Modul Machine Learning Terapan oleh Dicoding):

![Content Based Filtering](https://github.com/ahyansaputra/image/blob/main/content-base-filtering.jpeg)

## Data Understanding
> Berikut adalah isi konten dataset [Book Recomendation](https://www.kaggle.com/arashnic/book-recommendation-dataset).

![Book Recomendation Dataset](https://github.com/ahyansaputra/image/blob/main/book-rec-dataset.png)

1. Book.csv
* a. ISBN                 : Nomor identitas buku
* b. Book-Title           : Judul buku
* c. Book-Author          : Penulis buku
* d. Year-of-Publication  : Tahun terbit buku
* e. Publisher            : Penerbit buku
* f. Image-url-s          : Tautan gambar pendek
* g. Image-url-m          : Tautan gambar medium
* h. Image-url-l          : Tautan gambar panjang

2. Rating.csv
* a. User-Id              : Nomor identitas pengguna
* b. ISBN                 : Nomor identitas buku
* c. BookRating           : Rating buku

3. User.csv
* a. User-Id              : Nomor idenitas pengguna
* b. Location             : Kota tinggal pengguna
* c. Age                  : Usia pengguna

## Data Preparation
> Metode data preparation yang saya gunakan adalah mengatasi missing value. Berikut langkah-langkah yang saya lakukan

![Missing-Value1](https://github.com/ahyansaputra/image/blob/main/missing-value-1.png)
![Missing-Value2](https://github.com/ahyansaputra/image/blob/main/missing-value-2.png)
![Missing-Value3](https://github.com/ahyansaputra/image/blob/main/missing-value-3.png)

> Sebelum dimasukkan ke dalam model, perlu dilakukan penghapusan data duplikat pada dataset

![Data-clean](https://github.com/ahyansaputra/image/blob/main/data-clean.png)
![Data-clean2](https://github.com/ahyansaputra/image/blob/main/data-clean-2.png)

> Selanjutnya mengkonversi dataseries ke dalam list

![Dataseries-to-list](https://github.com/ahyansaputra/image/blob/main/dataseries-to-list.png)

> Tahap akhir yakni membuat dictionary untuk pasangan key-value
![Key:Value](https://github.com/ahyansaputra/image/blob/main/dict-key-value.png)

## Modelling
> Pada tahap modelling ini, model development yang digunakan yakni *Content Based Filtering*

> Modelling ini perlu dilakukan agar sistem dapat membangun sistem rekomendasi sederhana untuk recomendasi buku.

> Berikut top 5 buku hasil rekomendasi sistem:

![Top-5-Book-Recomendation](https://github.com/ahyansaputra/image/blob/main/model-recomendation.png)

> Dari gambar diatas, dapat dilihat terdapat 5 jenis buku karya Fern Michaels. Hal ini sesuai dengan model development yang digunakan. Bahwa sistem akan merekomendasikan buku berdasarkan kontennya saja. Berdasarkan sistem yang dibangun, sistem akan mencari author dari buku terkait, kemudian sistem akan menyajikan buku-buku dengan judul berbeda dari penulis yang sama atau penulis dengan nama yang hampir mirip.

## Evaluation
> Model development *Content Based Filtering* menggunakan 2 metrik untuk membangun sistem rekomendasinya:
1. TF-IDF Vectorizer

![TF-IDF-1](https://github.com/ahyansaputra/image/blob/main/tf-idf.png)

![TF-IDF-2](https://github.com/ahyansaputra/image/blob/main/tf-idf.png)

![TF-IDF-3](https://github.com/ahyansaputra/image/blob/main/tf-idf-3.png)

2. Cosine Similarity

![Cosine Similarity](https://github.com/ahyansaputra/image/blob/main/cossin-similarity.png)


### Kesimpulan
> Model yang disajikan sudah bisa memberikan rekomendasi buku menggunakan model development *Content Based Filtering*. Adapun metriks yang digunakan ialah TF-IDF Vectorizer dan Cosine Similarity. Tetapi model masih perlu perbaikan dan pengembangan misalnya menambahkan pemodelan *Colaborative Filtering* ke dalam sistem rekomendasi buku ini.
