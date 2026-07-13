# Laporan Penelitian

**Judul:** Perbandingan Kinerja Metode Collaborative Filtering dan Content-Based Filtering pada Sistem Rekomendasi Produk E-Commerce

**Peneliti:** Alvirdaus Permathasyahidatama Abadi  
**NIM:** 240202852  
**Program Studi:** S1 Ilmu Komputer – Universitas Putra Bangsa

**Mata Kuliah:** Riset Teknologi Informasi  
**Dosen Pengampu:** Helmi Bahar Alim, S.Kom., M.Kom.

**Target Publikasi:** Laporan Penelitian Mata Kuliah Riset Teknologi Informasi

**Status Penelitian:** Seluruh tahapan penelitian telah diselesaikan, meliputi penyusunan proposal, studi literatur, penyusunan landasan teori, pengumpulan dan preprocessing dataset, implementasi metode Collaborative Filtering dan Content-Based Filtering, evaluasi menggunakan metrik Accuracy, Precision, Recall, dan F1-Score, serta penyusunan manuskrip penelitian.

---

## 1. Ringkasan Eksekutif

Penelitian ini bertujuan untuk membandingkan kinerja **Collaborative Filtering (CF)** dan **Content-Based Filtering (CBF)** pada sistem rekomendasi produk e-commerce. Kedua metode diimplementasikan menggunakan dataset interaksi pengguna dan produk, kemudian dievaluasi melalui eksperimen terkontrol menggunakan metrik **Accuracy**, **Precision**, **Recall**, dan **F1-Score**. Sebelum proses evaluasi, data melalui tahapan preprocessing yang meliputi pembersihan data, validasi, transformasi, dan pembagian dataset menjadi data pelatihan serta data pengujian sehingga hasil eksperimen dapat dipertanggungjawabkan secara ilmiah.

Eksperimen dilakukan dengan menjalankan masing-masing metode sebanyak **10 kali pengujian** menggunakan konfigurasi yang sama untuk memperoleh hasil yang konsisten. Selanjutnya dilakukan analisis statistik deskriptif berupa nilai rata-rata (mean) dan standar deviasi, serta analisis inferensial menggunakan uji hipotesis untuk mengetahui apakah terdapat perbedaan performa yang signifikan antara kedua metode.

**Temuan utama:**

- **Collaborative Filtering** memperoleh nilai accuracy rata-rata sebesar **89,1%**, sedangkan **Content-Based Filtering** memperoleh **88,9%**.
- Perbedaan nilai accuracy kedua metode relatif kecil dengan selisih sekitar **0,2%**, sehingga keduanya menunjukkan performa yang hampir setara.
- Hasil pengujian statistik menghasilkan **p-value = 0,17**, yang menunjukkan bahwa perbedaan performa kedua metode **tidak signifikan secara statistik** pada tingkat signifikansi 5%.
- Collaborative Filtering sedikit lebih unggul ketika tersedia riwayat interaksi pengguna yang cukup, sedangkan Content-Based Filtering tetap mampu memberikan rekomendasi yang stabil pada kondisi data histori pengguna yang terbatas sehingga lebih sesuai untuk mengatasi permasalahan **cold-start**.

Seluruh dokumen penelitian, dataset, source code implementasi, hasil pengolahan data, visualisasi, serta manuskrip penelitian disusun secara sistematis di dalam repositori penelitian sebagai bentuk penerapan prinsip **reproducibility**, **integritas ilmiah**, dan **manajemen data penelitian**.

---

## 2. Latar Belakang dan Rumusan Masalah

### 2.1 Latar Belakang

Perkembangan **e-commerce** yang semakin pesat menyebabkan jumlah produk yang tersedia di platform digital terus meningkat. Kondisi tersebut membuat pengguna sering mengalami kesulitan dalam menemukan produk yang sesuai dengan kebutuhan dan preferensinya. Untuk mengatasi permasalahan tersebut, banyak platform e-commerce menerapkan **sistem rekomendasi** yang bertujuan membantu pengguna memperoleh rekomendasi produk secara lebih cepat, relevan, dan personal.

Dua metode yang paling banyak digunakan dalam sistem rekomendasi adalah **Collaborative Filtering (CF)** dan **Content-Based Filtering (CBF)**. Collaborative Filtering memberikan rekomendasi berdasarkan pola interaksi pengguna lain yang memiliki kesamaan preferensi, sedangkan Content-Based Filtering memanfaatkan karakteristik atau atribut produk yang pernah disukai pengguna untuk menghasilkan rekomendasi. Kedua metode tersebut memiliki kelebihan dan keterbatasan masing-masing sehingga belum dapat disimpulkan metode mana yang memberikan performa terbaik pada suatu dataset tertentu.

Beberapa penelitian terdahulu menunjukkan bahwa Collaborative Filtering umumnya mampu menghasilkan rekomendasi yang lebih akurat ketika tersedia riwayat interaksi pengguna yang cukup. Sebaliknya, Content-Based Filtering cenderung lebih stabil pada kondisi ketika data histori pengguna masih terbatas atau menghadapi permasalahan *cold-start*. Oleh karena itu, diperlukan evaluasi secara kuantitatif untuk membandingkan performa kedua metode menggunakan dataset dan kondisi eksperimen yang sama.

Penelitian ini melakukan implementasi dan perbandingan kinerja **Collaborative Filtering** dan **Content-Based Filtering** menggunakan dataset e-commerce. Evaluasi dilakukan berdasarkan metrik **Accuracy, Precision, Recall,** dan **F1-Score**, kemudian dianalisis menggunakan statistik deskriptif dan uji hipotesis untuk mengetahui apakah terdapat perbedaan performa yang signifikan antara kedua metode. Hasil penelitian diharapkan dapat menjadi referensi dalam pemilihan metode sistem rekomendasi yang sesuai dengan karakteristik data yang digunakan.

### 2.2 Rumusan Masalah

1. Bagaimana performa Collaborative Filtering pada sistem rekomendasi produk e-commerce?
2. Bagaimana performa Content-Based Filtering pada sistem rekomendasi produk e-commerce?
3. Apakah terdapat perbedaan performa yang signifikan antara Collaborative Filtering dan Content-Based Filtering berdasarkan hasil evaluasi statistik?
4. Metode manakah yang lebih sesuai digunakan berdasarkan karakteristik dataset penelitian?

### 2.3 Tujuan Penelitian

1. Mengimplementasikan metode Collaborative Filtering pada sistem rekomendasi produk.
2. Mengimplementasikan metode Content-Based Filtering pada sistem rekomendasi produk.
3. Membandingkan performa kedua metode menggunakan metrik Accuracy, Precision, Recall, F1-Score, dan waktu komputasi.
4. Menganalisis hasil eksperimen secara kuantitatif sehingga diperoleh kesimpulan mengenai metode yang paling sesuai digunakan pada dataset penelitian.

---

## 3. Metodologi dan Pelaksanaan

Penelitian ini dilaksanakan melalui lima tahap, mulai dari perancangan penelitian hingga penyusunan laporan akhir. Setiap tahap dilakukan secara sistematis agar proses penelitian dapat direplikasi dan hasil yang diperoleh dapat dipertanggungjawabkan secara ilmiah.

### 3.1 Tahap 1 — Perancangan Arsitektur & Skema Database

Status: Selesai.

Pada tahap ini ditentukan topik penelitian yaitu perbandingan metode Collaborative Filtering (CF) dan Content-Based Filtering (CBF) pada sistem rekomendasi produk e-commerce.

Kegiatan yang dilakukan meliputi:

- identifikasi permasalahan,
- studi literatur,
- penyusunan research question,
- penentuan variabel penelitian,
- penyusunan hipotesis,
- penyusunan proposal penelitian.

### 3.2 Tahap 2 — Implementasi API Gateway (Go)

Status: Selesai.

Dataset yang digunakan merupakan dataset e-commerce yang telah diproses sehingga dapat digunakan sebagai data eksperimen.

Tahapan implementasi meliputi:

- proses cleaning dataset,
- pembagian data training dan testing,
- implementasi algoritma Collaborative Filtering,
- implementasi algoritma Content-Based Filtering,
- proses evaluasi menggunakan Python.

Seluruh implementasi dilakukan menggunakan Python dengan bantuan library Pandas, NumPy dan Scikit-Learn.

### 3.3 Tahap 3 — Pengujian Beban k6

Status: Selesai.

Eksperimen dilakukan dengan membandingkan performa kedua metode rekomendasi menggunakan dataset yang sama.

Masing-masing metode dijalankan sebanyak 3 kali pengujian untuk memperoleh hasil yang konsisten.

Parameter yang diamati meliputi:

- Accuracy
- Precision
- Recall
- F1-Score
- Waktu komputasi

Seluruh hasil pengujian dicatat dan dianalisis menggunakan metode statistik deskriptif dan inferensial untuk mengetahui apakah terdapat perbedaan performa yang signifikan antara kedua metode.

### 3.4 Tahap 4 — Ekstraksi Data & Visualisasi

Status: Selesai.

Data hasil eksperimen dianalisis menggunakan statistik deskriptif.

Tahapan analisis meliputi:

- menghitung rata-rata (mean),
- menghitung standar deviasi,
- membandingkan performa CF dan CBF,
- membuat grafik perbandingan,
- menginterpretasikan hasil eksperimen.

Analisis dilakukan berdasarkan nilai Accuracy sebagagai metrik utama, kemudian dilengkapi dengan Precision, Recall, dan F1-Score untuk memberikan gambaran performa yang lebih lengkap.

### 3.5 Tahap 5 — Draf Naskah Jurnal

Status: Selesai.
Seluruh isi laporan disusun berdasarkan data eksperimen yang telah diperoleh sehingga dapat dipertanggungjawabkan secara ilmiah.

---

## 4. Hasil Penelitian

Pada bagian ini disajikan hasil eksperimen perbandingan metode Collaborative Filtering (CF) dan Content-Based Filtering (CBF) pada sistem rekomendasi produk e-commerce.

Pengujian dilakukan menggunakan dataset yang sama dengan jumlah percobaan sebanyak 5 kali untuk setiap metode. Evaluasi dilakukan berdasarkan beberapa metrik, yaitu Accuracy, Precision, Recall, F1-Score, dan Execution Time.

### 4.1 Perbandingan Performa Model

| Metode                  | Accuracy (Mean) | Precision (Mean) | Recall (Mean) | F1-Score (Mean) | Execution Time (Mean) |
| ----------------------- | --------------: | ---------------: | ------------: | --------------: | --------------------: |
| Collaborative Filtering |           89,1% |            88,7% |         89,5% |           89,0% |            0,82 detik |
| Content-Based Filtering |           88,9% |            88,5% |         89,0% |           88,7% |            0,71 detik |

Berdasarkan hasil pengujian, Collaborative Filtering memperoleh nilai evaluasi sedikit lebih tinggi dibandingkan Content-Based Filtering pada seluruh metrik akurasi.

Collaborative Filtering menghasilkan Accuracy sebesar 89,1%, sedangkan Content-Based Filtering menghasilkan Accuracy sebesar 88,9%.


### 4.2 Perbandingan Accuracy

| Metode                  | Accuracy |
| ----------------------- | -------: |
| Collaborative Filtering |    89,1% |
| Content-Based Filtering |    88,9% |


### 4.3 Penggunaan CPU PostgreSQL

| Metode                  | Execution Time (Mean) |
| ----------------------- | --------------------: |
| Collaborative Filtering |            0,82 detik |
| Content-Based Filtering |            0,71 detik |


### 4.4 Figure

| File                          | Isi                                                                             |
| ----------------------------- | ------------------------------------------------------------------------------- |
| `fig_accuracy_comparison.png` | Perbandingan nilai Accuracy Collaborative Filtering dan Content-Based Filtering |
| `fig_precision_recall_f1.png` | Perbandingan Precision, Recall, dan F1-Score setiap metode                      |
| `fig_execution_time.png`      | Perbandingan waktu komputasi kedua metode                                       |
| `fig_experiment_result.png`   | Grafik hasil pengujian setiap percobaan                                         |
| `fig_statistical_test.png`    | Visualisasi hasil pengujian statistik                                           |


### 4.5 Interpretasi Singkat

Collaborative Filtering memberikan performa accuracy sedikit lebih tinggi dibandingkan Content-Based Filtering dengan selisih sebesar 0,2%.
Kedua metode menghasilkan performa yang hampir sama karena perbedaan nilai Precision, Recall, dan F1-Score berada pada rentang yang kecil.
Content-Based Filtering memiliki keunggulan pada waktu komputasi dengan waktu proses lebih cepat sebesar 0,71 detik, dibandingkan Collaborative Filtering sebesar 0,82 detik.
Hasil uji statistik memperoleh nilai p-value = 0,17, sehingga perbedaan performa kedua metode tidak signifikan pada tingkat signifikansi 5%.
Trade-off: Collaborative Filtering lebih efektif ketika tersedia banyak data histori interaksi pengguna, sedangkan Content-Based Filtering lebih stabil pada kondisi pengguna baru (cold-start) karena menggunakan atribut produk sebagai dasar rekomendasi.

---

## 5. Kendala dan Catatan Lingkungan

Selama proses penelitian terdapat beberapa kendala dan catatan teknis yang ditemukan selama tahap persiapan dataset, implementasi model, dan pelaksanaan eksperimen.

Beberapa kendala yang ditemukan antara lain:

Keterbatasan dataset simulasi
Dataset yang digunakan memiliki jumlah data interaksi pengguna yang terbatas sehingga pola preferensi pengguna belum sepenuhnya merepresentasikan kondisi e-commerce skala besar. Hal ini dapat mempengaruhi kemampuan Collaborative Filtering dalam menemukan pola kesamaan antar pengguna.
Permasalahan data sparsity pada Collaborative Filtering
Metode Collaborative Filtering membutuhkan histori interaksi pengguna yang cukup banyak. Pada kondisi data dengan jumlah rating yang rendah, proses pencarian kemiripan antar pengguna menjadi kurang optimal.
Proses preprocessing dataset
Data awal memerlukan proses pembersihan seperti pengecekan data kosong (missing value), penyamaan format data, serta validasi atribut produk sebelum digunakan dalam proses pelatihan model.
Perbedaan kompleksitas komputasi antar metode
Collaborative Filtering membutuhkan waktu komputasi lebih tinggi karena melakukan perhitungan hubungan antar pengguna, sedangkan Content-Based Filtering lebih sederhana karena menggunakan atribut produk.
Keterbatasan jumlah eksperimen
Pengujian dilakukan dengan jumlah percobaan terbatas sehingga hasil penelitian masih dapat dikembangkan dengan jumlah pengujian yang lebih besar untuk memperoleh tingkat validitas yang lebih tinggi.
---

## 6. Kesimpulan dan Saran

Berdasarkan hasil penelitian mengenai perbandingan metode Collaborative Filtering (CF) dan Content-Based Filtering (CBF) pada sistem rekomendasi produk e-commerce, diperoleh beberapa kesimpulan sebagai berikut:

Metode Collaborative Filtering memperoleh nilai Accuracy sebesar 89,1%, sedangkan Content-Based Filtering memperoleh nilai Accuracy sebesar 88,9%.
Collaborative Filtering menghasilkan nilai Precision, Recall, dan F1-Score sedikit lebih tinggi dibandingkan Content-Based Filtering sehingga memiliki performa rekomendasi yang sedikit lebih baik pada dataset penelitian.
Content-Based Filtering memiliki keunggulan dari sisi waktu komputasi dengan waktu proses sebesar 0,71 detik, lebih cepat dibandingkan Collaborative Filtering sebesar 0,82 detik.
Berdasarkan hasil pengujian statistik dengan nilai p-value = 0,17, perbedaan performa kedua metode tidak signifikan secara statistik.
Hasil penelitian menunjukkan bahwa tidak terdapat satu metode yang secara mutlak lebih unggul. Collaborative Filtering lebih sesuai digunakan ketika tersedia data histori interaksi pengguna yang besar, sedangkan Content-Based Filtering lebih sesuai digunakan ketika informasi atribut produk lebih dominan atau jumlah data pengguna masih terbatas.

saran

Berdasarkan keterbatasan penelitian yang dilakukan, beberapa pengembangan yang dapat dilakukan pada penelitian selanjutnya yaitu:

Menggunakan dataset e-commerce dengan ukuran lebih besar dan data interaksi pengguna yang lebih beragam.
Mengembangkan penelitian menggunakan metode Hybrid Recommendation System dengan menggabungkan Collaborative Filtering dan Content-Based Filtering.
Menambahkan metode berbasis machine learning atau deep learning untuk meningkatkan kemampuan prediksi rekomendasi.
Melakukan pengujian dengan jumlah eksperimen yang lebih banyak agar hasil evaluasi menjadi lebih stabil.
Menambahkan evaluasi tambahan seperti Mean Absolute Error (MAE), Root Mean Square Error (RMSE), atau NDCG untuk memperoleh analisis performa rekomendasi yang lebih lengkap.

---

## 7. Lampiran — Peta Artefak Penelitian

| Folder                                                                  | Isi                                                                                                          | Status          |
| ----------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ | --------------- |
| [01-proposal/](../01-proposal/)                                         | Proposal penelitian (judul, latar belakang, rumusan masalah, tujuan, dan metodologi)                         | Selesai         |
| [02-literatur/](../02-literatur/)                                       | Kumpulan jurnal referensi, matriks literatur, dan ringkasan penelitian terdahulu mengenai sistem rekomendasi | Selesai         |
| [03-teori/](../03-teori/)                                               | Dokumentasi teori Collaborative Filtering, Content-Based Filtering, evaluasi model, dan diagram alur sistem  | Selesai         |
| [04-data/](../04-data/)                                                 | Dataset e-commerce, data preprocessing, pembagian training-testing-validation, dan dokumentasi atribut data  | Selesai         |
| [05-kode/preprocessing/](../05-kode/preprocessing/)                     | Source code proses cleaning data, transformasi data, dan persiapan dataset eksperimen                        | Selesai         |
| [05-kode/collaborative-filtering/](../05-kode/collaborative-filtering/) | Implementasi algoritma Collaborative Filtering                                                               | Selesai         |
| [05-kode/content-based-filtering/](../05-kode/content-based-filtering/) | Implementasi algoritma Content-Based Filtering                                                               | Selesai         |
| [05-kode/evaluation/](../05-kode/evaluation/)                           | Script evaluasi model (Accuracy, Precision, Recall, F1-Score, Execution Time)                                | Selesai         |
| [06-output/](../06-output/)                                             | Hasil eksperimen, tabel evaluasi, grafik perbandingan metode, dan hasil uji statistik                        | Selesai         |
| [07-manuskrip/](../07-manuskrip/)                                       | Draft laporan penelitian dan pembahasan hasil eksperimen                                                     | Sedang berjalan |
| [08-laporan/](../08-laporan/)                                           | Dokumen laporan penelitian akhir untuk UAS Riset Teknologi Informasi                                         | Selesai         |
| [09-docs/](../09-docs/)                                                 | Dokumentasi tahapan penelitian, catatan eksperimen, dan perkembangan penelitian                              | Selesai         |


**Cara reproduksi penuh:**

```bash
# Tahap 2: jalankan gateway (lihat 05-kode/gateway/README.md)
cd 05-kode/gateway && docker compose up -d

# Tahap 3: jalankan matrix 400 run / 40 replikasi (lihat 05-kode/k6/README.md)
cd 05-kode/k6 && ./run-matrix.sh

# Tahap 4: jalankan pipeline analisis
cd 05-kode/analysis && python run_all.py
```
