# Laporan Proyek Machine Learning - Sistem Rekomendasi Buku

## Domain Proyek 
Goodreads adalah situs web sosial berbasis buku milik Amazon bagi anggota untuk berbagi buku, membaca, meninjau buku, menilai buku, dan terhubung dengan pembaca lain [[4](https://asistdl.onlinelibrary.wiley.com/doi/abs/10.1002/asi.23733)]. Sebanyak puluhan juta ulasan buku tersedia di Goodreads. Informasi berupa judul buku, kode bahasa, nama penulis, nilai rata-rata rating, banyak rating, banyak ulasan teks, dan jumlah halaman buku bisa digunakan pengguna untuk untuk memilih buku yang relevan. Namun, tersedianya pilihan jutaan buku di Goodreads, kadan menyulitkan pengguna untuk memilih buku yang relevan. 

Sistem rekomendasi dapat membantu pengguna Goodreads untuk mendapatkan rekomendasi buku yang relevan. Sistem rekomendasi merupakan sistem yang bertujuan untuk memberikan rekomendasi produk atau layanan online yang dipersonalisasi kepada pengguna untuk menangani masalah kelebihan informasi online yang meningkat [[3](https://www.sciencedirect.com/science/article/pii/S0167923615000627
)]. Sistem rekomendasi dibagi menjadi dua, yaitu Content-Based Filtering dan Collaborative Filtering. Sistem rekomendasi Content-Based Filtering dapat dibangun menggunakan teknik Cosine Similarity [[1](https://ejurnal.umri.ac.id/index.php/coscitech/article/view/5131)]. Di sisi lain, sistem rekomendasi Collaborative Filtering dapat dibangun menggunakan algoritma K-Nearest Neighbors (KNN) [[2](https://www.mikroskil.ac.id/ejurnal/index.php/jsm/article/view/659)].

Pada proyek ini, akan dibangun dua sistem rekomendasi buku. Keduanya meliputi sistem rekomendasi Content-Based Filtering menggunakan teknik Cosine Similarity, yang memanfaatkan informasi mengenai kode bahasa dan nama penulis sebagai filternya, serta sistem rekomendasi Collaborative Filtering menggunakan algoritma K-Nearest Neighbors (KNN), yang memanfaatkan informasi mengenai nilai rata-rata rating, banyak rating, banyak ulasan teks, dan jumlah halaman. 

## Business Understanding
Pengembangan sistem rekomendasi buku bertujuan untuk memberikan manfaat kepada pengguna Goodreads, salah satu manfaat tersebut yaitu untuk membantu pengguna Goodreads mendapatkan rekomendasi buku yang relevan.

### Problem Statements
- Bagaimana cara mengolah *dataset* sehingga bisa digunakan untuk mengembangkan sistem rekomendasi Content-Based Fitering menggunakan teknik Cosine Similarity dan sistem rekomendasi Collaborative Filtering menggunakan algoritma KNN?
- Bagaimana cara mengidentifikasi karakteristik *dataset*?
- Bagaimana cara mengevaluasi performa sistem rekomendasi Content-Based Fitering menggunakan teknik Cosine Similarity dan sistem rekomendasi Collaborative Filtering menggunakan algoritma KNN sehingga diperoleh model dengan performa terbaik?
  
### Goals
- Mengetahui cara mengolah *dataset* sehingga bisa digunakan untuk mengembangkan sistem rekomendasi Content-Based Fitering menggunakan teknik Cosine Similarity dan sistem rekomendasi Collaborative Filtering menggunakan algoritma KNN.
- Mengetahui cara mengidentifikasi karakteristik *dataset*.
- Mengetahui cara mengevaluasi performa sistem rekomendasi Content-Based Fitering menggunakan teknik Cosine Similarity dan sistem rekomendasi Collaborative Filtering menggunakan algoritma KNN sehingga diperoleh model dengan performa terbaik.

### Solution Statements
- Untuk mengolah *dataset* sehingga bisa digunakan untuk mengembangkan sistem rekomendasi Content-Based Fitering menggunakan teknik Cosine Similarity dan sistem rekomendasi Collaborative Filtering menggunakan algoritma KNN, dilakukan *Data Assesing* dan *Data Preparation*. *Data Preparation* yang dilakukan meliputi *Data Cleaning*, representasi fitur, reduksi fitur, dan *Scaling* fitur numerik.
- Untuk mengidentifikasi karakteristik dari *dataset*, dilakukan analisis univariat, baik terhadap fitur kategori maupun fitur numerik. Analsis univariat terhadap fitur kategori dilakukan menggunakan *bar plot* dan *wordclod*. Di sisi lain, analisis univariat terhadap fitur numerik dilakukan menggunakan *histogram plot*.
- Untuk mengevaluasi performa sistem rekomendasi Content-Based Fitering menggunakan teknik Cosine Similarity digunakan metrik *precision*. Di sisi lain, untuk mengevaluasi performa sedangkan performa sistem rekomendasi Collaborative Filtering menggunakan algoritma KNN, digunakan metrik *Davies Bouldien Score*. Lebih lanjut, dibandingkan interpretasi hasil metrik evaluasi kedua model sehingga diperoleh model dengan performa terbaik. 


## Data Understanding
Data yang digunakan dalam proyek ini merupakan data sekunder yang diperoleh dari Kaggle dengan nama dataset yaitu 'goodreads-books'. Data tersebut dapat diakses melalui tautan berikut:
https://www.kaggle.com/datasets/jealousleopard/goodreadsbooks/data

Lebih lanjut, detail mengenai *dataset* tersebut diberikan sebagai berikut:
- Dataset berupa file CSV.
- Dataset terdiri dari 11127 *record* (pengamatan) dan 12 fitur. 
- Dataset terdiri dari 6 fitur kategori (;title', 'authors', 'isbn', 'language_code', 'publication_date', dan 'publisher') dan 6 fitur numerik ('average_rating', 'book_id', 'isbn13', 'num_of_pages', 'rating_count', dan 'text_reviews_count').

### Variabel-Variabel dari goodreads-book Dataset
Berdasarkan informasi di Kaggle, variabel-variabel pada *dataset* adalah sebagai berikut:
Berdasarkan informasi dari Kaggle, variabel-variabel pada dataset adalah sebagai berikut:
1. bookID: nomor identifikasi unik untuk setiap buku.
2. title: judul buku.
3. author: penulis buku tertentu.
4. average_rating: peringkat rata-rata untuk setiap buku (0-5)
5. ISBN: momor yang memberi tahu informasi tentang buku, secara lebih spesifik tenatang edisi dan penerbit
6. isbn13: format baru untuk ISBN yang terdiri 13 digit dan mulai diterapkan pada tahun 2007 
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
   
### Data Assesing 
Pada tahap *Data Assesing*, dilakukan pengecekan terhadap:
1. Deskripsi statistik fitur numerik.
2. *Unique value* fitur kategori.
3. Data duplikat (data yang bernilai sama dengan data lainnya).
4. *Missing value* (data yang hilang atau tidak tersedia).
5. *Outlier* (data yang menyimpang dari rata-rata sekumpulan data yang ada).

Hasil *Data Assesing* yang sudah dilakukan, sebagai berikut:
1. Berdasarkan pengecekan deskripsi statistik, diperoleh bahwa fitur 'average_rating', 'ratings_count', 'num_of_pages' dan 'text_reviews_count' mempunyai nilai minimum 0, yang berarti:
   - Terdapat buku yang tidak dinilai maupun di-review oleh pengguna goodreads.
   - Terdapat buku tanpa halaman.
   - Terdapat ada buku tanpa ulasan (berupa teks) yang diberikan oleh pengguna Goodreads.
3. Berdasarkan pengecekan *unique value* fitur kategori, diperoleh bahwa:
   - Fitur 'title' mempunyai 10214 *unique value*.
   - Fitur 'authors' mempunyai 6548 *unique value*.
   - Fitur 'language_code' mempunyai 26 *unique value*.
   - Terdapat buku dengan nama penulis yang terdiri lebih dari satu orang. Namun, jika ditelusuri lebih lanjut sebanarnya hanya nama pertama yang merupakan penulis buku, nama kedua atau ketiga bukan merupakan penulis, tetapi pihak ketiga yang terlibat dalam pembuatan buku seperti menjadi ilustrator atau lainnya.
   - Terdapat kode bahasa pada fitur 'language_code' yang tidak sesuai standar kode bahasa ISO 639-2.
4. Terdapat 685 buku dengan 'title' dan 'author' yang sama. 
5. Tidak ada *missing value*.
6. Fitur 'average_rating','num_of_pages','ratings_count', dan 'text_reviews_count' mempunyai 'outlier'.

### Analisis Univariat 
Data yang sudah dibersihkan digunakan untuk analisis univariat. Analisis univariat dilakukan untuk mengetahui karakterisitik dari setiap fitur. 

a. Fitur Kategori

Diperhatikan Gambar 1a berikut ini yang menyajikan top 10 buku dengan nilai peringkat tertinggi. 

![1a](https://github.com/rzknra/idcamp_mlt_recommmender_system/assets/94267677/07f85980-8a7d-4abf-9009-b944f5bc3d5d)

Gambar 1a. Top 10 Buku dengan Nilai Peringkat Tertinggi.

Berdasarkan Gambar 1a di atas, diperoleh bahwa:
1. Buku 'The John Deere Two-Cylinder Tractor Encyclopedia: The Complete Model by Model History' menjadi buku dengan nilai peringkat tertinggi.
2. Top 10 buku dengan nilai peringkat tertinggi mempunyai nilai rating yang tidak jauh berbeda, yang masing-masing nilai peringkat berkisar antara 4.7-4.83.


Selanjutnya, diperhatikan Gambar 1b berikut ini yang menyajikan top 10 buku yang paling banyak dinilai peringkatnya.

![1b](https://github.com/rzknra/idcamp_mlt_recommmender_system/assets/94267677/b25b2174-0546-4e45-a18c-1d4ebd259d06)

Gambar 1b. Top 10 Buku yang Paling Banyak Dinilai Peringkatnya.

Berdasarkan Gambar 1b di atas, diperoleh bahwa:
1. Buku 'The Pelican Grief' menjadi buku yang paling banyak dinilai rating-nya oleh pengguna goodreads.
2. Top 10 buku yang paling banyak dinilai peringkatnya mempunyai nilai rating yang berkisar antara 270-350 ribu rating.

Selanjutnya, diperhatikan Gambar 1c berikut ini yang top 10 buku dengan jumlah halaman terbanyak.

![1c](https://github.com/rzknra/idcamp_mlt_recommmender_system/assets/94267677/5e0d4d44-449e-4d49-82f1-fed5c18e8af8)

Gambar 1c. Top 10 Buku dengan Jumlah Halaman Terbanyak.

Berdasarkan Gambar 1c di atas, diperoleh bahwa:
1. Buku 'Chemistry: The Central Science' menjadi buku dengan jumlah halaman terbanyak.
2. Top 10 buku dengan jumlah halaman terbanyak mempunyai jumlah halaman yang tidak jauh berbeda, yang masing-masing nilainya berkisar antara 1024-1046 halaman.

Selanjutnya, diperhatikan Gambar 1d berikut ini yang menyajikan top 10 penulis dengan Total buku terbanyak yang ada di Goodreads.

![1d](https://github.com/rzknra/idcamp_mlt_recommmender_system/assets/94267677/e0f43285-b3fa-447e-ab8e-a6d0f878727b)

Gambar 1d. Top 10 Penulis dengan Total Buku Terbanyak yang Ada di Goodreads.

Berdasarkan Gambar 1d di atas, diperoleh bahwa:
1. Stephen King menjadi penulis dengan total buku terbanyak, yaitu 58 buku.
2. Top 10 penulis dengan total buku terbanyak mempunyai nilai total buku berkisar antara 32-58 buku.

Selanjutnya, diperhatikan Gambar 1e berikut ini yang menyajikan *wordcloud* dari judul buku.

![1e](https://github.com/rzknra/idcamp_mlt_recommmender_system/assets/94267677/2233c01a-10a4-4452-b59d-950b989b4f8e)

Gambar 1e. *Wordcloud* dari Judul Buku

Berdasarkan Gambar 1e di atas, terlihat bahwa kata yang sering digunakan dalam judul buku, yaitu *Life, Book, World, History, Tale, Guide* dst.

Selanjutnya, diperhatikan Gambar 1f berikut ini.

![1f](https://github.com/rzknra/idcamp_mlt_recommmender_system/assets/94267677/e5a33372-b233-4977-898e-3d9740f03508)

Gambar 1f. Kode Bahasa.

Berdasarkan Gambar 1f di atas, terlihat bahwa sebagian besar buku berbahasa Inggris.
<br/><br/>

b. Fitur Numerik

Diperhatikan Gambar 1b berikut ini.

![1g](https://github.com/rzknra/idcamp_mlt_recommmender_system/assets/94267677/d29067d4-69a8-4c39-a6ee-ee4ef1fc9fb5)

Gambar 1b. Analisis Univariat (Fitur Numerik)

Berdasarkan Gambar 1b di atas, diperoleh bahwa:
1. Distribusi 'average_rating' cenderung mendekati distribusi normal.
2. Distribusi 'num_of_pages', 'ratings_count', dan text_reviews_count' cenderung miring ke kanan.
3. Nilai 'ratings_count' sebagian besar berada pada rentang 0-50.000. Di lain hal, nilai 'text_reviews_count' sebagian besar berada pada rentang 0-1000.

## Data Preparation 
*Data preparation* dilakukan untuk mentransformasi data sehingga menjadi bentuk yang cocok dalam proses pemodelan. Pada bagian ini, dilakukan tiga tahap *data preparation*, yaitu:

1. *Data Cleaning*
   
Berdasarkan hasil dari *Data Assesing*, maka kemudian dilakukan *Data Cleaning* atau yang meliputi:
  - Penghapusan *record* dengan 'average_rating', 'ratings_count', dan 'num_of_pages' bernilai nol karena mempengaruhi performa model. Lebih lanjut, *record* dengan 'text_reviews_count' bernilai 0 tidak dihilangkan karena memungkinkan bagi pengguna untuk memberikan penilaian rating tanpa memberi ulasan teks.
  - Pembuatan fitur baru 'only_author' yang hanya memuat nama penulis saja dan penhapusan fitur 'authors' dihapuskan dari dataset.
  - Penghapusan 685 *record* yang terduplikat.
  - Penggunaan *z-score* untuk mengatasi *outlier*. Setiap data dihitung nilai *z-score*-nya dengan menggunakan rumusan berikut.
  $$z = \frac{x - \mu}{\sigma}$$
dengan:
    - $z$ = nilai data yang dihitung z-score-nya.
    - $x$ = nilai data.
    - $\mu$ = nilai rata-rata
    - $\sigma$ = standar deviasi.
Lebih lanjut, digunakan threshold z-score sebesar 3, yang berarti data dengan nilai z-score lebih dari 3 diasumsikan sebagai outlier sehingga perlu dihilangkan dari dataset. Hasil akhir dari data cleaning menghasilkan dataset baru yang terdiri dari 9902 *record* (pengamatan) dan 7 fitur. *Dataset* inilah yang akan digunakan dalam tahap selanjutnya.

2. *Data preparation* untuk membangun sistem rekomendasi Content-Based Filtering menggunakan dengan teknik Cosine Similarity, berupa:
    - Representasi Fitur.
Sistem rekomendasi Content-Based Filtering menggunakan dengan teknik Cosine Similarity akan dibangun menggunakan fitur 'language_code' dan 'only_author' sebagai filternya. Oleh karena itu, kedua fitur tersebut direpresentasikan menjadi vektor tf-idf. Vektor tersebut selanjutnya dibentuk menjadi matriks sehingga bisa diproses dengan baik oleh model cosine similarity. 

3. *Data preparation* untuk membangun sistem rekomendasi Collaborative Filtering menggunakan algoritma KNN, meliputi:
    - Reduksi Fitur.
Fitur yang tidak digunakan untuk membangun sistem rekomendasi Collaborative Filtering menggunakan algoritma KNN, yaitu 'language_code' dan 'only_author' dihilangkan dari dataset sehingga dihasilkan dataset baru tanpa kedua fitur tersebut.
    - Scaling Fitur Numerik.
Scaling atau penyekelaan ialah proses mengubah data sehingga mempunyai nilai dalam rentang tertentu. Untuk fitur numerik, salah satu teknik yang umum untuk digunakan yaitu MinMaxScaler dari library Scikitlearn. MinMaxScaler mentransformasi data sehingga nilainya berada dalam rentang 0 hingga 1. MinMaxScaler melakukan proses penyekalaan fitur dengan mengurangkan nilai minimal fitur (min) kemudian membaginya dengan selisih dari nilai minimal fitur (min) dan nilai maksimal fitur(max), yaitu
$$x_{scaled} = \frac{x - min}{max - min},$$
dengan:
      - $x_{scaled}$ = hasil scaling data.
      - $x$ = nilai data pada fitur yang di scaling.
      - $min$ = nilai minimal fitur.
      - $max$ = nilai maksimal fitur.


## Modeling
Pada tahap ini dikembangkan model sistem rekomendasi, yaitu 
1. Model Content-Based Filtering menggunakan teknik Cosine Similarity.
2. Model Collaborative Filtering menggunakan algoritma KNN.

Kedua model tersebut bisa membantu mengukur kemiripan antar data. Penjelasan lebih lanjut tentang kedua model tersebut diberikan sebagai berikut.

1. Cosine Similarity.
   
Cosine similarity mengukur kesamaan antara dua vektor dan menentukan apakah kedua vektor tersebut menunjuk ke arah yang sama. Hal tersebut dilakukan dengan menghitung sudut cosinus antara dua vektor. Semakin kecil sudut cosinus, maka semakin besar nilai cosine similarity. Berikut ini diberika rumusan cosine similarity.
$$cos(\theta) = \frac{\overrightarrow{a} \cdot \overrightarrow{b}}{||\overrightarrow{a}|| * || \overrightarrow{b} ||}$$
dengan:    
  - $cos(\theta)$ = nilai cosinus vektor $\overrightarrow{a}$ dan vektor $\overrightarrow{b}$.
  - $\overrightarrow{a} \cdot \overrightarrow{b}$ = nilai *dot product* dari vektor $\overrightarrow{a}$ dan vektor $\overrightarrow{b}$.
  - $|| \overrightarrow{a} ||$ = norma euclidean dari vektor $\overrightarrow{a}$.
  - $|| \overrightarrow{b} ||$ = norma euclidean dari vektor $\overrightarrow{b}$.

Kelebihan dan kekurangan teknik cosine similarity diberikan sebagai berikut.
1. Kelebihan.
    - Berlaku untuk Berbagai Bentuk Data: Metode ini dapat digunakan untuk mengukur kesamaan dalam berbagai bentuk data, termasuk teks, gambar, dan suara.
    - Implementasi Mudah: Perhitungan cosine similarity relatif mudah diimplementasikan menggunakan perangkat lunak komputer1.
    - Relevansi Pencarian: Dalam pengolahan data dan mesin pencarian, cosine similarity membantu menemukan dokumen-dokumen yang paling relevan dengan query yang dimasukkan1.
2. Kekurangan.
    - Tidak Memperhatikan Urutan: Cosine similarity hanya memperhatikan sudut kosinus antara dua vektor, sehingga tidak memperhitungkan urutan kata atau elemen dalam dokumen.
    - Sensitif terhadap Frekuensi: Metode ini dapat sensitif terhadap frekuensi kata dalam dokumen. Jika suatu kata muncul lebih sering, maka akan mempengaruhi nilai cosine similarity3.
    - Tidak Memperhitungkan Makna: Meskipun mengukur kesamaan secara matematis, cosine similarity tidak memperhitungkan makna kata atau konteks4.

Model Content-Based Filtering menggunakan teknik Cosine Similarity dikembangkan dengan dua filter, yaitu 'language_code' dan 'only_author'. Model Content-Based Filtering menggunakan teknik Cosine Similarity (dengan filter 'language_code') diuji cobakan untuk memberi rekomendasi buku yang mirip dengan buku 'La Place de la Concorde Suisse' yang berbahasa prancis. Diperoleh hasil rekomendasi berikut:

Tabel 1a. Model Content-Based Filtering menggunakan Teknik Cosine Similarity (dengan Filter 'language_code').

|    | title                              | language_code   |
|----|------------------------------------|-----------------|
|  0 | Bright Lights  Big City            | fre             |
|  1 | La Petite Fille du Lac             | fre             |
|  2 | L'Épée de Darwin                   | fre             |
|  3 | Les Fils des ténèbres              | fre             |
|  4 | Da Vinci Code (Robert Langdon  #2) | fre             |

Terlihat bahwa model yang dibangun tersebut berhasil memberikan rekomendasi 5 judul buku lainnya yang juga berbahasa prancis.

Selanjutnya, Model Content-Based Filtering menggunakan teknik Cosine Similarity (dengan filter 'language_code') diuji cobakan untuk memberi rekomendasi buku yang mirip dengan buku 'The Passion' karya penulis Jeanette Winterson. Diperoleh hasil rekomendasi berikut:

Tabel 1b. Hasil Rekomendasi Model Content-Based Filtering menggunakan Teknik Cosine Similarity (dengan Filter 'author').

|    | title                                         | only_author        |
|----|-----------------------------------------------|--------------------|
|  0 | Art and Lies                                  | Jeanette Winterson |
|  1 | Sexing the Cherry                             | Jeanette Winterson |
|  2 | Art Objects: Essays on Ecstasy and Effrontery | Jeanette Winterson |
|  3 | Lighthousekeeping                             | Jeanette Winterson |
|  4 | Written on the Body                           | Jeanette Winterson |

Terlihat bahwa model yang dibangun tersebut berhasil memberikan rekomendasi 5 judul buku lainnya yang juga ditulis oleh Jeanette Winterson.

3. KNN

K-Nearest Neighbors (KNN) merupakan algoritma pengelompokan yang sederhana. Algoritma KNN merupakan algoritma pengelompokan yang bekerja dengan mengambil sejumlah K data terdekat (tetangganya) sebagai acuan untuk menentukan kelompok dari data baru. Algoritma ini mengelompokan data berdasarkan similarity atau kemiripan atau kedekatannya terhadap data lainnya. Pada proyek ini, metrik pengukur kemiripan data yang digunakan yaitu *euclidean distance* dengan rumusan sebagai berikut. 
$$euc(a,b) = \sqrt{\sum_{i=1}^{k}(a_i-b_i)^2}$$

dengan:
- $a_i$ = nilai fitur ke-i dari data $a$.
- $b_i$ = nilai fitur ke-i dari data $b$.

Kelebihan dan kekurangan algoritma KNN, diberikan sebagai berikut:
1. Kelebihan.
    - Mudah diimplementasikan dan dipahami.
    - Tidak memerlukan proses pelatihan yang kompleks.
    - Cocok untuk dataset yang relatif kecil.
    - KNN merupakan algoritma non-parametrik, yang berarti tidak membuat asumsi tertentu tentang distribusi data.
2. Kekurangan.
    - Sangat sensitif terhadap data pencilan (outliers).
    - Memerlukan penyimpanan data yang besar karena harus menyimpan seluruh dataset.
    - Memerlukan waktu komputasi yang tinggi untuk menghitung jarak antara setiap titik data.
    - Performa algoritma dapat menurun jika jumlah fitur (dimensi) data sangat besar.
    - KNN tidak dapat menangani data kategori yang hilang atau data yang tidak lengkap.
    
Model Collaborative Filtering menggunakan algoritma KNN yang dikembangkan menggunakan nilai parameter K=6, yang berarti model akan memberikan 6 buku rekomenadasi yang mirip dengan buku yang ingin dicari rekomendasinya oleh pengguna. Salah satu dari judul buku hasil rekomendasi model tersebut nenpunyai judul yang sama dengan buku yang ingin dicari rekomendasinya oleh pengguna. Akibatnya, dari sini terhitung bahwa model sebanarnya hanya memberikan rekomendasi 5 buku yang relevan. Buku yang mempunyai judul yang sama dengan buku yang ingin dicari pengguna tersebut bisa diabaikan dan tidak dijadikan keluaran model.  

Telah dilakukan uji coba Model Collaborative Filtering menggunakan algoritma KNN tersebut dengan hasil rekomendasi berikut:

Tabel 3. Hasil Rekomendasi Model Collaborative Filtering menggunakan Algoritma KNN.

|    | Book Title                                         | Similiarity Score   |
|----|----------------------------------------------------|---------------------|
|  0 | Philosophy: The Classics                           | 100.0%              |
|  1 | The Odes                                           | 100.0%              |
|  2 | Pyramids of Montauk: Explorations in Consciousness | 100.0%              |
|  3 | Buddhism: A Concise Introduction                   | 99.99%              |
|  4 | Sliding Scales (Pip & Flinx #10)                   | 99.99%              |

Model yang dibuat tersebut berhasil memberikan rekomendasi 5 judul buku yang serup dengan buku 'The Untouchables' dengan tingkat kemiripan 99.9%-100%.

## Evaluation
Model rekomendasi yang sudah dibangun dievaluasi menggunakan metrik berikut:

1. Precision.

Model Content Based-Filtering dengan teknik Cosine Similarity dievaluasi menggunakan metrik *precision* (presisi). Untuk sistem rekomendasi, rumusan metrik presisi diberikan sebagai berikut.

$$ Precision = \frac{Rel}{Rec},$$

dengan:
  - $Rel$ = banyak item hasil rekomendasi yang relevan.
  - $Rec$ = banyak item hasil rekomendasi.
  
Berdasarkan uji coba Model Content Based-Filtering menggunakan teknik Cosine Similarity di atas, diperoleh bahwa $\frac{5}{5}$ hasil rekomendasi mempunyai kode bahasa atau penulis yang serupa dengan buku yang digunakan oleh pengguna. Oleh karena itu, diperoleh Model Content Based-Filtering menggunakan teknik Cosine Similarity mempunyai presisi sebesar $\frac{5}{5} = 1$ atau dengan kata lain model tersebut mempunyai presisi $100$%.

2. Davies-Bouldin Score.

Model Collaborative Filtering menggunakan algoritma KNN dievaluasi menggunakan metrik *Davies-Bouldin Score*, yaitu metrik evaluasi yang digunakan untuk mengukur kualitas pengelompokan dalam analisis klaster. Skor ini mengukur seberapa baik sebuah klaster dipisahkan satu sama lain dan seberapa serupa objek dalam klaster yang sama. Semakin rendah nilai *Davies-Bouldin Score*, semakin baik separasi tiap kluster yang dihasilkan model. Metrik ini mempunyai rumusan sebagai berikut.

$$DB = \frac{1}{k}\sum_{i=1}^{k}max(\frac{\Delta(x_i)+\Delta(x_j)}{\delta(x_i,x_j)}),$$

dengan:
- $\Delta(x_i)$ = jarak rata-rata setiap titik data pada kluster $i$ dengan centroid kluster $i$.
- $\Delta(x_j)$ = jarak rata-rata setiap titik data pada kluster $i$ dengan centroid kluster $j$.
- $\delta(x_i,x_j)$ = jarak centroid kluster $i$ dan centroid kluster $j$.

Kode berikut ini digunakan untuk menghitung *Davies-Bouldin Score*.
```
db_score = davies_bouldin_score(book_cf, book_title)
print(db_score)
```
Kode tersebut menghasilkan *output* *Davies-Bouldin Score* sebesar 3.8725434409129003. Skor tersebut cukup kecil. Hal ini mengindikasikan bahwa separasi tiap kluster yang dihasilkan model cukup baik. Dengan separasi tiap kulster yang cukup baik, maka model mampu memberikan hasil rekomendasi yang cukup baik. Hal ini terlihat pada uji coba model KNN untuk memberikan 5 rekomendasi buku yang mirip dengan buku 'The Untouchables', diperoleh tingkat kemiripan buku 'The Untouchables' dengan buku-buku yang direkomendasikan sebesar 99,9%-100%.  

Dengan demikian, berdasarkan hasil evaluasi tersebut, diperoleh bahwa:
1. Model Content Based-Filtering dengan teknik Cosine Similarity menpunyai presisi 100%, yang berarti model tersebut mampu memberikan hasil rekomenadasi buku yang baik atau relevan.
2. Model Collaborative Filtering menggunakan algoritma KNN mempunyai *Davies-Bouldin Score* sebesar 3.8725434409129003, yang berarti mampu memberikan hasil rekomenadasi buku yang cukup baik atau relevan.
Oleh karena itu, model Content Based-Filtering dengan teknik Cosine Similarity menjadi model dengan performa terbaik untuk memberi rekomendasi buku yang relevan. 

## Referensi
[1] Ardiansyah, R., Bianto, M. A., & Saputra, B. D. (2023). Sistem Rekomendasi Buku Perpustakaan Sekolah menggunakan Metode Content-Based Filtering. Jurnal CoSciTech (Computer Science and Information Technology), 4(2), 510-518.

[2] Gohzali, H., Megawan, S., Erwin, E., & Onggo, J. (2019). Rekomendasi Buku Menggunakan K-Nearest Neighbor (KNN) dan Binary Particle Swarm Optimization (BPSO). Jurnal SIFO Mikroskil, 20(1), 81-92.

[3] Lu, J., Wu, D., Mao, M., Wang, W., & Zhang, G. (2015). Recommender system application developments: a survey. Decision support systems, 74, 12-32.

[4] Thelwall, M., & Kousha, K. (2017). Goodreads: A social network site for book readers. Journal of the Association for Information Science and Technology, 68(4), 972-983.


 
