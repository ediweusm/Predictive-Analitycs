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
- Mengambil dataset dari kaggle, di lokasi [Student Attitude and Behavior](https://www.kaggle.com/datasets/susanta21/student-attitude-and-behavior)
- Jumlah Data: 235 entri.
- Usability Level : 10.0
- Kondisi Data: Dataset lengkap dengan informasi personal, akademik, dan preferensi mahasiswa.

### Variabel-variabel pada dataset tersebut adalah sebagai berikut:
- Certification Course: Sertifikasi tambahan yang diikuti mahasiswa.
- Gender: Jenis kelamin mahasiswa.
- Department: Jurusan (Sistem Informasi, Manajemen Bisnis, Akuntansi, dll.).
- Hobbies: Hobi mahasiswa, seperti membaca atau bermain video game.
- Prefer to Study In: Waktu belajar yang disukai mahasiswa.
- Salary Expectation: Ekspektasi gaji.
- Willingness to Pursue a Career Based on Their Degree: Persentase minat untuk bekerja sesuai jurusan.
- Nilai Akademik (Kelas 10, Kelas 12, Kuliah):
  - Nilai rata-rata dari semua mata pelajaran yang diambil pada kelas 10 dan 12.
  - Nilai kuliah dianggap sebagai rata-rata kumulatif (Cumulative Grade Point Average, CGPA) dari semua mata kuliah.

 
## Data Preparation
### 1. Handling Missing Values
- Tujuan: Memastikan tidak ada nilai kosong yang dapat memengaruhi proses pelatihan model.
- Pendekatan:
  - Drop Missing Values: 
    - Jika jumlah data yang hilang kecil dan tidak signifikan, baris atau kolom yang mengandung nilai kosong dihapus.
  - Imputasi: Jika data hilang signifikan, nilai yang hilang diisi dengan:
    - Mean (rata-rata)
    - Median (nilai tengah)
    - Mode (nilai yang paling sering muncul)
  - Implementasi Code :
     ```ruby
    df = df.dropna()
     ```
     ```ruby
     # Kode ini tidak dipakai, hanya contoh jika ada data yang hilang, maka diisi dengan nilai mean
    df['Close_XRP'].fillna(df['Close_XRP'].mean(), inplace=True)
    df['Close_USDT'].fillna(df['Close_USDT'].mean(), inplace=True)
     ```

### 2. Handling Outlier
- Tujuan: Mengatasi nilai yang terlalu ekstrem yang dapat memengaruhi performa model.
- Pendekatan:
  - Z-Score: Menghapus data dengan Z-Score di luar ambang batas (misalnya, |Z| > 3).
  - IQR (Interquartile Range): Menghapus nilai di luar rentang [Q1 = -1.5, Q3 = 1.5].
- Implementasi Code :

   ```ruby
   # Menggunakan IQR untuk menangani outlier
  Q1 = df['close_XRP'].quantile(0.25)  
  Q3 = df['close_XRP'].quantile(0.75)
  IQR = Q3 - Q1

  # Hapus outlier dari XRP
  df = df[~((df['close_XRP'] < (Q1 - 1.5 * IQR)) | (df['close_XRP'] > (Q3 + 1.5 * IQR)))]
   ```

### 3. Feature Engineering
- Tujuan: Membuat fitur baru yang relevan dan dapat membantu model memahami pola dalam data.
- Pendekatan:
  - Technical Indicators: Membuat indikator teknikal seperti moving average (SMA), exponential moving average (EMA), atau relative strength index (RSI).
  - Lag Features: Menambahkan kolom harga sebelumnya sebagai prediktor.
- Implementasi dalam project : Moving Average (7 hari)
  ```ruby
  df['SMA_7_XRP'] = df['close_XRP'].rolling(window=7).mean()
  df['SMA_7_USDT'] = df['close_USDT'].rolling(window=7).mean()
  ```

### 4. Data Transformation
- Tujuan: Mengubah skala data agar lebih sesuai untuk algoritma machine learning.
- Pendekatan:
  - Normalisasi Data: Data harga dinormalisasi menggunakan MinMaxScaler agar semua nilai berada dalam rentang [0, 1]. Hal ini membantu model LSTM untuk lebih cepat melakukan konvergensi selama pelatihan.
  - Min-Max Scaling: Mengubah skala data ke rentang [0, 1], digunakan untuk LSTM.
  - Standardization: Mengubah data menjadi distribusi dengan mean 0 dan standar deviasi 1.
- Langkah Implementasi dalam project:
  ```ruby
   from sklearn.preprocessing import MinMaxScaler  
   scaler = MinMaxScaler()
   df['Close_XRP_Normalized'] = scaler.fit_transform(df[['Close_XRP']])
   df['Close_USDT_Normalized'] = scaler.fit_transform(df[['Close_USDT']])
  ```

### 5. Splitting Data
- Tujuan: Membagi data menjadi data pelatihan dan pengujian untuk evaluasi model yang adil.
- Pendekatan:
   - Data dibagi dalam rasio 80:20 untuk pelatihan dan pengujian.
   - Data time series harus dibagi dengan mempertahankan urutan waktu.
   ```ruby
   # Split data menjadi train-test
   train_size = int(len(X_xrp) * 0.8)
   X_xrp_train, X_xrp_test = X_xrp[:train_size], X_xrp[train_size:]
   y_xrp_train, y_xrp_test = y_xrp[:train_size], y_xrp[train_size:] 
   X_usdt_train, X_usdt_test = X_usdt[:train_size], X_usdt[train_size:]
   y_usdt_train, y_usdt_test = y_usdt[:train_size], y_usdt[train_size:]
   ```

### 6. Validasi Data
- Tujuan: Memastikan data bebas dari masalah setelah preprocessing.
- Pendekatan:
  - Cek kembali data setelah preprocessing untuk memastikan tidak ada nilai kosong, outlier, atau fitur yang hilang.
- Langkah Implementasi:
  ```ruby
  # Periksa apakah ada nilai kosong
  print(df.isnull().sum())
  
  # Periksa dimensi data
  print(df.shape)
  ```

# Modeling
<p align="justify">Pada tahap ini, model yang digunakan adalah Long Short-Term Memory (LSTM), salah satu jenis Recurrent Neural Network (RNN). LSTM dipilih karena kemampuannya dalam menangkap pola temporal dan hubungan jangka panjang pada data time series, seperti harga aset cryptocurrency. LSTM dirancang untuk mengatasi masalah vanishing gradient yang sering terjadi pada RNN klasik. Dengan menggunakan struktur internal yang terdiri dari "cell state" dan "gates", LSTM dapat mengontrol informasi mana yang harus diingat, diperbarui, atau dilupakan</p>

## Arsitektur Model LSTM:
- Input Layer:
  - Menerima data dalam bentuk urutan (sequence) dengan fitur tunggal (harga).
- Hidden Layers:
  - Dua lapisan LSTM digunakan untuk menangkap pola temporal.
  - Dropout dapat ditambahkan (opsional) untuk mengurangi risiko overfitting.
- Output Layer:
  - Satu neuron pada lapisan akhir memprediksi nilai harga berikutnya.

## Kompilasi Model:
- Optimizer: Adam Optimizer digunakan karena adaptif terhadap perubahan gradien selama pelatihan.
- Loss Function: Mean Squared Error (MSE) digunakan untuk mengukur perbedaan antara prediksi dan nilai aktual.

## Pelatihan Model:
- Model dilatih dengan beberapa epoch (misalnya, 20–50 epoch) untuk mencapai kinerja optimal.
- Batch Size: Data diproses dalam batch kecil (misalnya, 32) untuk efisiensi pelatihan.
- Evaluasi Model: Model diuji pada data test untuk menghitung Mean Squared Error (MSE) atau Root Mean Squared Error (RMSE) sebagai metrik kinerja.
- Prediksi harga di masa depan dibandingkan dengan nilai aktual untuk mengevaluasi akurasi model.

## Implementasi Kode dengan keras:
```ruby
from tensorflow.keras.callbacks import EarlyStopping
# Callback Early Stopping untuk menghentikan pelatihan jika tidak ada peningkatan
early_stopping = EarlyStopping(monitor='val_loss', patience=5, restore_best_weights=True)

# Fungsi untuk membuat model LSTM
def build_lstm_model():
    model = Sequential([
        LSTM(50, return_sequences=True, input_shape=(look_back, 1)),
        LSTM(50, return_sequences=False),
        Dense(1)
    ])
    model.compile(optimizer='adam', loss='mean_squared_error')
    return model

# Model untuk XRP
model_xrp = build_lstm_model()
model_xrp.fit(X_xrp_train, y_xrp_train, epochs=100, batch_size=32, validation_data=(X_xrp_test, y_xrp_test), callbacks=[early_stopping], verbose=1)

# Model untuk USDT
model_usdt = build_lstm_model()
model_usdt.fit(X_usdt_train, y_usdt_train, epochs=100, batch_size=32, validation_data=(X_usdt_test, y_usdt_test), callbacks=[early_stopping], verbose=1)
```
# Evaluation
## Metrik Evaluasi yang Digunakan
- Mean Squared Error (MSE): Mengukur rata-rata kesalahan kuadrat antara nilai prediksi dan nilai aktual
  - Interpretasi: Semakin kecil nilai MSE, semakin baik performa model, Sensitif terhadap outlier karena menghitung kuadrat dari kesalahan.
- Root Mean Squared Error (RMSE): Akar kuadrat dari MSE, yang memberikan interpretasi langsung dalam skala yang sama dengan data asli.
  - Interpretasi: RMSE lebih intuitif dibandingkan MSE karena dalam unit asli harga (USD), Digunakan untuk mengevaluasi tingkat deviasi prediksi dari nilai aktual.
- Mean Absolute Error (MAE): Mengukur rata-rata kesalahan absolut antara nilai prediksi dan nilai aktual.
  - Interpretasi: Lebih robust terhadap outlier dibandingkan MSE, Memberikan indikasi rata-rata kesalahan dalam unit asli data.

## Hasil pengujian terhadap model adalah sebagai berikut :
### Metrics XRP
- Mean Squared Error (MSE): 0.00185
  - MSE mengukur rata-rata kesalahan kuadrat antara nilai prediksi dan nilai aktual.
  - Nilai 0.00185 menunjukkan bahwa model memiliki tingkat kesalahan kuadrat rata-rata yang kecil.
  - Karena MSE sensitif terhadap outlier, kesalahan besar pada satu prediksi akan lebih memengaruhi hasil.
- Root Mean Squared Error (RMSE): 0.04306
  - RMSE adalah akar kuadrat dari MSE, memberikan kesalahan rata-rata dalam unit asli (normalisasi).
  - Nilai 0.04306 menunjukkan bahwa prediksi rata-rata meleset sekitar 4.3% dari skala normalisasi data XRP.
- Mean Absolute Error (MAE): 0.03140
  - MAE mengukur rata-rata kesalahan absolut antara prediksi dan nilai aktual.
  - Nilai 0.03140 berarti bahwa, rata-rata, prediksi model meleset sekitar 3.1% dalam skala normalisasi.
- Kesimpulan XRP:
  - Model memiliki performa yang cukup baik dengan kesalahan prediksi rata-rata relatif kecil (sekitar 3.1–4.3%).
  -- Namun, MSE menunjukkan bahwa kesalahan besar (jika ada) memengaruhi hasil lebih signifikan.

### Metrics USDT
- Mean Squared Error (MSE): 0.00000
  - Nilai 0.00000 menunjukkan bahwa model memiliki kesalahan kuadrat rata-rata yang sangat kecil, mendekati nol.
  - Hal ini mengindikasikan prediksi sangat dekat dengan nilai aktual pada skala normalisasi.
- Root Mean Squared Error (RMSE): 0.00062
  - RMSE sebesar 0.00062 menunjukkan bahwa prediksi rata-rata meleset kurang dari 0.1% dari skala normalisasi data USDT.
- Mean Absolute Error (MAE): 0.00052
  - MAE sebesar 0.00052 berarti rata-rata kesalahan prediksi hanya sekitar 0.05%, menunjukkan performa prediksi yang sangat akurat.
- Kesimpulan USDT:
  - Model memiliki performa luar biasa dengan kesalahan prediksi yang hampir tidak signifikan.
  - Hasil ini mungkin menunjukkan bahwa pola harga USDT lebih mudah diprediksi oleh model dibandingkan XRP.
 
### Perbandingan XRP dan USDT
- MSE:
  - XRP memiliki MSE lebih besar (0.00185) dibandingkan USDT (0.00000), menunjukkan model lebih kesulitan dalam memprediksi harga XRP.
- RMSE dan MAE:
  - XRP memiliki kesalahan rata-rata yang lebih besar (RMSE: 0.04306, MAE: 0.03140) dibandingkan USDT (RMSE: 0.00062, MAE: 0.00052).
  - Hal ini menunjukkan bahwa prediksi harga USDT lebih stabil dan akurat dibandingkan XRP.
- Stabilitas Prediksi:
  - Model lebih efektif dalam memprediksi USDT, kemungkinan karena pola harga USDT lebih linear atau lebih sedikit volatil dibandingkan XRP.

### Makna Z-Score untuk XRP dan USDT
- Menganalisis Relasi:
  - Z-Score membantu memahami bagaimana harga XRP dan USDT berubah relatif terhadap distribusi mereka.
  - Jika Z-Score XRP tinggi (+ve) dan USDT rendah (-ve), ada kemungkinan hubungan negatif di antara mereka.
- Mengidentifikasi Outlier:
  - Harga dengan ∣Z∣>2 dianggap outlier. Ini penting untuk memahami volatilitas harga.
- Rekomendasi Perdagangan:
  - Ketika Z-Score XRP jauh lebih tinggi dari rata-rata (+ve) dan USDT jauh lebih rendah (-ve), pertukaran XRP ke USDT mungkin menguntungkan.
  - Sebaliknya, jika Z-Score XRP rendah (-ve) dan USDT tinggi (+ve), pertukaran USDT ke XRP dapat dipertimbangkan.

## Kesimpulan
- Model dapat menghasilkan rekomendasi yang jelas terkait kapan harus ditukar dan kapan harus di tahan untuk pasangan kedua mata uang crypto, dengan mempertimbangkan nilai Z-Score antar keduanya.
- Dengan cara ini, meskipun nilai tukar terhadap mata uang fiat harga cryptocurrency mengalami penurunan, tetapi total asset crypto akan terus mengalami kenaikan, dengan menggunakan pertukaran antar crypto yang memiliki korelasi negatif.
- Investasi dalam teknology cryptocurrency memiliki resiko yang tinggi, terkait fluktuasi harga nilai tukar yang sangat volatile, tetapi yang perlu diingat adalah bahwa teknologi cryptocurrency belum mengalami fase mass adoption, teknologi ini masih bersifat prototype, jika suatu saat cryptocurrency sudah diadopsi secara massal, maka aset yang kita miliki akan memberikan nilai return yang sangat baik.

## Saran
- Meskipun secara teori, sistem rekomendasi ini menguntungkan, tetapi investasi ini cukup beresiko, oleh karena itu "jangan tempatkan aset hanya dalam satu keranjang saja". Investasi crypto hanya sifatnya diversifikasi dari instrument aset yang lain.
- Karena aset cryptocurrency diperdagangkan dalam varian yang sangat banyak, dengan frekuensi transaksi yang sangat tinggi, maka variabel yang digunakan  untuk pengujian algoritma dapat ditambahkan dengan aspek yang lain. Misalnya volume perdagangan dan isyu seputar teknologi dan kebijakan internasional terkait cryptocurrency. 

### Referensi

[1] F. Firmahsyah and T. Gantini, “Penerapan Metode Content-Based Filtering Pada Sistem Rekomendasi Kegiatan Ekstrakulikuler (Studi Kasus di Sekolah ABC)”, JuTISI, vol. 2, no. 3, Dec. 2016.

[2]	Habibi, Roni, and Muhammad Dzihan Albanna. "Analisis Sistem Rekomendasi Pada Job Recommendation Berdasarkan Profil Linkedin Menggunakan Cosine Similarity: ANALISIS SISTEM REKOMENDASI PADA JOB RECOMMENDATION BERDASARKAN PROFIL LINKEDIN MENGGUNAKAN COSINE SIMILARITY." Jurnal Teknik Informatika 14, no. 3 (2022): 118-122.

[3]	Crismastiana Koloman, Raihan Maulana, Raisya Dwi Zahra Putri, and Wahyu Abadi Harahap, “Sistem Rekomendasi Pekerjaan di bidang IT Menggunakan Algoritma Content-Based Filtering”, jcsr-politama, vol. 1, no. 6, pp. 78–88, Dec. 2023.

[4]	D. Astuti, A. Pinandito, dan R. K. Dewi, “Sistem Rekomendasi Lowongan Pekerjaan Untuk Fresh Graduate Menggunakan Metode Weighted Product Berbasis Android”, J-PTIIK, vol. 1, no. 12, hlm. 1518–1525, Jul 2017.
