# Laporan Proyek Machine Learning - Edi Widodo

# 1. Domain Proyek
<p align="justify"> 
Pemilihan jalur karir merupakan salah satu keputusan penting yang dihadapi mahasiswa, terutama di era modern di mana persaingan kerja semakin ketat dan kebutuhan pasar terus berkembang. Menentukan karir yang sesuai dengan minat, kemampuan, dan pendidikan dapat menjadi tantangan besar, terutama ketika mahasiswa tidak memiliki panduan yang cukup untuk memahami pilihan yang tersedia [1]. Sistem rekomendasi karir hadir sebagai solusi inovatif untuk membantu mahasiswa dalam pengambilan keputusan ini[2]. Dengan memanfaatkan data seperti nilai akademik, minat, dan atribut personal lainnya, sistem ini dapat memberikan rekomendasi yang personal dan relevan, sehingga membantu mahasiswa memahami potensi karir yang sesuai dengan profil mereka[3].
Berbagai penelitian telah menunjukkan manfaat sistem rekomendasi dalam domain pendidikan dan karir [4]. Teknik rekomendasi seperti Content-based Filtering dan Collaborative Filtering telah terbukti efektif dalam memberikan rekomendasi yang relevan dan meningkatkan pengalaman pengguna. Dalam konteks pendidikan, sistem rekomendasi dapat mengarahkan mahasiswa ke jalur karir yang sesuai berdasarkan pola preferensi dan atribut individu. Penelitian juga menunjukkan bahwa analisis data pendidikan dapat digunakan untuk memprediksi performa dan preferensi mahasiswa, yang kemudian dapat diintegrasikan ke dalam sistem rekomendasi.
Melalui penerapan sistem rekomendasi karir, mahasiswa dapat mengakses daftar profesi yang sesuai dengan jurusan, nilai, dan preferensi mereka. Hal ini tidak hanya meningkatkan akurasi dalam pengambilan keputusan, tetapi juga memberikan panduan praktis yang membantu mereka menavigasi dunia kerja yang dinamis dan kompetitif.

# 2. Business Understanding
<p align="justify">Mahasiswa sering menghadapi tantangan dalam menentukan jalur karir yang sesuai dengan kemampuan, minat, dan latar belakang pendidikan mereka. Ketidaktahuan terhadap pilihan karir yang tersedia serta ketidakcocokan antara jurusan yang dipilih dan preferensi karir dapat mengakibatkan pengambilan keputusan yang tidak optimal. Hal ini berdampak pada kesenjangan antara kompetensi mahasiswa dan kebutuhan pasar kerja, sehingga mengurangi peluang kesuksesan mereka di dunia profesional. Untuk mengatasi masalah ini, diperlukan sistem rekomendasi berbasis data yang dapat membantu mahasiswa memahami potensi karir berdasarkan interaksi historis dan preferensi serupa dari mahasiswa lainnya. Pendekatan Collaborative Filtering digunakan untuk memberikan rekomendasi personal dengan menganalisis pola interaksi antara mahasiswa (user) dan departemen pendidikan (item). Sistem ini memanfaatkan data seperti preferensi karir, jurusan yang diambil, dan minat individu (hobi) untuk memprediksi profesi yang relevan.</p>

Dengan memanfaatkan Collaborative Filtering, sistem ini dapat:
1. Memberikan Rekomendasi Personal:
   - Berdasarkan pola interaksi mahasiswa dengan departemen tertentu dan profesi terkait.
2. Mengatasi Masalah Cold Start:
   - Sistem dapat memberikan rekomendasi meskipun data historis interaksi pengguna terbatas, dengan mempertimbangkan profil dasar seperti gender dan hobi.
3. Mendukung Pengambilan Keputusan yang Tepat:
   - Mahasiswa dapat memahami pilihan karir yang sesuai dengan latar belakang pendidikan dan preferensi mereka.
4. Meningkatkan Keterhubungan dengan Kebutuhan Pasar Kerja:
   - Membantu institusi pendidikan menyelaraskan program pendidikan dengan kebutuhan dunia profesional.
<p align="justify"> 
Pendekatan berbasis Collaborative Filtering ini memberikan solusi berbasis data yang tidak hanya memudahkan mahasiswa dalam menentukan jalur karir, tetapi juga mendukung institusi pendidikan untuk meningkatkan relevansi program akademik mereka di era pasar kerja yang dinamis.</p>

## 2.1 Problem Statements
- Mahasiswa seringkali menghadapi kesulitan dalam menentukan profesi yang sesuai dengan jurusan dan preferensi mereka. Salah satu tantangan utama adalah bagaimana membuat sistem rekomendasi yang dapat mencocokkan mahasiswa dengan profesi yang tepat, mengingat berbagai faktor seperti minat pribadi dan tren pasar kerja.

## 2.2 Goals
- Untuk mengatasi permasalahan tersebut, perlu dikembangkan sistem rekomendasi karir berbasis data yang dapat memberikan rekomendasi yang relevan dan terpersonalisasi bagi mahasiswa. Sistem ini akan menggunakan teknik Collaborative Filtering untuk menganalisis pola preferensi mahasiswa lainnya, sehingga dapat menghasilkan daftar profesi yang lebih akurat. Output dari sistem ini adalah daftar top-N profesi yang dapat membantu mahasiswa dalam memilih jalur karir yang sesuai dengan jurusan dan minat mereka.
  
# 3. Data Understanding
- Mengambil dataset dari kaggle, di lokasi [Student Attitude and Behavior](https://www.kaggle.com/datasets/susanta21/student-attitude-and-behavior) https://www.kaggle.com/datasets/susanta21/student-attitude-and-behavior
- Jumlah Data: 235 entri.
- Jumlah Kolom : 19 kolom.
- Usability Level : 10.0 (berdasarkan rating kaggle)
- Kondisi Data: Dataset lengkap dengan informasi personal, akademik, dan preferensi mahasiswa.
- Dataset ini beberapa labelnya harus ditambahkan atau dimodifikasi untuk menyesuaikan kebutuhan Indonesia, seperti data Departemen dan Profesi dalam departement yang ada di Indonesia.
- Untuk variabel nilai, dataset ini menggunakan nilai kelas 10, dianggap disesuaikan dengan Indonesia adalah nilai kelas 9.
- Nilai pada jenjang perkuliahan, menggunakan skala 1-100. Artinya, input IPK yang diakui di Indonesia dengan skala 1-4, harus disesuaikan secara manual

## 3.1 Fitur atau Variable pada dataset 
  1. Certification Course
     - Tipe Data: Kategorikal (Ya/No)
     - Deskripsi: Menunjukkan apakah individu mengikuti kursus sertifikasi tambahan selain kuliah.
  2. Gender
     - Tipe Data: Kategorikal (Male/Female)
     - Deskripsi: Menunjukkan jenis kelamin individu.
  3. Department
     - Tipe Data: Kategorikal (contoh: BCA)
     - Deskripsi: Menunjukkan jurusan atau program studi mahasiswa, data ini akan disesuaikan dengan jurusan di Indonesia
  4. Height (CM)
     - Tipe Data: Numerik (integer)
     - Deskripsi: Tinggi badan individu dalam sentimeter.
  5. Weight (KG)
     - Tipe Data: Numerik (integer)
     - Deskripsi: Berat badan individu dalam kilogram.
  6. 10th Mark
     - Tipe Data: Numerik (persentase)
     - Deskripsi: Nilai akademik individu saat kelas 10 dalam persentase.
  7. 12th Mark
     - Tipe Data: Numerik (persentase)
     - Deskripsi: Nilai akademik individu saat kelas 12 dalam persentase.
  8. College Mark
     - Tipe Data: Numerik (persentase)
     - Deskripsi: Nilai akademik individu di perguruan tinggi dalam persentase.
  9. Hobbies
     - Tipe Data: Kategorikal (contoh: Video Games, Cinema)
     - Deskripsi: Menunjukkan hobi individu.
  10. Daily Studying Time
      - Tipe Data: Kategorikal (contoh: 0 - 30 minute, 30 - 60 minute)
      - Deskripsi: Durasi belajar harian individu.
  11. Prefer to Study In
      - Tipe Data: Kategorikal (contoh: Morning)
      - Deskripsi: Waktu yang disukai individu untuk belajar (pagi, siang, malam).
  12. Salary Expectation
      - Tipe Data: Numerik (contoh: 40000)
      - Deskripsi: Ekspektasi gaji individu setelah lulus.
  13. Do You Like Your Degree?
      - Tipe Data: Kategorikal (Ya/No)
      - Deskripsi: Menunjukkan apakah individu menyukai program studi mereka.
  14. Willingness to Pursue a Career Based on Their Degree
      - Tipe Data: Numerik (persentase)
      - Deskripsi: Persentase minat individu untuk bekerja sesuai jurusannya.
  15. Social Media & Video
      - Tipe Data: Kategorikal (contoh: 1.30 - 2 hour)
      - Deskripsi: Waktu yang dihabiskan individu untuk media sosial dan menonton video setiap hari.
  16. Travelling Time
      - Tipe Data: Kategorikal (contoh: 30 - 60 minutes)
      - Deskripsi: Waktu perjalanan harian individu.
  17. Stress Level
      - Tipe Data: Kategorikal (contoh: Bad)
      - Deskripsi: Tingkat stres individu (baik, sedang, buruk).
  18. Financial Status
      - Tipe Data: Kategorikal (contoh: Bad)
      - Deskripsi: Kondisi keuangan individu.
  19. Part-Time Job
      - Tipe Data: Kategorikal (Ya/No)
      - Deskripsi: Menunjukkan apakah individu memiliki pekerjaan paruh waktu.
     
## 3.2 Outlier Data
- Fitur yang diseleksi dan potensi outlier :
  -  10th Mark, Numerik, Potensi memiliki outlier.
  -  12th Mark, Numerik, Potensi memiliki outlier.
  -  college mark, Numerik, Potensi memiliki outlier.
  -  willingness, Numerik, Potensi memiliki outlier.
  -  Untuk fitur kategorikal, hanya perlu memvalidasi data untuk memastikan tidak ada nilai yang salah ketik atau tidak relevan.
- Hasil deteksi outlier pada fitur numerik 10th Mark, 12th Mark, dan college mark adalah sebagai berikut:
  - 10th Mark:
    - Batas bawah (Lower Bound): 45.625
    - Batas atas (Upper Bound): 110.625
    - Jumlah Outlier: 4
    - Outliers: [40.0, 7.4, 45.0, 45.0]
  - 12th Mark:
    - Batas bawah (Lower Bound): 36.0
    - Batas atas (Upper Bound): 100.0
    - Jumlah Outlier: 0
    - Outliers: Tidak ada.
  - college mark:
    - Batas bawah (Lower Bound): 30.0
    - Batas atas (Upper Bound): 110.0
    - Jumlah Outlier: 5
    - Outliers: [3.0, 1.0, 7.5, 12.0, 2.0]
  - willingness
    - Batas bawah : 0.7
    - Batas atas : 1.0
    - Outliers: Tidak ada.


# 4. Data Preparation
## 4.1 Data Cleansing
   a. Handling Missing Value.
   -  Mengisi atau menghapus data yang hilang agar tidak menyebabkan error atau bias.
      ```ruby
      data.fillna('', inplace=True)
      ```
   b. Handling Duplicate
   - Menghapus data duplikat untuk menghindari bias
     ```ruby
     duplicates = data.duplicated()
     if duplicates.sum() > 0:
         print(f"Jumlah baris duplikat: {duplicates.sum()}")
         data = data.drop_duplicates()
         print("Duplikasi telah dihapus.")
     ```
   c. Handling Outlier
   - Mendeteksi outlier dari numerikal selected feature, dan jika ada outlier akan direplace dengan nilai Median
     ```ruby        
     numeric_features = [feature for feature in selected_features if data[feature].dtype in ['int64', 'float64']]
     # Handling outliers by replacing them with the median using IQR         
     for column in numeric_features:
         Q1 = data[column].quantile(0.25)
         Q3 = data[column].quantile(0.75)
         IQR = Q3 - Q1
         lower_bound = Q1 - 1.5 * IQR
         upper_bound = Q3 + 1.5 * IQR
     # Calculate median
     median = data[column].median()
     # Replace outliers with the median
     data[column] = data[column].apply(lambda x: median if x < lower_bound or x > upper_bound else x)
     # Display the processed numeric features after outlier handling
     data[numeric_features].describe()
     ```
## 4.2 Data Transformation
1. Mengubah data bernilai % (persen) menjadi angka
   ```ruby
   data['willingness'] = (
       data['willingness to pursue a career based on their degree  ']
       .str.rstrip('%')
       .fillna('0')
       .astype(float)
       / 100
   )
   ```
2. Encoding Categorical Data
   - Menyelaraskan skala data numerik agar algoritma dapat bekerja dengan optimal.
    ```ruby
    label_encoder = LabelEncoder()
    data['Gender'] = label_encoder.fit_transform(data['Gender'])
    data['selected_department'] = label_encoder.fit_transform(data['Department'])
    data['Hobbies'] = label_encoder.fit_transform(data['hobbies'])
    ```
3. Normalisasi
   - Normalisasi nilai numerik menggunakan Min-Max Scaling.
   ```ruby
   scaler = MinMaxScaler()
   data[['10th Mark', '12th Mark', 'college mark','willingness']] = scaler.fit_transform(
        data[['10th Mark', '12th Mark', 'college mark','willingness']]
   )
   ```
## 4.3 Feature Selection
  - Dalam Collaborative Filtering, biasanya hanya fitur user_id, item_id, dan rating yang digunakan.
  - Seleksi fitur dapat digunakan untuk menentukan apakah atribut tambahan (Gender, Hobbies, Nilai) relevan untuk dimasukkan.
  - Mencari korelasi antar fitur untuk menetukan fitur terpilih
  ```ruby
  # Memilih Fitur
  selected_features = ['10th Mark', '12th Mark', 'college mark', 'Gender', 'hobbies', 'Department','willingness']
  # Correlate additional features with willingness
  correlation_matrix = data[['willingness', 'Gender', 'Hobbies', '10th Mark', '12th Mark', 'college mark']].corr()
  # Display correlation matrix
  plt.figure(figsize=(10, 6))
  sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', fmt=".2f", linewidths=0.5)
  plt.title("Correlation Matrix of Features")
  plt.show()
  ```

# 5. Modelling and Result
## 5.1 Hybrid Filtering:
   - Collaborative Filtering (CF) adalah pendekatan yang memanfaatkan pola interaksi pengguna terhadap item (misalnya, rating, preferensi, atau perilaku eksplisit/implisit lainnya).
   - Menggunakan algoritma Singular Value Decomposition (SVD) untuk menemukan pola preferensi berbasis data mahasiswa lain, dari pustaka surprise.
   - SVD membantu mendekomposisi matriks user-item (yang merepresentasikan interaksi atau preferensi) menjadi beberapa latent factor (faktor tersembunyi)
   - Melalui proses ini, sistem dapat memprediksi rating atau tingkat kesukaan pengguna terhadap item tertentu.
   - Model dilatih dengan data preferensi mahasiswa terhadap jurusan.
   - Collaborative Filtering memberikan rekomendasi berbasis pola mahasiswa lain.
   - Karena dataset tidak terdapat item_id, maka item_id berasal dari kolom Department dalam dataset, yang mewakili item unik (departemen atau posisi pekerjaan). Kolom ini telah diolah menggunakan metode factorize() untuk menghasilkan representasi numerik.

### Kelemahan dari CF :
- Masalah cold start muncul ketika ada pengguna baru yang belum memiliki riwayat interaksi apa pun, atau ketika ada item baru yang belum memiliki rating atau ulasan dari pengguna.
- Tanpa data interaksi, pendekatan CF murni tidak mampu memberikan rekomendasi yang relevan, karena CF sangat bergantung pada data historis (rating, klik, dll.).

### Mengatasi Masalah Cold Start dengan Content Based Filtering :
- Tanpa data interaksi, pendekatan CF murni tidak mampu memberikan rekomendasi yang relevan, karena CF sangat bergantung pada data historis (rating, klik, dll.).
- Pada kasus dataset ini, digunakan pendekatan Content Based filtering (CB). dengan cara menganalisis kesamaan antar fitur pengguna, misalnya 10th Mark, 12th Mark, college mark, Gender, Hobbies, dll.
- Dengan cosine similarity, sistem dapat mencari pengguna lain yang memiliki profil fitur mirip, lalu menggunakan preferensi (riwayat) pengguna yang mirip tersebut untuk memprediksi minat pengguna baru.
   - Contohnya, jika ada pengguna baru dengan hobbies dan gender tertentu, maka sistem dapat mencari pengguna lama dengan hobi dan gender serupa, melihat jurusan/bidang apa yang pengguna lama sukai, lalu merekomendasikannya kepada pengguna baru.

### Kelemahan CB :
- CB cenderung hanya melihat sisi kesamaan fitur dan kurang bisa menangkap pola preferensi kolektif dari banyak pengguna.
- Selain itu, jika fitur konten tidak cukup kaya atau tidak direpresentasikan dengan baik, akurasi prediksi rekomendasi akan menurun.

### Kolaborasi CB dan CF (Hybrid) :
- Dengan menggabungkan collaborative filtering (untuk memanfaatkan pola kesamaan perilaku antar pengguna) dan content-based filtering (untuk memanfaatkan kesamaan fitur pengguna dalam mengatasi cold start), sistem rekomendasi menjadi lebih tangguh.
- CF dapat memberikan rekomendasi yang sangat relevan ketika data riwayat cukup (banyak interaksi).
- CB dapat menolong di awal ketika data riwayat pengguna baru masih minim (cold start), sehingga sistem tetap bisa memberikan rekomendasi walaupun data interaksi sedikit atau bahkan belum ada.
- Collaborative Filtering SVD akan “belajar” dari preferensi (rating, klik, willingness, dsb.) di antara pengguna yang sudah ada, menghasilkan rekomendasi yang lebih personal dan berbasis pola perilaku.
- Content-Based Filtering akan mengisi kekosongan ketika data riwayat belum memadai, yaitu dengan membandingkan kesamaan atribut pengguna (misalnya nilai ujian, gender, hobbies) untuk menebak minat jurusan/bidang yang kemungkinan disukai. 

### Solusi yang diusulkan :
- Saat pengguna sudah memiliki data interaksi yang cukup, sistem CF berbasis SVD akan mendominasi untuk menghasilkan rekomendasi yang lebih akurat.
- Namun saat pengguna baru masuk atau memiliki sedikit interaksi, sistem CB (melalui cosine similarity berbasis fitur) akan lebih berperan sampai data interaksi pengguna tersebut memadai untuk diolah oleh CF.

## 5.2 Hybrid Filtering Preparation
   - Mempersiapkan dataset agar kompatibel dengan pustaka Surprise, yang digunakan untuk membangun model Collaborative Filtering.
     ```ruby
     data_surprise = Dataset.load_from_df(data[['user_id', 'item_id', 'willingness']], Reader(rating_scale=(0, 1)))
     ```
   - Split Data: Membagi data untuk pelatihan dan pengujian model.
     ```ruby
     trainset, testset = train_test_split(data_surprise, test_size=0.2, random_state=42)
     ```
   - Train Model: Melatih model Collaborative Filtering dengan algoritma SVD. Singular Value Decomposition (SVD) adalah algoritma yang digunakan untuk Collaborative Filtering berbasis matriks dekomposisi.
     ```ruby
     model = SVD()
     model.fit(trainset)
     ```
   - Predict and Recommend: Menghasilkan prediksi dan memberikan rekomendasi berdasarkan skor relevansi.
     ```ruby
     predictions = model.test(testset)
     ```
   - Tampilkan Top N
     ```ruby
     recommended_professions[:top_n]
     ```
     
## 5.3 Evaluation
### Evaluasi Collaborative Filtering:
  - RMSE (Root Mean Squared Error): Mengukur kesalahan prediksi rata-rata pada rating.
  - MAE (Mean Absolute Error): Mengukur kesalahan prediksi absolut rata-rata pada rating.

### Hasil pengujian terhadap model Collaborative Filtering adalah sebagai berikut :
Di kode, metrik RMSE dan MAE diimplementasikan menggunakan pustaka Surprise:
1. Melatih Model:
   - Model SVD yang telah dilatih menggunakan trainset diuji pada testset.
   - Menghasilkan daftar prediksi yang mencakup nilai aktual dan prediksi.
   ```ruby
   data['user_id'] = range(len(data))
   data['item_id'] = data['Department'].factorize()[0]
   data_surprise = Dataset.load_from_df(data[['user_id', 'item_id', 'willingness']], Reader(rating_scale=(0, 1)))
   trainset, testset = train_test_split(data_surprise, test_size=0.2, random_state=42)
   model = SVD()
   model.test(testset)
   accuracy.rmse(predictions, verbose=True):
   ```
2. Menghitung Root Mean Squared Error (RMSE).
   - verbose=True menampilkan hasil RMSE di konsol secara langsung.
   ```ruby
   accuracy.mae(predictions, verbose=True):
   ```
3. Menghitung Mean Absolute Error (MAE).
   ```ruby
   mae = accuracy.mae(predictions, verbose=True)
   ```
4. Pengujian    
   ```ruby 
   Masukkan informasi berikut untuk merekomendasikan karier yang sesuai:
   Nilai Akhir Kelas 10 (dalam skala 0-100): 90
   Nilai Akhir Kelas 12 (dalam skala 0-100): 98
   Masukkan nilai GPA kuliah Anda (dalam skala 1-4): 4
   Jenis Kelamin Anda (Laki-laki[1]/Perempuan[0]): 1
    
   Daftar Hobi:
   1. Video Games
   2. Cinema
   3. Reading books
   4. Sports
    
   Masukkan nomor hobi yang ingin Anda pilih: 1
    
   Anda memilih hobi: Video Games
   Seberapa besar minat Anda terhadap pekerjaan berbasis hobi ini? (0-1): 1
    
   Collaborative Filtering Recommendations (Professions):
   1. Analis Sistem
   2. Manajer Proyek IT
   3. Administrator Sistem
   4. Pengembang ERP
   5. Spesialis Data Warehouse
   ```
### Keterangan Hasil uji Collaborative Filtering
1. Hasil Evaluasi:
   - RMSE (Root Mean Squared Error): 0.2705
      - Mengukur rata-rata perbedaan kuadrat antara nilai prediksi dan nilai aktual.
      - Semakin kecil RMSE, semakin baik model.
   - MAE (Mean Absolute Error): 0.2030
      - Mengukur rata-rata perbedaan absolut antara nilai prediksi dan nilai aktual.
      - Semakin kecil MAE, semakin baik model.
2. Analisis:
   - Kinerja: Nilai RMSE dan MAE menunjukkan bahwa prediksi model cukup akurat, dengan kesalahan prediksi kecil.
   - Konteks: Hasil ini menunjukkan Collaborative Filtering bekerja dengan baik dalam memprediksi preferensi terhadap jurusan berbasis pola data pengguna lain.

# 6. Kesimpulan
## Collaborative Filtering:
   - Model ini menunjukkan hasil terbaik dalam hal kesalahan prediksi (RMSE dan MAE rendah).
   - Cocok untuk memprediksi relevansi jurusan berbasis pola data pengguna lain.
   - Dataset yang digunakan pada pengujian ini, tidak cocok untuk penerapan CF secara sepenuhnya, dan juga tidak cocok sepenuhnya menggunakan CB filtering.
   - Solusi dari permasalahan ini digunakan metode Hybrid Filtering.
     
## Hybrid Filtering:
   - untuk mengatasi masalah cold start pada collaborative filtering, dicari kesamaan antar fitur pengguna seperti 10th Mark, 12th Mark, college mark, Gender, dan Hobbies dengan menggunakan cosine similarity untuk mengidentifikasi pengguna yang mirip, sehingga memungkinkan prediksi rekomendasi untuk pengguna baru berdasarkan preferensi pengguna yang serupa. 

# 7. Saran
## Collaborative Filtering:
   - Mencoba menggunakan algoritma yang lebih kompleks (misalnya, kNN atau Matrix Factorization lebih lanjut).

## Referensi

[1] F. Firmahsyah and T. Gantini, “Penerapan Metode Content-Based Filtering Pada Sistem Rekomendasi Kegiatan Ekstrakulikuler (Studi Kasus di Sekolah ABC)”, JuTISI, vol. 2, no. 3, Dec. 2016.

[2]	Habibi, Roni, and Muhammad Dzihan Albanna. "Analisis Sistem Rekomendasi Pada Job Recommendation Berdasarkan Profil Linkedin Menggunakan Cosine Similarity: ANALISIS SISTEM REKOMENDASI PADA JOB RECOMMENDATION BERDASARKAN PROFIL LINKEDIN MENGGUNAKAN COSINE SIMILARITY." Jurnal Teknik Informatika 14, no. 3 (2022): 118-122.

[3]	Crismastiana Koloman, Raihan Maulana, Raisya Dwi Zahra Putri, and Wahyu Abadi Harahap, “Sistem Rekomendasi Pekerjaan di bidang IT Menggunakan Algoritma Content-Based Filtering”, jcsr-politama, vol. 1, no. 6, pp. 78–88, Dec. 2023.

[4]	D. Astuti, A. Pinandito, dan R. K. Dewi, “Sistem Rekomendasi Lowongan Pekerjaan Untuk Fresh Graduate Menggunakan Metode Weighted Product Berbasis Android”, J-PTIIK, vol. 1, no. 12, hlm. 1518–1525, Jul 2017.
