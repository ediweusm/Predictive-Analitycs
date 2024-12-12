# Laporan Proyek Machine Learning - Edi Widodo

## Domain Proyek
<p align="justify"> 
Pemilihan jalur karir merupakan salah satu keputusan penting yang dihadapi mahasiswa, terutama di era modern di mana persaingan kerja semakin ketat dan kebutuhan pasar terus berkembang. Menentukan karir yang sesuai dengan minat, kemampuan, dan pendidikan dapat menjadi tantangan besar, terutama ketika mahasiswa tidak memiliki panduan yang cukup untuk memahami pilihan yang tersedia [1]. Sistem rekomendasi karir hadir sebagai solusi inovatif untuk membantu mahasiswa dalam pengambilan keputusan ini[2]. Dengan memanfaatkan data seperti nilai akademik, minat, dan atribut personal lainnya, sistem ini dapat memberikan rekomendasi yang personal dan relevan, sehingga membantu mahasiswa memahami potensi karir yang sesuai dengan profil mereka[3].
Berbagai penelitian telah menunjukkan manfaat sistem rekomendasi dalam domain pendidikan dan karir [4]. Teknik rekomendasi seperti Content-based Filtering dan Collaborative Filtering telah terbukti efektif dalam memberikan rekomendasi yang relevan dan meningkatkan pengalaman pengguna. Dalam konteks pendidikan, sistem rekomendasi dapat mengarahkan mahasiswa ke jalur karir yang sesuai berdasarkan pola preferensi dan atribut individu. Penelitian juga menunjukkan bahwa analisis data pendidikan dapat digunakan untuk memprediksi performa dan preferensi mahasiswa, yang kemudian dapat diintegrasikan ke dalam sistem rekomendasi.
Melalui penerapan sistem rekomendasi karir, mahasiswa dapat mengakses daftar profesi yang sesuai dengan jurusan, nilai, dan preferensi mereka. Hal ini tidak hanya meningkatkan akurasi dalam pengambilan keputusan, tetapi juga memberikan panduan praktis yang membantu mereka menavigasi dunia kerja yang dinamis dan kompetitif.

## Business Understanding
<p align="justify"> Mahasiswa sering menghadapi tantangan dalam menentukan jalur karir yang sesuai dengan kemampuan, minat, dan latar belakang pendidikan mereka. Ketidaktahuan terhadap pilihan yang tersedia serta ketidakcocokan antara jurusan dan preferensi karir dapat menyebabkan pengambilan keputusan yang tidak optimal. Masalah ini diperparah dengan kurangnya panduan berbasis data yang dapat membantu mahasiswa memahami potensi karir berdasarkan profil mereka. Oleh karena itu, diperlukan sistem yang mampu memberikan rekomendasi personal dan relevan untuk membantu mahasiswa memilih jalur karir yang sesuai.
Sistem rekomendasi karir menawarkan solusi dengan memanfaatkan teknik Content-based Filtering dan Collaborative Filtering. Sistem ini menganalisis atribut seperti nilai akademik, jenis kelamin, dan hobi mahasiswa untuk memberikan daftar profesi yang sesuai. Pendekatan ini tidak hanya memudahkan mahasiswa dalam menentukan pilihan karir, tetapi juga membantu institusi pendidikan dalam mendukung pengembangan kompetensi mahasiswa sesuai kebutuhan pasar kerja.</p> 

## Problem Statements
- Bagaimana sistem rekomendasi dapat membantu mencocokkan mahasiswa dengan profesi yang sesuai dengan jurusan dan preferensi mereka.
- Bagaimana teknik Content-based Filtering dan Hybrid Collaborative Filtering dapat diintegrasikan untuk menghasilkan rekomendasi karir yang personal dan akurat.

### Goals
- Mengembangkan sistem rekomendasi karir berbasis data yang mampu memberikan rekomendasi personal dan relevan bagi mahasiswa.
- Menerapkan teknik Content-based Filtering untuk mencocokkan profil individu dengan profesi yang relevan.
- Menggunakan Collaborative Filtering untuk meningkatkan akurasi rekomendasi dengan mempertimbangkan pola preferensi dari mahasiswa lainnya.
- Menyediakan output berupa daftar top-N profesi yang dapat membantu mahasiswa menentukan jalur karir yang sesuai.
  
## Data Understanding
- Mengambil dataset dari kaggle, di lokasi [Student Attitude and Behavior](https://www.kaggle.com/datasets/susanta21/student-attitude-and-behavior) https://www.kaggle.com/datasets/susanta21/student-attitude-and-behavior
- Jumlah Data: 235 entri.
- Jumlah Kolom : 19 kolom.
- Usability Level : 10.0 (berdasarkan rating kaggle)
- Kondisi Data: Dataset lengkap dengan informasi personal, akademik, dan preferensi mahasiswa.
- Dataset ini beberapa labelnya harus ditambahkan atau dimodifikasi untuk menyesuaikan kebutuhan Indonesia, seperti data Departemen dan Profesi dalam departement yang ada di Indonesia.
- Untuk variabel nilai, dataset ini menggunakan nilai kelas 10, dianggap disesuaikan dengan Indonesia adalah nilai kelas 9.
- Nilai pada jenjang perkuliahan, menggunakan skala 1-100. Artinya, input IPK yang diakui di Indonesia dengan skala 1-4, harus disesuaikan secara manual

### Fitur atau Variable pada dataset 
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
     
### Outlier Data
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
- Penanganan Outlier :
  -  Mendeteksi outlier dari numerikal selected feature, dan jika ada outlier akan direplace dengan nilai Median

## Data Preparation
### Teknik Data Preparation
1. Handling Missing Value.
   - Mengisi atau menghapus data yang hilang agar tidak menyebabkan error atau bias.
     ```ruby
     data.fillna('', inplace=True)
     ```
2. Handling Duplicate
   - Menghapus data duplikat untuk menghindari bias
     ```ruby
     duplicates = data.duplicated()
     if duplicates.sum() > 0:
         print(f"Jumlah baris duplikat: {duplicates.sum()}")
         data = data.drop_duplicates()
         print("Duplikasi telah dihapus.")
     ```
3. Normalization
   - Normalisasi nilai numerik menggunakan Min-Max Scaling.
     ```ruby
     scaler = MinMaxScaler()
     data[['10th Mark', '12th Mark', 'college mark','willingness']] = scaler.fit_transform(
          data[['10th Mark', '12th Mark', 'college mark','willingness']]
     )
     ```
4. Encoding Categorical Data
   - Menyelaraskan skala data numerik agar algoritma dapat bekerja dengan optimal.
    ```ruby
    label_encoder = LabelEncoder()
    data['Gender'] = label_encoder.fit_transform(data['Gender'])
    data['selected_department'] = label_encoder.fit_transform(data['Department'])
    data['Hobbies'] = label_encoder.fit_transform(data['hobbies'])
    ```     
## Feature Selection
  - Dalam Collaborative Filtering, biasanya hanya fitur user_id, item_id, dan rating yang digunakan.
  - Seleksi fitur dapat digunakan untuk menentukan apakah atribut tambahan (Gender, Hobbies, Nilai) relevan untuk dimasukkan.
  - Mencari korelasi antar fitur untuk menetukan fitur terpiliha
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

## Collaborative Filtering Preparation
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
     
## Modelling and Result
### Uji Coba Data
    
    Masukkan informasi berikut untuk merekomendasikan karier yang sesuai:
    Nilai Akhir Kelas 10 (dalam skala 0-100): 90
    Nilai Akhir Kelas 12 (dalam skala 0-100): 89
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
    
## Sistem Rekomendasi
### Collaborative Filtering:
   - Menggunakan algoritma Singular Value Decomposition (SVD) untuk menemukan pola preferensi berbasis data mahasiswa lain, dari pustaka surprise.
   - Model dilatih dengan data preferensi mahasiswa terhadap jurusan.
   - Collaborative Filtering memberikan rekomendasi berbasis pola mahasiswa lain.
   - Karena dataset tidak terdapat item_id, maka item_id berasal dari kolom Department dalam dataset, yang mewakili item unik (departemen atau posisi pekerjaan). Kolom ini telah diolah menggunakan metode factorize() untuk menghasilkan representasi numerik.
     ```ruby
     data['item_id'] = data['Department'].factorize()[0]
     ```
   - 5 Profesi Teratas
       1. Analis Sistem
       2. Manajer Proyek IT
       3. Administrator Sistem
       4. Pengembang ERP
       5. Spesialis Data Warehouse

# Evaluation
## Metrik Evaluasi yang Digunakan
### Evaluasi Collaborative Filtering:
  - RMSE (Root Mean Squared Error): Mengukur kesalahan prediksi rata-rata pada rating.
  - MAE (Mean Absolute Error): Mengukur kesalahan prediksi absolut rata-rata pada rating.

## Hasil pengujian terhadap model adalah sebagai berikut :
### Collaborative Filtering
1. Hasil Evaluasi:
   - RMSE (Root Mean Squared Error): 0.226
      - Mengukur rata-rata perbedaan kuadrat antara nilai prediksi dan nilai aktual.
      - Semakin kecil RMSE, semakin baik model.
   - MAE (Mean Absolute Error): 0.172
      - Mengukur rata-rata perbedaan absolut antara nilai prediksi dan nilai aktual.
      - Semakin kecil MAE, semakin baik model.
2. Analisis:
   - Kinerja: Nilai RMSE dan MAE menunjukkan bahwa prediksi model cukup akurat, dengan kesalahan prediksi kecil.
   - Konteks: Hasil ini menunjukkan Collaborative Filtering bekerja dengan baik dalam memprediksi preferensi terhadap jurusan berbasis pola data pengguna lain.

## Kesimpulan
### Collaborative Filtering:
   - Model ini menunjukkan hasil terbaik dalam hal kesalahan prediksi (RMSE dan MAE rendah).
   - Cocok untuk memprediksi relevansi jurusan berbasis pola data pengguna lain.

## Saran
### Collaborative Filtering:
   - Mencoba menggunakan algoritma yang lebih kompleks (misalnya, kNN atau Matrix Factorization lebih lanjut).

### Referensi

[1] F. Firmahsyah and T. Gantini, “Penerapan Metode Content-Based Filtering Pada Sistem Rekomendasi Kegiatan Ekstrakulikuler (Studi Kasus di Sekolah ABC)”, JuTISI, vol. 2, no. 3, Dec. 2016.

[2]	Habibi, Roni, and Muhammad Dzihan Albanna. "Analisis Sistem Rekomendasi Pada Job Recommendation Berdasarkan Profil Linkedin Menggunakan Cosine Similarity: ANALISIS SISTEM REKOMENDASI PADA JOB RECOMMENDATION BERDASARKAN PROFIL LINKEDIN MENGGUNAKAN COSINE SIMILARITY." Jurnal Teknik Informatika 14, no. 3 (2022): 118-122.

[3]	Crismastiana Koloman, Raihan Maulana, Raisya Dwi Zahra Putri, and Wahyu Abadi Harahap, “Sistem Rekomendasi Pekerjaan di bidang IT Menggunakan Algoritma Content-Based Filtering”, jcsr-politama, vol. 1, no. 6, pp. 78–88, Dec. 2023.

[4]	D. Astuti, A. Pinandito, dan R. K. Dewi, “Sistem Rekomendasi Lowongan Pekerjaan Untuk Fresh Graduate Menggunakan Metode Weighted Product Berbasis Android”, J-PTIIK, vol. 1, no. 12, hlm. 1518–1525, Jul 2017.
