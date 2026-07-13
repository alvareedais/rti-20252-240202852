# WS-13: Data Preprocessing

> **Bab 13 — Preprocessing & Persiapan Data untuk Analisis**

---

## Ringkasan Materi

### Data Refinement Pipeline

```
Raw Data → Cleaning → Transformation → Normalization → Processed Data → Analysis Ready
```

Setiap tahap memiliki tujuan berbeda. **Preprocessing bukan langkah teknis biasa** — setiap keputusan preprocessing adalah keputusan riset yang bisa mengubah kesimpulan.

### Empat Prinsip Preprocessing

| Prinsip | Deskripsi |
|---------|----------|
| **Consistency** | Metode sama untuk data yang sama |
| **Transparency** | Setiap langkah terdokumentasi |
| **Reproducibility** | Orang lain bisa mengulang dengan hasil sama |
| **Minimal Distortion** | Ubah sesedikit mungkin; jika normalisasi tidak perlu, jangan lakukan |

### Cleaning Triad

| Masalah | Strategi | Risiko |
|---------|---------|--------|
| **Missing values** | | |
| — Listwise deletion | Missing < 5%, random | Data loss |
| — Mean/median imputation | Sedikit missing, dist. normal | Mengurangi variabilitas |
| — Model-based imputation | Banyak missing, pola sistematis | Introduces dependency |
| — Flag & separate | Missing karena alasan substantif | Kompleksitas analisis |
| **Duplikat** | Identifikasi → verifikasi → hapus | False positive (data mirip ≠ duplikat) |
| **Error format** | Standardisasi tipe, encoding | Kehilangan informasi saat konversi |

### Normalisasi — Kapan & Metode Mana

| Metode | Formula | Output | Sensitif Outlier? |
|--------|---------|--------|-------------------|
| Min-max | (x-min)/(max-min) | [0, 1] | Ya |
| Z-score | (x-mean)/std | Unbounded | Lebih robust |
| Robust scaling | (x-median)/IQR | Unbounded | Paling robust |

**Kunci:** Parameter normalisasi harus dihitung dari **training set saja** — bukan seluruh data. Pelanggaran = **data leakage**.

### Data Leakage Prevention

Data leakage terjadi ketika informasi dari test set "bocor" ke preprocessing:
- Normalisasi parameter dari seluruh dataset ← **SALAH**
- Cross-validation dilakukan sebelum split ← **SALAH**
- Feature selection menggunakan label test set ← **SALAH**

### Jebakan Kognitif

1. "Preprocessing cuma teknis — tidak perlu detail" → bisa ubah kesimpulan
2. "Lebih banyak preprocessing = lebih bersih = lebih baik" → over-processing distorsi data
3. "Normalisasi selalu diperlukan" → belum tentu, tergantung metode analisis
4. "Imputation sama untuk semua situasi" → strategi harus sesuai konteks

---

## Template A.13 — Preprocessing Documentation Log

```
PREPROCESSING LOG

Dataset           : RecSys 2020 E-commerce Dataset
Jumlah data awal  :
- Train : 11.495.242 records
- Validation : 2.466.048 records
- Test : 2.781.480 records

Cleaning

| Masalah | Jumlah Kasus | Penanganan | Justifikasi |
|----------|-------------:|------------|-------------|
| Missing value (brand) | 4.512 | Diisi dengan label "unknown" | Tidak mempengaruhi identitas produk dan menjaga konsistensi data |
| Missing value (category) | 1.276 | Dihapus | Jumlah kecil (<0.1%) sehingga tidak mempengaruhi distribusi |
| Duplikat | 325 | Dihapus | Merupakan duplikasi event yang sama |
| Error format | 0 | Tidak ada tindakan | Semua kolom memiliki tipe data sesuai |

Transformation

| Transformasi | Variabel | Detail | Alasan |
|--------------|----------|--------|--------|
| Konversi timestamp | event_time | String → Datetime | Memudahkan analisis waktu |
| Encoding kategori | event_type | cart=0, view=1, purchase=2 | Digunakan sebagai input model |
| Feature selection | product_id, user_id, event_type | Memilih fitur utama | Mengurangi fitur yang tidak digunakan |

Normalization

Metode    : Tidak dilakukan

Alasan    : Collaborative Filtering dan Content-Based Filtering tidak memerlukan normalisasi numerik karena rekomendasi dibangun berdasarkan interaksi pengguna dan representasi item.

Parameter : Tidak diterapkan

Leakage Check

[✓] Parameter preprocessing berasal dari training set
[✓] Tidak menggunakan informasi test set
[✓] Train-validation-test sudah dipisahkan sebelum preprocessing

Jumlah data akhir :
- Train : 11.489.129 records
- Validation : 2.464.772 records
- Test : 2.781.480 records

Script tersedia :
[✓] Ya → src/preprocessing.py
```

---

## Latihan 1 — Cleaning Plan

Periksa dataset Anda (atau dataset contoh) dan dokumentasikan masalah yang ditemukan.

| Masalah                     | Jumlah Kasus | Penanganan      | Justifikasi                       |
| --------------------------- | -----------: | --------------- | --------------------------------- |
| Missing value pada brand    |        4.512 | Diisi "unknown" | Menghindari kehilangan data       |
| Missing value pada category |        1.276 | Dihapus         | Jumlah sangat kecil               |
| Duplikat event              |          325 | Dihapus         | Mencegah bias pada data interaksi |


**Jumlah data sebelum cleaning:** 16.742.770 records
**Jumlah data setelah cleaning:** 16.742.469 records
**Persentase data yang hilang/berubah:** 0.004%

---

## Latihan 2 — Normalisasi Decision

Tentukan apakah data Anda perlu normalisasi, dan jika ya, metode apa yang tepat.

| Variabel   | Range Asli         | Distribusi   | Outlier | Metode            | Alasan                                       |
| ---------- | ------------------ | ------------ | ------- | ----------------- | -------------------------------------------- |
| Price      | 0.5–2574 USD       | Right-skewed | Ya      | Tidak dilakukan   | Tidak digunakan langsung sebagai fitur utama |
| Event Type | view/cart/purchase | Kategorikal  | Tidak   | Encoding          | Data kategorikal                             |
| Product ID | ID unik            | Nominal      | Tidak   | Tidak perlu       | Identifier                                   |
| User ID    | ID unik            | Nominal      | Tidak   | Tidak perlu       | Identifier                                   |
| Timestamp  | Datetime           | Time-series  | Tidak   | Konversi datetime | Analisis temporal                            |

**Apakah normalisasi diperlukan?** [ ] Ya / [✓] Tidak
**Justifikasi:**
> Penelitian menggunakan algoritma Collaborative Filtering dan Content-Based Filtering yang memanfaatkan hubungan antar pengguna dan item, bukan jarak antar fitur numerik. Oleh karena itu, normalisasi numerik tidak memberikan manfaat yang signifikan terhadap performa model.

**Leakage check:**
- [✓] Parameter dihitung dari training set
- [✓] Preprocessing dilakukan setelah train-validation-test split

---

## Latihan 3 — Preprocessing Report

Buat ringkasan preprocessing lengkap — dokumentasi yang cukup bagi orang lain untuk mereplikasi.

```
PREPROCESSING SUMMARY

1. Dataset
   RecSys 2020 E-commerce Dataset

2. Data awal
   16.742.770 records
   19 features

3. Cleaning
   - Missing values : 5.788 kasus
     Metode : imputasi ("unknown") dan deletion

   - Duplikat : 325 kasus
     Tindakan : dihapus

   - Error format : 0
     Tindakan : tidak diperlukan

4. Transformation
   - Konversi event_time menjadi datetime
   - Encoding event_type
   - Seleksi fitur yang digunakan model

5. Normalisasi
   Tidak dilakukan
   Parameter : -

6. Data akhir
   16.736.657 records
   19 features

7. Leakage Check
   [✓] Lulus
``` 

---

## Refleksi

> Apakah Anda pernah melakukan normalisasi "karena biasa dilakukan" tanpa mempertimbangkan apakah benar-benar diperlukan? Apa risiko over-preprocessing?

> Normalisasi tidak selalu diperlukan pada setiap penelitian. Penggunaannya harus disesuaikan dengan karakteristik algoritma yang digunakan. Pada penelitian ini, Collaborative Filtering dan Content-Based Filtering tidak memerlukan normalisasi numerik karena rekomendasi dibangun berdasarkan interaksi pengguna dan representasi item. Melakukan normalisasi tanpa alasan yang jelas dapat menyebabkan over-preprocessing, meningkatkan kompleksitas proses, bahkan berpotensi mengubah karakteristik data sehingga hasil penelitian menjadi kurang representatif.

> ___________________________________________________
