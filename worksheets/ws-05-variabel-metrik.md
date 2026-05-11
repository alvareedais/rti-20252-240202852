# WS-05: Variabel & Metrik

> **Bab 5 — Metric, Measurement & Data**

---

## Ringkasan Materi

### Measurement Alignment Model

Setiap pengukuran yang valid harus bisa ditelusuri melalui rantai ini tanpa lompatan logis:

```
Problem → Concept → Variable → Metric → Data → Result
```

### Operationalization = Keputusan Desain

Menerjemahkan konsep abstrak menjadi variabel terukur bukan proses mekanis. "Code quality" yang diukur via SonarQube code smells membawa asumsi implisit. Setiap operasionalisasi harus didokumentasikan dan dijustifikasi.

### Empat Tipe Data (NOIR)

| Tipe | Ciri | Contoh | Operasi Valid |
|------|------|--------|---------------|
| **Nominal** | Kategori, tanpa urutan | Jenis algoritma (RF, SVM, CNN) | Modus, chi-square |
| **Ordinal** | Urutan, interval tidak sama | Skala Likert (1-5) | Median, Spearman |
| **Interval** | Jarak bermakna, tanpa nol absolut | Suhu Celsius | Mean, Pearson, t-test |
| **Ratio** | Jarak bermakna + nol absolut | Waktu eksekusi (ms) | Semua operasi |

Tipe data menentukan uji statistik yang valid. Kebanyakan metrik performa TI = ratio; persepsi pengguna = ordinal.

### Kriteria Pemilihan Metrik

- **Representative** — Mewakili konsep yang diteliti
- **Sensitive** — Cukup peka menangkap perbedaan bermakna (hindari ceiling effect)
- **Feasible** — Bisa dikumpulkan dalam batasan waktu dan biaya

### Pre-registration

Metrik harus ditentukan **sebelum** eksperimen. Memilih metrik setelah melihat data = **p-hacking**. Metrik tambahan yang ditemukan kemudian dilaporkan sebagai *exploratory*, bukan *confirmatory*.

### Primary vs Secondary Metric

- **Primary Metric** — Langsung terikat ke hipotesis, menentukan kesimpulan
- **Secondary Metric** — Pendukung, dilaporkan di samping primary; statusnya suplementer

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Pemilihan metrik | Berdasarkan kebiasaan/tool yang ada | Berdasarkan construct validity |
| Anomali | Dihapus untuk laporan bersih | Diinvestigasi — bisa jadi temuan |
| Kapan dipilih | Setelah sistem jadi (monitoring) | Sebelum eksperimen (by design) |

### Istilah Penting

- **Operationalization** — Transformasi konsep abstrak menjadi variabel terukur
- **Construct Validity** — Sejauh mana pengukuran benar-benar mengukur konsep yang dimaksud
- **Measurement Scale** — Klasifikasi data (NOIR) yang menentukan analisis valid
- **Multi-metric Evaluation** — Menggunakan beberapa metrik untuk menangkap konsep kompleks

---

## Template A.5 — Definisi Variabel, Metrik & Justifikasi

```
VARIABLE & METRIC DEFINITION

Research Question: Apakah Collaborative Filtering menghasilkan precision dan recall lebih tinggi dibandingkan Content-Based Filtering pada sistem rekomendasi produk e-commerce?

| Variabel            | Tipe | Konsep                        | Metrik                      | Skala   | Satuan     | Cara Mengukur                         | Justifikasi                      |
| ------------------- | ---- | ----------------------------- | --------------------------- | ------- | ---------- | ------------------------------------- | -------------------------------- |
| Jenis algoritma     | IV   | Pendekatan sistem rekomendasi | CF vs CBF                   | Nominal | —          | Menentukan model yang digunakan       | Variabel utama yang dibandingkan |
| Akurasi rekomendasi | DV   | Kualitas rekomendasi          | Precision, Recall, F1-Score | Ratio   | %          | Bandingkan rekomendasi vs data aktual | Mewakili performa sistem         |
| Dataset             | CV   | Sumber data                   | Dataset yang sama           | Nominal | —          | Gunakan dataset identik               | Menghindari bias                 |
| Jumlah data         | CV   | Ukuran dataset                | Jumlah user & item          | Ratio   | Data count | Menyamakan jumlah data                | Menjaga fairness                 |
| Parameter model     | CV   | Setting model                 | Hyperparameter tetap        | Nominal | —          | Set nilai tetap                       | Agar hasil valid                 |


Alignment Check:
  RQ → Concept → Variable → Metric → Data → Result
    ✔ Problem: Rekomendasi tidak akurat
    ✔ Concept: Akurasi rekomendasi
    ✔ Variable: Precision, Recall
    ✔ Metric: Nilai % precision & recall
    ✔ Data: Dataset interaksi user
    ✔ Result: Perbandingan performa CF vs CBF
  [✓]Setiap langkah terdokumentasi
  [✓]Tidak ada "lompatan logis"
  [✓]Metrik mengukur apa yang dimaksud (construct validity)
```

---

## Latihan 1 — Operationalization Chain

Gunakan RQ dari WS-04. Definisikan variabel dan metriknya.

**RQ:** Apakah Collaborative Filtering lebih baik dari Content-Based Filtering dalam precision & recall?

| Variabel        | Tipe | Konsep Abstrak       | Metrik Konkret        | Skala (NOIR) | Satuan |
| --------------- | ---- | -------------------- | --------------------- | ------------ | ------ |
| Jenis algoritma | IV   | Metode rekomendasi   | CF vs CBF             | Nominal      | —      |
| Akurasi         | DV   | Kualitas rekomendasi | Precision, Recall, F1 | Ratio        | %      |
| Dataset         | CV   | Data uji             | Dataset user-item     | Nominal      | —      |


**Apakah ada lompatan logis dalam rantai?** [ ] Ya / [✓] Tidak
> Jika ya, di mana? ____________________________________

---

## Latihan 2 — Evaluasi Metrik

Evaluasi metrik DV yang dipilih di Latihan 1 menggunakan 3 kriteria.

| Kriteria       | Skor (1-5) | Justifikasi                                                |
| -------------- | ---------- | ---------------------------------------------------------- |
| Representative | 5          | Precision & Recall langsung mengukur relevansi rekomendasi |
| Sensitive      | 4          | Bisa membedakan performa model                             |
| Feasible       | 5          | Mudah dihitung dari data                                   |


**Apakah perlu secondary metric?** [✓] Ya / [ ] Tidak
> Jika ya, apa dan mengapa? __Secondary metric: F1-Score dan Waktu komputasi, Kenapa? karena F1 = gabungan precision & recall dan Waktu komputasi = efisiensi sistem

**Contoh kasus ceiling effect untuk metrik ini:**
> Jika semua model menghasilkan precision di atas 95%, maka sulit membedakan performa karena semua terlihat “bagus”

---

## Latihan 3 — Data Quality Check

Bayangkan data yang akan dikumpulkan dari eksperimen. Evaluasi 4 dimensi kualitas data.

| Dimensi            | Pertanyaan                   | Jawaban      | Strategi Mitigasi      |
| ------------------ | ---------------------------- | ------------ | ---------------------- |
| Completeness       | Apakah semua data terkumpul? | Tidak selalu | Bersihkan missing data |
| Consistency        | Apakah ada kontradiksi?      | Bisa ada     | Validasi dataset       |
| Validity           | Apakah sesuai konsep?        | Ya           | Gunakan data real user |
| Representativeness | Apakah mewakili user?        | Belum tentu  | Gunakan data beragam   |


---

## Refleksi

> Mengapa memilih metrik setelah melihat data dianggap p-hacking? Apa bedanya dengan eksplorasi data yang sah?

**Jawaban:**
> Memilih metrik setelah melihat data disebut p-hacking karena peneliti bisa memilih metrik yang menguntungkan hasil, sehingga tidak objektif. 
> Berbeda dengan eksplorasi data yang sah, eksplorasi dilakukan setelah analisis utama dan dilaporkan sebagai temuan tambahan, bukan untuk mendukung hipotesis utama.
