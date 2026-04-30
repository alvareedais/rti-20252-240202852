# WS-03: Literature Mapping & Gap

> **Bab 3 — Literature Review, Research Gap & Baseline**

---

## Ringkasan Materi

### Literature Review = Positioning, Bukan Ringkasan

Literature review bukan merangkum paper satu per satu. Pendekatan yang benar adalah **concept-centric** — organisasi berdasarkan tema, metode, atau variabel. Tujuan: menemukan **pola, kontradiksi, dan gap**.

### Empat Jenis Research Gap

| Jenis Gap | Deskripsi | Contoh |
|-----------|----------|--------|
| **Performance Gap** | Performa belum memadai | Akurasi deteksi hanya 78% pada kasus tertentu |
| **Method Gap** | Pendekatan belum diterapkan | Belum ada yang pakai transformer untuk task ini |
| **Data Gap** | Dataset terbatas/tidak representatif | Semua studi pakai dataset sintetis |
| **Context Gap** | Belum diuji pada konteks berbeda | Belum ada evaluasi di negara berkembang |

Gap terkuat = kombinasi 2+ jenis.

### Systematic Search Strategy

1. **Database**: IEEE Xplore, ACM DL, Scopus, Google Scholar
2. **Boolean query** yang terdokumentasi eksplisit
3. **Snowballing**: backward (telusuri referensi) + forward (cari yang mengutip)
4. Klaim "belum ada penelitian" harus didukung **bukti pencarian**

### Baseline Selection — 3 Kriteria

| Kriteria | Pertanyaan |
|----------|-----------|
| **Relevan** | Apakah menyelesaikan masalah yang sama? |
| **Representatif** | Apakah mewakili common practice? |
| **State-of-the-Art** | Apakah terbaru/terbaik? |

Membandingkan deep learning 2024 dengan decision tree sederhana tanpa justifikasi = **straw man comparison** (perbandingan tidak jujur).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan baca literatur | Mencari solusi yang sudah ada | Memahami apa yang belum terjawab |
| Cara membaca paper | Tutorial, how-to | Metode, limitasi, gap |
| Baseline | Framework terpopuler | State-of-the-art yang rigorous |
| Dokumentasi pencarian | Tidak diperlukan | Wajib (reproducible) |

### Istilah Penting

- **Concept-centric** — Organisasi literatur berdasarkan konsep/metode, bukan per penulis
- **Snowballing** — Backward (telusuri referensi) + Forward (cari yang mengutip paper kunci)
- **Research Position** — Pernyataan eksplisit posisi riset terhadap studi sebelumnya
- **Straw man comparison** — Memilih baseline lemah agar metode sendiri terlihat lebih baik

---

## Template A.3 — Literature Mapping & Gap Identification

```
LITERATURE MAPPING

Topik      : Pengaruh algoritma rekomendasi terhadap akurasi rekomendasi produk pada e-commerce
Database   : Google Scholar
Query      : "recommender system e-commerce collaborative filtering content-based Indonesia"
Tahun      : 2020–2025
Hasil awal : 150 paper → Screening → 5 paper final

Literature Matrix (concept-centric):

| Study                                | Tahun | Method                  | Data                  | Result               | Limitation                    |
| ------------------------------------ | ----- | ----------------------- | --------------------- | -------------------- | ----------------------------- |
| Sistem Rekomendasi Produk E-commerce | 2021  | Collaborative Filtering | Data rating pengguna  | Akurasi cukup baik   | Cold start problem            |
| Rekomendasi Produk Berbasis Konten   | 2022  | Content-Based Filtering | Data deskripsi produk | Relevansi tinggi     | Tidak personal                |
| Hybrid Recommender System            | 2023  | Hybrid (CF + CBF)       | Data user & produk    | Akurasi lebih tinggi | Kompleksitas tinggi           |
| Deep Learning Recommender            | 2024  | Neural Network          | Dataset besar         | Akurasi tinggi       | Butuh resource besar          |
| Sistem Rekomendasi Marketplace       | 2020  | Collaborative Filtering | Data transaksi        | Mudah diimplementasi | Kurang akurat di data sedikit |

Pola yang ditemukan:
  Metode dominan     : Collaborative Filtering dan Content-Based Filtering
  Dataset umum       : Data rating pengguna dan data deskripsi produk
  Limitasi berulang  : Cold start problem dan kurang akurat di data sedikit

GAP IDENTIFICATION

Gap 1: [Jenis: Performance Gap + Method Gap]
  Deskripsi    : Belum ada perbandingan yang jelas antara beberapa algoritma rekomendasi (CF, CBF, Hybrid) dalam konteks e-commerce lokal
  Bukti        : Studi hanya fokus pada satu metode tanpa membandingkan performanya secara langsung
  Signifikansi : Penting untuk mengetahui algoritma mana yang paling optimal dalam meningkatkan akurasi rekomendasi

Gap 2: [Jenis: Context Gap]
  Deskripsi    : Penelitian belum banyak dilakukan pada platform e-commerce seperti Shopee dan Tokopedia
  Bukti        : Banyak studi menggunakan dataset umum, bukan dari marketplace besar
  Signifikansi : Perilaku pengguna di marketplace besar bisa berbeda dan lebih kompleks

Baseline Selection:
| Baseline                | Relevansi                | Representatif           | Source     |
| ----------------------- | ------------------------ | ----------------------- | ---------- |
| Collaborative Filtering | Metode utama rekomendasi | Paling sering digunakan | Studi 2021 |
| Content-Based Filtering | Alternatif metode        | Umum digunakan          | Studi 2022 |

```

---

## Latihan 1 — Concept-Centric Literature Table

Gunakan topik riset dari WS-02. Cari minimal 5 paper relevan menggunakan Google Scholar atau database lain.

**Topik riset:** Pengaruh algoritma rekomendasi terhadap akurasi rekomendasi produk
**Query pencarian:** "recommender system e-commerce accuracy collaborative filtering"
**Database:** Google Scholar

| # | Study            | Tahun | Method                  | Dataset       | Result         | Limitasi       |
| - | ---------------- | ----- | ----------------------- | ------------- | -------------- | -------------- |
| 1 | CF E-commerce    | 2021  | Collaborative Filtering | Data rating   | Akurasi baik   | Cold start     |
| 2 | CBF Produk       | 2022  | Content-Based           | Data produk   | Relevan        | Tidak personal |
| 3 | Hybrid System    | 2023  | Hybrid                  | Data gabungan | Akurasi tinggi | Kompleks       |
| 4 | Deep Learning RS | 2024  | Neural Network          | Big data      | Sangat akurat  | Mahal          |
| 5 | Marketplace RS   | 2020  | CF                      | Transaksi     | Mudah          | Kurang akurat  |

**Pola yang terlihat — Metode dominan:** Collaborative Filtering
**Limitasi yang berulang:** Cold start problem dan kurang akurat di data sedikit

---

## Latihan 2 — Gap Identification

Berdasarkan tabel di Latihan 1, identifikasi gap.

| Jenis Gap       | Ditemukan? | Gap Statement                      |
| --------------- | ---------- | ---------------------------------- |
| Performance Gap | [✓] Ya     | Akurasi masih belum optimal        |
| Method Gap      | [✓] Ya     | Belum ada perbandingan metode      |
| Data Gap        | [ ] Tidak  | Data cukup banyak                  |
| Context Gap     | [✓] Ya     | Belum spesifik ke Shopee/Tokopedia |


**Gap utama yang dipilih:** Method Gap + Performance Gap
**Mengapa gap ini penting (bukan sekadar "belum ada yang meneliti")?**
> Karena belum ada penelitian yang secara langsung membandingkan performa berbagai algoritma rekomendasi dalam meningkatkan akurasi pada konteks e-commerce, sehingga belum diketahui metode mana yang paling optimal.
---

## Latihan 3 — Baseline Selection

Pilih 2 baseline dari literatur yang sudah dibaca.

| # | Baseline                | Mengapa Relevan              | Mengapa Representatif | Apakah SOTA? | Sumber     |
| - | ----------------------- | ---------------------------- | --------------------- | ------------ | ---------- |
| 1 | Collaborative Filtering | Digunakan luas di e-commerce | Metode paling umum    | Tidak        | Studi 2021 |
| 2 | Content-Based Filtering | Alternatif populer           | Banyak dipakai        | Tidak        | Studi 2022 |

**Apakah pemilihan baseline ini bisa dianggap straw man?** [ ] Ya / [✓] Tidak
> Justifikasi: Baseline dipilih karena mewakili metode yang umum digunakan dan relevan dengan penelitian, sehingga perbandingan tetap adil.

---

## Refleksi

> Apa perbedaan antara "belum ada yang meneliti ini" (klaim tanpa bukti) dengan research gap yang valid? Bagaimana cara membuktikan bahwa sebuah gap benar-benar ada?

**Jawaban:**
> Research gap yang valid harus didukung dengan analisis beberapa penelitian sebelumnya yang menunjukkan keterbatasan yang sama. Berbeda dengan klaim tanpa bukti, gap yang valid diperoleh dari perbandingan literatur yang menunjukkan adanya kekurangan yang belum teratasi.
> ___________________________________________________
