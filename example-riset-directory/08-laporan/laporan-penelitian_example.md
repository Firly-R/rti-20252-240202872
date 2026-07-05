# Laporan Penelitian

| Judul: | Analisis Pengaruh Algoritma Weighted Probability terhadap Peluang Rare Item pada Sistem Gacha Game |
| :---- | :---- |
| Nama: | Muhammad Firly Ramadhan |
| **NIM:** | 240202872 |
| **Mata Kuliah:** | Riset Teknologi Informasi |
| **Status Penelitian::** | Seluruh tahap (Tahap 1–5) selesai; naskah jurnal final tersedia di ([../07-manuskrip/naskah-jurnal.md](../07-manuskrip/naskah-jurnal.md)) |

---

## 1. Ringkasan Eksekutif

Penelitian ini merancang, mengimplementasikan, dan mengevaluasi secara empiris perbandingan algoritma **Fixed Probability** (baseline) dengan **Weighted Probability** bersistem *pity* (intervensi) pada mekanisme gacha game. Evaluasi dilakukan melalui eksperimen komparatif berbasis simulasi komputasi Python dengan parameter yang identik — probabilitas dasar 0,6%, *soft pity* pull ke-50, *hard pity* pull ke-70 — terhadap populasi 100.000 responden virtual, diulang sebanyak **10 kali run** menggunakan *seed* yang berbeda-beda untuk menjamin keandalan statistik.

**Temuan utama:**

- Algoritma *Weighted Probability* **memangkas rata-rata jumlah pull sebesar ~72,4%** — dari rata-rata 167,91 pull (Fixed) menjadi 46,35 pull (Weighted).
- *Cumulative probability* kedua kondisi hampir identik pada pull ke-1 hingga ke-49 (selisih < 5%), lalu **divergen tajam setelah *soft pity*** karena injeksi bobot linear.
- Pada *hard pity* (pull ke-70), sistem Weighted telah menjamin **100% pemain mendapat *rare item***, sementara Fixed hanya mencapai ~34% populasi.
- Sistem Weighted **mengeliminasi ekor distribusi tak terbatas** (*extreme variance*) yang ada pada sistem Fixed, menjamin batas pengeluaran maksimum bagi pemain.

Seluruh kode sumber, data eksperimen (10 run × 100.000 iterasi), skrip analisis, tabel, dan figure tersedia di repositori ini.

---

## 2. Latar Belakang dan Rumusan Masalah

### 2.1 Latar Belakang

Sistem *gacha* merupakan mekanisme distribusi item virtual berbasis probabilitas yang lazim digunakan pada game mobile modern sebagai strategi monetisasi. Pada implementasi awal, sistem ini bergantung pada **Fixed Probability** — yaitu peluang mendapatkan *rare item* yang konstan di setiap percobaan (*pull*). Mekanisme ini menyimpan celah berupa **ketidakpastian ekstrem** (*extreme variance*): seorang pemain bisa gagal beratus-ratus kali secara berturut-turut, yang berujung pada frustrasi dan penurunan retensi pemain.

Untuk mengatasi kelemahan tersebut, game gacha modern berevolusi menggunakan **Weighted Probability** yang dipadukan dengan *pity system*. Melalui mekanisme *soft pity* dan *hard pity*, sistem secara dinamis meningkatkan peluang pemain setelah serangkaian kegagalan hingga akhirnya memberikan jaminan pasti (100%) pada threshold tertentu. Namun, meskipun implementasi ini sangat lazim, dampak aktual dari algoritma dinamis ini terhadap *cumulative probability* secara kuantitatif masih kurang terdokumentasi dalam literatur akademik — mayoritas penelitian lebih berfokus pada dampak psikologis, perilaku perjudian, dan model penetapan harga.

### 2.2 Rumusan Masalah

> **Research Question:** Seberapa besar signifikansi perbedaan *cumulative probability* dan jumlah rata-rata *pull* dalam memperoleh *rare item* antara sistem *Weighted Probability* dibandingkan sistem *Fixed Probability*?

### 2.3 Hipotesis

Terdapat peningkatan *cumulative probability* yang signifikan dan penurunan rata-rata jumlah *pull* pada penerapan intervensi *weighted probability* dibandingkan baseline *fixed probability*, terutama saat jumlah percobaan mendekati batas *pity threshold*.

### 2.4 Tujuan Penelitian

1. Menganalisis dan membandingkan secara kuantitatif distribusi *cumulative probability* perolehan *rare item* antara algoritma Fixed Probability dan Weighted Probability.
2. Mengukur selisih rata-rata jumlah *pull* (*Average Pulls to Rare*) antara kedua kondisi.
3. Mengidentifikasi titik divergensi signifikan pada kurva kumulatif kedua algoritma.
4. Menghasilkan *prototype* simulator gacha yang dapat digunakan untuk penelitian lanjutan.

---

## 3. Metodologi dan Pelaksanaan

Penelitian dilaksanakan dalam 5 tahap (studi literatur → desain eksperimen → implementasi → eksekusi & pengumpulan data → analisis & penulisan). Bagian ini merangkum implementasi dan verifikasi setiap tahap.

### 3.1 Tahap 1 — Studi Literatur & Perumusan Masalah

**Status: Selesai.** Dilakukan kajian literatur terhadap 10+ referensi yang mencakup topik: algoritma probabilitas pada sistem *loot box* dan *gacha* (Fixed vs Weighted), *pity system* (soft pity, hard pity), dampak gacha terhadap perilaku konsumtif dan psikologi pemain, serta regulasi transparansi probabilitas dan monetisasi game. Ditemukan *research gap*: studi yang secara spesifik mengukur perbedaan *cumulative probability* secara komparatif menggunakan simulasi masih terbatas.

### 3.2 Tahap 2 — Perancangan Eksperimen & Desain Simulasi

**Status: Selesai.** Dirancang eksperimen komparatif dua kondisi dengan parameter identik:
- **Kondisi A (Baseline):** Fixed Probability — $p = 0,006$ konstan setiap pull.
- **Kondisi B (Intervensi):** Weighted Probability + *pity system* — $p$ meningkat secara linear setelah pull ke-50 (*soft pity*), mencapai $p = 1,0$ pada pull ke-70 (*hard pity*).

Fungsi probabilitas Kondisi B pada pull ke-$x$:
- Jika $x < 50$: $P(x) = 0,006$
- Jika $50 \le x < 70$: $P(x) = 0,006 + \frac{x - 49}{70 - 50}$
- Jika $x = 70$: $P(x) = 1,0$

Variabel kontrol: probabilitas dasar (0,6%), jumlah responden virtual (100.000), dan spesifikasi RNG Python (`random.random()`).

### 3.3 Tahap 3 — Implementasi Simulator (Python)

**Status: Selesai.** Prototype *gacha simulator* diimplementasikan dalam Python dengan struktur modul:

| Modul | Fungsi |
|---|---|
| `gacha.py` | *Probability engine* + *pull simulator* + *cumulative probability calculator* + ekspor CSV |
| `runner.py` | *Multi-run executor* — loop 10 seed berbeda, simpan output per-run ke `04-data/` |
| `analysis.py` | Pipeline agregasi data 10 run → `aggregated_stats.csv` + plot `fig_cumulative_probability.png` |

**Verifikasi fungsional:**
- Kondisi A: setiap pull independen, $p$ konstan 0,6% ✔
- Kondisi B: $p$ tetap 0,006 sampai pull ke-49; meningkat linear mulai pull ke-50; forced $p = 1,0$ pada pull ke-70 ✔
- Output CSV per run tervalidasi (71 baris data: pull ke-1 s.d. ke-70 + header) ✔
- Reproduktibilitas terjamin via seed eksplisit sebelum setiap run ✔

### 3.4 Tahap 4 — Eksekusi Eksperimen & Pengumpulan Data

**Status: Selesai — matrix 10 run telah dijalankan.**

**Execution plan:**

| Run # | Seed | Status | Output File |
|-------|------|--------|-------------|
| 1 | 42 | ✔ Selesai | `hasil_simulasi_gacha_1.csv` |
| 2 | 123 | ✔ Selesai | `hasil_simulasi_gacha_2.csv` |
| 3 | 999 | ✔ Selesai | `hasil_simulasi_gacha_3.csv` |
| 4 | 2026 | ✔ Selesai | `hasil_simulasi_gacha_4.csv` |
| 5 | 8888 | ✔ Selesai | `hasil_simulasi_gacha_5.csv` |
| 6 | 111 | ✔ Selesai | `hasil_simulasi_gacha_6.csv` |
| 7 | 2222 | ✔ Selesai | `hasil_simulasi_gacha_7.csv` |
| 8 | 3333 | ✔ Selesai | `hasil_simulasi_gacha_8.csv` |
| 9 | 4444 | ✔ Selesai | `hasil_simulasi_gacha_9.csv` |
| 10 | 5555 | ✔ Selesai | `hasil_simulasi_gacha_10.csv` |

**Total iterasi:** 10 run × 2 kondisi × 100.000 responden virtual = **2.000.000 simulasi pull**.

Output per run: `hasil_simulasi_gacha_N.csv` (kolom: `Pull_Ke`, `Cumulative_Probability_Fixed`, `Cumulative_Probability_Weighted`), disimpan di `04-data/`. Tidak ada anomali atau run gagal.

### 3.5 Tahap 5 — Analisis Data, Visualisasi & Penulisan Naskah

**Status: Selesai.** Pipeline analisis Python (`analysis.py`) membaca 10 file CSV, melakukan agregasi rata-rata per `Pull_Ke`, menghasilkan:
- **`aggregated_stats.csv`** — statistik rata-rata kumulatif 10 run ([../06-output/tables/](../06-output/tables/))
- **`fig_cumulative_probability.png`** — grafik perbandingan kedua algoritma ([../06-output/figures/](../06-output/figures/))

Draf naskah jurnal lengkap (Abstrak, Pendahuluan, Tinjauan Pustaka, Metodologi, Hasil & Analisis, Kesimpulan, Daftar Pustaka) telah disusun di [../07-manuskrip/naskah-jurnal.md](../07-manuskrip/naskah-jurnal.md).

---

## 4. Hasil Penelitian

### 4.1 Rata-Rata Jumlah Pull (*Average Pulls to Rare*)

| Kondisi | Rata-Rata Pull | Keterangan |
|---|---|---|
| Kondisi A — Fixed Probability | **167,91 pull** | Sesuai ekspektasi teoretis geometrik $E(X) = 1/p = 166,\overline{6}$ |
| Kondisi B — Weighted Probability | **46,35 pull** | Reduksi ~72,4% dibanding Fixed |

Sistem *Weighted Probability* memangkas rata-rata jumlah pull sebesar **~72,4%** berkat eliminasi ekor distribusi panjang (*long tail*) oleh mekanisme *pity system*.

### 4.2 Perbandingan *Cumulative Probability* pada Titik Kritis

Data agregat dari 10 run (rata-rata dari `aggregated_stats.csv`):

| Pull Ke-$N$ | Cum. Prob. Fixed | Cum. Prob. Weighted | Δ (Selisih) |
|:---:|:---:|:---:|:---:|
| 1 | 0,60% | 0,59% | ≈0% |
| 10 | 5,82% | 5,84% | +0,02% |
| 30 | 16,51% | 16,58% | +0,07% |
| 50 (*Soft Pity*) | 25,96% | 29,78% | **+3,82%** |
| 55 | 28,17% | 78,32% | **+50,15%** |
| 60 | 30,31% | 99,01% | **+68,70%** |
| 70 (*Hard Pity*) | 34,36% | **100,00%** | **+65,64%** |

### 4.3 Analisis Divergensi Kurva

Pergerakan *cumulative probability* kedua kondisi hampir identik dari pull ke-1 hingga ke-49, karena pada rentang tersebut Kondisi B masih beroperasi pada konstanta $p = 0,006$. Divergensi dramatis terjadi setelah *soft pity*:

- Pull ke-55: Weighted **78,32%** vs Fixed **28,17%**
- Pull ke-60: Weighted **99,01%** vs Fixed **30,31%**
- Pull ke-70: Weighted **100,00%** (hard pity terjamin) vs Fixed **34,36%**

Pada pull ke-70, lebih dari **65% populasi sistem Fixed masih belum mendapatkan *rare item*** — inilah *extreme variance* yang dieliminasi oleh *Weighted Probability*.

### 4.4 Figure

| File | Isi |
|---|---|
| [`fig_cumulative_probability.png`](../06-output/figures/fig_cumulative_probability.png) | Grafik komparatif *Cumulative Probability* (%) Fixed vs Weighted per pull (pull ke-1 s.d. ke-70), dilengkapi penanda *soft pity* (garis merah) dan *hard pity* (garis hijau) |

### 4.5 Interpretasi Singkat

1. **Fase identik (pull 1–49):** Kedua algoritma menghasilkan *cumulative probability* yang hampir sama — sistem Weighted belum mengaktifkan mekanisme pembobotannya.
2. **Fase divergensi (*soft pity*, pull 50–69):** Injeksi bobot linear pada Weighted menyebabkan *cumulative probability* meroket — mencapai ~99% pada pull ke-60, jauh melampaui ~30% pada Fixed.
3. **Fase jaminan (*hard pity*, pull 70):** Weighted mencapai 100% persis pada pull ke-70; Fixed hanya ~34%.
4. **Trade-off:** Penurunan rata-rata pull dari 167,91 → 46,35 memotong potensi pendapatan dari pemain yang sangat tidak beruntung, namun meningkatkan kepuasan dan retensi pemain secara keseluruhan — keseimbangan yang disengaja oleh perancang game.

---

## 5. Kendala dan Catatan Pelaksanaan

- **Manajemen state RNG global:** Modul `gacha.py` memanggil `random.seed(RANDOM_SEED)` di level modul saat pertama kali diimpor. Pada `runner.py`, seed di-override via `random.seed(seed)` sebelum tiap run — ini sudah berfungsi karena `runner.py` memanggil ulang `random.seed()` setelah import. Untuk reproduktibilitas penuh di masa mendatang, disarankan memisahkan instance `random.Random()` per run alih-alih menggunakan state global.
- **Cakupan simulasi terbatas:** Simulasi merepresentasikan satu banner/sesi tanpa mempertimbangkan mekanisme *shared pity* antar banner, *featured vs standard pool*, atau *guarantee carry-over* yang umum di game modern (misal sistem 50/50 di Genshin Impact). Ini merupakan batasan yang disadari dan telah didokumentasikan di §6.2 Saran naskah jurnal.
- **Ukuran sampel sudah memadai:** 100.000 iterasi per kondisi per run cukup untuk menormalkan variansi RNG pada probabilitas 0,6% — hasil antar 10 run konsisten dengan variasi < 0,5% pada titik kritis.
- **Tidak ada anomali run:** Seluruh 10 run menghasilkan output yang valid; tidak ada yang perlu dieksklusi.

---

## 6. Kesimpulan dan Saran

**Inti kesimpulan:** Algoritma *Weighted Probability* dengan *pity system* terbukti secara empiris jauh lebih menguntungkan pemain dibandingkan *Fixed Probability*. Dengan rata-rata hanya **46,35 pull** (vs 167,91 pada Fixed) dan jaminan 100% pada pull ke-70, sistem ini mengeliminasi *extreme variance* sekaligus memberikan batas pengeluaran maksimum yang transparan — menjawab *research question* dengan kesimpulan bahwa perbedaan antara kedua algoritma **signifikan dan bermakna** terutama setelah threshold *soft pity*.

---

## 7. Lampiran — Peta Artefak Penelitian

| Folder | Isi | Status |
|---|---|---|
| [01-proposal/](../01-proposal/) | Proposal penelitian (latar belakang, RQ, metode, jadwal) | ✔ Selesai |
| [02-literatur/](../02-literatur/) | Matriks literatur (10 referensi, peta gap penelitian) + BibTeX | ✔ Selesai |
| [03-teori/](../03-teori/) | Diagram arsitektur sistem simulasi & skema parameter | ✔ Selesai |
| [04-data/](../04-data/) | Data mentah 10 run × CSV (*cumulative probability* per pull ke-1–70) | ✔ Tersedia |
| [05-kode/](../05-kode/) | Source code simulator Python (`gacha.py`, `runner.py`, `analysis.py`) | ✔ Selesai |
| [06-output/](../06-output/) | Tabel agregat (`aggregated_stats.csv`) & figure (`fig_cumulative_probability.png`) | ✔ Selesai |
| [07-manuskrip/](../07-manuskrip/) | Naskah jurnal lengkap (siap submit) | ✔ Selesai |
| [08-laporan/](../08-laporan/) | Laporan penelitian ini (dokumen ini) | ✔ Selesai |

