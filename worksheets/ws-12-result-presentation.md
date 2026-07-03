# WS-12: Result Presentation & Visualization

> **Bab 12 — Penyajian Hasil & Visualisasi**

---

## Ringkasan Materi

### Data → Insight Model

```
Validated Data → Structured Presentation → Visualization → Pattern Recognition → Insight
```

Penyajian **mendahului** analisis. Tabel dan grafik membantu peneliti "melihat" data sebelum menghitung. Langsung ke uji statistik tanpa visualisasi berisiko kesimpulan yang secara teknis benar tapi kontekstual salah (Anscombe's Quartet, 1973).

### Tabel = Presisi, Grafik = Pola

Keduanya **saling melengkapi**:
- Tabel: angka presisi, self-contained (dipahami tanpa teks), sortable
- Grafik: pola visual, tren, perbandingan cepat

### Jenis Grafik Berdasarkan Tujuan

| Tujuan | Jenis Grafik |
|--------|-------------|
| Perbandingan antar-skenario | Bar chart (grouped/stacked) |
| Distribusi per-skenario | Box plot / violin plot |
| Tren temporal | Line chart |
| Korelasi dua variabel | Scatter plot |
| Proporsi (total = 100%) | Pie chart (hati-hati!) |

### Contoh Tabel Hasil yang Baik

| Model | Accuracy (%) | F1-Score (%) | Training Time (min) |
|-------|-------------|-------------|---------------------|
| BERT | 88.4 ± 1.2 | 87.1 ± 1.4 | 45.2 ± 3.1 |
| LSTM | 86.1 ± 1.8 | 84.5 ± 2.0 | 12.8 ± 1.2 |
| SVM | 82.3 ± 0.9 | 80.7 ± 1.1 | 0.3 ± 0.1 |

*N=10 per model. Mean ± std. Diurutkan berdasarkan Accuracy.*

### Visualization Bias — Yang Harus Dihindari

| Bias | Deskripsi | Dampak |
|------|----------|--------|
| Truncated axis | Y tidak dari 0 | Memperbesar perbedaan kecil |
| Inconsistent scale | Dua grafik skala beda | Perbandingan menyesatkan |
| Cherry-picked data | Hanya tampilkan yang "menang" | Selektif, tidak jujur |
| 3D effects | Efek 3D tanpa dimensi data ke-3 | Distorsi tanpa informasi |
| Missing error bar | Tidak ada variabilitas | Menyembunyikan ketidakpastian |

### Engineering vs Research Presentation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan grafik | Dashboard monitoring | Mendukung argumen ilmiah |
| Informasi wajib | KPI, threshold | Mean, std, CI, N, p-value |
| Bias handling | Less critical | Wajib dihindari (peer-review) |

---

## Template A.12 — Result Presentation Plan

```
RESULT PRESENTATION PLAN

Research Question : Seberapa besar signifikansi perbedaan cumulative probability dan jumlah rata-rata pull dalam memperoleh rare item antara sistem weighted probability dibandingkan sistem fixed probability?
Metrik Utama      : Cumulative Probability dan Average Pulls to Rare

Tabel Hasil:
| Skenario | Average Pulls (mean ± std) | Cum. Prob di Pull 90 (%) | n |
|----------|----------------------------|--------------------------|---|
| Kondisi A (Fixed) |  166.6 ± 0.6 pull |      41.7 ± 0.2 pull     | 10 |
| Kondisi B (Weighted)| 62.4 ± 0.3 pull |       100.0 ± 0.0 %      | 10 |

Visualisasi yang Direncanakan:
| # | Jenis Grafik | Pesan Utama | Metrik |
|---|-------------|-------------|--------|
| 1 | Line chart  | Tren peningkatan peluang rare item per pull | Cumulative Probability |
| 2 | Box plot    | Distribusi dan variabilitas jumlah pull | Average Pulls to Rare |

Bias Check:
  [X] Y-axis mulai dari 0 (atau dijustifikasi)
  [X] Error bar/CI ditampilkan
  [X] Semua data disertakan (tidak cherry-picked)
  [X] Tidak menggunakan 3D tanpa alasan
```

---

## Latihan 1 — Tabel Hasil

Buat tabel hasil eksperimen Anda (boleh dengan data simulasi jika belum punya data riil).

| Skenario | Average Pulls (mean ± std) | Cum. Prob di Pull 90 (mean ± std) | n |
|----------|----------------------|----------------------|---|
| Kondisi A (Fixed Probability) | *166.7 ± 0.6 pull* | *41.7 ± 0.2 %* | *10* |
| Kondisi B (Weighted Probability) | *62.4 ± 0.3 pull* | *100.0 ± 0.0 %* | *10* |


**Checklist tabel:**
- [x] Self-contained (judul jelas, satuan ada, N tercantum)
- [x] Mean ± std (bukan single number)
- [x] Diurutkan berdasarkan metrik utama
- [x] Format konsisten di semua baris

---

## Latihan 2 — Rencana Visualisasi

Rencanakan 2-3 grafik untuk menyajikan data dari Latihan 1. Setiap grafik = satu pesan.

| # | Jenis Grafik | Pesan | Data yang Digunakan |
|---|-------------|-------|---------------------|
| 1 | *Line chart* | *Tren peningkatan kumulatif untuk melihat kapan intervensi soft pity (pull ke-50) mulai memperlebar jarak peluang dibandingkan baseline.* | *Data Cumulative Probability dari pull ke-1 hingga ke-90 untuk kedua skenario.* |
| 2 | *Bar chart (grouped) + Error bar* | *Perbandingan rata-rata pull absolut yang dibutuhkan pemain untuk memicu satu rare item pada masing-masing kondisi.* | *Mean Average Pulls ± std untuk Kondisi A dan Kondisi B.* |
| 3 | *Box plot* | *Memvalidasi stabilitas algoritma Random Number Generator dan mendeteksi ketiadaan outlier ekstrem dari 1 juta sampel per kondisi.* | *Seluruh data raw pulls dari 10 run simulasi.* |

---

## Latihan 3 — Bias Detection

Evaluasi visualisasi berikut untuk bias (skenario dari contoh):

**Skenario:** Metode A = 91.2%, Metode B = 90.8%. Bar chart dengan Y-axis mulai dari 90%.

| Pertanyaan | Jawaban |
|-----------|---------|
| Apakah Y-axis menyesatkan? | *Ya. Sumbu Y yang dipangkas (truncated) akan memberikan ilusi optik seolah performa Metode A jauh meninggalkan Metode B, padahal selisih aktualnya kurang dari 1%.* |
| Apakah error bar ditampilkan? | *Tidak. Ketiadaan error bar menghapus konteks variabilitas; bisa jadi standar deviasinya menutupi margin selisih tersebut.* |
| Apa solusinya? | *Memulai Y-axis dari 0 dan menambahkan penanda variabilitas (error bars) pada grafik.* |

**Evaluasi grafik Anda sendiri dari Latihan 2:**
- [x] Semua bias check lulus
- [ ] Ada yang perlu diperbaiki: -

---

## Refleksi

> Mengapa tabel dan grafik keduanya diperlukan — tidak cukup salah satu saja? Pernahkah Anda membuat grafik yang (tanpa sengaja) menyesatkan?

> Tabel memastikan bahwa data yang disajikan memiliki tingkat presisi dan akurasi yang absolut, sehingga detail standar deviasi dan nilai persentase yang spesifik bisa dikutip secara objektif. Namun, deretan angka di tabel tidak mampu menyampaikan titik balik (turning point) secara instan. Grafik visual, seperti line chart, sangat krusial di sini untuk langsung menunjukkan bagaimana peluang pemain melonjak tajam tepat setelah fase soft pity dimulai. Keduanya harus berdampingan untuk menyajikan konteks secara menyeluruh tanpa mengorbankan akurasi. Menyembunyikan error bar atau memanipulasi rentang sumbu (axis) merupakan bias visual yang kini wajib dihindari.
