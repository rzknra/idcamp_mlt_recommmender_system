# Laporan Proyek Machine Learning - Sistem Rekomendasi Buku

## Domain Proyek 

## Bisnis Understanding
Pengembangan sistem rekomendasi buku bertujuan tentunya untuk memberi manfaat kepada pengguna GoodReads, salah satunya untuk membantu pengguna GoodReads mendapatkan rekomendasi buku.

### Problem Statements
- Bagaimana cara mengolah *dataset* sehingga bisa digunakan untuk mengembangkan sistem rekomendasi menggunakan teknik Cosine Similarity dan algoritma KNN?
- Bagaimana cara membangun sistem rekomendasi menggunakan teknik Cosine Similarity dan algoritma KNN.
- Bagaimana cara mengevaluasi performa sistem rekomendasi menggunakan teknik Cosine Similarity dan algoritma KNN?
  
### Goals
- Mengetahui cara mengolah *dataset* sehingga bisa digunakan untuk mengembangkan sistem rekomendasi menggunakan teknik Cosine Similarity dan algoritma KNN.
- Mengetahui cara membangun sistem rekomendasi dengan teknik Cosine Similarity dan algoritma KNN.
- Mengetahui cara mengevaluasi performa sistem rekomendasi dengan teknik Cosine Similarity dan algoritma KNN.

### Solution Statements
- Untuk mengolah *dataset* sehingga bisa digunakan untuk mengembangkan sistem rekomendasi dengan teknik Cosine Similarity dan algoritma KNN, dilakukan *Data Wragling* dan *Data Preparation*. *Data Wragling* yang dilakukan berupa *Data Assesing* dan *Data Cleaning*. *Data Preparation* yang dilakukan untuk mengembangkan sistem rekomendasi dengan teknik Cosine Similarity berupa representasi fitur. Di sisi lain, *Data Preparation* yang dilakukan untuk mengembangkan sistem rekomendasi dengan algoritma KNN yaitu reduksi fitur, dan **Scaling* fitur numerik. Selain, itu juga dilakukan analisis univariat untuk mengetahui lebih dalam karakteristik dari data.
- Untuk mengevaluasi performa sistem rekomendasi dengan teknik Cosine Similarity digunakan metrik *precision*. Di sisi lain, untuk mengevaluasi performa sedangkan performa sistem rekomendasi dengan algoritma KNN, digunakan metrik *Davies Bouldien Score*


## Data Understanding
Data yang digunakan dalam proyek ini merupakan data sekunder yang diperoleh dari Kaggle dengan nama dataset yaitu 'goodreads-books'. Data tersebut dapat diakses melalui tautan berikut:
https://www.kaggle.com/datasets/jealousleopard/goodreadsbooks/data

Lebih lanjut, detail mengenai *dataset* tersebut diberikan sebagai berikut:
- Dataset berupa file CSV.
- Dataset terdiri dari 11127 *record* (pengamatan) dan 12 fitur. 
- Dataset terdiri dari 6 fitur kategori (title, authors, isbn, language_code, publication_date, dan publisher) dan 6 fitur numerik (average_rating, book_id, isbn13, num_of_pages, rating_count, dan text_reviews_count).

### Variabel-Variabel dari goodreads-book Dataset
Berdasarkan informasi di Kaggle, variabel-variabel pada *dataset* adalah sebagai berikut:
Berdasarkan informasi dari Kaggle, variabel-variabel pada dataset adalah sebagai berikut:
1. bookID: nomor identifikasi unik untuk setiap buku.
2. title: judul buku.
3. author: penulis buku tertentu.
4. average_rating: peringkat rata-rata untuk setiap buku (0-5)
5. ISBN: momor yang memberi tahu informasi tentang buku, secara lebih spesifik tenatang edisi dan penerbit
6. isbn13: format baru untuk ISBN, diterapkan pada tahun 2007 dengan 13 digit
7. language_code: bahasa buku
8. num_pages: jumlah halaman buku
9. ratings_count: banyaknya rating yang diberikan untuk setiap buku
10. text_reviews_count: banyaknya ulasan yang diberikan oleh pengguna untuk masing-masing buku.
11. publication_date: waktu buku dipublikasi
12. publisher: penerbit buku

Semua variabel atau fitur pada dataset dapat digunakan untuk membangun sistem rekomendasi. Namun, pada proyek ini hanya akan digunakan fitur berikut:                 
1. title                  
2. authors                
3. average_rating        
4. language_code          
5. num_of_pages            
6. ratings_count           
7. text_reviews_count                  

Lebih lanjut:
1. Fitur 'title', 'authors', dan 'language_code' digunakan untuk mengembangkan sistem rekomendasi dengan teknik cosine similarity.
2. Fitur 'title', 'average rating', 'num_of_pages',  'ratings_count', dan    'text_reviews_count' digunakan untuk mengembangkan sistem rekomendasi dengan algoritma KNN.
   
### Data Assesing dan Data Cleaning
Pada tahap ini, dilakukan pengecekan terhadap:
1. Deskripsi statistik fitur numerik.
2. *Unique value* fitur kategori.
3. Data duplikat (data yang bernilai sama dengan data lainnya).
4. *Missing value* (data yang hilang atau tidak tersedia).
5. *Outlier* (data yang menyimpang dari rata-rata sekumpulan data yang ada).

Hasil *Data Assesing* yang sudah dilakukan, sebagai berikut:
1. Berdasarkan pengecekan deskripsi statistik, diperoleh bahwa fitur 'average_rating', 'ratings_count', 'num_of_pages' dan 'text_reviews_count' mempunyai nilai minimum 0. Lebih lanjut, diperhatikan bahwa:
   - Nilai minimum fitur 'average_rating' dan 'ratings_count' adalah 0, yang berarti terdapat buku yang tidak dinilai maupun di-review oleh pengguna goodreads.
   - Nilai minimum fitur 'num_of_pages' adalah 0, yang berarti ada buku tanpa halaman.
   - Nilai minimum fitur 'text_reviews_count' adalah 0, yang berarti ada buku tanpa review (berupa teks) yang diberikan oleh pengguna goodreads.
2. Berdasarkan pengecekan *unique value* fitur kategori, diperoleh jumlah *unique value* dari setiap fitur kategori, yaitu:
   - Fitur 'title' mempunyai 10214 *unique value*.
   - Fitur 'authors' mempunyai 6548 *unique value*.
   - Fitur 'language_code' mempunyai 26 *unique value*.
Lebih lanjut, diperoleh juga bahwa:
   - Terdapat buku dengan nama penulis yang terdiri lebih dari satu orang. Namun, jika ditelusuri lebih lanjut sebanarnya hanya nama pertama yang merupakan penulis buku, nama kedua atau ketiga bukan merupakan penulis, tetapi pihak ketiga yang terlibat dalam pembuatan buku seperti menjadi ilustrator atau lainnya.
   - Terdapat kode bahasa pada fitur 'language_code' yang tidak sesuai standar kode bahasa ISO 639-2.
3. Terdapat 685 buku dengan 'title' dan 'author' yang sama. 
4. Tidak ada *missing value*.
5. Fitur 'average_rating','num_of_pages','ratings_count','text_reviews_count' mempunyai 'outlier'.

Berdasarkan hasil dari *Data Assesing*, maka selanjutnya dilakukan *Data Cleaning* atau pembersihan data yang meliputi:
1. Penghapusan *record* dengan 'average_rating', 'ratings_count', dan 'num_of_pages' bernilai nol karena mempengaruhi performa model. Lebih lanjut, *record* dengan 'text_reviews_count' bernilai 0 tidak dihilangkan karena memungkinkan bagi pengguna untuk memberikan penilaian rating tanpa memberi ulasan teks.
2. Pembuatan fitur baru 'only_author' yang hanya memuat nama penulis saja. Di sisi lain, fitur 'authors' dihapuskan dari dataset.
3. Penghapusan 685 *record* yang terduplikat.
4. Penggunaan *z-score* untuk mengatasi *outlier*. Seriap *record* dihitung nilai *z-score*-nya dengan menggunakan rumusan berikut.
$$z = \frac{x - \mu}{\sigma}$$
dengan:
  - $z$ = nilai data yang dihitung z-score-nya.
  - $x$ = nilai data.
  - $\mu$ = nilai rata-rata
  - $\sigma$ = standar deviasi.
Lebih lanjut, digunakan threshold z-score sebesar 3, yang berarti data dengan nilai z-score lebih dari 3 diasumsikan sebagai outlier sehingga perlu dihilangkan dari dataset.

Hasil akhir dari data cleaning menghasilkan dataset baru yang terdiri dari 9902 *record* dan 7 fitur. *Dataset* inilah yang akan digunakan dalam tahap selanjutnya. 

### Analisis Univariat 
Data yang sudah dibersihkan selanjutnya bisa digunakan untuk analisis univariat. Analisis univariat dilakukan untuk mengetahui dan mengindentifikasi karakterisitik dari setiap fitur. 

a. Fitur Kategori

Diperhatikan Gambar 1a berikut ini yang menyajikan top 10 buku dengan nilai peringkat tertinggi. 
Gambar 1a. Top 10 Buku dengan Nilai Peringkat Tertinggi
Berdasarkan Gambar 1a di atas, diperoleh bahwa:
1. Buku 'The John Deere Two-Cylinder Tractor Encyclopedia: The Complete Model by Model History' menjadi dengan nilai peringkat tertinggi.
2. Top 10 buku dengan nilai peringkat tertinggi mempunyai nilai rating yang tidak jauh berbeda, yang masing-masing nilai peringkat berkisar antara 4.7-4.83.

Diperhatikan Gambar 1b berikut ini yang menyajikan top 10 buku yang paling banyak dinilai peringkatnya.
Gambar 1b. Top 10 Buku yang Paling Banyak Dinilai Peringkatnya
Berdasarkan Gambar 1b di atas, diperoleh bahwa:
1. Buku 'The Pelican Grief' menjadi buku yang paling banyak dinilai rating-nya oleh pengguna goodreads.
2. Top 10 buku yang paling banyak dinilai peringkatnya mempunyai nilai rating yang berkisar antara 270-350 ribu rating.

Diperhatikan Gambar 1c berikut ini yang top 10 buku dengan jumlah halaman terbanyak.
Gambar 1c. Top 10 Buku dengan Jumlah Halaman Terbanyak
Berdasarkan Gambar 1c di atas, diperoleh bahwa:
1. Buku 'Chemistry: The Central Science' menjadi buku dengan jumlah halaman terbanyak.
2. Top 10 buku dengan jumlah halaman terbanyak mempunyai jumlah halaman yang tidak jauh berbeda, yang masing-masing nilainya berkisar antara 1024-1046 halaman.

Diperhatikan Gambar 1d berikut ini yang menyajikan top 10 penulis dengan Total buku terbanyak yang ada di GoodReads.
Gambar 1d. Top 10 Penulis dengan Total Buku Terbanyak yang Ada di GoodReads
Berdasarkan Gambar 1d di atas, diperoleh bahwa:
1. Stephen King menjadi penulis dengan total buku terbanyak, yaitu 58 buku.
2. Top 10 penulis dengan total buku terbanyak mempunyai nilai total buku berkisar antara 32-58 buku.

Diperhatikan Gambar 1e berikut ini yang menyajikan *wordcloud* dari judul buku.
Gambar 1e. *Wordcloud* dari Judul Buku
Berdasarkan Gambar 1e di atas, terlihat bahwa kata yang sering digunakan dalam judul buku, yaitu Life, Book, World, History, Tale, Guide dst.

Diperhatikan Gambar 1f berikut ini.
Gambar 1f. Distribusi Kode Bahasa.
Berdasarkan Gambar 1f di atas, terlihat bahwa sebagian besar buku berbahasa Inggris.

b. Fitur Numerik
Diperhatikan Gambar 1b berikut ini.
Gambar 1b. Analisis Univariat (Fitur Numerik)
Berdasarkan Gambar 1b di atas, diperoleh bahwa:
1. Distribusi 'average_rating' cenderung mendekati distribusi normal.
2. Distribusi 'num_of_pages', 'ratings_count', dan text_reviews_count' cenderung miring ke kanan.
3. Nilai 'ratings_count' sebagian besar berada pada rentang 0-50.000. Di lain hal, nilai 'text_reviews_count' sebagian besar berada pada rentang 0-1000.

### Data Preparation

## Modeling
## Evaluation

