# WS-12: Result Presentation & Visualization

> **Bab 12 — Penyajian Hasil & Visualisasi**

---

## Ringkasan Materi

### Data → Insight Model

```
Validated Data → Structured Presentation → Visualization → Pattern Recognition → Insight
```

Penyajian **mendahului** analisis. Tabel dan grafik membantu peneliti "melihat" data sebelum menghitung. Langsung ke uji statistik tanpa visualisasi berisiko kesimpulan yang secara teknis benar tapi kontekstual salah (Anscombe's Quartet, 1973).

### Tabel = Presisi, Grafik = Pola

Keduanya **saling melengkapi**:
- Tabel: angka presisi, self-contained (dipahami tanpa teks), sortable
- Grafik: pola visual, tren, perbandingan cepat

### Jenis Grafik Berdasarkan Tujuan

| Tujuan | Jenis Grafik |
|--------|-------------|
| Perbandingan antar-skenario | Bar chart (grouped/stacked) |
| Distribusi per-skenario | Box plot / violin plot |
| Tren temporal | Line chart |
| Korelasi dua variabel | Scatter plot |
| Proporsi (total = 100%) | Pie chart (hati-hati!) |

### Contoh Tabel Hasil yang Baik

| Model | Accuracy (%) | F1-Score (%) | Training Time (min) |
|-------|-------------|-------------|---------------------|
| BERT | 88.4 ± 1.2 | 87.1 ± 1.4 | 45.2 ± 3.1 |
| LSTM | 86.1 ± 1.8 | 84.5 ± 2.0 | 12.8 ± 1.2 |
| SVM | 82.3 ± 0.9 | 80.7 ± 1.1 | 0.3 ± 0.1 |

*N=10 per model. Mean ± std. Diurutkan berdasarkan Accuracy.*

### Visualization Bias — Yang Harus Dihindari

| Bias | Deskripsi | Dampak |
|------|----------|--------|
| Truncated axis | Y tidak dari 0 | Memperbesar perbedaan kecil |
| Inconsistent scale | Dua grafik skala beda | Perbandingan menyesatkan |
| Cherry-picked data | Hanya tampilkan yang "menang" | Selektif, tidak jujur |
| 3D effects | Efek 3D tanpa dimensi data ke-3 | Distorsi tanpa informasi |
| Missing error bar | Tidak ada variabilitas | Menyembunyikan ketidakpastian |

### Engineering vs Research Presentation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan grafik | Dashboard monitoring | Mendukung argumen ilmiah |
| Informasi wajib | KPI, threshold | Mean, std, CI, N, p-value |
| Bias handling | Less critical | Wajib dihindari (peer-review) |

---

## Template A.12 — Result Presentation Plan

```
RESULT PRESENTATION PLAN

Research Question :
Bagaimana perbandingan performa Collaborative Filtering dan Content-Based Filtering pada dataset RecSys 2020 E-commerce Dataset?

Metrik Utama :
Accuracy (%)

Tabel Hasil:

| Skenario                | Accuracy (mean ± std) | F1-Score (mean ± std) | n |
|--------------------------|----------------------:|----------------------:|--:|
| Collaborative Filtering  | 90.0 ± 0.3 %          | 89.3 ± 0.4 %          | 5 |
| Content-Based Filtering  | 88.7 ± 0.4 %          | 88.0 ± 0.5 %          | 5 |

Visualisasi yang Direncanakan:

| # | Jenis Grafik | Pesan Utama | Metrik |
|---|--------------|-------------|--------|
| 1 | Bar Chart + Error Bar | Membandingkan performa kedua metode | Mean Accuracy ± Std |
| 2 | Box Plot | Menunjukkan distribusi Accuracy tiap metode | Accuracy seluruh run |
| 3 | Scatter Plot | Hubungan Accuracy dengan waktu komputasi | Accuracy vs Execution Time |

Bias Check:
[✓] Y-axis mulai dari 0
[✓] Error bar ditampilkan
[✓] Semua data disertakan
[✓] Tidak menggunakan efek 3D
```

---

## Latihan 1 — Tabel Hasil

Buat tabel hasil eksperimen Anda (boleh dengan data simulasi jika belum punya data riil).

| Skenario                | Accuracy (mean ± std) | F1-Score (mean ± std) |     n |
| ----------------------- | --------------------: | --------------------: | ----: |
| Collaborative Filtering |      **90.0 ± 0.3 %** |      **89.3 ± 0.4 %** | **5** |
| Content-Based Filtering |      **88.7 ± 0.4 %** |      **88.0 ± 0.5 %** | **5** |


**Checklist tabel:**
- [✓] Self-contained (judul jelas, satuan ada, N tercantum)
- [✓] Mean ± std
- [✓] Diurutkan berdasarkan Accuracy
- [✓] Format konsisten

---

## Latihan 2 — Rencana Visualisasi

Rencanakan 2-3 grafik untuk menyajikan data dari Latihan 1. Setiap grafik = satu pesan.

| # | Jenis Grafik          | Pesan                                                                      | Data yang Digunakan         |
| - | --------------------- | -------------------------------------------------------------------------- | --------------------------- |
| 1 | Bar Chart + Error Bar | Membandingkan Accuracy Collaborative Filtering dan Content-Based Filtering | Mean Accuracy ± Std         |
| 2 | Box Plot              | Menampilkan distribusi Accuracy pada setiap run eksperimen                 | Seluruh nilai Accuracy      |
| 3 | Scatter Plot          | Menganalisis hubungan Accuracy dengan waktu komputasi                      | Accuracy dan Execution Time |

---

## Latihan 3 — Bias Detection

Evaluasi visualisasi berikut untuk bias (skenario dari contoh):

**Skenario:** Collaborative Filtering = 90.0%, Content-Based Filtering = 88.7%. Grafik batang menggunakan sumbu-Y mulai dari 88%.

| Pertanyaan                        | Jawaban                                                                                                                             |
| --------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Apakah Y-axis menyesatkan?        | **Ya.** Perbedaan terlihat jauh lebih besar padahal selisih sebenarnya hanya sekitar **1,3%**.                                      |
| Apakah error bar ditampilkan?     | **Belum**, sehingga variasi hasil eksperimen tidak terlihat.                                                                        |
| Apakah semua kondisi ditampilkan? | **Ya**, kedua metode dibandingkan secara bersamaan.                                                                                 |
| Apa solusinya?                    | Gunakan sumbu-Y mulai dari **0%** atau berikan alasan jika dipotong, serta tambahkan **error bar** untuk menunjukkan variasi hasil. |

**Evaluasi grafik Anda sendiri dari Latihan 2:**
- [✓] Semua bias check lulus
- [ ] Ada yang perlu diperbaiki: ____

---

## Refleksi

> Mengapa tabel dan grafik keduanya diperlukan — tidak cukup salah satu saja? Pernahkah Anda membuat grafik yang (tanpa sengaja) menyesatkan?

> Tabel dan grafik memiliki fungsi yang saling melengkapi. Tabel menyajikan nilai numerik secara rinci dan presisi sehingga memudahkan pembaca melihat hasil pengukuran setiap metrik. Grafik memudahkan identifikasi pola, tren, dan perbandingan antar-metode secara visual. Penggunaan keduanya membuat hasil penelitian lebih mudah dipahami sekaligus mengurangi risiko kesalahan interpretasi. Selain itu, penyusunan grafik harus memperhatikan skala sumbu, error bar, dan penyajian seluruh data agar tidak menimbulkan bias visual.

> ___________________________________________________
