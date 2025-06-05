# Laporan Proyek Machine Learning - Dewi Rachmawati

## Project Overview

Di era digital yang serba cepat, pengguna semakin bergantung pada layanan streaming untuk menikmati hiburan. Namun, dengan ribuan pilihan film yang tersedia, banyak pengguna mengalami choice overload, di mana terlalu banyak opsi justru membuat mereka kesulitan mengambil keputusan. Fenomena ini sering kali berujung pada decision fatigue, yaitu kondisi di mana kualitas pengambilan keputusan menurun akibat terlalu banyak pilihan atau keputusan yang harus dibuat. Dalam konteks layanan streaming, pengguna yang mengalami decision fatigue cenderung memilih film secara acak, mengulang tontonan lama, atau bahkan menunda keputusan sepenuhnya (Wu, 2022). Untuk mengatasi tantangan ini, sistem rekomendasi menjadi alat penting dalam membantu pengguna menemukan film yang sesuai dengan preferensi mereka tanpa harus tersesat dalam katalog yang luas.

Dua pendekatan utama dalam sistem rekomendasi adalah Content-Based Filtering dan Collaborative Filtering. Content-Based Filtering bekerja dengan menganalisis karakteristik film, seperti genre, sutradara, dan aktor, untuk memberikan rekomendasi berdasarkan kesamaan dengan film yang telah ditonton pengguna. Sementara itu, Collaborative Filtering memanfaatkan pola perilaku pengguna lain yang memiliki preferensi serupa untuk menyarankan film yang mungkin disukai. Studi terbaru menunjukkan bahwa pendekatan ini dapat meningkatkan kualitas rekomendasi dan mengurangi beban kognitif pengguna dalam memilih konten (Liao, 2023). Selain itu, sistem rekomendasi berbasis Collaborative Filtering telah terbukti meningkatkan keterlibatan pengguna dan mengurangi waktu pencarian, sehingga meningkatkan kepuasan dalam pengalaman menonton (Harper & Konstan, 2020).

Proyek ini bertujuan untuk mengembangkan sistem rekomendasi berbasis Content-Based Filtering dan Collaborative Filtering, menggunakan dataset MovieLens ml-latest-small, yang telah terbukti bersih dan bebas dari missing values. Dengan pendekatan ini, sistem rekomendasi diharapkan dapat memberikan rekomendasi yang lebih akurat dan membantu pengguna menemukan film yang sesuai dengan preferensi mereka tanpa mengalami kesulitan dalam pengambilan keputusan akibat banyaknya opsi yang tersedia.

### Referensi
- Harper, F. M., & Konstan, J. A. (2020). The MovieLens datasets: History and context. *ACM Transactions on Interactive Intelligent Systems, 5*(4), 19:1–19:19. https://doi.org/10.1145/2827872  
- Liao, M. (2023). Understanding the effects of personalized recommender systems on political news perceptions: A comparison of content-based, collaborative, and editorial choice-based news recommender system. *Journal of Broadcasting & Electronic Media, 67*(3), 294–322. https://doi.org/10.1080/08838151.2023.2206662   
- Wu, X. (2022). Comparison between collaborative filtering and content-based filtering. *Proceedings of the International Conference on Information Science and Technology*, 1–10. https://pdfs.semanticscholar.org/3b99/05ffb0aed764cd5fbeb3ed5dff0843cf9103.pdf  

## Business Understanding

Berdasarkan latar belakang di atas, dapat dibuat rumusan masalah sebagai berikut:
1. Bagaimana Content-Based Filtering dapat digunakan untuk meningkatkan relevansi rekomendasi dalam sistem rekomendasi film berdasarkan karakteristik film yang telah ditonton pengguna?
2. Bagaimana Collaborative Filtering dapat meningkatkan akurasi rekomendasi dengan menganalisis pola perilaku pengguna lain yang memiliki preferensi serupa?

Goals (Tujuan):
1. Mengembangkan sistem rekomendasi berbasis Content-Based Filtering yang mampu meningkatkan relevansi rekomendasi dengan menganalisis karakteristik film yang telah ditonton pengguna, sehingga rekomendasi yang diberikan lebih sesuai dengan preferensi individu
2. Menerapkan Collaborative Filtering untuk meningkatkan akurasi rekomendasi dengan mengidentifikasi pola perilaku pengguna lain yang memiliki kesamaan preferensi, sehingga sistem dapat menyarankan film yang mungkin disukai oleh pengguna berdasarkan data historis pengguna lain

Solution Approach 
1. Content-Based Filtering\
   Pendekatan ini bertumpu pada karakteristik film yang telah ditonton pengguna, memungkinkan sistem untuk mengidentifikasi kemiripan antara film dan memberikan rekomendasi berbasis fitur seperti genre.
  - Ekstraksi fitur genre dari dataset untuk membangun profil film berdasarkan kategorisasi genre yang tersedia
  - Transformasi metadata menggunakan TF-IDF, di mana setiap genre dikonversi ke dalam representasi numerik agar dapat dibandingkan dengan film lainnya
  - Penggunaan Cosine Similarity untuk menghitung tingkat kemiripan antar film, memastikan film yang direkomendasikan memiliki keterkaitan erat dengan yang telah ditonton pengguna
  - Generasi rekomendasi berdasarkan skor kesamaan tertinggi, sehingga pengguna mendapatkan daftar film yang relevan dengan preferensi mereka
Pendekatan ini sangat efektif dalam memberikan rekomendasi tanpa memerlukan riwayat interaksi dengan pengguna lain, sehingga dapat membantu menangani cold-start problem bagi item baru (Harper & Konstan, 2020).

2. Collaborative Filtering\
   Pendekatan ini berfokus pada pembelajaran hubungan laten antara pengguna dan film menggunakan embedding-based recommendation system. Model ini memanfaatkan Neural Networks untuk menangkap pola interaksi dalam dataset rating.
  - Representasi pengguna dan film dalam embedding space
     - Setiap pengguna dan film direpresentasikan dalam vektor numerik yang dipelajari secara otomatis melalui embedding
     - User Embedding dan Film Embedding digunakan untuk menangkap preferensi laten maisng-maisng entitas dalam sistem rekomendasi
     - Model mengembangkan pemahaman terhadap pola interaksi berdasarkan data historis rating
  - Perhitungan keterkaitan laten antara pengguna dan film
    - Dot product antara embedding pengguna dan film menentukan seberapa kompatibel pasangan pengguna-film berdasarkan pembelajaran sistem
    - Bias untuk pengguna dan film digunakan untuk meningkatkan akurasi dengan menangkap kecenderungan rating spesifik setiap entitas
  - Prediksi rating dnegan aktivasi sigmoid
    - Fungsi aktivasi sigmoid mengonversi hasil perhitungan interaksi ke dalam skala probabilitas untuk mendukung prediksi rating
    - Model menghasilkan skor yang mencerminkan kemungkinan pengguna menyukai suatu film berdasarkan keterkaitan laten
  - Pemilihan film dengan prediksi rating tertinggi
    - Setelah model memprediksi rating untuk film yang belum ditonton oleh pengguna, sistem menyaring film dengan nilai prediksi tertinggi
    - Daftar film direkomendasikan dengan mempertimbangkan film yang memiliki keterkaitan laten paling tinggi dengan preferensi pengguna

## Data Understanding
Dataset yang digunakan dalam proyek ini berasal dari MovieLens, sebuah kumpulan data rekomendasi film yang dikembangkan oleh GroupLens Research. Dataset yang dipilih adalah MovieLens Latest Small, yang berisi informasi interaksi pengguna terhadap film dalam bentuk rating. Dataset ini sering digunakan dalam penelitian sistem rekomendasi karena memiliki format yang terstruktur dan mencerminkan pola preferensi pengguna terhadap berbagai judul film. MovieLens Small mengandung 100,000 rating yang diberikan oleh 610 pengguna terhadap 9,000+ film, sehingga cukup representatif untuk analisis rekomendasi dalam skala kecil. Dataset ini dapat diunduh melalui tautan resmi GroupLens pada halaman berikut: [MovieLens Small Dataset](https://grouplens.org/datasets/movielens/latest/).

Dataset ini terdiri dari beberapa file yang menyimpan berbagai informasi, namun saya hanya mengambil 2 file utama:
1. movies.csv: berisi informasi metadata tentang film
   - `movieId`: ID unik setiap film
   - `title`: judul film beserta tahun rilisnya dalam tanda kurung
   - `genres`: genre film, dapat lebih dari 1 atau 2 kategori (dipisahkan dengan |)
2. ratings.csv: berisi informasi interaksi pengguna terhadap film melalui rating
   - `userId`: ID unik untuk setiap pengguna
   - `movieId`: ID film yang diberi rating oleh pengguna
   - `rating`: peringkat atau nilai rating yang diberikan oleh pengguna (skala 0,5 - 5,0 dengan interval 0,5)
   - `timestamp`: waktu ketika penilaian (rating) diberikan

**Rubrik/Kriteria Tambahan:** Melakukan Exploratory Data Analysis\
1. Analisis statistik deskriptif\
**Dataset Movies:**
  - `movieId`: nilai ID berkisar antara 1 hingga 193609 dengan rata-rata 42200. Sebagian besar ID film berada dalam kisaran 3248 hingga 76232 (kuartil ke-1 hingga ke-3)
  - `year_of_release`: tahun rilis berkisar antara tahun 1902 hingga 2018 dengan rata-rata di tahun 1994. Sebagian besar film berada dalam kisaran tahun 1988 hingga 2008 (kuartil ke-1 hingga ke-3)
  - `genre_count`: jumlah genre yang dimiliki oleh tiap film berkisar antara 1 hingga 10 dengan rata-rata 2 genre. Sebagian besar film memiliki genre dalam kisaran 1 hingga 3 (kuartil ke-1 hingga ke-3)

**Dataset Rating**
  - `userId`: ID pengguna berkisar antara 1 hingga 610 dengan rata-rata ID pengguna berada di angka 326. Sebagian besar memiliki ID dalam kisaran 177 hingga 477 (kuartil ke-1 hingga ke-3)
  - `movieId`: ID film yang diberi rating oleh pengguna berada dalam rentang 1 hingga 193609 dengan rata-rata 19435. Sebagian besar film yang diberi rating berada dalam ID 1199 hingga 8122. Ini menunjukkan bahwa film-film dengan ID lebih kecil cenderung lebih banyak diberi rating.
  - `rating`: rating yang diberikan pengguna berkisar antara 0,5 hingga 5 dengan rata-rata rating adalah 3,5. Sebagian besar rating berada pada rentang 3,0 hingga 4,0. Ini menunjukkan adanya kecenderungan pengguna memberikan rating cukup positif terhadap film yang mereka tonton.
  - `timestamp`: aktivitas rating yang dilakukan oleh pengguna berkisar antara pukul 18.36 tanggal 29/3/1996 hingga pukul 14.27 tanggal 24/9/2018 dengan rata-rata aktivitas rating yang dilakukan pengguna berkisar pada pukul 17.01 tanggal 19/3/2008. Kemudian sebagian besar aktivitas rating dilakukan antara pukul 09.57 tanggal 18/4/2002 hingga pukul 07.15 tanggal 4/7/2015. Ini menunjukkan bahwa aktivitas dominan terjadi dalam kurun waktu tahun 2002 hingga 2015.

**Dataset Gabungan**
  - `movieId`: ID film yang diberi rating oleh pengguna berkisar antara 1 hingga 193609 dengan rata-rata 19365. Sebagian besar film yang diberi rating berada dalam rentang ID 1198 hingga 8014. Ini menandakan bahwa ID lebih kecil cenderung memiliki lebih banyak film yang diberi rating.
  - `year_of_release`: tahun rilis film berkisar antara tahun 1902 hingga 2018 dengan rata-rata di tahun 1994. Sebagian besar film dirilis berada dalam kisaran tahun 1990 hingga 2003. Ini menandakan bahwa banyak film yang diproduksi pada rentang tahun 1990 hingga 2003.
  - `genre_count`: jumlah genre yang dimiliki oleh tiap film berkisar antara 1 hingga 10 dengan rata-rata 2 genre. Sebagian besar film memiliki genre dalam kisaran 1 hingga 3 (kuartil ke-1 hingga ke-3). Ini menandakan bahwa banyak film yang memiliki banyak genre.
  - `userId`: ID pengguna berkisar antara 1 hingga 510 edngan rata-rata ID pengguna berada di angka 326. Sebagian besar pengguna memiliki ID dalam kisaran 177 hinga 477. Ini menunjukkan bahwa kecenderungan pengguna yang memberi rating adalah pada rentang ID pengguna 177 hingga 477.
  - `rating`: rating yang diberikan pengguna berkisar antara 0,5 hingga 5 dengan rata-rata rating adalah 3,5. Sebagian besar rating berada pada rentang 3,0 hingga 4,0. Ini menunjukkan adanya kecenderungan pengguna memberikan rating cukup positif terhadap film yang mereka tonton.
  - `timestamp`: aktivitas rating yang dilakukan oleh pengguna berkisar antara pukul 18.36 tanggal 29/3/1996 hingga pukul 14.27 tanggal 24/9/2018 dengan rata-rata aktivitas rating yang dilakukan pengguna berkisar pada pukul 18.34 tanggal 17/3/2008. Kemudian sebagian besar aktivitas rating dilakukan antara pukul 12.46 tanggal 7/4/2002 hingga pukul 07.04 tanggal 4/7/2015. Ini menunjukkan bahwa aktivitas dominan terjadi dalam kurun waktu tahun 2002 hingga 2015.

2. Distribusi Rating Film
   ![alt text]()
