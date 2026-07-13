# WS-14: Analysis, Interpretation & Failure Analysis

> **Bab 14 — Analisis Data, Interpretasi & Failure Analysis**

---

## Ringkasan Materi

### Data → Knowledge Model

```
Data → Analysis → Interpretation → Explanation → Knowledge
```

Tiga level yang berbeda:
- **Analysis** — "Apa yang terjadi?" (deskriptif + inferensial)
- **Interpretation** — "Apa artinya?" (konteks RQ + literatur)
- **Failure Analysis** — "Mengapa tidak berhasil?" (boundary conditions)

### Beyond p-value

**Statistical significance ≠ practical significance.** Selalu laporkan:
1. p-value (signifikansi statistik)
2. Effect size (besarnya efek)
3. Confidence interval (rentang ketidakpastian)

| Effect Size (Cohen's d) | Interpretasi |
|-------------------------|-------------|
| < 0.2 | Small |
| 0.2 – 0.8 | Medium |
| > 0.8 | Large |

### Pemilihan Uji Statistik

| Kondisi | Uji yang Tepat |
|---------|---------------|
| 2 grup, normal, paired | Paired t-test |
| 2 grup, non-normal | Wilcoxon signed-rank |
| > 2 grup, normal | One-way ANOVA + post-hoc |
| > 2 grup, non-normal | Kruskal-Wallis + post-hoc |
| 2 variabel kontinu | Pearson (normal) / Spearman (rank) |

### Failure Analysis as Contribution

Hipotesis yang ditolak adalah **temuan yang berharga**:

| Dataset | New (F1) | Baseline (F1) | p-value | Cohen's d |
|---------|---------|--------------|---------|-----------|
| DS-1 (small, clean) | 94.2±1.1 | 89.3±1.5 | <0.001 | **3.7** |
| DS-4 (medium, noisy) | 78.3±3.2 | 82.1±2.8 | 0.008 | **-1.3** |
| DS-5 (large, noisy) | 71.6±4.1 | 80.5±3.0 | <0.001 | **-2.5** |

**Insight:** Metode baru unggul di data bersih tapi gagal di data noisy → asumsi Gaussian dilanggar → **boundary condition** ditemukan → hybrid approach direkomendasikan.

**Partial failure + deep analysis = kontribusi lebih kaya daripada full success tanpa analisis.**

### Limitation Types

| Jenis | Contoh |
|-------|--------|
| Internal validity | Confounders yang tidak dikontrol |
| External validity | Generalisasi ke domain lain |
| Construct validity | Metrik mengukur apa yang dimaksud? |
| Statistical limitation | Sample size, asumsi distribusi |

### Jebakan Kognitif

1. "Signifikan statistik = penting secara praktis" → cek effect size
2. "Hipotesis tidak didukung → cari sudut baru" → p-hacking
3. "Kegagalan tidak perlu dilaporkan detail" → missed insight
4. "Limitasi cukup disebutkan, tidak perlu dianalisis" → kedalaman hilang

---

## Template A.14 — Analysis & Interpretation Report

```
ANALYSIS & INTERPRETATION

1. Statistik Deskriptif

| Skenario | Mean | Std | Median | Min | Max | n |
|-----------|------|------|--------|------|------|---|
| Collaborative Filtering | 90.0 | 0.3 | 90.0 | 89.6 | 90.4 | 5 |
| Content-Based Filtering | 88.7 | 0.4 | 88.7 | 88.2 | 89.2 | 5 |

2. Uji Hipotesis

Uji yang digunakan :
Independent Sample t-test

Justifikasi :
Penelitian membandingkan dua metode rekomendasi yang berbeda menggunakan nilai Accuracy dari beberapa run independen.

Hasil :
p = 0.021

Effect size (Cohen's d)
= 1.12

Confidence Interval 95%
= [0.32 ; 2.28]

3. Keputusan

☑ H0 ditolak

☑ H1 diterima

4. Interpretasi

Hubungan ke RQ

Collaborative Filtering menghasilkan akurasi yang lebih tinggi dibandingkan Content-Based Filtering pada dataset RecSys 2020.

Practical significance

Perbedaan rata-rata sekitar 1,3% cukup berarti untuk sistem rekomendasi karena dapat meningkatkan relevansi produk yang direkomendasikan kepada pengguna.

Perbandingan literatur

Hasil ini sejalan dengan penelitian sebelumnya yang menunjukkan bahwa Collaborative Filtering memiliki performa lebih baik ketika tersedia data interaksi pengguna yang cukup banyak.

5. Limitation

| Jenis | Ancaman | Dampak | Mitigasi |
|--------|----------|---------|----------|
| Statistical | Jumlah run hanya 5 | Variasi belum sepenuhnya terwakili | Menambah jumlah eksperimen |
| External Validity | Hanya menggunakan satu dataset | Generalisasi terbatas | Menguji dataset lain |
| Construct | Evaluasi hanya Accuracy dan F1 | Belum mencakup seluruh aspek rekomendasi | Menambahkan Precision@K dan Recall@K |

6. Failure Analysis

Tidak dilakukan karena hipotesis diterima.
```

---

## Latihan 1 — Pemilihan Uji Statistik

Tentukan uji statistik yang tepat untuk eksperimen Anda.

| Pertanyaan                        | Jawaban                                                                                        |
| --------------------------------- | ---------------------------------------------------------------------------------------------- |
| Berapa grup yang dibandingkan?    | **2 (Collaborative Filtering dan Content-Based Filtering)**                                    |
| Apakah data berpasangan (paired)? | **Tidak**                                                                                      |
| Apakah distribusi normal?         | **Diasumsikan normal (dummy)**                                                                 |
| **Uji yang dipilih**              | **Independent Sample t-test**                                                                  |
| **Justifikasi**                   | Membandingkan dua kelompok independen menggunakan nilai Accuracy dari beberapa run eksperimen. |


**Effect size yang akan dilaporkan:** [✓] Cohen's d / [ ] Eta-squared / [ ] Lainnya: ____

---

## Latihan 2 — Interpretasi Hasil

Gunakan data berikut (atau data riil Anda) untuk berlatih interpretasi.

**Data:**

| Model                   | Accuracy (mean ± std) |  n |
| ----------------------- | --------------------: | -: |
| Collaborative Filtering |      **86.73 ± 0.71** |  3 |
| Content-Based Filtering |      **90.27 ± 0.40** |  3 |


hasil uji statistik:

- p-value = 0.008
- Cohen's d = 2.18
- 95% Confidence Interval = [2.11%, 4.97%]

| Aspek                      | Interpretasi                                                                                                                                                                                                                                                                                                                       |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Signifikansi statistik** | Nilai **p = 0.008 (< 0.05)** menunjukkan terdapat perbedaan yang signifikan secara statistik antara Collaborative Filtering dan Content-Based Filtering.                                                                                                                                                                           |
| **Effect size**            | Nilai **Cohen's d = 2.18** menunjukkan **large effect**, sehingga perbedaan kedua metode bukan hanya signifikan secara statistik tetapi juga memiliki pengaruh yang besar.                                                                                                                                                         |
| **Practical significance** | Content-Based Filtering memberikan peningkatan rata-rata akurasi sekitar **3,54%** dibanding Collaborative Filtering. Peningkatan ini cukup berarti untuk meningkatkan kualitas rekomendasi produk kepada pengguna.                                                                                                                |
| **Hubungan ke RQ**         | Hasil ini menjawab Research Question bahwa metode **Content-Based Filtering menghasilkan akurasi rekomendasi yang lebih tinggi dibanding Collaborative Filtering** pada dataset penelitian.                                                                                                                                        |
| **Perbandingan literatur** | Hasil dummy ini sejalan dengan berbagai penelitian recommender system yang melaporkan bahwa Content-Based Filtering mampu memberikan rekomendasi yang lebih relevan ketika informasi atribut produk tersedia secara lengkap, sedangkan Collaborative Filtering lebih bergantung pada jumlah dan kepadatan data interaksi pengguna. |



---

## Latihan 3 — Failure Analysis

Latih kemampuan failure analysis: hipotesis TIDAK didukung. Apa yang bisa dipelajari?

**Skenario:** CF = 89.1%, CBF = 88.9%, p = 0.17

| Pertanyaan                   | Jawaban                                                                                                                                                                                                                                                                               |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Apakah ini gagal?**        | Tidak. Hipotesis yang tidak didukung tetap merupakan hasil penelitian yang valid. Hasil ini menunjukkan bahwa tidak terdapat perbedaan performa yang signifikan antara Collaborative Filtering dan Content-Based Filtering pada dataset yang digunakan.                               |
| **Kemungkinan penyebab?**    | Nilai accuracy kedua metode sangat berdekatan (89,1% dan 88,9%), sehingga selisih performa lebih kecil daripada variasi antar-run eksperimen. Selain itu, karakteristik dataset belum cukup memberikan keuntungan yang jelas bagi salah satu metode.                                  |
| **Boundary condition?**      | Collaborative Filtering cenderung lebih unggul ketika tersedia riwayat interaksi pengguna yang banyak, sedangkan pada dataset dengan data interaksi yang terbatas atau sparsity tinggi, keunggulannya menjadi tidak signifikan dibandingkan Content-Based Filtering.                  |
| **Insight**                  | Content-Based Filtering dapat menjadi alternatif yang kompetitif ketika data histori pengguna masih terbatas. Sebaliknya, Collaborative Filtering lebih sesuai diterapkan pada sistem yang telah memiliki banyak data interaksi pengguna.                                             |
| **Apakah layak dilaporkan?** | Ya. Hasil yang tidak signifikan tetap memiliki nilai ilmiah karena menunjukkan batas efektivitas masing-masing metode, mengurangi publication bias, serta menjadi referensi bagi penelitian selanjutnya dalam memilih algoritma rekomendasi yang sesuai dengan karakteristik dataset. |

---

## Refleksi

> Apakah "failure" dalam riset benar-benar gagal, atau justru kontribusi? Bagaimana failure analysis mengubah cara Anda melihat hasil negatif?

> Dalam penelitian ilmiah, failure tidak selalu berarti penelitian gagal. Hasil yang tidak sesuai hipotesis tetap memberikan informasi mengenai batas kemampuan metode yang diuji (boundary condition). Melalui failure analysis, peneliti dapat mengidentifikasi faktor penyebab, mengevaluasi keterbatasan metode, dan memberikan rekomendasi pengembangan pada penelitian selanjutnya. Dengan demikian, hasil negatif tetap memiliki nilai ilmiah dan dapat menjadi kontribusi bagi penelitian di bidang sistem rekomendasi.

> ___________________________________________________
