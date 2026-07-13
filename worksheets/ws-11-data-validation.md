# WS-11: Data Validation & Integrity

> **Bab 11 — Validasi Data & Integritas**

---

## Ringkasan Materi

### Data Trust Model

```
Raw Data → Data Cleaning → Consistency Check → Validation Process → Trusted Data
```

Data mentah belum bisa dipercaya. Harus melewati pipeline validasi sebelum siap untuk analisis statistik.

### Empat Pilar Data Quality

| Pilar | Deskripsi | Contoh Pelanggaran |
|-------|----------|-------------------|
| **Accuracy** | Nilai dalam range masuk akal | Akurasi = 1.5 (di luar [0,1]) |
| **Consistency** | Format seragam di semua run | Run 1: CSV, Run 2: JSON |
| **Completeness** | Tidak ada data hilang dari plan | 97 dari 100 run tercatat |
| **Validity** | Data sesuai desain eksperimen | Parameter baseline tercampur treatment |

### Proses Validasi Progresif

1. **Format validation** — Tipe file, header, kolom
2. **Range validation** — Nilai dalam batas logis
3. **Consistency validation** — Format seragam antar-run
4. **Logic validation** — Data cocok dengan desain eksperimen

Jika gagal di langkah awal → tidak perlu lanjut.

### Anomaly Detection — 3 Jenis

| Jenis | Deskripsi | Deteksi |
|-------|----------|---------|
| **Statistical outlier** | Nilai di luar distribusi normal | IQR: < Q1-1.5×IQR atau > Q3+1.5×IQR |
| **Contextual anomaly** | Normal absolut, abnormal dalam konteks | Run 1-10: ~91%, Run 11-20: ~88% |
| **Pattern anomaly** | Pola sistematis (bukan random) | Performa menurun berurutan |

**Prinsip:** Detect → Investigate → Document → Decide — **JANGAN langsung hapus.**

### Engineering vs Research Validation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Data sesuai spesifikasi bisnis | Data layak untuk analisis statistik |
| Missing data | Impute / set default | Investigasi penyebab → dokumentasi |
| Outlier | Bug → fix | Mungkin temuan → investigasi |
| Dokumentasi | Minimal (log error) | Komprehensif (anomali + keputusan) |

### Jebakan Kognitif

1. "Logging otomatis ≠ data benar" → bisa ada bug di logger
2. "Outlier = hapus" → bisa jadi temuan penting
3. "Dataset kecil tidak perlu validasi" → justru lebih rentan
4. "Mean normal = data benar" → [94, 95, 93, **44**, 94] → mean 84% terlihat wajar

---

## Template A.11 — Data Validation Checklist

```
DATA VALIDATION CHECKLIST

Completeness:
  [ ] Semua skenario tercakup
  [ ] Jumlah run sesuai rencana
  [ ] Tidak ada file output hilang
  Missing: ____ dari ____ data points

Format Consistency:
  [ ] Semua file format sama (CSV/JSON/...)
  [ ] Header konsisten
  [ ] Tipe data konsisten (numerik tetap numerik)

Range & Logic:
  [ ] Nilai dalam range masuk akal
  [ ] Tidak ada waktu negatif
  [ ] Metrik 0–100%, tidak di luar range
  Anomali ditemukan: ____________________

Cross-Validation:
  [ ] Run identik → hasil mendekati
  [ ] Trend konsisten dengan ekspektasi teori

Keputusan:
  [ ] Data siap analisis
  [ ] Perlu cleaning
  [✓] Perlu re-run (skenario: ____)
```

---

## Latihan 1 — Completeness Check

Verifikasi apakah semua data yang direncanakan sudah terkumpul.

| Skenario                | Run Direncanakan | Run Tercatat | Missing | Alasan                    |
| ----------------------- | ---------------- | ------------ | ------- | ------------------------- |
| Collaborative Filtering | 3                | 3            | 0       | Semua eksperimen berhasil |
| Content-Based Filtering | 3                | 3            | 0       | Semua eksperimen berhasil |



**Total expected:** 6 | **Total actual:** 6 | **Missing:** 0

**Keputusan untuk data missing:**
> Tidak terdapat data yang hilang sehingga seluruh hasil eksperimen dapat digunakan pada tahap analisis statistik.

---

## Latihan 2 — Anomaly Investigation

Periksa data Anda untuk anomali. Gunakan metode IQR atau z-score.

**Dataset sampel (atau data Anda sendiri):**

| Run | Accuracy (%) |
| --- | ------------ |
| 1   | **89.8**     |
| 2   | **90.1**     |
| 3   | **90.0**     |
| 4   | **84.7**     |
| 5   | **89.9**     |


**Deteksi outlier:**
Data terurut:

84.7, 89.8, 89.9, 90.0, 90.1

- Q1 = 89.8
- Q3 = 90.0
- IQR = 0.2
- Batas bawah = 89.8 − (1.5 × 0.2) = 89.5
- Batas atas = 90.0 + (1.5 × 0.2) = 90.3
- Outlier terdeteksi = Run 4 (84.7%)

**Investigasi (untuk setiap outlier):**

| Outlier | Nilai | Kemungkinan Penyebab                                                                                                                  | Keputusan                                                                                                                                                         |
| ------- | ----- | ------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Run 4   | 84.7% | Kemungkinan terjadi kesalahan konfigurasi parameter, proses training belum konvergen, atau terdapat gangguan saat eksekusi eksperimen | Data tidak langsung dihapus. Dilakukan investigasi dan re-run untuk memastikan apakah nilai tersebut merupakan kesalahan eksperimen atau karakteristik algoritma. |


---

## Latihan 3 — Validation Report

Buat laporan validasi ringkas untuk dataset eksperimen Anda.

**1. Completeness:** 100% data terkumpul
**2. Format:** [✓] Konsisten / [ ] Ada inkonsistensi: ____
**3. Range check (anomali):** Ditemukan satu nilai outlier pada Run 4 (84.7%) berdasarkan metode Interquartile Range (IQR). Nilai tersebut akan diverifikasi melalui proses re-run sebelum diputuskan untuk digunakan atau dikeluarkan dari analisis.
**4. Logic check:** [✓] Parameter sesuai plan / [ ] Ada ketidaksesuaian: ____

**Kesimpulan:** [✓] Data siap dianalisis, namun satu data outlier memerlukan proses verifikasi terlebih dahulu. Setelah investigasi selesai, dataset dapat digunakan untuk analisis statistik dan evaluasi performa Collaborative Filtering serta Content-Based Filtering.

---

## Refleksi

> Apa perbedaan antara "data yang benar" dan "data yang dipercaya"? Mengapa proses validasi formal diperlukan meskipun data dikumpulkan secara otomatis?

> Data yang benar belum tentu dapat langsung dipercaya. Data perlu melalui proses validasi agar dipastikan lengkap, konsisten, dan sesuai dengan rancangan eksperimen. Meskipun proses pengumpulan dilakukan secara otomatis, kesalahan konfigurasi, data yang hilang, maupun anomali masih dapat terjadi. Oleh karena itu, validasi formal diperlukan agar hasil penelitian dapat dipertanggungjawabkan secara ilmiah.
> ___________________________________________________
