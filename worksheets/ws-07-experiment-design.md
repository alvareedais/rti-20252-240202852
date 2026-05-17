# WS-07: Experimental Design & Validity

> **Bab 7 — Experimental Design & Validity**

---

## Ringkasan Materi

### Correlation ≠ Causality

Kausalitas membutuhkan 3 syarat:
1. **Covariance** — X dan Y bergerak bersama
2. **Temporal precedence** — X berubah sebelum Y
3. **Elimination of alternatives** — Tidak ada faktor lain yang menjelaskan Y

Controlled experiment adalah satu-satunya metode yang bisa membuktikan kausalitas.

### Empat Jenis Validitas

| Jenis | Pertanyaan | Ancaman Umum |
|-------|-----------|-------------|
| **Internal** | Apakah hubungan IV→DV nyata? | Confounding variable, selection bias |
| **External** | Apakah bisa digeneralisasi? | Dataset terlalu spesifik |
| **Construct** | Apakah mengukur konsep yang benar? | Metrik tidak sesuai |
| **Conclusion** | Apakah kesimpulan statistik valid? | Sample size kecil, uji salah |

Internal dan external validity sering berkonflik: semakin terkontrol (internal kuat) → semakin artificial (external lemah).

### Tiga Tipe Eksperimen dalam Riset TI

| Tipe | Deskripsi | Kapan Digunakan |
|------|----------|----------------|
| **Comparison Study** | Metode A vs B pada kondisi identik | Membandingkan pendekatan berbeda |
| **Ablation Study** | Full system → lepas komponen satu per satu | Mengukur kontribusi tiap komponen |
| **Parameter Study** | Variasikan satu parameter, amati dampak | Uji sensitifitas/robustness |

### Fairness dalam Perbandingan

Perbandingan yang adil = **kondisi identik** untuk semua metode: dataset sama, preprocessing sama, tuning effort sebanding, environment sama, metrik sama.

Contoh tidak adil: Transformer (30 fitur tambahan + Bayesian optimization) vs RF (default params) → hasilnya misleading.

### Threats to Validity = Diidentifikasi Sebelum Eksperimen

Ancaman validitas harus diidentifikasi **sebelum** eksperimen dan mitigasinya dirancang sebagai bagian dari desain — bukan ditulis sebagai boilerplate setelah selesai.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan testing | Memastikan sistem memenuhi requirement | Membuktikan hubungan kausal antar variabel |
| Baseline | Versi sebelumnya (last release) | Metode tervalidasi dari literatur |
| Kegagalan | Bug → fix → release | H₀ tidak ditolak → tetap kontribusi ilmiah |
| Sukses | 100% test pass | Evidence valid — mendukung atau menolak hipotesis |

### Istilah Penting

- **Causality** — Hubungan sebab-akibat (covariance + temporal + elimination)
- **Controlled Experiment** — Ubah satu variabel, kontrol sisanya, amati efek
- **Fairness** — Semua metode diuji pada kondisi yang benar-benar identik
- **Threats to Validity** — Faktor yang bisa melemahkan kesimpulan jika tidak dimitigasi
- **Conclusion Validity** — Validitas statistik: power, sample size, uji yang tepat

---

## Template A.7 — Desain Eksperimen Lengkap

```
EXPERIMENT DESIGN

Research Question :
Apakah Collaborative Filtering menghasilkan precision dan recall lebih tinggi dibandingkan Content-Based Filtering pada sistem rekomendasi produk e-commerce?

Hypothesis :
H₁ : Collaborative Filtering memiliki precision dan recall lebih tinggi dibandingkan Content-Based Filtering.

Tipe Eksperimen :
[✓] Comparison  [ ] Ablation  [ ] Parameter

| Kondisi   | Deskripsi                   | IV Value                | CV Settings                                                    |
| --------- | --------------------------- | ----------------------- | -------------------------------------------------------------- |
| Control   | Baseline metode rekomendasi | Content-Based Filtering | Dataset sama, preprocessing sama, split 80:20, parameter tetap |
| Treatment | Metode yang diuji           | Collaborative Filtering | Dataset sama, preprocessing sama, split 80:20, parameter tetap |


Fairness Checklist:
  [✓] Dataset identik untuk semua kondisi
  [✓] Preprocessing setara
  [✓] Tuning effort setara
  [✓] Environment identik
  [✓] Metrik evaluasi sama

Threat Analysis:
| Threat Type | Ancaman Spesifik                                         | Mitigasi                                        |
| ----------- | -------------------------------------------------------- | ----------------------------------------------- |
| Internal    | Data leakage antara train dan test                       | Menggunakan train-test split yang konsisten     |
| External    | Dataset hanya berasal dari satu jenis marketplace        | Menggunakan data dengan variasi produk dan user |
| Construct   | Precision saja tidak cukup mengukur kualitas rekomendasi | Menambahkan Recall dan F1-Score                 |
| Conclusion  | Jumlah data terlalu sedikit                              | Menggunakan dataset dengan ukuran memadai       |


Statistical Plan:
  Uji statistik   : Independent t-test
  Justifikasi      : Membandingkan rata-rata performa dua metode
  Alpha            : 0.05
  Effect size min  : 0.2
```

---

## Latihan 1 — Desain Eksperimen

Susun desain eksperimen berdasarkan RQ, variabel, dan sistem dari WS-04 sampai WS-06.

**RQ:** Apakah Collaborative Filtering menghasilkan precision dan recall lebih tinggi dibandingkan Content-Based Filtering?

**Tipe eksperimen:** [✓] Comparison / [ ] Ablation / [ ] Parameter

| Kondisi   | Deskripsi            | IV Value | CV Settings                      |
| --------- | -------------------- | -------- | -------------------------------- |
| Control   | Baseline rekomendasi | CBF      | Dataset sama, preprocessing sama |
| Treatment | Algoritma utama      | CF       | Dataset sama, preprocessing sama |


---

## Latihan 2 — Fairness Checklist

Evaluasi apakah desain eksperimen di Latihan 1 sudah fair.

| Kriteria             | Status | Detail                               |
| -------------------- | ------ | ------------------------------------ |
| Dataset identik      | ✅      | Dataset yang sama digunakan          |
| Preprocessing setara | ✅      | Cleaning & transformasi sama         |
| Tuning effort setara | ✅      | Parameter dituning dengan usaha sama |
| Environment identik  | ✅      | Hardware & software sama             |
| Metrik evaluasi sama | ✅      | Precision, Recall, F1 sama           |


**Ada yang tidak fair?** [ ] Ya / [✓] Tidak
> Jika ya, bagaimana cara memperbaikinya? ________________

---

## Latihan 3 — Threat Analysis

Identifikasi ancaman validitas untuk desain eksperimen ini.

| Threat Type | Ancaman Spesifik                  | Mitigasi              |
| ----------- | --------------------------------- | --------------------- |
| Internal    | Overlap data train-test           | Gunakan split tetap   |
| External    | Dataset tidak mewakili semua user | Gunakan data beragam  |
| Construct   | Precision tidak cukup             | Tambahkan Recall & F1 |
| Conclusion  | Sample size kecil                 | Tambahkan jumlah data |


**Ancaman mana yang paling sulit dimitigasi?** External validity

**Mengapa?**
> Karena perilaku pengguna e-commerce sangat beragam sehingga sulit membuat dataset yang benar-benar mewakili seluruh pengguna marketplace seperti Shopee dan Tokopedia.

---

## Refleksi

> Sebuah paper melaporkan "metode kami mengalahkan semua baseline." Apa 3 pertanyaan pertama yang harus diajukan untuk mengevaluasi klaim ini?

**Jawaban:**
1. Apakah semua metode diuji menggunakan dataset dan preprocessing yang sama?
2. Apakah baseline yang digunakan benar-benar relevan dan representatif?
3. Apakah perbedaan hasil terbukti signifikan secara statistik?
