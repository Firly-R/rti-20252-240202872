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

Mata kuliah ini menggunakan pendekatan **Positivist** (fenomena TI bisa diukur objektif melalui eksperimen terkontrol) diperkuat **Design Science Research** (DSR). Penting untuk membedakan keduanya:

| Paradigma | Cara Kerja | Contoh di TI |
|-----------|-----------|---------------|
| **Positivis** | Uji hipotesis dengan eksperimen terkontrol | Apakah CNN lebih akurat dari RF pada dataset X? |
| **Design Science Research** | Bangun artefak (sistem/model/framework) untuk menguji proposisi | Dapatkah arsitektur hybrid CNN+LSTM membuktikan peningkatan recall ≥5%? |
| **Interpretivis** | Pahami makna melalui konteks & kualitatif | Bagaimana peneliti manafsirkan anomali data sensor IoT? |

Dalam DSR, artefak **bukan tujuan akhir** — ia adalah instrumen untuk menghasilkan pengetahuan. Pertanyaan riset tetap harus difalsifikasi.

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

## A.1 — Research Mindset Self-Assessment

```
Nama Peneliti    : Muhammad Firly Ramadhan
Tanggal          : 24 April 2026

1. Ketika membaca klaim "metode X 95% akurat":
   - Pertanyaan pertama saya: Apakah akurasi tersebut dihitung dari dataset yang cukup besar dan beragam, serta apakah data training dan testing dipisahkan dengan benar?
   - Data yang dibutuhkan untuk verifikasi: Dataset yang digunakan, jumlah data, pembagian data (train, validasi, test), serta metrik evaluasi seperti confusion matrix, precision, dan recall.

2. Posisi paradigma:
   - Pendekatan: [✔] Positivis  [ ] Interpretivis  [✔] Design Science  [ ] Mixed
   - Alasan: Penelitian menggunakan pendekatan kuantitatif dengan mengukur performa model melalui akurasi (positivis), serta membangun sistem face recognition sebagai artefak (design science).

3. Identifikasi distorsi:
   - Asumsi tersembunyi: Sistem dianggap akurat dan dapat digunakan secara umum meskipun hanya diuji pada dataset yang terbatas.
   - Sumber bias potensial: Dataset hanya terdiri dari sedikit individu dan kondisi gambar yang tidak beragam (pencahayaan, blur, sudut wajah).
   - Langkah mitigasi: Menambah jumlah dataset yang lebih beragam, menggunakan metode evaluasi yang lebih lengkap, serta melakukan pengujian pada data yang benar-benar baru.

4. Komitmen etika:
   - Data yang tidak akan dimanipulasi: Data hasil pengujian termasuk data yang menghasilkan kesalahan (false recognition) tidak akan dihapus atau diubah.
   - Batasan yang diakui sejak awal: Dataset yang digunakan terbatas dan hasil penelitian belum tentu dapat digeneralisasi ke kondisi dunia nyata yang lebih luas.
```

---

## Latihan 1 — Identifikasi Distorsi

**Paper yang dipilih:**
> Judul: Face Recognition Untuk Akses Pegawai Bank Menggunakan Deep Learning 
Dengan Metode CNN.
> Penulis (Tahun): Muhammad Arsal, Bheta Agus Wardijono, Dina Anggraini (2020)

| Tahap | Apa yang Dilakukan | Potensi Distorsi |
|-------|-------------------|-----------------|
| Reality → Data | Mengambil data wajah pegawai bank (5 orang) | Dataset sangat kecil dan tidak representatif |
| Data → Processing | Preprocessing (grayscale, cropping, dll) | Kualitas gambar berbeda (blur, pencahayaan) |
| Processing → Analysis | Training CNN (VGG16) dengan data train, validasi, test | Overfitting karena data sedikit |
| Analysis → Inference | Menghasilkan akurasi 92%–95% | Hanya pakai akurasi, tidak pakai precision/recall |
| Inference → Knowledge | Menyimpulkan sistem berhasil digunakan di bank | Generalisasi berlebihan (belum diuji di lingkungan lain) |

**Distorsi paling besar di tahap:** Dataset terlalu kecil dan tidak beragam

**Dua distorsi spesifik yang teridentifikasi:**
1. Dataset hanya terdiri dari 5 orang
2. Kualitas gambar mempengaruhi hasil (blur menyebabkan gagal identifikasi)

---

## Latihan 2 — Analisis Kasus Etika

Skenario: Seorang peneliti menemukan bahwa jika 3 data point outlier dihapus, hasil eksperimennya menjadi signifikan. Dengan outlier, hasilnya tidak signifikan.

| Perspektif | Analisis |
|------------|---------|
| Kejujuran ilmiah | Harus melaporkan hasil dengan dan tanpa outlier |
| Transparansi | Menjelaskan alasan penghapusan outlier |
| Peer review | Reviewer akan mempertanyakan manipulasi data |

**Keputusan akhir dan justifikasi:**
> Data tidak boleh dihapus sembarangan. Peneliti harus melaporkan kedua kondisi dan menjelaskan alasan keberadaan outlier.

---

## Latihan 3 — Posisi Paradigma

**Topik riset:** Face Recognition menggunakan CNN

> **Skala 1–5:** 1 = tidak sesuai sama sekali dengan topik ini, 5 = sangat sesuai dan dominan digunakan pada riset bertopik serupa.

| Kriteria | Positivis | Interpretivis | Design Science |
|----------|-----------|---------------|----------------|
| Kesesuaian dengan topik (1–5) | 5 | 1 | 4 |
| Jenis data yang dikumpulkan | *Akurasi, Data set* | *-* | *Hasil sistem* |
| Limitasi paradigma | *Terlalu fokus angka* | *Tidak cocok* | *Fokus ke artefak* |

**Paradigma yang dipilih:** Positivis + Design Science.

**Alasan:** Karena penelitian menguji akurasi sekaligus membangun sistem.

---

## Refleksi

> Sebelum membaca materi ini, apakah pernah mempertanyakan klaim "95% akurat"? Setelah memahami rantai distorsi, pertanyaan apa yang sekarang akan diajukan saat membaca paper?

**Jawaban:**
> Sebelum mempelajari materi ini, saya cenderung langsung percaya pada klaim akurasi yang tinggi. Namun setelah memahami adanya potensi distorsi, saya akan mempertanyakan ukuran dataset, metode evaluasi, serta apakah hasil tersebut dapat digeneralisasi ke kondisi lain.

