# Laporan Proyek Machine Learning Terapan - Muh. Ahyan Saputra (M295R5286)

## Project Overview

### Latar Belakang
> Sistem rekomendasi merupakan aplikasi yang menawarkan suatu item atau produk berdasarkan kriteria tertentu. Semua perusahaan berbasis teknologi contohnya seperti Netflix, Spotify dan lain sebagainya membutuhkan sistem rekomendasi untuk memudahkan pelanggan mereka untuk menikmati layanan perusahaan terkait. Tidak terkecuali pada aplikasi yang merekomendasikan buku kepada penikmat buku.

### Masalah
> Terdapat banyak layanan penyedia buku online (ebooks) seperti googole play books, open library, good Read's dan lain sebagainya. Pengguna yang menggunakan layanan diatas selalu memilih buku yang sesuai dengan selera mereka. Tetapi terdapat ratusan bahkan ribuan buku yang disediakan di aplikasi tersebut. Mereka akan kesulitan mendapatkan buku yang ingin mereka baca, atau bahkan menghabiskan waktu di internet untuk menemukan buku bacaan kesukaan mereka.

### Mengapa perlu diselesaikan?
> Membutuhkan waktu yang sangat banyak jika pengguna layanan ebooks harus memeriksa satu persatu buku yang ada di layanan yang mereka gunakan. Maka dari itu dibutuhkan sebuah sistem yang dapat merekomendasikan buku berdasarkan preferensi (dalam hal ini rating) pengguna. Sehingga para penikmat buku dapat dengan mudah menemukan buku kesukaan mereka dan dapat mengefisiensikan waktu mereka.

> Untuk menyelesaikan masalah tersebut, saya menggunakan dataset [Book Reviews](https://www.kaggle.com/arashnic/book-recommendation-dataset) untuk membangun sebuah sistem rekomendasi buku. Dataset ini berisi tentang kumpulan data buku dan hasil review dari pengguna.

### Referensi terkait:
* [Colaborative Filtering](https://www.kaggle.com/rishitarya/collaborative-filtering)
* [Book Recomender System](https://www.kaggle.com/hocohelper/book-recommender-system)
* [Book Recomendation](https://www.kaggle.com/aadarshraj4444/book-recommendation)

## Business Understanding
### Problem Statement
- Pada dasarnya sistem rekomendasi akan menyajikan data yang dibutuhkan oleh pengguna. Terutama pada proyek ini, bagaimana sistem mampu merekomendasikan buku berdasarkan preferensi pengguna?

### Goals
- Tujuan dari proyek ini ialah, sistem mampu menampilkan rekomendasi buku dengan ketentuan: menampilkan top recomended buku dengan nilai rating tertinggi dan merekomendasikan buku yang dianggap sesuai dengan keinginan pengguna (dengan catatan buku tersebut belum pernah dibaca oleh pengguna).

### Solution Approach
- *Colaborative Filtering*
> Colaborative Filtering merupakan jenis recommender system yang didasari matriks preferensi antara pengguna dan konten di dalamnya. Collaborative filtering bergantung pada pendapat komunitas pengguna. Ia tidak memerlukan atribut untuk setiap itemnya seperti pada sistem berbasis konten. Collaborative filtering dibagi lagi menjadi dua kategori, yaitu: model based (metode berbasis model machine learning) dan memory based (metode berbasis memori).

> Ilustrasi pemodelan sistem rekomendasi menggunakan content based filtering (Sumber: Modul Machine Learning Terapan oleh Dicoding):
1. User Based

![User Based](https://raw.githubusercontent.com/ahyansaputra/image/main/colaborative-image.png)

> Seperti namanya, sistem ini berdasarkan kesamaan antar pengguna. Idenya adalah mencari pengguna dengan selera yang sama. Sebagai contoh, Galih dan Ratna memberikan rating tinggi untuk sejumlah film action. Jika Galih menyukai film The Avengers, Ratna juga kemungkinan besar akan menyukai film tersebut.

2. Item Based

![Item Based](https://raw.githubusercontent.com/ahyansaputra/image/main/claborative-image-2.png)

> Item based filtering bekerja dengan cara menghitung kesamaan antara masing-masing item. Sebagai contoh, Galih dan Ratna menyukai film The Avengers dan Transformers. Kemudian, Milea juga ternyata suka film Avengers. Sehingga, sistem akan merekomendasikan film Transformers kepada Milea. Film Transformers direkomendasikan pada Milea (pengguna baru) karena dianggap mirip (similar) dengan film The Avengers.


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

Sebelum masuk ke Data preparation terlebih dahulu saya menggabungkan dataset Book.csv dan Rating.csv dengan kriteria tertentu. Berikut kode yang saya gunakan:

```
all_book_rate = ratings
all_book_name = pd.merge(all_book_rate, books[['ISBN','Book-Title', 'Book-Author']], on='ISBN', how='left')

all_book_name
```

Berikut outputnya:

![Data Preprocessing](https://raw.githubusercontent.com/ahyansaputra/image/main/data-preprocessing.png)

## Data Preparation

1. Missing Value 

> Alasan saya menggunakan metode ini karena mayoritas algoritma Machine Learning tidak dapat berfungsi apabila ada missing values pada variabel-variabel features. Sebelum dimasukkan didalam model, maka dataframe harus bersih dari field yang kosong.

Berikut langkah-langkah yang saya lakukan

![Missing-Value1](https://raw.githubusercontent.com/ahyansaputra/image/main/missing-value-1.png)

* untuk mengatasi missing value tersebut kita hapus saja menggunakan fungsi dropna()

![Missing-Value2](https://raw.githubusercontent.com/ahyansaputra/image/main/missing-value-2.png)

* cek data setelah di hapus missing valuenya

![Missing-Value3](https://raw.githubusercontent.com/ahyansaputra/image/main/missing-value-3.png)

> Sebelum dimasukkan ke dalam model, perlu dilakukan penghapusan data duplikat pada dataset

* data duplikat yang akan dihapus yakni data dengan unique value **ISBN**

* buat valiabel bernama preparation

![Data-clean](https://raw.githubusercontent.com/ahyansaputra/image/main/data-clean.png)

* gunakan fungsi drop_duplicates() untuk menghapus data duplikat

![Data-clean2](https://raw.githubusercontent.com/ahyansaputra/image/main/data-clean-2.png)

> Selanjutnya mengkonversi dataseries ke dalam list

![Dataseries-to-list](https://raw.githubusercontent.com/ahyansaputra/image/main/dataseries-to-list.png)

> Tahap selanjutnya yakni membuat dictionary untuk pasangan key-value

![Key:Value](https://raw.githubusercontent.com/ahyansaputra/image/main/dict-key-value.png)

> Selanjutnya mengambil sampel acak dari data preparation sebanyak 10000 sampel agar data mudah diolah.

![1000 Sample](https://raw.githubusercontent.com/ahyansaputra/image/main/Preparation-1000.png)

2. Melakukan Encodeing Data

> Alasan saya menggunakan metode ini karena saya perlu menyandikan data sampel acak dalam bentuk integer. Dan juka terdapat beberapa nilai ISBN yang bertipe objek, sehingga perlu disandikan ke dalam bentuk integer.

> encoding fitur user
```
# Mengubah userID menjadi list tanpa nilai yang sama
user_ids = df['UserID'].unique().tolist()
print('list UserID: ', user_ids)
 
# Melakukan encoding userID
user_to_user_encoded = {x: i for i, x in enumerate(user_ids)}
print('encoded UserID : ', user_to_user_encoded)
 
# Melakukan proses encoding angka ke ke userID
user_encoded_to_user = {i: x for i, x in enumerate(user_ids)}
print('encoded angka ke userID: ', user_encoded_to_user)
```
Berikut sebagian outputnya:

![Encoding User](https://raw.githubusercontent.com/ahyansaputra/image/main/encoding-user-1.png)

![Encoded User](https://raw.githubusercontent.com/ahyansaputra/image/main/encoding-user-2.png)

> encoding fitur isbn
```
# Mengubah ISBN menjadi list tanpa nilai yang sama
book_ids = df['ISBN'].unique().tolist()
 
# Melakukan proses encoding ISBN
book_to_book_encoded = {x: i for i, x in enumerate(book_ids)}
 
# Melakukan proses encoding angka ke ISBN
book_encoded_to_book = {i: x for i, x in enumerate(book_ids)}
 
#Selanjutnya, petakan userID dan ISBN ke dataframe yang berkaitan.
 
# Mapping userID ke dataframe user
df['user'] = df['UserID'].map(user_to_user_encoded)
 
# Mapping ISBN ke dataframe book
df['book'] = df['ISBN'].map(book_to_book_encoded)
```

> mendapatkan jumlah user dan mengubah tipe data rating yang awalnya integer ke tipe data float
```
# Mendapatkan jumlah user
num_users = len(user_to_user_encoded)
print(num_users)
 
# Mendapatkan jumlah book
num_book = len(book_encoded_to_book)
print(num_book)
 
# Mengubah BookRating menjadi nilai float
df['BookRating'] = df['BookRating'].values.astype(np.float32)
 
# Nilai minimum BookRating
min_BookRating = min(df['BookRating'])
 
# Nilai maksimal BookRating
max_BookRating = max(df['BookRating'])
 
print('Number of User: {}, Number of book: {}, Min BookRating: {}, Max BookRating: {}'.format(
    num_users, num_book, min_BookRating, max_BookRating
))
```
Berikut outputnya:

![User dan Rating](https://raw.githubusercontent.com/ahyansaputra/image/main/jumlah-user-rating.png)

> mengacak dataset sebelum melakukan Train Test Split

![Dataset Acak](https://raw.githubusercontent.com/ahyansaputra/image/main/mengacak-dataset-1000.png)

3. Train Test Split

> Terakhir adalah menggunakan Train-Test-Split. Saya menggunakan metode ini karena saya perlu mempertahankan sebagian data yang ada untuk menguji seberapa baik generalisasi model terhadap data baru.

```
# Membuat variabel x untuk mencocokkan data user dan book menjadi satu value
x = df[['user', 'book']].values
 
# Membuat variabel y untuk membuat rating dari hasil 
y = df['BookRating'].apply(lambda x: (x - min_BookRating) / (max_BookRating - min_BookRating)).values
 
# Membagi menjadi 80% data train dan 20% data validasi
train_indices = int(0.8 * df.shape[0])
x_train, x_val, y_train, y_val = (
    x[:train_indices],
    x[train_indices:],
    y[:train_indices],
    y[train_indices:]
)
 
print(x, y)
```

Berikut outputnya:
![Train Test Split](https://raw.githubusercontent.com/ahyansaputra/image/main/train-test-split.png)

## Modelling
> Pada tahap modelling ini, model development yang digunakan yakni *Colaborative Filtering*

> Modelling ini perlu dilakukan agar sistem dapat membangun sistem rekomendasi sederhana untuk recomendasi buku.

> Pada tahap ini, model menghitung skor kecocokan antara user dan buku dengan teknik embedding. Pertama, kita melakukan proses embedding terhadap data user dan buku. Selanjutnya, lakukan operasi perkalian dot product antara embedding user dan resto. Selain itu, kita juga dapat menambahkan bias untuk setiap user dan resto. Skor kecocokan ditetapkan dalam skala [0,1] dengan fungsi aktivasi sigmoid.

> Di sini, kita membuat class RecommenderNet dengan keras Model class.

> Berikut kode yang digunakan:

```
class RecommenderNet(tf1.keras.Model):
 
  # Insialisasi fungsi
  def __init__(self, num_users, num_book, embedding_size, **kwargs):
    super(RecommenderNet, self).__init__(**kwargs)
    self.num_users = num_users
    self.num_book = num_book
    self.embedding_size = embedding_size
    self.user_embedding = layers.Embedding( # layer embedding user
        num_users,
        embedding_size,
        embeddings_initializer = 'he_normal',
        embeddings_regularizer = keras.regularizers.l2(1e-6)
    )
    self.user_bias = layers.Embedding(num_users, 1) # layer embedding user bias
    self.book_embedding = layers.Embedding( # layer embeddings book
        num_book,
        embedding_size,
        embeddings_initializer = 'he_normal',
        embeddings_regularizer = keras.regularizers.l2(1e-6)
    )
    self.book_bias = layers.Embedding(num_book, 1) # layer embedding book bias
 
  def call(self, inputs):
    user_vector = self.user_embedding(inputs[:,0]) # memanggil layer embedding 1
    user_bias = self.user_bias(inputs[:, 0]) # memanggil layer embedding 2
    book_vector = self.book_embedding(inputs[:, 1]) # memanggil layer embedding 3
    book_bias = self.book_bias(inputs[:, 1]) # memanggil layer embedding 4
 
    dot_user_book = tf1.tensordot(user_vector, book_vector, 2) 
 
    x = dot_user_book + user_bias + book_bias
    
    return tf1.nn.sigmoid(x) # activation sigmoid
```
> Selanjutnya melakukan compile model. Model ini menggunakan Binary Crossentropy untuk menghitung loss function, Adam (Adaptive Moment Estimation) sebagai optimizer, dan root mean squared error (RMSE) sebagai metrics evaluation. 

```
model = RecommenderNet(num_users, num_book, 50) # inisialisasi model
 
# model compile
model.compile(
    loss = tf1.keras.losses.BinaryCrossentropy(),
    optimizer = keras.optimizers.Adam(learning_rate=0.001),
    metrics=[tf1.keras.metrics.RootMeanSquaredError()]
)
```

> Melakukan Proses Training
```
# Memulai training
 
history = model.fit(
    x = x_train,
    y = y_train,
    batch_size = 8,
    epochs = 100,
    validation_data = (x_val, y_val)
)
```
> Berikut sebagian output dari hasil training model:

![Training Data](https://raw.githubusercontent.com/ahyansaputra/image/main/training-data.png)

> Mendapatkan N-Rekomendasi
Untuk mendapatkan rekomendasi buku, pertama kita ambil sampel user secara acak dan definisikan variabel book_not_read yang merupakan daftar buku yang belum pernah dibaca oleh pengguna. Hal ini karena daftar book_not_read inilah yang akan menjadi book yang kita rekomendasikan. Sebelumnya, pengguna telah memberi rating pada beberapa buku yang telah mereka baca. Kita menggunakan rating ini untuk membuat rekomendasi buku yang mungkin cocok untuk pengguna. Nah, buku yang akan direkomendasikan tentulah buku yang belum pernah dibaca oleh pengguna. Oleh karena itu, kita perlu membuat variabel book_not_read sebagai daftar buku untuk direkomendasikan pada pengguna.Variabel book_not_read diperoleh dengan menggunakan operator bitwise (~) pada variabel book_read_by_user.

Terapkan kode berikut.
```
book_df = book_new
 
# Mengambil sample user
user_id = df.UserID.sample(1).iloc[0]
book_read_by_user = df[df.UserID == user_id]

book_not_read = book_df[~book_df['id'].isin(book_read_by_user.ISBN.values)]['id'] 
book_not_read = list(
    set(book_not_read)
    .intersection(set(book_to_book_encoded.keys()))
)
 
book_not_read = [[book_to_book_encoded.get(x)] for x in book_not_read]
user_encoder = user_to_user_encoded.get(user_id)
user_book_array = np.hstack(
    ([[user_encoder]] * len(book_not_read), book_not_read)
)
```

```
ratings = model.predict(user_book_array).flatten()
 
top_ratings_indices = ratings.argsort()[-10:][::-1]
recommended_book_ids = [
    book_encoded_to_book.get(book_not_read[x][0]) for x in top_ratings_indices
]
 
print('Showing recommendations for users: {}'.format(user_id))
print('===' * 9)
print('book with high ratings from user')
print('----' * 8)
 
top_book_user = (
    book_read_by_user.sort_values(
        by = 'BookRating',
        ascending=False
    )
    .head(5)
    .ISBN.values
)
 
book_df_rows = book_df[book_df['id'].isin(top_book_user)]
for row in book_df_rows.itertuples():
    print(row.book_name, ':', row.author_name)
 
print('----' * 8)
print('Top 10 book recommendation')
print('----' * 8)
 
recommended_book = book_df[book_df['id'].isin(recommended_book_ids)]
for row in recommended_book.itertuples():
    print(row.book_name, ':', row.author_name)
```

Berikut hasil recomendasi buku menggunakan model Colaborative Filtering:
![Top Recomendation](https://raw.githubusercontent.com/ahyansaputra/image/main/rek-colaborative-img.png)

> Dari informasi gambar diatas, sistem sudah bisa menampilkan data buku dengan rating tertinggi dan buku yang direkomendasikan kepada pengguna. Buku yang direkomendasikan berdasarkan rating yang diberikan oleh beberapa user yang kemudian dijadikan preferensi kepada user tertentu yang dianggap sesuai dengan keinginan user tersebut.

## Evaluation

> Model evaluation yang digunakan adalah RMSE atau Root Mean Squared Error. RMSE bekerja dengan cara mengkuadratkan error (Predicted - Observed) dibagi dengan jumlah data (= rata-rata) lalu diakarkan.

> Untuk memudahkan visualisasi metriks RMSE dapat menggunakan fungsi plotting. Gunakan kode berikut:

```
plt.plot(history.history['root_mean_squared_error'])
plt.plot(history.history['val_root_mean_squared_error'])
plt.title('model_metrics')
plt.ylabel('root_mean_squared_error')
plt.xlabel('epoch')
plt.legend(['train', 'test'], loc='upper left')
plt.show()
```
![Model Metric](https://raw.githubusercontent.com/ahyansaputra/image/main/model-metricks.png)

> Dari gambar diatas dapat diperoleh informasi bahwa nilai error akhir untuk data training yakni 5% dan pada data validasinya menunjukkan nilai error 40%. 

### Kesimpulan
> Model yang disajikan sudah bisa memberikan rekomendasi buku menggunakan model development *Colaborative Filtering*. Adapun metriks yang digunakan ialah RMSE atau Root Mean Squared Error. Tetapi model masih perlu perbaikan dan pengembangan misalnya menambahkan pemodelan *Content Based Filtering* atau *Hybrid Recomender System* ke dalam sistem rekomendasi buku ini. Selain itu diharapkan sistem dapat mengolah data dengan jumlah yang besar dikarenakan pada proyek ini saya hanya mengambil 40.000 data rating dan 10.000 data untuk ditraining. Adapun kendalanya bisa jadi karena faktor internal bahwa PC saya tidak mampu mengolah data dengna jumlah yang lebih dari pada sampel yang telah ditentukan.