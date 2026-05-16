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

## A.5 — Definisi Variabel, Metrik & Justifikasi

## VARIABLE & METRIC DEFINITION

### Research Question
Bagaimana algoritma Weighted Probability memengaruhi peluang memperoleh item rare pada sistem gacha game?

| Variabel | Tipe | Konsep | Metrik | Skala | Satuan | Cara Mengukur | Justifikasi |
|----------|------|--------|--------|--------|--------|----------------|-------------|
| Weighted Probability | IV | Algoritma pengaturan peluang item | Nilai drop rate per pull | Ratio | % | Menghitung perubahan probabilitas tiap pull | Weighted probability merupakan inti sistem probabilitas pada gacha modern |
| Jumlah Pull | IV | Banyaknya percobaan gacha | Pull ke-1, ke-2, dst | Ratio | Pull | Menghitung total percobaan pemain | Jumlah pull memengaruhi perubahan probabilitas |
| Peluang Item Rare | DV | Output probabilitas sistem | Cumulative probability rare item | Ratio | % | Menghitung peluang total memperoleh rare item | Digunakan untuk mengukur efektivitas algoritma |
| Pity Threshold | CV | Batas jaminan rare item | Maksimum pull sebelum guaranteed | Ratio | Pull | Menentukan batas pity system | Digunakan untuk mengontrol distribusi probabilitas |
| Base Probability | CV | Peluang awal rare item | Drop rate awal | Ratio | % | Mengambil nilai probabilitas awal | Digunakan sebagai pembanding weighted probability |

---

# Alignment Check

Problem → Concept → Variable → Metric → Data → Result

- [x] Setiap langkah terdokumentasi
- [x] Tidak ada lompatan logis
- [x] Metrik sesuai dengan konsep yang diukur

---

## Latihan 1 — Operationalization Chain

Gunakan RQ dari WS-04. Definisikan variabel dan metriknya.

**RQ:** Bagaimana algoritma Weighted Probability memengaruhi peluang memperoleh item rare pada sistem gacha game?

| Variabel | Tipe | Konsep Abstrak | Metrik Konkret | Skala (NOIR) | Satuan |
|----------|------|---------------|----------------|-------------|--------|
| Weighted Probability | IV | Sistem probabilitas dinamis | Persentase perubahan drop rate | Ratio | % |
| Jumlah Pull | IV | Percobaan gacha | Banyaknya pull | Ratio | Pull |
| Peluang Item Rare | DV | Keberhasilan sistem | Cumulative probability | Ratio | % |
| Pity Threshold | CV | Sistem jaminan rare item | Maksimum pull pity | Ratio | Pull |
| Base Probability | CV | Probabilitas awal | Drop rate awal | Ratio | % |

---

**Apakah ada lompatan logis dalam rantai?** [ ] Ya / [x] Tidak
> Tidak ada lompatan logis karena setiap tahapan penelitian saling terhubung secara jelas, mulai dari konsep Weighted Probability, variabel probabilitas gacha, metrik cumulative probability, data perubahan drop rate, hingga hasil berupa peluang memperoleh item rare.

---

## Latihan 2 — Evaluasi Metrik

Evaluasi metrik DV yang dipilih di Latihan 1 menggunakan 3 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Representative | 5 | *Cumulative probability secara langsung merepresentasikan peluang memperoleh item rare pada algoritma Weighted Probability.* |
| Sensitive | 4 | *Metrik cukup sensitif karena perubahan kecil pada drop rate atau pity system dapat memengaruhi cumulative probability.* |
| Feasible | 5 | *Data probabilitas dan jumlah pull mudah diperoleh melalui simulasi maupun dokumentasi sistem gacha.* |

---

**Apakah perlu secondary metric?** [x] Ya / [ ] Tidak
> Jika ya, apa dan mengapa? *Secondary metric yang digunakan adalah jumlah pull rata-rata hingga memperoleh item rare. Metrik ini digunakan untuk mendukung cumulative probability agar hasil analisis lebih mudah dipahami dalam konteks implementasi sistem gacha.*


**Contoh kasus ceiling effect untuk metrik ini:**
> *Ceiling effect dapat terjadi ketika pity system mencapai guaranteed rare item, misalnya pada pull ke-90 peluang rare item menjadi 100%. Pada kondisi tersebut cumulative probability tidak lagi menunjukkan variasi performa algoritma karena semua pemain pasti memperoleh rare item.*

---

## Latihan 3 — Data Quality Check

Bayangkan data yang akan dikumpulkan dari eksperimen. Evaluasi 4 dimensi kualitas data.

| Dimensi | Pertanyaan | Jawaban | Strategi Mitigasi |
|---------|-----------|---------|------------------|
| Completeness | Apakah semua data point terkumpul? | Data probabilitas, jumlah pull, dan perubahan drop rate dapat terkumpul secara lengkap melalui simulasi algoritma gacha. | Menggunakan simulasi otomatis agar seluruh data pull tercatat tanpa ada data yang hilang. |
| Consistency | Apakah ada kontradiksi internal? | Kemungkinan terdapat inkonsistensi jika nilai cumulative probability tidak sesuai dengan perubahan drop rate pada setiap pull. | Memvalidasi hasil perhitungan probabilitas menggunakan rumus dan pengecekan ulang pada setiap tahap simulasi. |
| Validity | Apakah benar-benar mengukur yang dimaksud? | Data yang dikumpulkan benar-benar mengukur efektivitas algoritma Weighted Probability terhadap peluang rare item. | Menggunakan metrik cumulative probability dan jumlah pull yang langsung berkaitan dengan sistem probabilitas gacha. |
| Representativeness | Apakah sampel mewakili populasi target? | Sampel berupa simulasi pull mewakili mekanisme umum sistem gacha modern yang menggunakan weighted probability dan pity system. | Menggunakan parameter probabilitas yang umum digunakan pada game gacha seperti Genshin Impact agar hasil lebih representatif. |

---

## Refleksi

> Mengapa memilih metrik setelah melihat data dianggap p-hacking? Apa bedanya dengan eksplorasi data yang sah?

**Jawaban:**
> Memilih metrik setelah melihat data dianggap p-hacking karena peneliti bisa memilih metrik yang paling mendukung hasil yang diinginkan, sehingga penelitian menjadi bias dan kurang valid.

> Sedangkan eksplorasi data yang sah dilakukan untuk mencari pola atau insight tambahan tanpa mengubah metrik utama yang sudah ditentukan sejak awal. Hasil eksplorasi dilaporkan sebagai temuan tambahan, bukan bukti utama penelitian.
