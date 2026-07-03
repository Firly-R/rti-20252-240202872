# WS-02: Problem Statement

> **Bab 2 — Problem Formulation & System Context**

---

## Ringkasan Materi

### Problem Formation Model

Masalah riset melewati 5 tahap transformasi. Melompat langsung dari Reality ke Variable adalah kesalahan paling umum.

```
Reality → Observed Issue (Symptom) → Diagnosed Problem (Root Cause)
→ Researchable Problem (Scoped) → Measurable Variable (Operationalized)
```

### Topic ≠ Problem ≠ Research Problem

| Level | Contoh | Status |
|-------|--------|--------|
| **Topik** | Keamanan IoT | Terlalu luas, tidak bisa diuji |
| **Problem** | MQTT tidak terenkripsi | Spesifik tapi belum riset |
| **Research Problem** | Belum ada studi membandingkan overhead TLS 1.3 vs DTLS pada MQTT di IoT RAM < 64KB | Bisa dirancang eksperimennya |

### Symptom vs Root Cause

Apa yang diamati (gejala) ≠ mengapa terjadi (akar masalah). Gunakan **5 Whys** atau **Fishbone Diagram** untuk menggali.

Contoh: "User meninggalkan checkout" (symptom) → "Waktu loading > 8 detik karena API call sequential" (root cause).

### System Thinking

Setiap masalah riset TI harus terikat pada komponen sistem: **Input → Process → Output → Outcome → Constraints → Stakeholders**.

### Problem Quality Check

Masalah riset yang layak harus memenuhi 5 kriteria:
- **Clarity** — Satu orang membaca akan paham
- **Measurability** — Ada metrik kuantitatif
- **Relevance** — Penting untuk domain
- **Testability** — Bisa gagal (falsifiable)
- **Impact** — Ada kontribusi jika terjawab

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Menyelesaikan masalah (*solve*) | Memahami dan membuktikan (*understand & prove*) |
| Masalah | Bug, error, fitur belum ada | Gap dalam pengetahuan |
| Scope | Selesaikan semua yang perlu | Batasi agar bisa dibuktikan |
| Output | Working system | Evidence, paper, replicable findings |

### Istilah Penting

- **Problem Statement** — Formulasi tertulis: konteks sistem + gap + dampak + justifikasi
- **System Context** — Deskripsi lengkap: input, proses, output, outcome, constraints, stakeholders
- **Problem Drift** — Masalah "bermutasi" dari pendahuluan ke metodologi karena statement awal tidak presisi
- **Solution-First Thinking** — Memulai dari solusi tanpa masalah yang jelas — berbahaya dalam riset
- **Operational Definition** — Definisi variabel yang cukup jelas agar peneliti lain bisa mengukur hal yang sama

---

## Template A.2 — Problem Statement Builder

```
PROBLEM STATEMENT BUILDER

Domain & Konteks
  Domain   : Game Development / Algoritma Probabilitas Game Modern
  Konteks  : Mekanisme penyeimbangan ekonomi distribusi item virtual (loot box) berbasis Pity System.

System Context
  Input       : Request "pull" dari pemain, base probability (0.6%), ambang batas soft pity (50) dan hard pity (70).
  Process     : Pemrosesan angka acak oleh RNG (Random Number Generator) dan penambahan bobot peluang secara dinamis berdasarkan akumulasi riwayat kegagalan (logika weighted probability).
  Output      : Berkas log transaksi mentah (raw log data) berisi urutan nomor pull dan status perolehan item.
  Outcome     : Grafik kurva distribusi cumulative probability dan nilai rata-rata pull (average pulls to rare) untuk pembuktian efisiensi sistem.
  Constraints : Batasan runtime eksekusi pemrograman Python dan sifat keacakan RNG komputer yang harus terdistribusi uniform.
  Stakeholders: Game Developer (desainer game/ekonomi makro) dan Pemain Game (konsumen/komunitas akademik).

Fenomena → Problem
  Fenomena yang diamati             : Pemain game gacha modern sering mengalami frustrasi dan berhenti bermain (churn rate tinggi) akibat ketidakpastian tinggi dalam memperoleh item langka.
  Gejala (symptom) yang terukur     : Rendahnya cumulative probability pada sistem fixed rate membuat rata-rata jumlah pull sangat tinggi (~166 pull) untuk mendapatkan satu rare item, memicu ketidakseimbangan kepuasan pemain.
  Masalah yang didiagnosis          : Algoritma fixed probability murni tidak memiliki komponen memori untuk menyesuaikan peluang secara responsif terhadap riwayat kegagalan berulang pemain.
  Masalah riset (researchable)      : Belum adanya analisis kuantitatif berskala besar (100.000 iterasi) yang mengevaluasi pengaruh intervensi algoritma weighted probability bertingkat (soft pity 50 dan hard pity 70) terhadap akselerasi cumulative probability dan penurunan nilai rata-rata penarikan.
  Variabel yang terukur             : Variabel Independen: Jenis Algoritma (Fixed vs Weighted). Variabel Dependen: Nilai persentase Cumulative Probability (%) dan Average Pulls to Rare (jumlah pull).

Problem Quality Check
  [x] Clarity — Apakah satu orang membaca akan paham?
  [x] Measurability — Apakah ada metrik kuantitatif?
  [x] Relevance — Apakah penting untuk domain?
  [x] Testability — Apakah bisa gagal?
  [x] Impact — Apakah ada kontribusi jika terjawab?

Problem Statement (1 paragraf):
  Mekanisme gacha berbasis fixed probability konstan sering kali memicu frustrasi pemain akibat tingginya variansi dan rata-rata jumlah penarikan yang dibutuhkan untuk memperoleh rare item, yang berdampak buruk pada tingkat retensi pengguna di industri game. Masalah utamanya terletak pada ketiadaan sistem penyesuaian peluang adaptif yang mampu merespons riwayat kegagalan berulang pemain. Meskipun konsep pity system mulai banyak diterapkan secara komersial, belum ada studi evaluatif di bidang ilmu komputer yang secara eksplisit memetakan dampak algoritma weighted probability dinamis terhadap lonjakan grafik cumulative probability dan efisiensi rata-rata penarikan menggunakan pendekatan simulasi laboratorium terkontrol berskala besar (100.000 iterasi) dengan batasan ketat soft pity di pull ke-50 dan hard pity di pull ke-70. Oleh karena itu, penelitian ini penting dilakukan untuk menyediakan bukti empiris dan acuan matematis yang presisi bagi pengembangan skema probabilitas game yang lebih seimbang.
```

---

## Latihan 1 — Dari Topik ke Masalah Riset

Pilih satu topik di bidang TI yang diminati. Transformasikan melalui 5 tahap Problem Formation Model.

**Topik awal:** Analisis Evaluatif Algoritma Weighted Probability pada Sistem Gacha Game melalui Eksperimen Simulasi Komparatif

| Tahap | Hasil |
|-------|-------|
| Reality | Industri game modern menggunakan sistem monetisasi gacha untuk mendistribusikan item virtual langka kepada pengguna |
| Observed Issue (Symptom) | Munculnya keluhan masif dari komunitas pemain mengenai sistem gacha yang tidak adil (*ampas*) serta tingginya biaya/jumlah *pull* yang fluktuatif untuk mendapatkan item langka |
| Diagnosed Problem (Root Cause) | Penggunaan algoritma *fixed probability* murni (0.6%) tidak memiliki memori penentu keberhasilan, sehingga peluang mendapatkan item selalu sama di setiap percobaan, yang berakibat pada lambatnya pertumbuhan kurva peluang kumulatif pemain |
| Researchable Problem | Bagaimana penerapan intervensi algoritma *weighted probability* dengan skema bertingkat (*soft pity* 50 dan *hard pity* 70) secara signifikan mampu mengubah akselerasi kurva *cumulative probability* dan memangkas rata-rata jumlah penarikan dibandingkan sistem *fixed* konstan? |
| Measurable Variable | Nilai persentase *cumulative probability* per urutan penarikan (skala 0% - 100%) dan metrik rata-rata jumlah *pull* sukses (*average pulls to rare*) |

**Apakah terjebak solution-first thinking?** [ ] Ya / [X] Tidak
> Jika ya, kembali ke tahap mana? ________________________

---

## Latihan 2 — System Context Decomposition

Gambarkan konteks sistem dari masalah riset di Latihan 1.

| Komponen | Deskripsi |
|----------|----------|
| Input | Benih acak komputer (*RNG seed*), jumlah iterasi responden virtual (100.000), nilai batas *soft pity* (50), batas *hard pity* (70), dan *base rate* probabilitas dasar (0.6%) |
| Process | Evaluasi urutan nomor penarikan aktif, manipulasi bobot peluang $+5\%$ per penarikan pasca-*pull* ke-50, pemaksaan peluang mutlak ($1.0$) pada *pull* ke-70, dan eksekusi pengundian angka acak menggunakan *Random Number Generator* |
| Output | Berkas log transaksi mentah (*raw data log*) dalam format CSV yang mencatat urutan *pull* sukses dari setiap entitas responden virtual |
| Outcome | Representasi kurva distribusi visual grafik peluang kumulatif serta kepastian angka efisiensi statistik rata-rata penarikan untuk penarikan kesimpulan ilmiah |
| Constraints | Pembatasan model simulasi yang hanya menguji penarikan tunggal (*single-pull*), aturan penulisan *file library I/O* Python, dan keterbatasan spesifikasi perangkat keras komputer |
| Stakeholders | Peneliti algoritma game, desainer sistem monetisasi (developer game), serta komunitas akademik ilmu komputer |

**Komponen mana yang paling relevan dengan masalah riset?** **Process** (Karena di sinilah algoritma *weighted probability* bekerja secara dinamis memanipulasi angka peluang dasar berdasarkan riwayat kegagalan penarikan)

---

## Latihan 3 — Problem Quality Check

Evaluasi problem statement yang sudah dibuat menggunakan 5 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Clarity | 5 | Sangat jelas. Masalah didefinisikan secara konkret menggunakan parameter kuantitatif numerik (batas 50 dan 70 *pull*) sehingga terhindar dari ambiguitas |
| Measurability | 5 | Sangat terukur. Variabel yang digunakan berupa persentase peluang kumulatif dan rata-rata jumlah penarikan yang dihitung secara eksak melalui operasi matematika statistik deskriptif |
| Relevance | 4 | Relevan dengan tren riset industri game modern saat ini yang berfokus pada optimasi retensi pengguna dan pemodelan sistem komputasi probabilitas  |
| Testability | 5 | Sangat bisa diuji (*falsifiable*). Hipotesis bisa langsung dinyatakan gugur/salah jika hasil akhir kodingan simulasi membuktikan tidak adanya perbedaan rata-rata jumlah *pull* antara kedua kelompok |
| Impact | 4 | Memberikan kontribusi nyata berupa cetak biru (*blueprint*) arsitektur sistem *gacha simulator* yang modular dan dapat direplikasi oleh peneliti lanjutan di bidang sejenis. |

**Skor total:** 23 / 25

**Problem statement versi final (1 paragraf):**
> Mekanisme gacha berbasis *fixed probability* konstan sering kali memicu frustrasi pemain akibat tingginya variansi dan rata-rata jumlah penarikan yang dibutuhkan untuk memperoleh *rare item*, yang berdampak buruk pada tingkat retensi pengguna di industri game. Masalah utamanya terletak pada ketiadaan sistem penyesuaian peluang adaptif yang mampu merespons riwayat kegagalan berulang pemain. Meskipun konsep *pity system* mulai banyak diterapkan secara komersial, belum ada studi evaluatif di bidang ilmu komputer yang secara eksplisit memetakan dampak algoritma *weighted probability* dinamis terhadap lonjakan grafik *cumulative probability* dan efisiensi rata-rata penarikan menggunakan pendekatan simulasi laboratorium terkontrol berskala besar (100.000 iterasi) dengan batasan ketat *soft pity* di *pull* ke-50 dan *hard pity* di *pull* ke-70. Oleh karena itu, penelitian ini penting dilakukan untuk menyediakan bukti empiris dan acuan matematis yang presisi bagi pengembangan skema probabilitas game yang lebih seimbang

---

## Refleksi

> Bandingkan "masalah" yang biasa ditemui saat coding (bug, error) dengan masalah riset. Apa perbedaan fundamental dalam cara mendefinisikan dan mendekati keduanya?

**Jawaban:**
> Masalah yang ditemui saat *coding* sehari-hari (*bug* atau *error*) bersifat deterministik, praktis, dan berorientasi pada perbaikan (*how to fix it*). Tujuannya adalah memperbaiki kerusakan sintaksis atau logika internal program agar sistem dapat berjalan normal kembali sesuai spesifikasi rekayasa perangkat lunak.
> 
> Sebaliknya, masalah riset berfokus pada celah pengetahuan (*gap of knowledge*) yang bersifat investigatif, teoritis, dan berorientasi pada pembuktian (*why and to what extent*). Pendekatan terhadap masalah riset tidak sekadar menuntut kode program dapat dieksekusi tanpa *error*, melainkan bagaimana kode program tersebut dirancang secara sistematis sebagai laboratorium buatan yang steril untuk menguji perilaku sebuah algoritma, mengumpulkan data statistiknya secara objektif, serta menarik kesimpulan ilmiah baru yang dapat dipertanggungjawabkan dan direplikasi oleh peneliti lain (*reproducible*).
