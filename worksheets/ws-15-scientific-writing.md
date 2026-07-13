# WS-15: Scientific Writing

> **Bab 15 — Penulisan Ilmiah**

---

## Ringkasan Materi

### Scientific Argument Flow

```
Problem → Gap → RQ → Method → Result → Analysis → Conclusion → Contribution
```

Paper ilmiah adalah **satu argumen utuh** dari masalah ke kontribusi. Setiap node harus terhubung logis ke node sebelum dan sesudahnya.

### Struktur IMRAD

| Section | Peran | Pertanyaan Kunci |
|---------|-------|-----------------|
| **Introduction** | Motivasi + frame | Why is this needed? |
| **Method** | Deskripsi (reproducible) | How was it done? |
| **Results** | Laporan objektif | What was found? |
| **Discussion** | Interpretasi + refleksi | What does it mean? |
| **Conclusion** | Ringkasan + kontribusi | So what? |

### Logical Flow — "Red Thread"

Setiap paragraf menjawab satu pertanyaan dan memicu pertanyaan berikutnya. Alur logis ini harus terasa di tiga level:
1. **Antar-kalimat** dalam paragraf
2. **Antar-paragraf** dalam section
3. **Antar-section** dalam paper

### Internal Consistency

Setiap elemen yang dijanjikan di Introduction harus hadir di Discussion/Conclusion.

**Consistency Matrix:**
```
           Intro  Method  Result  Discuss  Conclude
RQ1          ✓      ✓       ✓       ✓        ✓
RQ2          ✓      ✓       ✓       ✗ ←      ✓
Metrik-X     ✗      ✗       ✓ ←     ✗        ✗
```
**Masalah:** RQ2 dibahas di semua bagian kecuali Discussion. Metrik-X muncul di Result tapi tidak diperkenalkan di Method.

### Writing Quality Triad

| Kualitas | Deskripsi | Contoh Buruk → Baik |
|----------|----------|---------------------|
| **Clarity** | Dipahami sekali baca | "Performa meningkat" → "Accuracy meningkat dari 85.3% ke 89.7%" |
| **Precision** | Istilah eksak, tanpa ambiguitas | "signifikan" → "signifikan secara statistik (p=0.003, d=1.2)" |
| **Conciseness** | Setiap kata menambah informasi | Hapus kalimat redundan, filler words |

### Urutan Penulisan yang Disarankan

1. **Method & Results** — paling stabil, tulis pertama
2. **Discussion** — interpretasi berdasarkan hasil
3. **Introduction** — frame sesuai temuan aktual
4. **Abstract & Conclusion** — terakhir

### Target Jumlah Kata

| Section | Target |
|---------|--------|
| Introduction | 500–700 |
| Related Work | 700–1000 |
| Method | 800–1200 |
| Results | 500–800 |
| Discussion | 600–900 |
| Conclusion | 200–400 |

### Jebakan Kognitif

1. "Lebih panjang = lebih lengkap" → conciseness lebih berharga
2. "Introduction harus ditulis pertama" → justru ditulis terakhir
3. "Jargon teknis = lebih ilmiah" → clarity lebih penting
4. "Discussion = ringkasan Results" → Discussion = interpretasi + konteks

---

## Template A.15 — Paper Structure Checklist

```
PAPER STRUCTURE CHECKLIST

Title   : Perbandingan Collaborative Filtering dan Content-Based Filtering
          pada Sistem Rekomendasi Produk Menggunakan Dataset Amazon Beauty

Target  : [ ] Jurnal  [ ] Konferensi  [✓] Laporan

Section Check:
  [✓] Abstract — masalah, metode, hasil utama, kontribusi (max 250 kata)
  [✓] Introduction — konteks → gap → RQ → kontribusi → struktur paper
  [✓] Related Work — concept-centric, gap positioning
  [✓] Method — reproducible: desain, variabel, metrik, setup, prosedur
  [✓] Results — tabel + grafik + observasi (tanpa interpretasi)
  [✓] Discussion — interpretasi, perbandingan, implikasi, limitation
  [✓] Conclusion — jawaban RQ, kontribusi, future work

Consistency Matrix:
  [✓] RQ di Introduction = RQ di Method = RQ di Conclusion
  [✓] Variabel di Method = variabel di Results
  [✓] Klaim di Discussion didukung data di Results
  [✓] Limitasi di Discussion di-address di Conclusion/Future Work

Writing Quality:
  [✓] Clarity — mudah dipahami tanpa re-read
  [✓] Precision — tidak ada istilah ambigu
  [✓] Conciseness — tidak ada kalimat redundan
```

---

## Latihan 1 — Paper Outline

Buat outline paper untuk riset Anda menggunakan struktur IMRAD.

| Section          | Konten Utama (2–3 kalimat)                                                                                                                                                                                                                                                                                                                                                                                         |  Target Kata |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -----------: |
| **Abstract**     | Penelitian ini membandingkan performa **Collaborative Filtering (CF)** dan **Content-Based Filtering (CBF)** pada sistem rekomendasi produk menggunakan dataset Amazon Beauty. Evaluasi dilakukan menggunakan metrik **Accuracy** berdasarkan beberapa kali pengujian. Hasil menunjukkan CF memperoleh rata-rata Accuracy sedikit lebih tinggi daripada CBF, namun perbedaannya tidak signifikan secara statistik. |  **200–250** |
| **Introduction** | Menjelaskan pentingnya sistem rekomendasi pada platform e-commerce untuk membantu pengguna menemukan produk yang relevan. Penelitian terdahulu menunjukkan CF dan CBF memiliki kelebihan masing-masing, namun perbandingan keduanya pada dataset Amazon Beauty dengan prosedur evaluasi yang sama masih terbatas. Penelitian ini bertujuan mengetahui apakah terdapat perbedaan performa kedua metode tersebut.    |  **500–700** |
| **Related Work** | Membahas konsep dasar sistem rekomendasi, Collaborative Filtering, Content-Based Filtering, penelitian terdahulu, serta research gap yang menjadi dasar penelitian. Selain itu dijelaskan posisi penelitian ini dibandingkan penelitian sebelumnya.                                                                                                                                                                | **700–1000** |
| **Method**       | Menjelaskan dataset Amazon Beauty, proses preprocessing, pembagian data train-test, implementasi Collaborative Filtering dan Content-Based Filtering, metrik Accuracy, serta prosedur eksperimen dan evaluasi yang digunakan. Seluruh tahapan dijelaskan agar penelitian dapat direplikasi.                                                                                                                        | **800–1200** |
| **Results**      | Menyajikan hasil eksperimen dalam bentuk tabel dan grafik yang membandingkan Accuracy kedua metode. Bagian ini hanya memaparkan hasil pengujian, nilai rata-rata, standar deviasi, dan hasil uji statistik tanpa memberikan interpretasi.                                                                                                                                                                          |  **500–800** |
| **Discussion**   | Menginterpretasikan hasil eksperimen dengan menjelaskan penyebab perbedaan performa CF dan CBF serta hubungannya dengan karakteristik dataset Amazon Beauty. Hasil dibandingkan dengan penelitian sebelumnya, kemudian dibahas implikasi, keterbatasan penelitian, dan peluang pengembangan di masa depan.                                                                                                         |  **600–900** |
| **Conclusion**   | Menyimpulkan jawaban terhadap research question bahwa Collaborative Filtering memperoleh Accuracy sedikit lebih tinggi dibandingkan Content-Based Filtering, namun perbedaannya belum signifikan secara statistik. Penelitian selanjutnya disarankan menggunakan dataset yang lebih besar, metrik evaluasi tambahan, serta pendekatan hybrid recommendation.                                                       |  **200–400** |


---

## Latihan 2 — Consistency Matrix

perbandingan Collaborative Filtering (CF) dan Content-Based Filtering (CBF).

| Komponen                           | Intro | Method | Result | Discussion | Conclusion |
| ---------------------------------- | :---: | :----: | :----: | :--------: | :--------: |
| **RQ1**                            |   ✓   |    ✓   |    ✓   |      ✓     |      ✓     |
| **RQ2**                            |   ✗   |    ✗   |    ✗   |      ✗     |      ✗     |
| **Metrik utama (Accuracy)**        |   ✓   |    ✓   |    ✓   |      ✓     |      ✓     |
| **Variabel IV (Metode: CF & CBF)** |   ✓   |    ✓   |    ✓   |      ✓     |      ✓     |
| **Variabel DV (Accuracy)**         |   ✓   |    ✓   |    ✓   |      ✓     |      ✓     |
| **Klaim/Kontribusi**               |   ✓   |    ✗   |    ✓   |      ✓     |      ✓     |


**Isi setiap sel:** ✓ (ada & konsisten), ✗ (missing), ~ (ada tapi inkonsisten)

**Inkonsistensi yang ditemukan:**
> Bagian Method belum menjelaskan secara eksplisit kontribusi penelitian, namun hal ini masih dapat diterima karena kontribusi utama biasanya dijelaskan pada Introduction, dibuktikan pada Results, dibahas pada Discussion, dan dirangkum kembali pada Conclusion. Selain itu, penelitian ini hanya memiliki satu Research Question (RQ1) sehingga RQ2 tidak digunakan.

**Tindakan perbaikan:**
> Menambahkan penjelasan singkat pada bagian Method mengenai tujuan eksperimen dan prosedur evaluasi agar selaras dengan Research Question. Memastikan seluruh bagian paper secara konsisten menggunakan metrik Accuracy serta membahas perbandingan Collaborative Filtering dan Content-Based Filtering sesuai tujuan penelitian.

---

## Latihan 3 — Writing Quality Check

Ambil satu paragraf dari tulisan Anda (atau tulis paragraf baru) dan evaluasi kualitasnya.

**Paragraf asli:**
> Penelitian ini membandingkan Collaborative Filtering dan Content-Based Filtering menggunakan dataset Amazon Beauty. Hasil penelitian menunjukkan Collaborative Filtering memiliki performa yang lebih baik dibandingkan Content-Based Filtering. Oleh karena itu, metode Collaborative Filtering lebih baik digunakan dalam sistem rekomendasi.

| Kriteria        | Evaluasi                                                                                   | Perbaikan                                                                        |
| --------------- | ------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------- |
| **Clarity**     | Kalimat "performa lebih baik" masih ambigu karena tidak menjelaskan metrik yang digunakan. | Jelaskan bahwa yang dibandingkan adalah **Accuracy**.                            |
| **Precision**   | Tidak mencantumkan hasil pengukuran maupun kondisi eksperimen.                             | Tambahkan nilai Accuracy rata-rata serta hasil uji statistik (misalnya p-value). |
| **Conciseness** | Kalimat terakhir menggeneralisasi hasil tanpa mempertimbangkan konteks penelitian.         | Ringkas menjadi kesimpulan yang sesuai dengan ruang lingkup penelitian.          |


**Paragraf setelah perbaikan:**
> Penelitian ini membandingkan metode Collaborative Filtering (CF) dan Content-Based Filtering (CBF) menggunakan dataset Amazon Beauty. Berdasarkan hasil eksperimen, CF memperoleh rata-rata Accuracy sebesar 89,1%, sedangkan CBF memperoleh 88,9%. Meskipun CF memiliki Accuracy sedikit lebih tinggi, hasil uji statistik menunjukkan p = 0,17, sehingga perbedaan tersebut tidak signifikan. Oleh karena itu, kedua metode memiliki performa yang relatif sebanding pada dataset yang digunakan, dengan CF hanya menunjukkan keunggulan kecil pada metrik Accuracy.

---

## Refleksi

> Apa perbedaan antara menulis "tentang" riset dan menulis sebagai "argumen" riset? Bagaimana urutan penulisan (Method → Discussion → Introduction) mengubah kualitas tulisan?

> Menulis "tentang" riset hanya menjelaskan apa yang dilakukan selama penelitian, sedangkan menulis sebagai "argumen" riset bertujuan menunjukkan bahwa setiap keputusan penelitian didukung oleh bukti yang mampu menjawab research question. Dengan demikian, setiap bagian paper saling terhubung mulai dari permasalahan, metode, hasil, hingga kesimpulan. Urutan penulisan dimulai dari Method, kemudian Results dan Discussion, lalu Introduction membantu penulis menyusun latar belakang yang benar-benar sesuai dengan hasil penelitian, sehingga alur tulisan menjadi lebih logis, konsisten, dan mudah dipahami.

> ___________________________________________________
