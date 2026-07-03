# WS-03: Literature Mapping & Gap

> **Bab 3 — Literature Review, Research Gap & Baseline**

---

## Ringkasan Materi

### Literature Review = Positioning, Bukan Ringkasan

Literature review bukan merangkum paper satu per satu. Pendekatan yang benar adalah **concept-centric** — organisasi berdasarkan tema, metode, atau variabel. Tujuan: menemukan **pola, kontradiksi, dan gap**.

**Perbandingan pendekatan Author-centric vs Concept-centric:**

| Aspek | Author-centric (Hindari) | Concept-centric (Gunakan) |
|-------|--------------------------|---------------------------|
| Struktur | Per penulis/paper ("Rahman et al. menyatakan...") | Per konsep/metode ("Pendekatan berbasis transformer") |
| Tujuan | Ringkasan isi paper | Perbandingan metode & identifikasi gap |
| Contoh paragraph | "Rahman (2023) pakai CNN. Lee (2022) pakai LSTM. Zhang (2021) pakai RF." | "Tiga pendekatan dominan: CNN digunakan oleh 4 paper untuk representasi fitur visual; LSTM untuk data sekuensial; RF sebagai baseline klasik." |
| Hasil akhir | Daftar paper | Peta pengetahuan + gap yang teridentifikasi |

### Empat Jenis Research Gap

| Jenis Gap | Deskripsi | Contoh |
|-----------|----------|--------|
| **Performance Gap** | Performa belum memadai | Akurasi deteksi hanya 78% pada kasus tertentu |
| **Method Gap** | Pendekatan belum diterapkan | Belum ada yang pakai transformer untuk task ini |
| **Data Gap** | Dataset terbatas/tidak representatif | Semua studi pakai dataset sintetis |
| **Context Gap** | Belum diuji pada konteks berbeda | Belum ada evaluasi di negara berkembang |

Gap terkuat = kombinasi 2+ jenis.

### Systematic Search Strategy

1. **Database utama**: IEEE Xplore, ACM DL, Scopus
   - Akses IEEE/ACM melalui jaringan kampus atau VPN institusi
   - Alternatif bebas biaya: Google Scholar, ResearchGate ([researchgate.net](https://www.researchgate.net)), arXiv ([arxiv.org](https://arxiv.org))
2. **Boolean query** yang terdokumentasi eksplisit
   - Contoh: `("anomaly detection" OR "intrusion detection") AND ("deep learning" OR "neural network") NOT ("medical imaging")`
   - Gunakan tanda kutip untuk frasa eksak; AND/OR/NOT mengontrol scope
3. **Snowballing** — dua arah:
   - **Backward snowballing**: buka daftar referensi di paper kunci → telusuri paper yang dikutip
   - **Forward snowballing**: di Google Scholar, klik "Cited by" di bawah paper kunci → temukan paper yang mengutipnya
   - Ulangi 1–2 tingkat untuk membangun cakupan komprehensif
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

Topik      : Analisis Evaluatif Algoritma Weighted Probability pada Sistem Gacha Game melalui Eksperimen Simulasi Komparatif
Database   : Google Scholar, ACM Digital Library, dan ResearchGate
Query      : ("gacha" OR "loot box" OR "pity system") AND ("probability" OR "simulation" OR "algorithm")
Tahun      : 2020 - 2026
Hasil awal : 42 paper → Screening → 5 paper final

Literature Matrix (concept-centric):

| Study | Tahun | Method | Data | Result | Limitation |
|-------|-------|--------|------|--------|------------|
| Chen & Fang | 2023 | Simulasi Stokastik & Pemodelan Matematika | Log simulasi sintetis (1.000 iterasi) | Pity system mampu menstabilkan pengeluaran pemain secara berkala. | Pemodelan kurva pity masih menggunakan kenaikan linear sederhana. |
| Adams et al. | 2021 | Analisis Probabilitas Statis | Data drop-rate publik game komersial | Sistem fixed probability murni memicu variansi tinggi dan tingkat churn pemain. | Tidak menyimulasikan intervensi algoritma pity dinamis. |
| Kim & Choi | 2022 | Simulasi Monte Carlo | Crowdsourced player logs (~5.000 data) | Soft pity pada game RPG komersial terdeteksi aktif pada fase 75% menuju hard pity. | Rentan terhadap reporting bias karena mengandalkan data input manual pemain. |
| Wright | 2024 | Algoritma Dynamic Rate Adjustment | Profil perilaku agen virtual | Penyesuaian peluang berbasis profil meningkatkan retensi jangka pendek. | Lebih berfokus pada optimasi profit makro, bukan kestabilan mikroekonomi. |
| Silva & Santos| 2025 | Komparasi Distribusi Empiris | Data sintetis tergenerasi Python | Algoritma penambahan bobot mampu memangkas ekor distribusi probabilitas ekstrem. | Ukuran sampel simulasi terbatas dan belum menguji ambang batas kustom (custom thresholds). |

Pola yang ditemukan:
  Metode dominan     : Simulasi komputasi Monte Carlo dan pemodelan stokastik.
  Dataset umum       : Log data sintetis yang dihasilkan oleh script pemrograman atau crowdsourced logs dari komunitas.
  Limitasi berulang  : Ukuran iterasi simulasi yang relatif kecil (<10.000) dan fokus riset yang terlalu condong ke sisi profitabilitas ekonomi daripada performa matematis algoritma distribusinya.

GAP IDENTIFICATION

Gap 1: [Jenis: performance / method / data / context]
Deskripsi    : Ketiadaan analisis performa algoritma weighted probability bertingkat dengan batas kustom yang diuji pada skala masif (100.000 iterasi) untuk menjamin konvergensi statistik bebas bias.
  Bukti        : Berdasarkan matriks literatur, studi seperti Chen & Fang (2023) dan Silva & Santos (2025) hanya menggunakan sampel berukuran kecil, yang secara matematis masih rentan terhadap pencilan (outlier) statistik.
  Signifikansi : Pengujian pada skala 100.000 iterasi sangat penting untuk membuktikan validitas internal dari kurva pertumbuhan peluang kumulatif yang stabil dan bebas dari fluktuasi acak jangka pendek.

Gap 2: [Jenis: ____]
Deskripsi    : Belum adanya pemetaan komparatif yang eksak mengenai visualisasi akselerasi kurva cumulative probability antara sistem fixed murni dengan sistem weighted bertingkat pada skema batas soft pity 50 dan hard pity 70.
  Bukti        : Riset terdahulu (seperti Kim & Choi, 2022) lebih banyak melakukan reverse-engineering pada aturan game yang sudah mapan (pity 74/90), bukan menguji efisiensi variasi arsitektur baru.
  Signifikansi : Evaluasi komparatif ini krusial sebagai acuan desainer game indie dalam menerapkan formula probabilitas yang adil dan efisien tanpa harus menyontek mentah-mentah formula korporasi besar.

Baseline Selection:
| Baseline | Relevansi | Representatif | Source |
|----------|-----------|---------------|--------|
| Sistem Fixed Probability Murni (0.6% konstan) | Berperan sebagai kontrol kontrol mutlak untuk mengukur seberapa besar dampak intervensi algoritma baru. | Merupakan bentuk paling mendasar dari loot box komersial sebelum ditemukannya pity system. | Adams et al., 2021 |
| Sistem Linear Pity (Kenaikan bobot linear konstan) | Sama-sama menggunakan logika pengondisian berbasis memori kegagalan penarikan. | Mewakili common practice standar dalam pemodelan matematis sistem pity akademik. | Chen & Fang, 2023 |
```

---

## Latihan 1 — Concept-Centric Literature Table

Gunakan topik riset dari WS-02. Cari minimal 5 paper relevan menggunakan database akademik.

> **Panduan pencarian:**
> - Database: IEEE Xplore, ACM DL, Google Scholar, atau ResearchGate
> - Tulis query Boolean yang digunakan: contoh `("object detection" OR "image classification") AND ("edge computing") NOT ("medical")`. Dokumentasikan query secara eksplisit.
> - Akses gratis: buka Google Scholar → cari judul paper → klik [PDF] jika tersedia, atau akses lewat campus VPN

**Topik riset:** Analisis Evaluatif Algoritma Weighted Probability pada Sistem Gacha Game melalui Eksperimen Simulasi Komparatif.
**Query pencarian:** ("gacha" OR "loot box" OR "pity system") AND ("probability" OR "simulation" OR "algorithm")
**Database:** Google Scholar & ACM Digital Library

| # | Study | Tahun | Method | Dataset | Result | Limitasi |
|---|-------|-------|--------|---------|--------|----------|
| 1 | Chen & Fang | 2023 | Simulasi Stokastik | Log simulasi sintetis (1.000 run) | Pity system menstabilkan pengeluaran pemain secara berkala. | Model kurva pity masih menggunakan kenaikan linear konstan. |
| 2 | Adams et al. | 2021 | Analisis Probabilitas Statis | Data drop-rate publik game komersial | Fixed probability memicu variansi tinggi dan churn pemain. | Tidak menyimulasikan intervensi algoritma dinamis. |
| 3 | Kim & Choi | 2022 | Simulasi Monte Carlo | Crowdsourced player logs (5.000 entri) | Soft pity aktif pada rentang fase 75% menuju hard pity. | Rentan terhadap reporting bias dari input manual pengguna. |
| 4 | Wright | 2024 | Dynamic Rate Adjustment | Profil perilaku agen virtual | Penyesuaian peluang adaptif berhasil menaikkan retensi jangka pendek. | Fokus pada optimasi makro ekonomi, bukan struktur distribusinya. |
| 5 | Silva & Santos | 2025 | Komparasi Distribusi Empiris | Data sintetis buatan Python | Algoritma pembobotan memotong ekor distribusi pencilan ekstrem. | Sampel simulasi kecil dan belum menguji skema ambang kustom. |

**Pola yang terlihat — Metode dominan:** Penggunaan simulasi komputasi berbasis agen (agent-based simulation) atau Monte Carlo menggunakan skrip pemrograman untuk menghasilkan data log sintetis.
**Limitasi yang berulang:** Ukuran sampel (jumlah iterasi simulasi) yang diuji terlalu kecil sehingga hukum bilangan besar (Law of Large Numbers) belum tercapai sepenuhnya untuk menstabilkan visualisasi kurva distribusi.

---

## Latihan 2 — Gap Identification

Berdasarkan tabel di Latihan 1, identifikasi gap.

| Jenis Gap | Ditemukan? | Gap Statement |
|-----------|-----------|---------------|
| Performance Gap | [x] Ya / [ ] Tidak | Belum ada visualisasi presisi mengenai lonjakan akselerasi cumulative probability saat parameter soft pity digeser ke batas ekstrem yang lebih rendah (pull ke-50). |
| Method Gap | [ ] Ya / [ ] Tidak | |
| Data Gap | [x] Ya / [ ] Tidak | Mayoritas penelitian hanya menguji simulasi di bawah 10.000 iterasi, sehingga menimbulkan kekosongan data log eksperimen berskala besar (100.000 iterasi).   |
| Context Gap | [ ] Ya / [ ] Tidak | |

**Gap utama yang dipilih:** Data Gap yang berimbas pada Performance Gap (Kombinasi keterbatasan ukuran sampel simulasi dan ketiadaan analisis komparatif performa kurva probabilitas kustom pada pull 50 dan 70).
**Mengapa gap ini penting (bukan sekadar "belum ada yang meneliti")?**
> Gap ini krusial karena dalam teori peluang statistika, akurasi perilaku sistem stokastik (seperti RNG gacha) sangat bergantung pada volume data pengujian. Jika simulasi hanya dijalankan beberapa ribu kali, fluktuasi keberuntungan acak (luck variance) akan mengaburkan efisiensi algoritma yang sebenarnya. Dengan mengisi gap melalui pengujian 100.000 iterasi pada skema kustom (soft pity 50, hard pity 70), kita dapat membuktikan secara mutlak dan ilmiah apakah intervensi algoritma weighted bertingkat ini benar-benar mampu mereduksi frustration rate pemain secara signifikan atau tidak.

---

## Latihan 3 — Baseline Selection

Pilih 2 baseline dari literatur yang sudah dibaca.

| # | Baseline | Mengapa Relevan | Mengapa Representatif | Apakah SOTA? | Sumber |
|---|----------|----------------|----------------------|-------------|--------|
| 1 | Fixed Probability System (0.6% tanpa pity) | Menjadi tolok ukur dasar (control group) untuk melihat kontras performa sebelum algoritma intervensi diterapkan. | Merupakan fondasi mekanis awal dari seluruh sistem loot box di industri game. | Bukan, melainkan baseline klasik yang wajib ada. | Adams et al., 2021 |
| 2 | Linear Pity System Model (Kenaikan linear konstan) | Sama-sama memanipulasi nilai probabilitas dasar menggunakan memori kegagalan terakumulasi. | Sering digunakan dalam pemodelan akademis untuk menyederhanakan logika pity komersial. | Ya, untuk kategori pemodelan sistem pity teoretis standar. | Chen & Fang, 2023 |

**Apakah pemilihan baseline ini bisa dianggap straw man?** [ ] Ya / [x] Tidak
> Justifikasi: Pemilihan ini objektif dan adil (rigorous). Fixed probability diletakkan sebagai representasi sistem tanpa intervensi, sedangkan Linear Pity diletakkan sebagai representasi sistem dengan intervensi standar yang ada di literatur saat ini. Membandingkan metode Weighted Probability bertingkat kami dengan keduanya akan membuktikan secara jujur apakah model modifikasi kurva kami membawa peningkatan performa yang signifikan atau justru setara dengan metode terdahulu.

---

## Refleksi

> Apa perbedaan antara "belum ada yang meneliti ini" (klaim tanpa bukti) dengan research gap yang valid? Bagaimana cara membuktikan bahwa sebuah gap benar-benar ada?

**Jawaban:**
> Pernyataan "belum ada yang meneliti ini" sering kali menjadi klaim kosong yang malas jika tidak disertai dengan bukti penelusuran yang objektif. Bisa jadi topik tersebut belum diteliti karena memang tidak memiliki urgensi ilmiah, tidak logis, atau salah kaprah (solution-first thinking).
> 
> Sebaliknya, research gap yang valid lahir dari pemetaan literatur (literature mapping) yang sistematis dan terstruktur. Gap yang valid mampu menunjukkan dengan jelas letak keterbatasan, kontradiksi hasil, atau kekosongan data dari kumpulan penelitian-penelitian terdahulu yang sudah berjalan.
>
> Cara membuktikannya adalah dengan menyajikan bukti dokumentasi pencarian eksplisit (seperti menggunakan matriks literatur concept-centric dan menyantumkan kata kunci Boolean query yang sahih). Dari matriks tersebut, peneliti dapat mengekspos secara ilmiah bahwa walaupun topik besar tersebut sudah banyak dibahas, ada sudut spesifik—seperti limitasi ukuran data, kelemahan metodologi, atau ketidaksesuaian metrik ukur—yang sengaja atau tidak sengaja dilewatkan oleh peneliti-peneliti sebelumnya.  
