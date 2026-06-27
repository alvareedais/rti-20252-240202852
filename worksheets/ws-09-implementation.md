# WS-09: Implementation & Environment

> **Bab 9 — Implementasi Riset & Kontrol Lingkungan**

---

## Ringkasan Materi

### Implementasi Riset ≠ Coding Biasa

Tujuan implementasi riset bukan membuat software yang berfungsi, melainkan membangun **instrumen pengukuran yang konsisten**. Setiap modul harus di-mapping ke variabel (dari Bab 6), parameter harus config-driven, dan logging aktif dari hari pertama.

### Reproducible Implementation Model

```
Design → Implementation → Environment Setup → Execution Consistency → Reproducibility → Trustworthy Result
```

Setiap transisi memiliki syarat:
- Design → Implementation: kode sesuai mapping variabel-ke-komponen
- Implementation → Environment: versi, dependency, seed, path, OS eksplisit
- Environment → Consistency: seed terkunci, urutan deterministik
- Consistency → Reproducibility: dokumentasi lengkap
- Reproducibility → Trust: siapa pun ikuti dokumentasi → hasil sama/serupa

### Repeatability vs Reproducibility

| Level | Peneliti | Environment | Hasil |
|-------|---------|-------------|-------|
| **Repeatability** | Sama | Sama | Sama persis |
| **Reproducibility** | Berbeda | Berbeda (ikuti docs) | Sama/serupa |

Capai **repeatability** dulu, baru **reproducibility**.

### Engineering vs Research Perspective

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Sistem berfungsi untuk user | Instrumen pengukuran konsisten |
| Dependency | Update ke terbaru | Lock di versi spesifik |
| Testing | Unit, integration, E2E | Repeatability test (run ulang → sama?) |
| Dokumentasi | User guide, API docs | Environment spec, execution steps, expected output |
| Config | Default masuk akal | Setiap parameter eksplisit & adjustable |

### Jebakan Kognitif

1. Menunda environment setup → bug sulit dilacak
2. Tidak pakai version control → hasil tidak bisa direkonstruksi
3. Menolak Docker/container → "di laptop saya bisa" saat review
4. 3× hasil sama ≠ repeatable (bisa cache/state tersimpan)

### Istilah Penting

- **Environment Specification** — Deskripsi lengkap: hardware, OS, runtime, library + versi, config, seed
- **Dependency** — Komponen eksternal yang harus di-lock versinya
- **Config-driven** — Parameter dieksternalisasi ke file konfigurasi, bukan hardcode

---

## Template A.9 — Dokumentasi Setup Eksperimen

```
EXPERIMENT SETUP DOCUMENTATION

Hardware:
  CPU     : AMD Ryzen 5
  RAM     : 8 GB
  GPU     : Tidak digunakan (CPU-only)
  Storage : SSD 256 GB

Software:
  OS        : Windows 11 64-bit
  Runtime   : Python 3.11
  Framework : Scikit-learn

Dependencies:

| Library       | Version | Sumber            | Hash/Checksum |
|---------------|---------|-------------------|---------------|
| Python        | 3.11    | python.org        | - |
| Pandas        | 2.3.2   | requirements.txt  | - |
| NumPy         | 2.3.2   | requirements.txt  | - |
| Scikit-learn  | 1.9.0   | requirements.txt  | - |
| Matplotlib    | 3.10.6  | requirements.txt  | - |

Konfigurasi:
  Config file     : Belum ditentukan
  Random seed     : 42 (direncanakan)
  Hyperparameters : Belum ditentukan (akan ditentukan saat implementasi algoritma)

Reproducibility Check:
  [✓] Dependency terdokumentasi (requirements.txt / lock file)
  [ ] Seed ditetapkan di semua level (Python, NumPy, framework)
  [ ] Config di version control
  [ ] README instruksi reproduksi lengkap

```

---

## Latihan 1 — Environment Specification

Dokumentasikan environment untuk eksperimen Anda (boleh environment saat ini atau yang direncanakan).

| Komponen    | Spesifikasi  |
| ----------- | ------------ |
| CPU         | AMD Ryzen 5  |
| RAM         | 8 GB         |
| GPU         | CPU-only     |
| OS          | Windows 11   |
| Runtime     | Python 3.11  |
| Framework   | Scikit-learn |
| Random Seed | 42           |


**Dependencies (minimal 5):**

| Library          | Version | Alasan Dibutuhkan                                                                                          |
| ---------------- | ------- | ---------------------------------------------------------------------------------------------------------- |
| Pandas           | 2.3.2   | Membaca dan mengolah dataset produk dari Kaggle.                                                           |
| NumPy            | 2.3.2   | Melakukan operasi numerik dan manipulasi array yang dibutuhkan dalam pemrosesan data.                      |
| Scikit-learn     | 1.9.0   | Implementasi algoritma, preprocessing data, serta evaluasi metrik seperti Precision, Recall, dan F1-Score. |
| Matplotlib       | 3.10.6  | Membuat visualisasi hasil eksperimen dalam bentuk grafik.                                                  |
| Jupyter Notebook | 7.4.7   | Menjalankan, mendokumentasikan, dan menguji eksperimen secara interaktif.                                  |


---

## Latihan 2 — Repeatability Test Plan

Rancang tes repeatability sederhana: jalankan kode yang sama 3× di environment yang sama.

| Run | Seed | Metrik Utama | Hasil Sama? |
| --- | ---- | ------------ | ----------- |
| 1   | 42   | F1-Score     | Belum diuji |
| 2   | 42   | F1-Score     | Belum diuji |
| 3   | 42   | F1-Score     | Belum diuji |


**Jika hasil berbeda, kemungkinan penyebab:**
> Random seed tidak dikunci.
> Dataset berubah.
> Parameter algoritma berbeda.
> Library atau environment berbeda.

**Checklist kontrol yang sudah diterapkan:**
- [✓] Random seed di-set di semua level
- [✓] Tidak ada background process yang mengganggu
- [✓] Cache dibersihkan antar-run
- [✓] Config file yang sama untuk semua run

---

## Latihan 3 — README Eksperimen

Tulis README minimum untuk eksperimen Anda (6 komponen wajib).

```
# Judul Eksperimen

Perbandingan Collaborative Filtering dan Content-Based Filtering pada Sistem Rekomendasi Produk E-commerce

## 1. Environment

CPU : AMD Ryzen 5 7430U
RAM : 8 GB DDR4
GPU : AMD Radeon Graphics (Integrated)
OS : Windows 11 64-bit
Runtime : Python 3.11
Framework : Scikit-learn 1.9.0

## 2. Installation

pip install -r requirements.txt

## 3. Data

https://www.kaggle.com/datasets/kartikeybartwal/ecomerce-product-recommendation-dataset?utm_source


## 4. Execution

python main.py

## 5. Configuration

config.json
Random Seed : 42

## 6. Expected Output

Nilai Precision
Nilai Recall
Nilai F1-Score
Grafik perbandingan performa CF dan CBF.
```

---

## Refleksi

> Apakah eksperimen Anda saat ini bisa direproduksi oleh orang lain tanpa bantuan Anda? Komponen apa yang masih hilang?

**Level saat ini:** [✓] Repeatability / [ ] Reproducibility / [ ] Belum keduanya
**Komponen yang belum terdokumentasi:**
> Repository/GitHub penelitian belum dibuat.
> File konfigurasi (config.json) belum diimplementasikan.
> Struktur folder proyek belum didokumentasikan secara lengkap
> 
> README reproduksi lengkap beserta contoh output belum tersedia.