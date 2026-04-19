# WS-02: Problem Statement

> **Bab 2 — Problem Formulation & System Context**

---

## Ringkasan Materi

### Problem Formation Model

Masalah riset melewati 5 tahap transformasi. Melompat langsung dari Reality ke Variable adalah kesalahan paling umum.

```
Reality → Observed Issue (Symptom) → Diagnosed Problem (Root Cause)
→ Researchable Problem (Scoped) → Measurable Variable (Operationalized)
```

### Topic ≠ Problem ≠ Research Problem

| Level | Contoh | Status |
|-------|--------|--------|
| **Topik** | Keamanan IoT | Terlalu luas, tidak bisa diuji |
| **Problem** | MQTT tidak terenkripsi | Spesifik tapi belum riset |
| **Research Problem** | Belum ada studi membandingkan overhead TLS 1.3 vs DTLS pada MQTT di IoT RAM < 64KB | Bisa dirancang eksperimennya |

### Symptom vs Root Cause

Apa yang diamati (gejala) ≠ mengapa terjadi (akar masalah). Gunakan **5 Whys** atau **Fishbone Diagram** untuk menggali.

Contoh: "User meninggalkan checkout" (symptom) → "Waktu loading > 8 detik karena API call sequential" (root cause).

### System Thinking

Setiap masalah riset TI harus terikat pada komponen sistem: **Input → Process → Output → Outcome → Constraints → Stakeholders**.

### Problem Quality Check

Masalah riset yang layak harus memenuhi 5 kriteria:
- **Clarity** — Satu orang membaca akan paham
- **Measurability** — Ada metrik kuantitatif
- **Relevance** — Penting untuk domain
- **Testability** — Bisa gagal (falsifiable)
- **Impact** — Ada kontribusi jika terjawab

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Menyelesaikan masalah (*solve*) | Memahami dan membuktikan (*understand & prove*) |
| Masalah | Bug, error, fitur belum ada | Gap dalam pengetahuan |
| Scope | Selesaikan semua yang perlu | Batasi agar bisa dibuktikan |
| Output | Working system | Evidence, paper, replicable findings |

### Istilah Penting

- **Problem Statement** — Formulasi tertulis: konteks sistem + gap + dampak + justifikasi
- **System Context** — Deskripsi lengkap: input, proses, output, outcome, constraints, stakeholders
- **Problem Drift** — Masalah "bermutasi" dari pendahuluan ke metodologi karena statement awal tidak presisi
- **Solution-First Thinking** — Memulai dari solusi tanpa masalah yang jelas — berbahaya dalam riset
- **Operational Definition** — Definisi variabel yang cukup jelas agar peneliti lain bisa mengukur hal yang sama

---

## Template A.2 — Problem Statement Builder

```
PROBLEM STATEMENT BUILDER

Domain & Konteks
  Domain   : E-commerce / Sistem Informasi
  Konteks  : Proses checkout pada platform e-commerce

System Context
  Input       : Data produk, keranjang belanja, dan request dari pengguna
  Process     : Sistem memproses checkout (validasi data, pembayaran, API call)
  Output      : Status transaksi (berhasil atau gagal)
  Outcome     : Pengguna menyelesaikan pembelian atau meninggalkan checkout
  Constraints : Kecepatan internet, performa server, kompleksitas sistem
  Stakeholders: Pengguna, penjual, platform e-commerce

Fenomena → Problem
  Fenomena yang diamati             : Banyak pengguna tidak menyelesaikan proses checkout
  Gejala (symptom) yang terukur     : Tingginya tingkat pembatalan (cart abandonment)
  Masalah yang didiagnosis          : Proses checkout lambat karena banyak request sistem (API) yang berjalan tidak efisien
  Masalah riset (researchable)      : Belum diketahui seberapa besar pengaruh waktu loading checkout terhadap tingkat penyelesaian transaksi
  Variabel yang terukur             : Waktu loading (detik) dan tingkat penyelesaian transaksi (%)

Problem Quality Check
  [✓] Clarity — Masalah jelas dan spesifik
  [✓] Measurability — Bisa diukur dengan waktu dan persentase
  [✓] Relevance — Sangat penting dalam e-commerce
  [✓] Testability — Bisa diuji dengan eksperimen/perbandingan data
  [✓] Impact — Bisa meningkatkan penjualan jika teratasi

Problem Statement (1 paragraf):
  Pada platform e-commerce, banyak pengguna yang tidak menyelesaikan proses checkout meskipun telah menambahkan produk ke keranjang. Fenomena ini ditunjukkan dengan tingginya tingkat pembatalan transaksi yang diduga disebabkan oleh lamanya waktu loading pada proses checkout. Namun, belum diketahui secara pasti seberapa besar pengaruh waktu loading terhadap keputusan pengguna untuk menyelesaikan transaksi. Oleh karena itu, penelitian ini bertujuan untuk menganalisis hubungan antara waktu loading checkout dengan tingkat penyelesaian transaksi menggunakan variabel waktu loading dalam detik dan persentase keberhasilan transaksi, sehingga dapat diketahui apakah performa sistem berpengaruh terhadap perilaku pengguna.
```

---

## Latihan 1 — Dari Topik ke Masalah Riset

Pilih satu topik di bidang TI yang diminati. Transformasikan melalui 5 tahap Problem Formation Model.

**Topik awal:** Proses checkout pada e-commerce

| Tahap                          | Hasil                                                                      |
| ------------------------------ | -------------------------------------------------------------------------- |
| Reality                        | Pengguna berbelanja di platform e-commerce                                 |
| Observed Issue (Symptom)       | Banyak pengguna tidak menyelesaikan checkout                               |
| Diagnosed Problem (Root Cause) | Waktu loading checkout lambat karena proses sistem tidak efisien           |
| Researchable Problem           | Apakah waktu loading checkout mempengaruhi tingkat penyelesaian transaksi? |
| Measurable Variable            | Waktu loading (detik), tingkat penyelesaian transaksi (%)                  |


**Apakah terjebak solution-first thinking?** [ ] Ya / [ ] Tidak
> Jika ya, kembali ke tahap mana? ________________________
> [ ] Ya / [✓] Tidak

---

## Latihan 2 — System Context Decomposition

Gambarkan konteks sistem dari masalah riset di Latihan 1.

| Komponen     | Deskripsi                                                  |
| ------------ | ---------------------------------------------------------- |
| Input        | Data produk, keranjang belanja, request pengguna           |
| Process      | Sistem memproses checkout (validasi, pembayaran, API call) |
| Output       | Status transaksi (berhasil atau gagal)                     |
| Outcome      | Pengguna menyelesaikan atau meninggalkan checkout          |
| Constraints  | Kecepatan internet, performa server                        |
| Stakeholders | Pengguna, penjual, platform                                |


**Komponen mana yang paling relevan dengan masalah riset?** 
Process (proses checkout & loading sistem)

---

## Latihan 3 — Problem Quality Check

Evaluasi problem statement yang sudah dibuat menggunakan 5 kriteria.

| Kriteria      | Skor (1-5) | Justifikasi                                  |
| ------------- | ---------- | -------------------------------------------- |
| Clarity       | 5          | Masalah jelas: loading mempengaruhi checkout |
| Measurability | 5          | Bisa diukur dengan detik & persentase        |
| Relevance     | 5          | Sangat penting di e-commerce                 |
| Testability   | 5          | Bisa diuji dengan data eksperimen            |
| Impact        | 5          | Bisa meningkatkan penjualan                  |


**Skor total:** 25 / 25

**Problem statement versi final (1 paragraf):**
> Pada platform e-commerce, banyak pengguna yang tidak menyelesaikan proses checkout meskipun telah menambahkan produk ke keranjang. Fenomena ini ditunjukkan dengan tingginya tingkat pembatalan transaksi yang diduga disebabkan oleh lamanya waktu loading pada proses checkout. Namun, belum diketahui secara pasti seberapa besar pengaruh waktu loading terhadap keputusan pengguna untuk menyelesaikan transaksi. Oleh karena itu, penelitian ini bertujuan untuk menganalisis hubungan antara waktu loading checkout dengan tingkat penyelesaian transaksi menggunakan variabel waktu loading dalam detik dan persentase keberhasilan transaksi.
---

## Refleksi

> Bandingkan "masalah" yang biasa ditemui saat coding (bug, error) dengan masalah riset. Apa perbedaan fundamental dalam cara mendefinisikan dan mendekati keduanya?

**Jawaban:**
> Masalah dalam coding biasanya berupa error atau bug yang harus segera diperbaiki agar sistem berjalan. Sedangkan dalam riset, masalah tidak langsung diselesaikan, tetapi dianalisis terlebih dahulu untuk mengetahui penyebab dan hubungan antar variabel. Riset lebih fokus pada pembuktian dengan data, sedangkan coding fokus pada penyelesaian masalah secara langsung.



