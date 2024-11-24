# Laporan Proyek Machine Learning - Edi Widodo

## Domain Proyek
<p align="justify"> 
Pasar cryptocurrency telah mengalami pertumbuhan signifikan dalam beberapa tahun terakhir, hal ini menarik minat investor pada pasar yang sedang berkembang ini karena potensi pengembalian keuntungan yang tinggi dan mengambil manfaat dari diversifikasi portofolio aset. Salah satu masalah utama dalam investasi portofolio cryptocurrency adalah tingginya volatilitas dan risiko yang terkait dengan pasar ini. Cryptocurrency dikenal dengan fluktuasi harga yang tinggi, yang dapat menghasilkan keuntungan atau kerugian signifikan dalam waktu singkat [1]. Hal ini menyulitkan investor untuk menentukan alokasi aset yang optimal dalam portofolio mereka dan mengelola risiko secara efektif [2,3]. Penelitian menunjukkan bahwa volatilitas tinggi pada cryptocurrency menjadi perhatian utama bagi investor, karena dapat menyebabkan kerugian signifikan dalam waktu singkat [1]. Volatilitas tinggi pada Bitcoin, misalnya, telah menyebabkan fluktuasi harga yang signifikan, sehingga sulit bagi investor untuk menentukan alokasi aset yang optimal dalam portofolio mereka [4]. Dari perubahan harga yang fluktuatif, terdapat stable coin yang memiliki harga relatif stabil terhadap US dollar, hal ini dapat memberikan potensi keuntungan perlindungan dari fluktuasi nilai aset crypto yang sangat tinggi. Naik turunnya nilai aset crypto yang beragam, memberikan gambaran bahwa beberapa pasangan crypto memiliki korelasi pergerakan harga yang negatif, artinya ketika satu crypto mengalami kenaikan, maka crypto pasangannya akan mengalami penurunan, salah satu pasangan crypto yang memiliki corelasi negatif adalah XRP dan USDT [17]. 
Project ini menggunakan prediksi harga XRP yang dibandingkan dengan harga USDT pada saat ini, untuk memprediksi harga keduanya, menggunakan LSTM, kemudian dari prediksi harga keduanya, akan dihitung nilai Z-Score yang ada untuk memberikan saran, apakah aset XRP harus ditukarkan dengan aset USDT atau ditahan, demikian juga sebaliknya. 
Dengan pendekatan ini, maka jumlah aset akan selalu mengalami kenaikan, meskipun jika nilai tukar aset terhadap US$ mengalami penurunan.
</p>
<br>
## Rubrik/Kriteria Tambahan (Opsional):

- Dengan menggunakan data nilai tukar XRP dan USDT harian yang didapat dari dataset Kaggle, dg LSTM dibuat prediksi harga di masa yang akan datang, harga tersebut kemudian dianalisis nilai Z-Score antara keduanya, jika nilai Z-Score menunjukkan negatif terhadap pasangannya, maka diberikan saran penukaran (Trade), jika positif maka diberikan saran untuk ditahan (Hold)

### Referensi

[1] D. G. Baur and T. Dimpfl, “The volatility of Bitcoin and its role as a medium of exchange and a store of value,” Empir. Econ., vol. 61, no. 5, pp. 2663–2683, 2021, doi: 10.1007/s00181-020-01990-5.

[2]	K. Schwab, K. Schwab, F. I. Revolution, and C. Directors, “Main ideas of the book To whom is this book indicated ? Overview of the book,” pp. 1–5, 2016.

[3]	C. W. Su, M. Qin, R. Tao, and M. Umar, “Financial implications of fourth industrial revolution: Can bitcoin improve prospects of energy investment?,” Technol. Forecast. Soc. Change, vol. 158, no. June, 2020, doi: 10.1016/j.techfore.2020.120178.

[4]	S. Zhang, M. Li, and C. Yan, “The Empirical Analysis of Bitcoin Price Prediction Based on Deep Learning Integration Method,” Comput. Intell. Neurosci., vol. 2022, 2022, doi: 10.1155/2022/1265837.

[5]	P. Katsiampa, K. Gkillas, and F. Longin, “Cryptocurrency Market Activity During Extremely Volatile Periods,” SSRN Electron. J., 2018, doi: 10.2139/ssrn.3220781.

[6]	S. P. Yadav, K. K. Agrawal, B. S. Bhati, F. Al-Turjman, and L. Mostarda, “Blockchain-Based Cryptocurrency Regulation: An Overview,” Comput. Econ., vol. 59, no. 4, pp. 1659–1675, 2022, doi: 10.1007/s10614-020-10050-0.
[7]	S. Corbet, D. J. Cumming, B. M. Lucey, M. Peat, and S. A. Vigne, “The destabilising effects of cryptocurrency cybercriminality,” Econ. Lett., vol. 191, 2020, doi: 10.1016/j.econlet.2019.108741.

[8]	A. Aspris, S. Foley, J. Svec, and L. Wang, “Decentralized exchanges: The ‘wild west’ of cryptocurrency trading,” Int. Rev. Financ. Anal., vol. 77, pp. 1–30, 2021, doi: 10.1016/j.irfa.2021.101845.

[9]	S. Sorsen, J. Schulz, S. Sorsen, and J. Schulz, “Association for Information Systems AIS Electronic Library ( AISeL ) Algorithmic Trading and Cryptocurrency- a literature review and key findings Algorithmic Trading and Cryptocurrency- a literature review and key findings,” 2022.

[10]	M. Hougan and D. Lawant, Cryptoassets: The Guide to Bitcoin, Blockchain, and Cryptocurrency for Investment Professionals. 2021. doi: 10.2139/ssrn.3792541.

[11]	P. Katsiampa, S. Corbet, and B. Lucey, “High frequency volatility co-movements in cryptocurrency markets,” J. Int. Financ. Mark. Institutions Money, vol. 62, pp. 35–52, 2019, doi: 10.1016/j.intfin.2019.05.003.

[12]	S. Qureshi, M. Aftab, E. Bouri, and T. Saeed, “Dynamic interdependence of cryptocurrency markets: An analysis across time and frequency,” Phys. A Stat. Mech. its Appl., vol. 559, p. 125077, Dec. 2020, doi: 10.1016/J.PHYSA.2020.125077.

[13]	Q. Ji, E. Bouri, C. Keung, M. Lau, and D. Roubaud, “Dynamic connectedness and integration among large cryptocurrencies,” Elsevier, pp. 1–41, 219AD, [Online]. Available: https://www.sciencedirect.com/science/article/pii/S1057521918305416

[14]	H. Akoglu, “Turkish Journal of Emergency Medicine User ’ s guide to correlation coe ffi cients,” Turkish J. Emerg. Med., vol. 18, no. August, pp. 91–93, 2018.

[15]	J. Hauke and T. Kossowski, “Comparison of values of pearson’s and spearman’s correlation coefficients on the same sets of data,” Quaest. Geogr., vol. 30, no. 2, pp. 87–93, 2011, doi: 10.2478/v10117-011-0021-1.

[16]	Y. Liu, Y. Mu, K. Chen, Y. Li, and J. Guo, “Daily Activity Feature Selection in Smart Homes Based on Pearson Correlation Coefficient,” Neural Process. Lett., vol. 51, no. 2, pp. 1771–1787, 2020, doi: 10.1007/s11063-019-10185-8.

[17] T. Winarti, E. Widodo, S. Handayni and A. Nugroho, "Utilizing Pearson Correlation Matrix to Identify Negative Correlations Among Cryptocurrencies," 2024 3rd International Conference on Creative Communication and Innovative Technology (ICCIT), Tangerang, Indonesia, 2024, pp. 1-7, doi: 10.1109/ICCIT62134.2024.10701159.

## Business Understanding

<p align="justify"> Perilaku perdagangan cryptocurrency paling umum dilakukan adalah dengan mengukur nilai tukar aset cryptocurrency terhadap mata uang fiat, baik dalam bentuk rupiah maupun dollar Amerika. Hal ini membuat banyak pelaku perdagangan cryptocurrency memanfaatkan volatilitas nilai tukar cryptocurrency untuk mendapatkan keuntungan jangka pendek. Sementara itu, teknologi cryptocurrency terus berkembang seiring dengan perkembangan teknologi internet, oleh karena itu peluang jangka panjang terhadap teknologi ini masih sangat terbuka.
Banyak pelaku perdagangan cryptocurrency mengalami kerugian besar, meskipun tidak sedikit yang mendapatkan untung besar juga, karena perubahan nilai tukar cryptocurrency terhadap mata uang fiat yang sangat fluktuatif. Sementara itu secara keseluruhan, grafik nilai tukar cryptocurrency terus bergerak naik. <br>
Dari analisa awal terhadap grafik pergerakan nilai tukar cryptocurrency, secara visual terlihat adanya hubungan antar masing-masing cryptocurrency. Pasangan cryptocurrency yang memiliki korelasi simpangan paling jauh memiliki arti bahwa sifat keduanya saling berlawanan, sehingga memiliki peluang terbesar untuk terus meningkatkan nilai aset yang dimiliki, dengan cara menukarkan aset cryptocurrency x terhadap aset cryptocurrency y dan sebaliknya. Jika aset x mengalami peningkatan nilai terhadap aset y, maka aset x harus dilepaskan untuk ditukar dengan aset y. Pertukaran dapat kembali dilakukan saat aset y nilainya meningkat terhadap aset x.
</p>

## Problem Statements
- Bagaimana menentukan rekomendasi apakah saat ini harus menukarkan Aset XRP menjadi USDT atau sebaliknya agar terhindar dari kerugian yang berlebih dari fluktuasi nilai tukar.
- Bagaimana Mengukur nilai Z-Score dari hasil prediksi nilai dimasa yang akan datang.

### Goals
- Membuat prediksi harga pasangan aset (XRP dan USDT) di masa yang akan datang berdasarkan harga masa lalu, dan harga saat ini.
- Dari prediksi harga masa yang akan datang, kemudian diukur nilai Z-Score antara keduanya, jika nilainya negatif, maka berikan saran untuk penukaran, jika positif maka lakukan langkah tahan aset.
- Sistem ini melakukan Prediksi dengan LSTM, sekaligus memberikan rekomendasi berdasarkan nilai Z-Score dari hasil prediksi algoritma LSTM.

**Rubrik/Kriteria Tambahan (Opsional)**:
- Mengambil dataset dari kaggle, di lokasi (https://www.kaggle.com/datasets/svaningelgem/crypto-currencies-daily-prices) khusus pada aset XRP dan USDT, berdasarkan riset yang telah dilakukan sebelumnya, bahwa kedua aset tersebut memiliki korelasi negatif yang cukup untuk menjadi pasangan pertukaran aset [17]
- Membuat prediksi harga dimasa depan menggunakan LSTM berdasarkan dari dataset masa lalu.
- Mengukur nilai Z-Score dari prediksi harga dimasa depan, dan memberikan solusi yang direkomendasikan

## Data Understanding
- Dataset diambil dari (https://www.kaggle.com/datasets/svaningelgem/crypto-currencies-daily-prices)   yang bersifat update harian.

### Variabel-variabel pada dataset tersebut adalah sebagai berikut:
- ticker : Label untuk nama asset cryptocurrency [XRP,USDT]
- date : merupakan tanggal data direkam yang bersifat harian.
- open : merupakan harga pembukaan transaksi pertukaran nilai asset dalam US$ sesuai tanggal.
- high : merupakan harga tertinggi dalam US$ harian sesuai tanggal.
- low : merupakan harga terendah harian dalam US$ sesuai tanggal.
- close : merupakan harga pada saat tanggal penutupan.

**Rubrik/Kriteria Tambahan (Opsional)**:
- Saya melakukan riset ini sejak lama, mengamati pergerakan grafik nilai tukar asset crypto, kemudian melakukan analisis pergerakan menggunakan pearson correlation
- Ternyata dari riset sebelumnya, ada korelasi negatif yang cukup antara asset XRP dan USDT.
- Pada analisis ini, saya melanjutkan riset sebelumnya untuk memberikan rekomendasi harus menukarkan aset atau harus menahannya dengan prediksi nilai dimasa depan yang dihitung z-score antara keduanya.
- Z-Score adalah ukuran statistik yang digunakan untuk menilai sejauh mana suatu titik data berbeda dari rata-rata dalam satuan standar deviasi. 
   
## Data Preparation
1. Conect ke GDRIVE
2. Mempersiapkan library
3. Membuat dataset time series
4. Muat dataset XRP dan USDT
5. Gabungkan Data
6. Tampilkan Visualisasi Pergerakan nilai
7. Hitung Matrix Korelasi & Normalisasi Data
8. Trainning Data
9. Membuat Model Prediksi LSTM
10. Prediksi Dataset
11. Fungsi Rekomendasi Action
12. Masukkan nilai XRP dan USDT
13. Tampilkan visualisasi data berdasarkan prediksi terakhir
14. Menampilkan rekomendasi grafik Trade atau Hold

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

**---Ini adalah bagian akhir laporan---**
