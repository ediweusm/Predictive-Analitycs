# Laporan Proyek Machine Learning - Edi Widodo

## Domain Proyek
<p align="justify"> 
Pasar cryptocurrency telah mengalami pertumbuhan signifikan dalam beberapa tahun terakhir, hal ini menarik minat investor pada pasar yang sedang berkembang ini karena potensi pengembalian keuntungan yang tinggi dan mengambil manfaat dari diversifikasi portofolio aset. Salah satu masalah utama dalam investasi portofolio cryptocurrency adalah tingginya volatilitas dan risiko yang terkait dengan pasar ini. Cryptocurrency dikenal dengan fluktuasi harga yang tinggi, yang dapat menghasilkan keuntungan atau kerugian signifikan dalam waktu singkat [1]. Hal ini menyulitkan investor untuk menentukan alokasi aset yang optimal dalam portofolio mereka dan mengelola risiko secara efektif [2],[3]. Penelitian menunjukkan bahwa volatilitas tinggi pada cryptocurrency menjadi perhatian utama bagi investor, karena dapat menyebabkan kerugian signifikan dalam waktu singkat [1]. Volatilitas tinggi pada Bitcoin, misalnya, telah menyebabkan fluktuasi harga yang signifikan, sehingga sulit bagi investor untuk menentukan alokasi aset yang optimal dalam portofolio mereka [4]. Dari perubahan harga yang fluktuatif, terdapat stable coin yang memiliki harga relatif stabil terhadap US dollar, hal ini dapat memberikan potensi keuntungan perlindungan dari fluktuasi nilai aset crypto yang sangat tinggi. Naik turunnya nilai aset crypto yang beragam, memberikan gambaran bahwa beberapa pasangan crypto memiliki korelasi pergerakan harga yang negatif, artinya ketika satu crypto mengalami kenaikan, maka crypto pasangannya akan mengalami penurunan, salah satu pasangan crypto yang memiliki corelasi negatif adalah XRP dan USDT [5]. 
Project ini menggunakan prediksi harga XRP yang dibandingkan dengan harga USDT pada saat ini, untuk memprediksi harga keduanya, menggunakan LSTM, kemudian dari prediksi harga keduanya, akan dihitung nilai Z-Score yang ada untuk memberikan saran, apakah aset XRP harus ditukarkan dengan aset USDT atau ditahan, demikian juga sebaliknya. 
Dengan pendekatan ini, maka jumlah aset akan selalu mengalami kenaikan, meskipun jika nilai tukar aset terhadap US$ mengalami penurunan.
</p>
<br>
Dari data nilai tukar XRP dan USDT harian yang didapat dari dataset Kaggle,maka dibuat prediksi harga di masa yang akan datang menggunakan algoritma LSTM. Hasil prediksi harga tersebut kemudian dianalisis nilai Z-Score antara keduanya, jika nilai Z-Score menunjukkan negatif terhadap pasangannya, maka diberikan saran penukaran (Trade), jika positif maka diberikan saran untuk ditahan (Hold)

## Business Understanding
<p align="justify"> Perilaku perdagangan cryptocurrency paling umum dilakukan adalah dengan mengukur nilai tukar aset cryptocurrency terhadap mata uang fiat, baik dalam bentuk rupiah maupun dollar Amerika. Hal ini membuat banyak pelaku perdagangan cryptocurrency memanfaatkan volatilitas nilai tukar cryptocurrency untuk mendapatkan keuntungan jangka pendek. Sementara itu, teknologi cryptocurrency terus berkembang seiring dengan perkembangan teknologi internet, oleh karena itu peluang jangka panjang terhadap teknologi ini masih sangat terbuka.
Banyak pelaku perdagangan cryptocurrency mengalami kerugian besar, meskipun tidak sedikit yang mendapatkan untung besar juga, karena perubahan nilai tukar cryptocurrency terhadap mata uang fiat yang sangat fluktuatif. Sementara itu secara keseluruhan, grafik nilai tukar cryptocurrency terus bergerak naik. <br>
Dari analisa awal terhadap grafik pergerakan nilai tukar cryptocurrency, secara visual terlihat adanya hubungan antar masing-masing cryptocurrency. Pasangan cryptocurrency yang memiliki korelasi simpangan paling jauh memiliki arti bahwa sifat keduanya saling berlawanan, sehingga memiliki peluang terbesar untuk terus meningkatkan nilai aset yang dimiliki, dengan cara menukarkan aset cryptocurrency x terhadap aset cryptocurrency y dan sebaliknya. Jika aset x mengalami peningkatan nilai terhadap aset y, maka aset x harus dilepaskan untuk ditukar dengan aset y. Pertukaran dapat kembali dilakukan saat aset y nilainya meningkat terhadap aset x.
</p>
Berdasarkan hasil riset yang dilakukan oleh widodo [5], dalam mengamati pergerakan grafik nilai tukar asset crypto dan  melakukan analisis pergerakan menggunakan pearson correlation, terdapat korelasi negatif yang cukup antara asset XRP dan USDT. 

## Problem Statements
- Bagaimana menentukan rekomendasi apakah saat ini harus menukarkan Aset XRP menjadi USDT atau sebaliknya agar terhindar dari kerugian yang berlebih dari fluktuasi nilai tukar.
- Bagaimana Mengukur nilai Z-Score dari hasil prediksi nilai dimasa yang akan datang.

### Goals
- Membuat prediksi harga pasangan aset (XRP dan USDT) di masa yang akan datang berdasarkan harga masa lalu, dan harga saat ini.
- Dari prediksi harga masa yang akan datang, kemudian diukur nilai Z-Score antara keduanya, jika nilainya negatif, maka berikan saran untuk penukaran, jika positif maka lakukan langkah tahan aset.
- Sistem ini melakukan Prediksi dengan LSTM, sekaligus memberikan rekomendasi berdasarkan nilai Z-Score dari hasil prediksi algoritma LSTM.

## Data Understanding
- Mengambil dataset dari kaggle, di lokasi (https://www.kaggle.com/datasets/svaningelgem/crypto-currencies-daily-prices) khusus pada aset XRP dan USDT, berdasarkan riset yang telah dilakukan sebelumnya, bahwa kedua aset tersebut memiliki korelasi negatif yang cukup untuk menjadi pasangan pertukaran aset [5]
- Jumlah data yang digunakan adalah XRP: 3.593 dan USDT: 2.822
- Hanya kolom date dan close, yang digunakan untuk melakukan prediksi harga dimasa yang akan datang.

### Variabel-variabel pada dataset tersebut adalah sebagai berikut:
- ticker : Label untuk nama asset cryptocurrency [XRP,USDT]
- date : merupakan tanggal data direkam yang bersifat harian.
- open : merupakan harga pembukaan transaksi pertukaran nilai asset dalam US$ sesuai tanggal.
- high : merupakan harga tertinggi dalam US$ harian sesuai tanggal.
- low : merupakan harga terendah harian dalam US$ sesuai tanggal.
- close : merupakan harga pada saat tanggal penutupan.
 
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
  
     `df = df.dropna()`

     `df['Close_XRP'].fillna(df['Close_XRP'].mean(), inplace=True)`
    
     `df['Close_USDT'].fillna(df['Close_USDT'].mean(), inplace=True)`
    
    

### 2. Handling Outlier
- Tujuan: Mengatasi nilai yang terlalu ekstrem yang dapat memengaruhi performa model.
- Pendekatan:
  - Z-Score: Menghapus data dengan Z-Score di luar ambang batas (misalnya, |Z| > 3).
  - IQR (Interquartile Range): Menghapus nilai di luar rentang [Q1 - 1.5IQR, Q3 + 1.5IQR].
- Implementasi Code :

  `Q1 = df['Close_XRP'].quantile(0.25)`
  `Q3 = df['Close_XRP'].quantile(0.75)`
  `IQR = Q3 - Q1`
  `df = df[~((df['Close_XRP'] < (Q1 - 1.5 * IQR)) | (df['Close_XRP'] > (Q3 + 1.5 * IQR)))]`

### 3. Feature Engineering
- Tujuan: Membuat fitur baru yang relevan dan dapat membantu model memahami pola dalam data.
- Pendekatan:
  - Technical Indicators: Membuat indikator teknikal seperti moving average (SMA), exponential moving average (EMA), atau relative strength index (RSI).
  - Lag Features: Menambahkan kolom harga sebelumnya sebagai prediktor.

# Modeling
## Preprocessing Data:
- Normalisasi Data: Data harga dinormalisasi menggunakan MinMaxScaler agar semua nilai berada dalam rentang [0, 1]. Hal ini membantu model LSTM untuk lebih cepat melakukan konvergensi selama pelatihan.
- Time Series Dataset: Dataset disusun menjadi urutan waktu dengan menggunakan jendela waktu (window). Misalnya, data 30 hari terakhir digunakan untuk memprediksi harga pada hari berikutnya.

## Pemisahan Data:
- Training Set (80%): Data ini digunakan untuk melatih model.
- Test Set (20%): Data ini digunakan untuk mengevaluasi kinerja model pada data yang belum pernah dilihat.

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

[1] D. G. Baur and T. Dimpfl, “The volatility of Bitcoin and its role as a medium of exchange and a store of value,” Empir. Econ., vol. 61, no. 5, pp. 2663–2683, 2021, doi: 10.1007/s00181-020-01990-5.

[2]	K. Schwab, K. Schwab, F. I. Revolution, and C. Directors, “Main ideas of the book To whom is this book indicated ? Overview of the book,” pp. 1–5, 2016.

[3]	C. W. Su, M. Qin, R. Tao, and M. Umar, “Financial implications of fourth industrial revolution: Can bitcoin improve prospects of energy investment?,” Technol. Forecast. Soc. Change, vol. 158, no. June, 2020, doi: 10.1016/j.techfore.2020.120178.

[4]	S. Zhang, M. Li, and C. Yan, “The Empirical Analysis of Bitcoin Price Prediction Based on Deep Learning Integration Method,” Comput. Intell. Neurosci., vol. 2022, 2022, doi: 10.1155/2022/1265837.

[5] T. Winarti, E. Widodo, S. Handayni and A. Nugroho, "Utilizing Pearson Correlation Matrix to Identify Negative Correlations Among Cryptocurrencies," 2024 3rd International Conference on Creative Communication and Innovative Technology (ICCIT), Tangerang, Indonesia, 2024, pp. 1-7, doi: 10.1109/ICCIT62134.2024.10701159.
