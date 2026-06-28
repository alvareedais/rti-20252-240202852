# WS-10: Experiment Execution & Data Collection

> **Bab 10 — Eksekusi Eksperimen & Pengumpulan Data**

---

## Ringkasan Materi

### Experiment Execution Pipeline

```
Design → Execution Plan → Controlled Execution → Data Collection → Data Logging → Dataset for Analysis
```

### Multiple Run = Non-Negotiable

Single run **tidak pernah cukup** untuk klaim ilmiah. Minimum 5-10 run per skenario dengan seed berbeda. Multiple run menghasilkan:
- Mean, std, confidence interval
- Distribusi hasil → uji statistik
- Variabilitas → error bar di grafik

### Execution Plan

Setiap eksperimen harus memiliki plan sebelum eksekusi:
- Daftar skenario
- Jumlah run per skenario
- Random seed per run (pre-determined!)
- Urutan eksekusi (randomisasi/counterbalancing)
- Pre-execution checklist

### Data Logging Komprehensif

Setiap run menghasilkan log terstruktur:
1. **Identitas** — Run ID, timestamp, skenario
2. **Konfigurasi** — Semua parameter, seed, code version
3. **Hasil** — Semua metrik, output detail
4. **Metadata** — Waktu eksekusi, resource usage, warning/error

Format: CSV/JSON/database — **bukan stdout yang di-copy-paste**.

### Engineering vs Research Execution

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Run | Sekali (deploy) | Multiple (min 5-10, seed berbeda) |
| Logging | Error log, access log | Semua parameter, metrik, metadata |
| Anomali | Bug → fix → redeploy | Investigasi → dokumentasi → analisis |
| Urutan | Tidak penting | Bisa bias — perlu randomisasi |

### Anomali = Dokumentasi, Bukan Hapus

Run gagal/anomali tidak boleh dihapus tanpa dokumentasi. Bisa jadi:
- **Bug** → fix & re-run (dokumentasikan!)
- **Batas kemampuan metode** → DNF = temuan
- **Data yang bias** jika hanya simpan run "berhasil"

### Jebakan Kognitif

1. "Satu angka cukup" → tanpa distribusi, tidak bisa diuji
2. "Seed tidak penting" → bahkan algoritma deterministik bisa dipengaruhi library stokastik
3. "Run gagal langsung hapus" → kehilangan temuan potensial
4. "Semua run harus hari ini" → thermal throttling, fatigue

---

## Template A.10 — Execution Plan & Data Log

```
EXECUTION PLAN

| Run # | Skenario                | Seed | Parameter                | Status  | Waktu | Output File  |
| ----- | ----------------------- | ---- | ------------------------ | ------- | ----- | ------------ |
| 1     | Collaborative Filtering | 42   | Train-Test Split = 80:20 | Planned | —     | cf_run1.csv  |
| 2     | Collaborative Filtering | 123  | Train-Test Split = 80:20 | Planned | —     | cf_run2.csv  |
| 3     | Collaborative Filtering | 2025 | Train-Test Split = 80:20 | Planned | —     | cf_run3.csv  |
| 4     | Content-Based Filtering | 42   | Train-Test Split = 80:20 | Planned | —     | cbf_run1.csv |
| 5     | Content-Based Filtering | 123  | Train-Test Split = 80:20 | Planned | —     | cbf_run2.csv |
| 6     | Content-Based Filtering | 2025 | Train-Test Split = 80:20 | Planned | —     | cbf_run3.csv |

Jumlah runs per skenario : 3
Total runs               : 6

DATA LOG (per run):
  Run ID    : run-001
  Timestamp : Akan dicatat saat eksperimen dijalankan.
  Skenario  : Collaborative Filtering
  Input     : * Dataset Kaggle (E-commerce Product Recommendation Dataset)
              * Random Seed = 42
              * Train-Test Split = 80:20
  Output    : * Precision
              * Recall
              * F1-Score
              * Execution Time
  Anomali   : blom ada
  Catatan   : Data log akan disimpan dalam format CSV untuk setiap proses eksperimen.

```

---

## Latihan 1 — Execution Plan

Susun execution plan untuk eksperimen Anda. Tentukan skenario, jumlah run, dan seed sebelum eksekusi.

| Run # | Skenario                | Seed | Parameter Kunci          | Status  |
| ----- | ----------------------- | ---- | ------------------------ | ------- |
| 1     | Collaborative Filtering | 42   | Train-Test Split = 80:20 | Planned |
| 2     | Collaborative Filtering | 123  | Train-Test Split = 80:20 | Planned |
| 3     | Collaborative Filtering | 2025 | Train-Test Split = 80:20 | Planned |
| 4     | Content-Based Filtering | 42   | Train-Test Split = 80:20 | Planned |
| 5     | Content-Based Filtering | 123  | Train-Test Split = 80:20 | Planned |
| 6     | Content-Based Filtering | 2025 | Train-Test Split = 80:20 | Planned |

**Total skenario:** 2
**Run per skenario:** 3
**Total run keseluruhan:** 6

---

## Latihan 2 — Data Log Terstruktur

Desain format data log untuk eksperimen Anda. Tentukan field apa saja yang akan dicatat.

**Identitas:**
| Field     | Contoh                  |
| --------- | ----------------------- |
| Run ID    | run-001                 |
| Timestamp | 2026-06-28 10:30:00     |
| Skenario  | Collaborative Filtering |

**Konfigurasi:**
| Field            | Contoh                                           |
| ---------------- | ------------------------------------------------ |
| Seed             | 42                                               |
| Dataset          | Kaggle E-commerce Product Recommendation Dataset |
| Train-Test Split | 80:20                                            |
| Framework        | Scikit-learn 1.9.0                               |

**Hasil:**
| Metrik         | Tipe Data | Range Valid |
| -------------- | --------- | ----------- |
| Precision      | Float     | 0.0 – 1.0   |
| Recall         | Float     | 0.0 – 1.0   |
| F1-Score       | Float     | 0.0 – 1.0   |
| Execution Time | Float     | > 0 detik   |

**Format output:**[✓] CSV / [ ] JSON / [ ] Database / [ ] Lainnya: -

---

## Latihan 3 — Anomaly Protocol

Rencanakan bagaimana menangani anomali. Untuk setiap jenis, tentukan langkah yang diambil.

| Jenis Anomali                 | Contoh                                                 | Tindakan                                                                                           |
| ----------------------------- | ------------------------------------------------------ | -------------------------------------------------------------------------------------------------- |
| Run gagal (crash)             | Program berhenti saat proses rekomendasi               | Dokumentasikan penyebab, perbaiki kesalahan, kemudian jalankan ulang dengan konfigurasi yang sama. |
| Hasil ekstrem                 | Nilai Precision atau Recall jauh berbeda dari run lain | Periksa dataset, parameter, dan random seed, kemudian lakukan validasi ulang.                      |
| Waktu eksekusi anomali        | Waktu proses jauh lebih lama dibanding run lain        | Periksa penggunaan CPU/RAM dan ulangi eksperimen setelah kondisi komputer stabil.                  |
| Inkonsistensi dengan run lain | Hasil berubah meskipun konfigurasi sama                | Pastikan dataset, library, dan random seed tidak berubah sebelum menjalankan ulang.                |

**Prinsip:** Detect → Investigate → Document → Decide

---

## Refleksi

> Pernahkah Anda melaporkan hasil riset/tugas dari single run? Apa risikonya? Bagaimana multiple run mengubah kepercayaan terhadap hasil?

**Pengalaman sebelumnya:**
> Pada tugas sebelumnya, hasil biasanya diperoleh hanya dari satu kali menjalankan program. Cara tersebut berisiko menghasilkan kesimpulan yang kurang akurat karena hasil dapat dipengaruhi oleh faktor acak atau kondisi tertentu.
**Yang akan dilakukan berbeda:**
> Pada penelitian ini, eksperimen akan dijalankan beberapa kali dengan random seed yang telah ditentukan sebelumnya. Hasil dari setiap run akan dicatat, kemudian dihitung rata-rata dan dibandingkan agar kesimpulan yang diperoleh lebih dapat dipercaya.