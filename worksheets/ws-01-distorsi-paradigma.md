# WS-01: Distorsi & Paradigma

> **Bab 1 — Research Mindset in IT**

---

## Ringkasan Materi

### Research Trust Model

Pengetahuan ilmiah tidak muncul langsung dari kenyataan. Ia melewati **6 tahap transformasi** yang masing-masing rawan distorsi:

```
Reality → Data → Processing → Analysis → Inference → Knowledge
```

Etika mencegah distorsi yang disengaja (fabrikasi, cherry-picking). Validitas mendeteksi distorsi yang tidak disengaja (confounding variable, sampling bias).

### Tiga Jenis Validitas

| Jenis | Pertanyaan | Contoh Ancaman |
|-------|-----------|----------------|
| **Internal Validity** | Apakah hubungan kausal benar ada? | Confounding variable |
| **External Validity** | Apakah bisa digeneralisasi? | Dataset terlalu homogen |
| **Construct Validity** | Apakah mengukur hal yang benar? | Metrik tidak sesuai klaim |

### Paradigma Riset

Mata kuliah ini menggunakan pendekatan **Positivist** (fenomena TI bisa diukur objektif melalui eksperimen terkontrol) diperkuat **Design Science Research** (artefak dibuat sebagai instrumen pengujian hipotesis, bukan tujuan akhir).

### Mode Berpikir Peneliti

**Curious** (mempertanyakan fenomena) → **Critical** (mengevaluasi klaim berdasarkan bukti) → **Systematic** (merancang investigasi terstruktur dan reproducible).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Membuat sistem yang bekerja | Menghasilkan pengetahuan yang valid |
| Pertanyaan khas | "Bagaimana membuatnya jalan?" | "Apakah klaim ini benar?" |
| Ukuran sukses | Sistem berfungsi, client puas | Hipotesis terjawab, temuan tervalidasi |
| Kegagalan | Harus dihindari | Harus dilaporkan (negative result = kontribusi) |

### Istilah Penting

- **Research Mindset** — Pola pikir yang menuntut bukti dan mempertanyakan asumsi
- **Research Ethics** — Prinsip perilaku: kejujuran, objektivitas, keterbukaan, akuntabilitas
- **HARKing** — Hypothesizing After Results are Known — merumuskan hipotesis setelah melihat data
- **Falsifiability** — Hipotesis harus bisa dibuktikan salah

---

## Template A.1 — Research Mindset Self-Assessment

```
Nama Peneliti    : Alvirdaus Permathasyahidatama Abadi
Tanggal          : 8 April 2026

1. Ketika membaca klaim "metode X 95% akurat":
   - Pertanyaan pertama saya: Bagaimana cara perhitungan akurasi 95% tersebut dan apakah dataset yang digunakan sudah representatif?
   - Data yang dibutuhkan untuk verifikasi: Dataset yang digunakan, jumlah data, metode pengujian seperti train-test split atau cross-validation, serta metrik evaluasi seperti confusion matrix.

2. Posisi paradigma:
   - Pendekatan: [✓] Positivis  [ ] Interpretivis  [✓] Design Science  [ ] Mixed
   - Alasan: Karena penelitian di bidang TI umumnya mengukur performa sistem secara objektif (positivis), serta sering melibatkan pembuatan artefak seperti model atau aplikasi untuk diuji (design science).

3. Identifikasi distorsi:
   - Asumsi tersembunyi: Data yang digunakan dianggap mewakili kondisi nyata secara umum.
   - Sumber bias potensial: Dataset tidak seimbang, pemilihan data yang terbatas, atau overfitting pada data training.
   - Langkah mitigasi: Menggunakan dataset yang beragam, validasi silang (cross-validation), dan melaporkan seluruh hasil termasuk yang tidak sesuai harapan.

4. Komitmen etika:
   - Data yang tidak akan dimanipulasi: Hasil eksperimen, nilai akurasi, dan data mentah penelitian.
   - Batasan yang diakui sejak awal: Keterbatasan dataset, keterbatasan metode yang digunakan, serta kemungkinan bias dalam pengambilan data.
```

## Latihan 1 — Identifikasi Distorsi

Pilih satu paper riset di bidang TI yang mengklaim "metode X meningkatkan performa." Telusuri setiap tahap Research Trust Model.

**Paper yang dipilih:**
> Judul: Deep Learning for Image Classification Improvement
> Penulis (Tahun): John Doe (2023)

| Tahap                 | Apa yang Dilakukan                            | Potensi Distorsi                                              |
| --------------------- | --------------------------------------------- | ------------------------------------------------------------- |
| Reality → Data        | Mengambil dataset gambar dari internet        | Dataset tidak representatif (hanya gambar berkualitas tinggi) |
| Data → Processing     | Melakukan preprocessing (resize, normalisasi) | Menghapus data tertentu tanpa alasan jelas                    |
| Processing → Analysis | Melatih model deep learning                   | Overfitting pada data training                                |
| Analysis → Inference  | Menyimpulkan model lebih akurat               | Tidak membandingkan dengan baseline yang adil                 |
| Inference → Knowledge | Mengklaim metode terbaik                      | Generalisasi berlebihan                                       |


**Distorsi paling besar di tahap:** Processing → Analysis

**Dua distorsi spesifik yang teridentifikasi:**
1. Overfitting karena model terlalu kompleks terhadap dataset kecil
2. Dataset tidak representatif sehingga hasil tidak bisa digeneralisasi

---

## Latihan 2 — Analisis Kasus Etika

Skenario: Seorang peneliti menemukan bahwa jika 3 data point outlier dihapus, hasil eksperimennya menjadi signifikan. Dengan outlier, hasilnya tidak signifikan.

| Perspektif       | Analisis                                                                                       |
| ---------------- | ---------------------------------------------------------------------------------------------- |
| Kejujuran ilmiah | Peneliti harus melaporkan hasil dengan dan tanpa outlier agar tidak menyesatkan                |
| Transparansi     | Harus menjelaskan alasan penghapusan outlier dan dampaknya terhadap hasil                      |
| Peer review      | Reviewer kemungkinan akan mempertanyakan validitas jika outlier dihapus tanpa justifikasi kuat |


**Keputusan akhir dan justifikasi:**
> Peneliti harus melaporkan kedua hasil (dengan dan tanpa outlier) serta memberikan alasan ilmiah terkait keberadaan outlier. Menghapus data tanpa transparansi melanggar etika penelitian dan dapat menyesatkan kesimpulan.
---

## Latihan 3 — Posisi Paradigma

**Topik riset:** Pengaruh penggunaan aplikasi belajar online terhadap nilai mahasiswa

| Kriteria                      | Positivis                    | Interpretivis           | Design Science                      |
| ----------------------------- | ---------------------------- | ----------------------- | ----------------------------------- |
| Kesesuaian dengan topik (1–5) | 5                            | 3                       | 2                                   |
| Jenis data yang dikumpulkan   | Nilai ujian, durasi belajar  | Pendapat mahasiswa      | Aplikasi belajar                    |
| Limitasi paradigma            | Tidak tahu perasaan pengguna | Tidak bisa diukur pasti | Fokus buat aplikasi, bukan analisis |

**Paradigma yang dipilih:** Positives
**Alasan:** Karena penelitian ini melihat hubungan antara penggunaan aplikasi dan nilai mahasiswa yang bisa diukur dengan angka, jadi lebih cocok pakai pendekatan yang objektif dan berbasis data.

---

## Refleksi

> Sebelum membaca materi ini, apakah pernah mempertanyakan klaim "95% akurat"? Setelah memahami rantai distorsi, pertanyaan apa yang sekarang akan diajukan saat membaca paper?

**Jawaban:**
> Sebelumnya saya langsung percaya dengan klaim seperti “95% akurat”. Tetapi, setelah memahami tentang distorsi, saya akan bertanya apakah data yang digunakan itu benar-benar dari kondisi nyata, bagaimana cara menghitung akurasinya, dan apakah hasilnya bisa benar-benar dipakai di dunia nyata.
> ___________________________________________________
