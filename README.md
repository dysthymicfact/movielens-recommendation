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
  - `movieId`: nilai ID berkisar antara 1 hingga 193609 dengan rata-rata 41798. Sebagian besar ID film berada dalam kisaran 3233 hingga 74809 (kuartil ke-1 hingga ke-3)
  - `year_of_release`: tahun rilis berkisar antara tahun 1902 hingga 2018 dengan rata-rata di tahun 1994. Sebagian besar film berada dalam kisaran tahun 1987 hingga 2008 (kuartil ke-1 hingga ke-3)
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
   ![alt text](https://github.com/dysthymicfact/movielens-recommendation/blob/main/images/distribusi%20rating.png?raw=true)\
Grafik distribusi rata-rata rating film menunjukkan bahwa mayoritas pengguna cenderung memberikan rating 3.5 dengan frekuensi sekitar 1400 lebih pengguna. Informasi lainnya, sebagian besar rating berkisar antara 3.0 dan 4.0 menunjukkan kecenderungan pengguna untuk menilai film secara positif.

3. Distribusi Genre Film
   ![alt text](https://github.com/dysthymicfact/movielens-recommendation/blob/main/images/10%20genre%20teratas.png?raw=true)
   ![alt text](https://github.com/dysthymicfact/movielens-recommendation/blob/main/images/distribusi%20genre.png?raw=true)\
Berdasarkan visualisasi data distribusi genre film di atas memberikan infromasi bahwa genre film yang paling banyak diproduksi adalah Drama dan Comedy sebanyak masing-masing 4000an dan lebih dari 3500 film. Ini berarti kedua genre tersebut telah mendominasi dunia perfilman. Dilanjutkan genre Thriller, Action, dan Romance yang cukup populer menjadi top 3,4, dan 5 film teratas. Di sisi lain, sebagian besar film memiliki 1 hingga 3 genre dengan jumlah tertinggi terdapat pada film yang memiliki 2 genre, diikuti oleh 1 dan 3.

4. Distribusi Tahun Rilis
   ![alt text](https://github.com/dysthymicfact/movielens-recommendation/blob/main/images/distribusi%20tahun%20rilis.png?raw=true)\
Distribusi jumlah film yang dirilis setiap tahun menunjukkan pola pertumbuhan yang mencerminkan dinamika industri perfilman selama lebih dari satu abad. Pada periode sebelum tahun 1970, produksi film berlangsung dalam skala yang lebih terbatas, dengan jumlah rilis yang cenderung stabil di bawah 50 film per tahun. Namun, memasuki dekade 1970-an, terjadi percepatan signifikan dalam jumlah produksi, yang kemudian meningkat lebih tajam setelah tahun 1980. Tren ini mencapai puncaknya pada awal 2000-an, dengan jumlah film yang dirilis per tahun melampaui 300 judul, menandai era ekspansi industri secara masif. Setelah tahun 2015, terlihat adanya penurunan tajam dalam jumlah film yang tercatat, yang kemungkinan besar bukan akibat dari berkurangnya produksi, melainkan keterbatasan data terbaru yang belum sepenuhnya terakumulasi. Secara keseluruhan, grafik ini mengilustrasikan bagaimana industri film mengalami evolusi yang pesat, didorong oleh berbagai faktor seperti teknologi, permintaan pasar, dan perubahan lanskap distribusi film dalam beberapa dekade terakhir.

5. Distribusi Rating per Film
   ![alt text](https://github.com/dysthymicfact/movielens-recommendation/blob/main/images/distribusi%20rating%20per%20film.png?raw=true)\
Histogram distribusi jumlah rating per film menunjukkan bahwa mayoritas film dalam dataset hanya menerima sedikit rating dari pengguna, dengan sebagian besar berada di kisaran 0–10 rating. Pola ini mencerminkan adanya long-tail effect, di mana hanya sejumlah kecil film yang menarik perhatian luas dan mendapatkan banyak ulasan, sementara sebagian besar film kurang dikenal atau kurang diminati. Tren ini mengindikasikan bahwa persebaran rating tidak merata, dengan beberapa film yang berhasil membangun popularitas besar, kemungkinan karena faktor seperti pemasaran, kualitas produksi, atau keterlibatan komunitas.

## Data Preparation
Teknik yang digunakan dalam Data Preparation adalah sebagai berikut:

1. Data Cleaning `movies.csv`\
   Dalam dataset movies.csv, informasi tahun rilis film digabungkan langsung dengan judul, sehingga perlu dipisahkan. Jika tidak ditangani dengan benar, kondisi ini dapat menyebabkan kesalahan interpretasi dalam tahap pelatihan model, terutama dalam analisis judul film sebagai fitur teks. Oleh karena itu, tahun rilis harus diekstrak dan dipindahkan ke dalam kolom terpisah agar dapat dianalisis secara terpisah tanpa memengaruhi pemrosesan judul film. Langkah ini memastikan bahwa model dapat mengenali pola dalam data dengan lebih akurat serta menghindari potensi inkonsistensi dalam pengolahan informasi film. 
2. Data Cleaning `ratings.csv`\
   Mengubah timestamps menjadi datetime agar mudah dipahami kapan pengguna melakukan penilaian (rating).
3. Data Merging `movies` dan `ratings`\
   Data dari movies dan ratings digabungkan menjadi satu tabel agar informasi tentang film dan penilaian pengguna dapat dianalisis secara bersamaan. Proses ini dilakukan dengan menyatukan kedua tabel berdasarkan kolom yang sama, sehingga setiap film dalam daftar memiliki informasi lengkap, termasuk rating yang diberikan oleh pengguna. Setelah digabungkan, hasilnya disimpan dalam variabel films, yang kemudian siap digunakan untuk pemrosesan lebih lanjut. 
4. Data Cleaning `films`\
   a. Menangani missing values\
      Data yang hilang, null, NaN atau tidak terbaca adalah masalah yang sering muncul dalam pemrosesan dataset. Jika tidak ditangani dengan baik, kondisi ini dapat memengaruhi hasil analisis dan performa model yang dibuat. Oleh karena itu, langkah yang diambil yaitu menghapus data yang missing value/bernilai kosong menggunakan `films.dropna()` agar hanya data yang bersih dan relevan yang digunakan dalam pemodelan. Kemudian terdapat salah satu missing values pada fitur yakni panda genre di mana terdapat entri label "(no genre listed)" yang menunjukkan bahwa film tersebut tidak memiliki informasi kategori genre yang jelas. Dengan menghapus entri semacam ini, data yang digunakan menjadi lebih akurat, memastikan bahwa setiap film memiliki informasi genre yang valid untuk analisis lebih lanjut.\
   b. Memperbaiki salah satu kategori ditur dalam genres\
      Dalam fitur genre, terdapat kategori Sci-Fi, akronim dari Science Fiction, sebuah istilah yang merujuk pada film bertema fiksi ilmiah. Namun, kehadiran tanda pisah (-) dalam akronim ini berpotensi menimbulkan masalah dalam tahap vektorisasi TF-IDF, karena sistem secara otomatis akan memisahkannya menjadi dua entitas terpisah, yaitu "Sci" dan "Fi". Kondisi ini dapat menyebabkan ketidakkonsistenan dalam pemrosesan teks, karena model akan menganggapnya sebagai dua kata yang tidak berkaitan, sehingga mengganggu analisis genre secara akurat. Oleh karena itu, sebelum dilakukan vektorisasi, tanda pisah perlu dihapus, agar istilah Sci-Fi tetap dikenali sebagai satu kesatuan, memastikan tokenisasi berjalan sesuai dengan makna asli dari genre tersebut.\
   c. Encoding Fitur Genres dengan TF-IDF\
      Untuk menerapkan content-based filtering, informasi genre film yang awalnya berbentuk teks perlu dikonversi menjadi format numerik agar dapat dianalisis. Salah satu pendekatan yang digunakan adalah Term Frequency-Inverse Document Frequency (TF-IDF), yang memberikan bobot pada setiap genre berdasarkan frekuensinya di seluruh dataset. Teknik ini membantu membedakan genre yang lebih umum dari yang jarang muncul, sehingga film dengan genre khas tidak tenggelam dalam dominasi kategori populer.\
   Setelah proses TF-IDF dilakukan, terbentuk sebuah matriks dengan dimensi (jumlah film × jumlah genre unik), di mana setiap baris mewakili satu film dan setiap kolom menunjukkan skor TF-IDF untuk masing-masing genre. Matriks ini berfungsi sebagai dasar untuk menghitung kemiripan antar film berdasarkan genre yang mereka miliki. Dengan memanfaatkan matriks ini, sistem dapat mendeteksi kesamaan antar film secara lebih objektif, memastikan bahwa rekomendasi yang diberikan tidak hanya didasarkan pada popularitas tetapi juga karakteristik spesifik film tersebut.

## Modelling
Dalam proyek ini, dikembangkan 2 model sistem rekomendasi yakni 

1. Content-Based Filtering\
   a. Cosine Similarity\
   Model rekomendasi ini bekerja dengan cara mengidentifikasi kesamaan genre antara film yang sudah disukai pengguna dan film lainnya dalam dataset. Untuk menentukan tingkat kesamaan tersebut, digunakan metode **Cosine Similarity**, yaitu teknik matematika yang membandingkan dua vektor berdasarkan sudut yang terbentuk di antara keduanya. Setiap film dikonversi menjadi **vektor fitur**, yang dalam hal ini berasal dari **TF-IDF genre**, agar model dapat melakukan perbandingan secara kuantitatif.

   Rumus cosine similarity:
   $$\cos(\theta) = \frac{A \cdot B}{||A|| \times ||B||}$$

   di mana:
   - A · B adalah dot product dari vektor A dan B
   - A dan B adalah panjang (magnitude) masing-masing vektor A dan B
     
   Cosine Similarity memiliki rentang nilai antara **-1 hingga 1**, yang menggambarkan seberapa dekat hubungan antar film:
   - **Nilai 1** menunjukkan bahwa genre dari dua film memiliki pola yang sangat mirip
   - **Nilai 0** mengindikasikan bahwa kedua film memiliki sedikit atau bahkan tidak ada kesamaan genre
   - **Nilai -1** berarti kedua film memiliki genre yang sangat berbeda
   
   Secara teknis, metode ini menghitung kesamaan dengan membandingkan arah vektor, bukan besarnya nilai numeriknya, sehingga cocok untuk analisis data yang memiliki **kepadatan rendah** (sparse matrix), seperti representasi genre dalam CBF. Teknik ini juga memungkinkan sistem untuk menangkap hubungan antar film secara lebih fleksibel, bahkan jika film memiliki jumlah genre berbeda. Dengan menggunakan pendekatan ini, rekomendasi yang diberikan menjadi lebih kontekstual dan mempertimbangkan pola genre yang benar-benar relevan bagi pengguna berdasarkan preferensi mereka sebelumnya.\

   b. Membuat fungsi khusus rekomendasi\
   Tahap ini adalah membangun fungsi khusus yang dapat mengidentifikasi film dengan tingkat kesamaan tertinggi berdasarkan input yang diberikan. Fungsi ini bekerja dengan mencari hubungan kemiripan antara film yang diinginkan dan seluruh film lain dalam dataset, lalu memilih kandidat rekomendasi yang memiliki pola genre paling mendekati.\
   Setelah proses perhitungan selesai, hasilnya disimpan dalam variabel closest, yang berisi daftar film dengan nilai kesamaan tertinggi. Untuk mengontrol jumlah film yang disarankan, digunakan parameter K, yang menentukan batasan jumlah rekomendasi yang akan diberikan. Agar hasil lebih akurat dan tidak mengulang informasi yang sudah diketahui, film yang menjadi titik referensi awal akan dihapus dari daftar rekomendasi. Sebagai langkah akhir, sistem akan mengembalikan rekomendasi dalam bentuk tabel, sehingga setiap film yang dipilih dapat ditampilkan secara jelas berdasarkan tingkat kesamaannya dengan film yang dicari.
   ![alt text](https://github.com/dysthymicfact/movielens-recommendation/blob/main/images/fungsi%20rekomendasi.png?raw=true)

   Berikut adalah hasil pencarian film dengan judul yang sama beserta informasi genrenya. Setelah itu, sistem melanjutkan dengan memberikan 5 rekomendasi teratas berdasarkan genre dari film "Steal Big, Steal Little". Proses rekomendasi telah berhasil, dan hasilnya menunjukkan bahwa film yang disarankan memiliki kemiripan genre, terutama dalam kategori Comedy.\

   ![alt text](https://github.com/dysthymicfact/movielens-recommendation/blob/main/images/top%205%20rekomendasi.png?raw=true)

Kelebihan Content-Based Filtering
- Sistem dapat merekomendasikan film berdasarkan preferensi spesifik pengguna
- Rekomendasi dibuat hanya berdasarkan karakteristik item yang sudah diberi nilai tanpa harus mengandalkan perilaku pengguna lain
- Jika pengguna memiliki kecenderungan menyukai suatu genre atau karakteristik tertentu, sistem akan terus menyarankan item dengan kesamaan tersebut
- Jika ada film baru yang belum mendapat rating, sistem tetap bisa merekomendasikannya berdasarkan deskripsi atau metadata seperti genre

Kekurangan Content-Based Filtering
- Jika pengguna belum pernah memberikan rating atau interaksi, sistem tidak memiliki informasi awal untuk membuat rekomendasi relevan
- Cenderung hanya menyarankan film yang serupa dengan yang sudah ditonton sehingga pengguna mungkin tidak menemukan sesuatu yang baru di luar preferensi biasa
- Jika dua film mirip dalam genre tetapi berbeda dalam aspek lain, sistem mungkin tetap merekomendasikannya tanpa mempertimbangkan konteks yang lebih luas
- Content-Based Filtering tidak menggunakan informasi dari pengguna lain, sehingga kurang efektif dalam menangkap tren atau rekomendasi yang berbasis komunitas

2. Collaborative Filtering\
   a. Data Preparation\
   Pada tahap ini, dilakukan encoding terhadap fitur `userId` dan `movieId` untuk mengonversi setiap nilai unik menjadi indeks numerik. Transformasi ini bertujuan untuk mempermudah pemrosesan data oleh model, terutama dalam pembelajaran hubungan antara pengguna dan film dalam ruang laten. Selain itu, rating pengguna terhadap film dinormalisasi ke dalam skala 0-1, memastikan bahwa nilai rating berada dalam kisaran yang lebih stabil, sehingga memudahkan model dalam memahami preferensi relatif antar pengguna.\

   b. Split Data Training & Validation\
   Dataset dibagi dengan rasio 80/20, yaitu 80% untuk pelatihan dan 20% untuk validasi. Pembagian ini dilakukan secara acak untuk menghindari bias dalam urutan data. Data input terdiri dari pasangan pengguna dan film yang telah diencoding, sementara output target adalah rating yang sudah dinormalisasi. Langkah ini memastikan bahwa model memiliki cukup data untuk belajar pola rekomendasi sekaligus mengevaluasi performanya pada data yang belum pernah dilihat sebelumnya.\

   c. Proses Training\
   Model rekomendasi dikembangkan menggunakan pendekatan _Neural Collaborative Filtering (NCF)_ yang menerapkan teknik embedding untuk merepresentasikan pengguna dan film dalam ruang laten. Embedding ini memungkinkan sistem untuk memahami interaksi tersembunyi antara pengguna dan film sehingga meningkatkan kualitas prediksi rekomendasi.\
   Dalam proses **kompilasi model**, beberapa teknik optimasi diterapkan:
   - **BinaryCrossentropy** sebagai loss function untuk mengukur kesalahan prediksi dibandingkan dengan nilai aktual
   - **Adam optimizer** dengan **learning rate 0.0001**, yang memungkinkan pembelajaran lebih stabil dan bertahap tanpa perubahan drastis dalam bobot model
   - **Root Mean Squared Error (RMSE)** sebagai metrik evaluasi, yang digunakan untuk menilai seberapa akurat prediksi yang dihasilkan oleh model

Proses pelatihan dilakukan selama 25 epochs dengan mekanisme Early Stopping (patience=5) sehingga training otomatis dihentikan jika tidak ada peningkatan signifikan dalam validasi RMSE selama beberapa iterasi. Batch size ditingkatkan dari 8 ke 16, membantu stabilitas pembelajaran dengan pemrosesan lebih banyak sampel dalam satu iterasi.\ 

   d. Visualisasi Evaluasi Model\
   Berdasarkan hasil visualisasi evaluasi model:
- **Training RMSE terus menurun**, mencapai nilai akhir sekitar **0.1813**, menunjukkan bahwa model dapat menangkap pola dengan baik pada data latih
- **Validation RMSE cenderung stabil di sekitar 0.19**, menandakan bahwa model berhasil menjaga keseimbangan antara akurasi dan generalisasi

  e. Mendapatkan Rekomendasi\
  Selanjutnya digunakan fungsi model.predict() untuk sistem memberikan rekomendasi film
  ![alt text](https://github.com/dysthymicfact/movielens-recommendation/blob/main/images/eval%20model%203.png?raw=true)

Kelebihan Collaborative FIltering
- Model mampu memberikan rekomendasi berdasarkan pola interaksi pengguna lain dengan preferensi serupa. Jika ada pengguna dengan preferensi unik, model tetap dapat menangkap pola rekomendasinya berdasarkan embedding representation

Kekurangan Collaborative FIltering
- Memerlukan jumlah data interaksi yang cukup besar agar rekoemndasi tidak bias atau terbatas hanya pada pengguna dengan banyak rating

## Evaluasi
Dalam proyek ini, performa model dievaluasi menggunakan **Root Mean Squared Error (RMSE)** sebagai metrik utama, yang berfungsi untuk mengukur seberapa jauh prediksi rating dari model dibandingkan dengan rating sebenarnya yang diberikan oleh pengguna. RMSE dihitung dengan mencari rata-rata akar kuadrat dari selisih kuadrat antara nilai aktual dan prediksi, menggunakan rumus berikut:  

$$ RMSE = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2} $$

di mana $$\( y_i \)$$ adalah rating yang diberikan pengguna, $$\( \hat{y}_i \)$$ adalah rating yang diprediksi model, dan \( n \) adalah jumlah sampel  
 
Cara kerja RMSE dapat diuraikan dalam beberapa tahap:  
1️. **Menghitung selisih antara nilai aktual dan prediksi:** Model menghasilkan prediksi rating untuk pengguna, lalu perbedaan antara rating yang sebenarnya dan prediksi tersebut dikalkulasi\
2️. **Menghitung kuadrat dari selisih tersebut:** Agar tidak ada kesalahan yang diabaikan—baik terlalu kecil atau terlalu besar—perbedaan nilai dikuadratkan untuk memberikan penalti lebih besar pada kesalahan signifikan\
3️. **Merata-rata kesalahan kuadrat:** Seluruh kesalahan dikalkulasi dalam rata-rata Mean Squared Error (MSE), yang memberikan gambaran umum tentang seberapa baik atau buruk model melakukan prediksi\
4️. **Mengambil akar kuadrat dari MSE:** RMSE mengambil akar kuadrat dari nilai ini agar hasil kembali ke skala yang sama dengan rating pengguna, menjadikannya lebih intuitif untuk interpretasi dalam sistem rekomendasi  

Karena penalti pada kesalahan besar lebih tinggi dalam RMSE dibandingkan dengan metrik lain seperti Mean Absolute Error (MAE), metrik ini sangat berguna dalam sistem rekomendasi, di mana prediksi yang tidak akurat bisa sangat memengaruhi pengalaman pengguna.  

### Hasil Evaluasi Model  
Eksperimen menunjukkan bahwa **Training RMSE** mengalami penurunan yang stabil, mencapai 0.17, menunjukkan bahwa model telah belajar pola dari data dengan baik. **Validation RMSE** tetap berada di kisaran 0.19, menunjukkan model mampu menjaga keseimbangan antara akurasi prediksi dan generalisasi terhadap data baru. Stabilitas ini dicapai melalui **optimasi learning rate (0.0001)** yang menghindari perubahan parameter yang terlalu agresif, serta peningkatan batch size (dari 8 ke 16) yang membantu pembaruan bobot lebih konsisten.  

### **Tantangan dan Pengembangan Model ke Depan**  
Meskipun performa cukup baik, tantangan utama yang masih perlu diperhatikan adalah **Cold Start Problem**, di mana pengguna baru atau item baru memiliki sedikit data interaksi, sehingga sulit mendapatkan rekomendasi yang akurat. Selain itu, model masih bergantung pada **data historis**, sehingga bias dapat terjadi jika pola interaksi dalam dataset tidak cukup beragam. Untuk mengatasi hal ini, pendekatan **Hybrid Filtering**, yang menggabungkan **Collaborative Filtering dan Content-Based Filtering**, dapat digunakan untuk meningkatkan akurasi dalam skenario pengguna dengan informasi terbatas.  

Ke depan, ada beberapa strategi untuk lebih meningkatkan model:  
- Eksplorasi arsitektur **Graph Neural Networks (GNN)**, untuk memahami hubungan antar pengguna dan film secara lebih kontekstual
- Menggunakan pretrained embeddings dari model BERT, sehingga representasi fitur menjadi lebih kaya dan meningkatkan kualitas rekomendasi  

## Kesimpulan
Dalam proyek ini, saya telah mengembangkan sistem rekomendasi film dengan pendekatan **Collaborative Filtering** dan **Content-Based Filtering**, masing-masing dengan karakteristik dan keunggulan yang berbeda. **Collaborative Filtering** memanfaatkan pola interaksi pengguna untuk memberikan rekomendasi berdasarkan kesamaan preferensi antar individu, sehingga dapat menghasilkan rekomendasi yang lebih personal. Di sisi lain, **Content-Based Filtering** lebih berfokus pada karakteristik film itu sendiri, seperti genre atau deskripsi, sehingga mampu memberikan rekomendasi yang relevan dengan film yang sebelumnya disukai pengguna.  

Meskipun model menunjukkan hasil yang cukup baik, ada keterbatasan yang perlu diperhatikan, terutama dalam cakupan dataset yang digunakan. Jumlah film yang tersedia dalam dataset relatif terbatas, yang dapat mempengaruhi variasi rekomendasi yang diberikan. Dalam skenario dunia nyata, model mungkin kurang optimal dalam menangani pengguna yang lebih tertarik pada film-film terbaru karena sistem rekomendasi berbasis historis cenderung menyarankan film yang lebih lama dengan lebih banyak riwayat interaksi. Untuk meningkatkan relevansi rekomendasi, **Hybrid Filtering** dapat menjadi solusi dengan menggabungkan kedua pendekatan guna mengakomodasi preferensi pengguna secara lebih fleksibel dan adaptif terhadap tren film terkini.  





