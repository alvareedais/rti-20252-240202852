# WS-06: System-Experiment Mapping

> **Bab 6 — System Design sebagai Experimental Artifact**

---

## Ringkasan Materi

### Sistem = Instrumen Pengujian, Bukan Produk

Seorang engineer bertanya "apakah sistem bekerja?" — seorang peneliti bertanya "apa yang bisa dibuktikan sistem ini?" Sistem dalam riset adalah **artifact** — objek yang sengaja dibuat untuk menguji klaim spesifik.

### System as Experiment Model

```
RQ → Variable → System Component → Experimental Setup → Output
```

Setiap komponen sistem harus bisa ditelusuri ke variabel riset (top-down), dan setiap pengukuran harus menjawab RQ (bottom-up).

### Mapping Variabel ke Komponen

| Tipe Variabel | Peran di Sistem | Contoh |
|---------------|----------------|--------|
| **IV** (Independent) | Modul yang bisa di-toggle/swap | Algoritma A vs B |
| **DV** (Dependent) | Modul pengukuran | Logger, metrics collector |
| **CV** (Control) | Config yang dikunci | Dataset, parameter tetap |

Jika variabel tidak bisa di-map ke komponen apapun → arsitektur perlu didesain ulang.

### 4 Prinsip Desain Eksperimental

| Prinsip | Pertanyaan Kunci |
|---------|-----------------|
| **Traceability** | Komponen ini melayani variabel yang mana? |
| **Modularity** | Bisakah IV diubah tanpa memengaruhi yang lain? |
| **Controllability** | Apakah CV dieksternalisasi ke config file? |
| **Measurability** | Apakah sistem otomatis menghasilkan data yang dibutuhkan? |

### Variable Isolation melalui Arsitektur

- **Modular architecture** — Pisahkan berdasarkan variabel
- **Configuration-driven** — Ubah config (YAML/JSON), bukan code
- **Feature toggles** — On/off flag untuk ablation study

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan sistem | Memenuhi kebutuhan user | Menguji hipotesis, menghasilkan bukti |
| Arsitektur | Optimasi performa & skalabilitas | Optimasi isolasi variabel & reprodusibilitas |
| Konfigurasi | Sering hardcoded | Dieksternalisasi ke config file |
| Fitur tambahan | Menambah nilai user | Menambah noise jika tidak terkait RQ |

### Istilah Penting

- **Artifact** — Objek yang sengaja dibuat untuk memecahkan masalah atau menguji proposisi
- **Traceability** — Kemampuan menelusuri hubungan RQ → variabel → komponen → output
- **Variable Isolation** — Mengubah hanya satu variabel sambil menahan yang lain konstan
- **Ablation Study** — Menguji kontribusi tiap komponen dengan melepasnya satu per satu
- **Configuration-driven Execution** — Semua parameter di config file, bukan hardcoded

---

## Template A.6 — Mapping RQ ke Arsitektur Sistem

```
SYSTEM-EXPERIMENT MAPPING

Research Question:
Apakah Collaborative Filtering menghasilkan precision dan recall lebih tinggi dibandingkan Content-Based Filtering pada sistem rekomendasi produk e-commerce?

| Variabel                    | Tipe | Komponen Sistem       | Cara Manipulasi / Pengukuran                  |
| --------------------------- | ---- | --------------------- | --------------------------------------------- |
| Jenis algoritma (CF vs CBF) | IV   | Recommendation Engine | Mengganti parameter `algorithm_type`          |
| Precision & Recall          | DV   | Evaluation Module     | Sistem otomatis menghitung precision & recall |
| Dataset pengguna            | CV   | Dataset Loader        | Menggunakan dataset yang sama                 |
| Jumlah data train/test      | CV   | Experiment Controller | Split data dibuat tetap                       |
| Hyperparameter              | CV   | Configuration File    | Parameter dikunci di config                   |


4 Prinsip Desain:
  [✓] Traceability — Setiap komponen bisa ditelusuri ke variabel
  [✓] Variable Isolation — IV bisa diubah tanpa mengubah CV
  [✓] Measurement Integration — Pengukuran DV built-in
  [✓] Reproducibility — Setup bisa direkonstruksi

Experimental Setup:
  Input data     : Dataset interaksi pengguna e-commerce
  Parameter      : Jenis algoritma, train-test split, hyperparameter
  Output format  : Precision & Recall
```

---

## Latihan 1 — Variable-to-Component Mapping

Gunakan RQ dan variabel dari WS-05. Petakan ke komponen sistem.

**RQ:** Apakah Collaborative Filtering menghasilkan precision dan recall lebih tinggi dibandingkan Content-Based Filtering pada sistem rekomendasi produk e-commerce?

| Variabel           | Tipe | Komponen Sistem       | Cara Manipulasi / Pengukuran |
| ------------------ | ---- | --------------------- | ---------------------------- |
| Jenis algoritma    | IV   | Recommendation Engine | Mengganti algoritma CF ↔ CBF |
| Precision & Recall | DV   | Evaluation Module     | Perhitungan otomatis         |
| Dataset            | CV   | Dataset Loader        | Dataset dibuat sama          |
| Hyperparameter     | CV   | Config File           | Nilai parameter dikunci      |


**Apakah semua variabel bisa di-map?** [✓] Ya / [ ] Tidak
> Jika tidak, komponen apa yang perlu ditambahkan? _________

---

## Latihan 2 — 4 Prinsip Desain

Evaluasi desain sistem terhadap 4 prinsip.

| Prinsip         | Status | Bukti / Penjelasan           |
| --------------- | ------ | ---------------------------- |
| Traceability    | ✅      | Semua modul terkait variabel |
| Modularity      | ✅      | Algoritma dapat diganti      |
| Controllability | ✅      | Parameter di config file     |
| Measurability   | ✅      | Metrik dihitung otomatis     |


**Prinsip mana yang paling sulit dipenuhi?** Variable Isolation
**Strategi untuk mengatasinya:**
> Menggunakan dataset, preprocessing, dan parameter yang sama agar hanya algoritma yang berubah saat eksperimen dilakukan

---

## Latihan 3 — Ablation Study Planning

Jika sistem memiliki 3 komponen utama, rencanakan ablation study.

| Kondisi | Komponen A (CF) | Komponen B (Preprocessing) | Komponen C (Evaluation) | Hasil yang Diharapkan    |
| ------- | --------------- | -------------------------- | ----------------------- | ------------------------ |
| Full    | ✅               | ✅                          | ✅                       | Hasil terbaik            |
| – A     | ❌ (CBF)         | ✅                          | ✅                       | Precision menurun        |
| – B     | ✅               | ❌                          | ✅                       | Data kurang optimal      |
| – C     | ✅               | ✅                          | ❌                       | Tidak ada evaluasi valid |


**Komponen mana yang diprediksi paling berkontribusi?** Recommendation Engine (algoritma rekomendasi)
**Mengapa?**
> Karena algoritma menentukan bagaimana sistem memprediksi preferensi pengguna sehingga sangat mempengaruhi precision dan recall.

---

## Refleksi

> Apa risiko jika sistem dibangun seperti produk (monolitik, fitur lengkap) lalu baru dilakukan eksperimen? Mengapa arsitektur modular penting untuk riset?

**Jawaban:**
> Jika sistem dibangun seperti produk monolitik dengan banyak fitur, maka eksperimen akan sulit dilakukan karena perubahan satu komponen dapat mempengaruhi komponen lain. Arsitektur modular penting dalam riset karena memudahkan isolasi variabel, penggantian komponen, dan reproduksi eksperimen secara adil dan terkontrol.
> ___________________________________________________
