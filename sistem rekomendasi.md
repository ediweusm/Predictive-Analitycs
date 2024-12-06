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
- Dataset ini beberapa labelnya harus ditambahkan atau dimodifikasi untuk menyesuaikan kebutuhan Indonesia, seperti data Departemen dan Profesi dalam departement yang ada di Indonesia.
- Untuk variabel nilai, dataset ini menggunakan nilai kelas 10, dianggap disesuaikan dengan Indonesia adalah nilai kelas 9.
- Nilai pada jenjang perkuliahan, menggunakan skala 1-100. Artinya, input IPK yang diakui di Indonesia dengan skala 1-4, harus disesuaikan secara manual

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
### Teknik Data Preparation
1. Cleaning: Membersihkan data dari kesalahan nama departemen dan mengonversi nilai dalam format yang konsisten.
   ```ruby
    # Mengatasi nilai kosong
    data.fillna('', inplace=True)

    # Normalize willingness column and handle empty strings
    data['willingness to pursue a career based on their degree  '] = (
        data['willingness to pursue a career based on their degree  ']
        .str.rstrip('%')
        .fillna('0')
        .astype(float)
        / 100
    )    

    # Dalam dataset tidak menyediakan nama departemen sesuai Indonesia
    # disini dilakukan penyesuaian nama agar lebih familier dengan user.
    data['Department'] = data['Department'].replace({
        'BCA': 'Teknologi Informasi',
        'Commerce': 'Manajemen Bisnis',
        'B.com Accounting and Finance ': 'Akuntansi dan Keuangan',
        'B.com ISM': 'Sistem Informasi Manajemen'
    })
   ```
3. Encoding: Menggunakan Label Encoding untuk mengubah fitur kategorikal menjadi numerik.
   ```ruby
   # Encode Gender and Hobbies
    label_encoder = LabelEncoder()
    data['Gender'] = label_encoder.fit_transform(data['Gender'])
    data['Hobbies'] = label_encoder.fit_transform(data['hobbies'])
    data['selected_department'] = label_encoder.fit_transform(data['Department'])
   ```
4. Scaling: Normalisasi nilai akademik menggunakan Min-Max Scaling.
   ```ruby
    # Normalize numerical columns
    scaler = MinMaxScaler()
    data[['10th Mark', '12th Mark', 'college mark', 'Height(CM)', 'Weight(KG)']] = scaler.fit_transform(
        data[['10th Mark', '12th Mark', 'college mark', 'Height(CM)', 'Weight(KG)']]
    )
    
    # Penambahan profesi ini bisa variatif, karena di dataset tidak tersedia, maka ditambahkan manual disini

    department_professions = {
        "Teknologi Informasi": [
            "Analis Data", "Pengembang Aplikasi", "Manajer Proyek IT",
            "Administrator Basis Data", "Konsultan IT", "Insinyur Jaringan",
            "Pengembang Web", "Spesialis Keamanan Siber", "Arsitek Sistem",
            "Ilmuwan Data"
        ],
        "Manajemen Bisnis": [
            "Manajer Pemasaran", "Analis Bisnis", "Manajer Operasi",
            "Manajer Keuangan", "Konsultan Bisnis", "Pengusaha",
            "Manajer Sumber Daya Manusia", "Spesialis Riset Pasar",
            "Manajer Logistik", "Manajer Proyek"
        ],
        "Akuntansi dan Keuangan": [
            "Akuntan Publik", "Auditor Internal", "Analis Keuangan",
            "Manajer Keuangan", "Akuntan Perpajakan", "Konsultan Keuangan",
            "Manajer Investasi", "Analis Risiko", "Akuntan Biaya",
            "Manajer Kredit"
        ],
        "Sistem Informasi Manajemen": [
            "Analis Sistem", "Manajer Proyek IT", "Administrator Sistem",
            "Pengembang ERP", "Spesialis Data Warehouse", "Analis Bisnis IT",
            "Manajer Layanan TI", "Konsultan IT", "Manajer Keamanan IT",
            "Manajer Jaringan"
        ]
   ```
6. Feature Selection: Memilih fitur penting seperti nilai akademik, hobi, dan jenis kelamin untuk digunakan dalam model.
   ```ruby
      # Feature Selection
      selected_features = ['10th Mark', '12th Mark', 'college mark', 'Gender', 'Hobbies', 'selected_department']
      print(f"Fitur yang dipilih untuk model: {selected_features}") 
   ```
## Modelling and Result
### Sistem Rekomendasi
  1. Content-based Filtering:
     - Menggunakan cosine similarity untuk mencocokkan preferensi individu (seperti nilai dan hobi) dengan data yang ada.
     - Memberikan rekomendasi berbasis profil pengguna.
     - Menampilkan 5 Profesi teratas
     ```ruby
     def recommend_career_content_based(input_profile, top_n=5):
         selected_features_cb = ['10th Mark', '12th Mark', 'college mark', 'Gender', 'Hobbies']
         similarity = cosine_similarity(
             [input_profile], 
             data[selected_features_cb]
         )
         indices = similarity.argsort()[0][-top_n:]
         departments = data.iloc[indices]['Department'].unique()
     
         professions = []
         for department in departments:
             professions.extend(department_professions.get(department, []))
    
         return professions[:top_n]
     ```
  2. Collaborative Filtering:
     - Menggunakan algoritma Singular Value Decomposition (SVD) untuk menemukan pola preferensi berbasis data mahasiswa lain, dari pustaka surprise.
     - Model dilatih dengan data preferensi mahasiswa terhadap jurusan.
     - Collaborative Filtering memberikan rekomendasi berbasis pola mahasiswa lain.
     - Karena dataset tidak terdapat item_id, maka item_id dibuat auto berdasarkan jumlah data unik.
     ```ruby
     # Prepare data for surprise library
     data['user_id'] = range(len(data))
     data['item_id'] = data['Department'].factorize()[0]
     data_surprise = Dataset.load_from_df(data[['user_id', 'item_id', 'willingness to pursue a career based on their degree  ']], Reader(rating_scale=(0, 1)))
      
     # Train-test split
     trainset, testset = train_test_split(data_surprise, test_size=0.2, random_state=42)
      
     # Train Collaborative Filtering model using SVD
     model = SVD()
     model.fit(trainset)
       
     def recommend_career_collaborative(user_id=None, top_n=5):
        # Jika user_id tidak tersedia (cold start), gunakan rata-rata prediksi item
        if user_id is None:
            item_ids = data['item_id'].unique()
            predictions = [
                (item_id, model.predict(uid=None, iid=item_id, r_ui=None).est) 
                for item_id in item_ids
            ]
        else:
            # Predict ratings for existing user
            item_ids = data['item_id'].unique()
            predictions = [
                (item_id, model.predict(user_id, item_id).est) 
                for item_id in item_ids
            ]
        
        # Sort predictions by estimated score
        predictions = sorted(predictions, key=lambda x: x[1], reverse=True)[:top_n]
    
        # Map item_id to professions
        recommended_professions = []
        for item_id, _ in predictions:
            department = data[data['item_id'] == item_id]['Department'].iloc[0]
            recommended_professions.extend(department_professions.get(department, []))
    
        return recommended_professions[:top_n]
     ```
  3. Hybrid Combination
     - Pada proyek ini, algoritma Hybrid Filtering adalah kombinasi dari Content-based Filtering dan Collaborative Filtering.
     - Pendekatan hybrid ini memanfaatkan kelebihan kedua metode untuk memberikan rekomendasi yang lebih akurat dan relevan.
     - Langkah-langkah Algoritma Hybrid:
       - Langkah Pertama (Content-based Filtering):
          - Rekomendasi jurusan dihasilkan berdasarkan atribut pengguna.
       - Langkah Kedua (Collaborative Filtering):
          - Dari hasil Content-based Filtering, Collaborative Filtering memprioritaskan jurusan dengan skor prediksi tertinggi.
       - Output Final:
          - Profesi yang relevan dengan jurusan yang direkomendasikan.
     - Implementasi Kode :
       ```ruby
       def recommend_career_hybrid(input_profile, top_n=5):
          recommendations_cb = recommend_career_content_based(input_profile, top_n)
          cb_departments = []
          for profession in recommendations_cb:
              for department, professions in department_professions.items():
                  if profession in professions:
                      cb_departments.append(department)
      
          item_ids = data[data['Department'].isin(cb_departments)]['item_id'].unique()
          predictions = [(item_id, model.predict(0, item_id).est) for item_id in item_ids]
          predictions = sorted(predictions, key=lambda x: x[1], reverse=True)[:top_n]
      
          recommended_professions = []
          for item_id, _ in predictions:
              department = data[data['item_id'] == item_id]['Department'].iloc[0]
              recommended_professions.extend(department_professions.get(department, []))
      
          return recommended_professions[:top_n]
       ```
     
# Evaluation
## Metrik Evaluasi yang Digunakan
1. Evaluasi Collaborative Filtering:
   - RMSE (Root Mean Squared Error): Mengukur kesalahan prediksi rata-rata pada rating.
   - MAE (Mean Absolute Error): Mengukur kesalahan prediksi absolut rata-rata pada rating.
    
2. Evaluasi Content-based Filtering:
   - Precision: Proporsi rekomendasi yang benar dari semua yang direkomendasikan.
   - Recall: Proporsi rekomendasi yang benar dari semua yang relevan.
    
3. Evaluasi Hybrid Model:
   - Sama seperti Content-based Filtering, tetapi menggunakan hasil dari Hybrid Filtering.

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

### Content-based Filtering
1. Hasil Evaluasi:
   - Precision: 0.502 (50.2%)
      - Proporsi rekomendasi yang benar (relevan) dari semua rekomendasi yang dihasilkan.
      - Semakin tinggi precision, semakin baik model memberikan rekomendasi yang tepat.
   - Recall: 0.251 (25.1%)
      - Proporsi rekomendasi yang benar (relevan) dari semua opsi yang seharusnya direkomendasikan.
      - Semakin tinggi recall, semakin baik cakupan model.
2. Analisis:
   - Precision Tinggi, Recall Rendah:
      - Model dapat memberikan rekomendasi yang relevan, tetapi cakupan rekomendasi (jumlah opsi relevan yang terjaring) masih rendah.
   - Konteks:
      - Content-based Filtering bergantung pada atribut pengguna (nilai akademik, hobi) sehingga cakupan rekomendasi terbatas pada data yang serupa.

### Hybrid Model
1. Hasil Evaluasi:
   - Precision: 0.285 (28.5%)
   - Recall: 0.143 (14.3%)
2. Analisis:
   - Precision dan Recall Lebih Rendah Dibanding Content-based Filtering:
   - Kombinasi Content-based dan Collaborative Filtering menghasilkan rekomendasi yang kurang spesifik, sehingga precision dan recall menurun.
3. Konteks:
   - Hybrid Filtering memperluas cakupan rekomendasi (memasukkan pola pengguna lain), tetapi menurunkan spesifisitas rekomendasi untuk profil tertentu.

## Kesimpulan
1. Collaborative Filtering:
   - Model ini menunjukkan hasil terbaik dalam hal kesalahan prediksi (RMSE dan MAE rendah).
   - Cocok untuk memprediksi relevansi jurusan berbasis pola data pengguna lain.
2. Content-based Filtering:
   - Precision tinggi menunjukkan model memberikan rekomendasi yang relevan.
   - Namun, cakupan rendah (Recall rendah) menunjukkan keterbatasan model pada data yang serupa.
3. Hybrid Model:
   - Kombinasi ini menunjukkan kinerja yang lebih rendah dibanding model lain, mungkin karena konflik antara pola Content-based dan Collaborative Filtering.
   - Namun, Hybrid masih relevan untuk mengatasi masalah cold start dan diversifikasi rekomendasi.

## Saran
1. Collaborative Filtering:
   - Mencoba menggunakan algoritma yang lebih kompleks (misalnya, kNN atau Matrix Factorization lebih lanjut).
2. Content-based Filtering:
   - Lakukan penambahan fitur (misalnya, preferensi mahasiswa terhadap profesi) untuk meningkatkan cakupan (Recall).
3. Hybrid Model:
   - Lakukan perbaikan keseimbangan antara Content-based dan Collaborative Filtering, misalnya dengan memberikan bobot berbeda pada kedua pendekatan.

### Referensi

[1] F. Firmahsyah and T. Gantini, “Penerapan Metode Content-Based Filtering Pada Sistem Rekomendasi Kegiatan Ekstrakulikuler (Studi Kasus di Sekolah ABC)”, JuTISI, vol. 2, no. 3, Dec. 2016.

[2]	Habibi, Roni, and Muhammad Dzihan Albanna. "Analisis Sistem Rekomendasi Pada Job Recommendation Berdasarkan Profil Linkedin Menggunakan Cosine Similarity: ANALISIS SISTEM REKOMENDASI PADA JOB RECOMMENDATION BERDASARKAN PROFIL LINKEDIN MENGGUNAKAN COSINE SIMILARITY." Jurnal Teknik Informatika 14, no. 3 (2022): 118-122.

[3]	Crismastiana Koloman, Raihan Maulana, Raisya Dwi Zahra Putri, and Wahyu Abadi Harahap, “Sistem Rekomendasi Pekerjaan di bidang IT Menggunakan Algoritma Content-Based Filtering”, jcsr-politama, vol. 1, no. 6, pp. 78–88, Dec. 2023.

[4]	D. Astuti, A. Pinandito, dan R. K. Dewi, “Sistem Rekomendasi Lowongan Pekerjaan Untuk Fresh Graduate Menggunakan Metode Weighted Product Berbasis Android”, J-PTIIK, vol. 1, no. 12, hlm. 1518–1525, Jul 2017.
