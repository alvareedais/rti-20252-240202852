# WS-04: Research Question & Hypothesis

> **Bab 4 — Research Question, Contribution & Hypothesis**

---

## Ringkasan Materi

### RQ Bukan Pertanyaan Biasa

Research Question yang baik secara implisit mengandung cetak biru eksperimen: subjek, baseline, metrik, domain, dataset.

| Kualitas | Contoh |
|----------|--------|
| **Buruk** | "Bagaimana pengaruh deep learning terhadap deteksi malware?" |
| **Baik** | "Apakah CNN menghasilkan F1-Score lebih tinggi dari RF pada CIC-MalMem-2022?" |

Perbedaan: RQ yang baik menyebutkan **metode spesifik**, **metrik terukur**, **baseline**, dan **dataset**.

### Tiga Jenis RQ

| Jenis | Pola | Kebutuhan |
|-------|------|-----------|
| **Comparison** | A vs B → mana lebih baik? | ≥ 2 metode, metrik sama |
| **Improvement** | A' vs A → modifikasi lebih baik? | Pre/post, bukti perbaikan |
| **Exploratory** | Faktor X₁...Xₙ → pengaruh terhadap Y? | Multi-variabel, korelasi/regresi |

### Contribution Statement

Tiga jenis kontribusi: **Improvement** (metode terbukti lebih baik), **Comparison** (perbandingan sistematis yang belum ada), **Novel Approach** (pendekatan baru). Kontribusi harus terhubung langsung dengan gap — kontribusi tanpa gap = klaim tanpa justifikasi.

### Hypothesis H₀ / H₁

- **H₀** (Null) = Tidak ada perbedaan signifikan — asumsi default, harus dibuktikan salah
- **H₁** (Alternative) = Ada perbedaan signifikan — diterima hanya jika H₀ ditolak
- Harus **falsifiable**, mengandung **metrik terukur**, dirumuskan **SEBELUM eksperimen**

### Rantai Operasionalisasi

```
RQ → Variable → Metric → Data → Analysis
```

Jika rantai ini tidak lengkap, RQ belum mature. Bi-directional: RQ yang tidak bisa jadi hipotesis testable harus direvisi mundur.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan pertanyaan | Apa yang harus dibangun? | Apa yang harus dibuktikan? |
| Bentuk jawaban | Sistem yang berfungsi | Bukti empiris terukur |
| Sukses diukur oleh | User satisfaction, uptime | Signifikansi statistik, effect size |
| Jika gagal | Debug dan perbaiki | Laporkan, analisis mengapa |

### Istilah Penting

- **Research Question (RQ)** — Pertanyaan spesifik: variabel terukur + metrik + konteks
- **Contribution Statement** — Apa yang diketahui setelah riset selesai yang sebelumnya belum ada
- **H₀ / H₁** — Null vs Alternative Hypothesis
- **Falsifiability** — Kondisi hipotesis ditolak harus bisa didefinisikan sebelum eksperimen
- **Operationalization** — Proses mewujudkan konsep abstrak menjadi variabel terukur

---

## Template A.4 — RQ-Contribution-Hypothesis

```
RQ-CONTRIBUTION-HYPOTHESIS

Gap Statement  : Belum ada perbandingan yang jelas antara Collaborative Filtering dan Content-Based Filtering dalam meningkatkan akurasi rekomendasi produk pada e-commerce.

Research Question:
  Tipe         : [✓] Comparison  [ ] Improvement  [ ] Exploratory
  Formulasi    : Apakah Collaborative Filtering menghasilkan akurasi, precision, dan recall yang lebih tinggi dibandingkan Content-Based Filtering pada sistem rekomendasi produk e-commerce menggunakan dataset transaksi pengguna?
  Variabel IV  : Jenis algoritma (Collaborative Filtering vs Content-Based Filtering)
  Variabel DV  : Akurasi rekomendasi
  Metrik       : Accuracy, Precision, Recall
  Dataset      : Dataset transaksi pengguna e-commerce (Shopee/Tokopedia-like dataset)
  Baseline     : Content-Based Filtering

Quality Check RQ:
  [✓] Variabel spesifik
  [✓] Metrik jelas
  [✓] Baseline ada
  [✓] Konteks disebutkan
  [✓] Memerlukan eksperimen

Contribution Statement:
  Apa yang baru diketahui : Mengetahui algoritma mana yang lebih optimal dalam meningkatkan akurasi rekomendasi produk pada e-commerce.
  Jenis kontribusi        : [✓] Comparison  [ ] Improvement  [ ] Novel approach
  Gap yang diisi          : Perbandingan performa antar algoritma rekomendasi yang belum dilakukan secara langsung

Hypothesis Pair:
  H₀ : Tidak terdapat perbedaan signifikan antara Collaborative Filtering dan Content-Based Filtering dalam menghasilkan akurasi, precision, dan recall pada sistem rekomendasi produk.
  H₁ : Collaborative Filtering menghasilkan akurasi, precision, dan recall yang lebih tinggi dibandingkan Content-Based Filtering.
  Threshold              : p-value < 0.05
  Justifikasi threshold  : Nilai 0.05 merupakan standar umum dalam penelitian untuk menentukan signifikansi statistik.
```

---

## Latihan 1 — Dari Gap ke RQ

Gunakan gap yang ditemukan di WS-03. Transformasikan menjadi Research Question.

**Gap dari WS-03:** Belum ada perbandingan langsung algoritma rekomendasi terhadap akurasi rekomendasi produk pada e-commerce.

**RQ versi pertama (tulis bebas):**
> Algoritma mana yang lebih baik untuk rekomendasi produk?

**Evaluasi RQ:**

| Komponen        | Ada?  | Isi           |
| --------------- | ----- | ------------- |
| Metode spesifik | Tidak | Belum disebut |
| Metrik terukur  | Tidak | Belum ada     |
| Baseline        | Tidak | Belum ada     |
| Dataset/konteks | Tidak | Belum jelas   |


**Tipe RQ:** [✓] Comparison / [ ] Improvement / [ ] Exploratory

**RQ versi revisi (setelah evaluasi):**
> Apakah Collaborative Filtering menghasilkan akurasi, precision, dan recall yang lebih tinggi dibandingkan Content-Based Filtering pada sistem rekomendasi produk e-commerce menggunakan dataset transaksi pengguna?

---

## Latihan 2 — Hypothesis Pair

Rumuskan pasangan hipotesis dari RQ di Latihan 1.

| Komponen              | Isi                                                                   |
| --------------------- | --------------------------------------------------------------------- |
| H₀                    | Tidak ada perbedaan signifikan precision dan recall antara CF dan CBF |
| H₁                    | CF memiliki precision dan recall lebih tinggi                         |
| Metrik                | Precision, Recall                                                     |
| Threshold             | 0.05                                                                  |
| Justifikasi threshold | Standar penelitian statistik                                          |


**Apakah hipotesis ini falsifiable?** [✓] Ya / [ ] Tidak
> Bagaimana cara membuktikannya salah? Jika hasil uji statistik menunjukkan p-value > 0.05, maka H₀ tidak dapat ditolak, yang berarti tidak ada bukti cukup untuk mendukung H₁. Jika p-value < 0.05, maka H₀ ditolak, mendukung H₁ bahwa CF lebih baik dari CBF.

---

## Latihan 3 — Rantai Operasionalisasi

Lengkapi rantai dari RQ hingga metode analisis.

| Tahap           | Isi                                                     |
| --------------- | ------------------------------------------------------- |
| RQ              | Apakah CF lebih baik dari CBF dalam precision & recall? |
| Variable (IV)   | Jenis algoritma (CF vs CBF)                             |
| Variable (DV)   | Akurasi rekomendasi                                     |
| Metric          | Precision, Recall, F1-Score                             |
| Data source     | Dataset interaksi pengguna e-commerce                   |
| Analysis method | Uji statistik (t-test / perbandingan mean)              |


**Apakah rantai lengkap?** [✓] Ya / [ ] Tidak
> Jika tidak, tahap mana yang perlu direvisi?  karena seluruh komponen dari RQ hingga metode analisis telah terdefinisi secara jelas dan dapat diuji secara empiris.
---

## Refleksi

> Ambil satu judul skripsi/paper yang pernah dibaca. Coba ekstrak RQ-nya. Apakah RQ tersebut memenuhi semua komponen (metode, metrik, baseline, konteks)? Jika tidak, apa yang hilang?

**Judul:** Sistem Rekomendasi Produk Menggunakan Collaborative Filtering
**RQ yang diekstrak:** Apakah Collaborative Filtering efektif dalam rekomendasi produk?
**Komponen yang hilang:** Metrik, baseline, dan dataset tidak disebutkan secara jelas
