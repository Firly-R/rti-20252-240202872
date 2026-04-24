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

## A.2 — Problem Statement Builder

```
PROBLEM STATEMENT BUILDER

Domain & Konteks
  Domain   : Computer Vision / Artificial Intelligence / Sistem Keamanan
  Konteks  : Sistem keamanan akses pintu pegawai bank menggunakan teknologi face recognition berbasis CNN

System Context
  Input       : Citra wajah pegawai dari kamera
  Process     : Akuisisi gambar, preprocessing, ekstraksi fitur, klasifikasi, identifikasi menggunakan CNN
  Output      : Identitas pegawai
  Outcome     : Identitas pegawai
  Constraints : Kualitas gambar, jumlah dataset, kondisi pencahayaan, variasi ekspresi wajah
  Stakeholders: Pegawai bank, manajemen bank, pengembang sistem

Fenomena → Problem
  Fenomena yang diamati             : Sistem keamanan pintu masih menggunakan metode konvensional seperti kunci fisik dan kartu akses
  Gejala (symptom) yang terukur     : Kartu akses bisa tertinggal / hilang, Akses tidak bisa dilakukan saat kartu tidak tersedia, Ketergantungan pada media fisik
  Masalah yang didiagnosis          : Sistem keamanan masih bergantung pada autentikasi berbasis objek fisik, bukan biometrik
  Masalah riset (researchable)      : Belum optimalnya performa sistem face recognition berbasis CNN dalam mengidentifikasi wajah secara akurat pada kondisi dataset terbatas dan variasi kualitas gambar
  Variabel yang terukur             : Akurasi sistem, Jumlah dataset wajah, Kualitas citra (blur, pencahayaan), Tingkat keberhasilan identifikasi

Problem Quality Check
  [✔] Clarity — Cukup jelas, tetapi masih terlalu umum dan belum membatasi kondisi spesifik seperti skenario real-time atau lingkungan kompleks.
  [✔] Measurability — Ada metrik akurasi (±92%–95%), namun hanya satu metrik sehingga evaluasi masih kurang mendalam.
  [✔] Relevance — Relevan untuk sistem keamanan, tetapi topik face recognition sudah banyak diteliti sehingga kebaruan rendah.
  [✔] Testability —  Bisa diuji, namun pengujian terbatas pada dataset kecil dan kondisi terkontrol sehingga validitas belum kuat.
  [ ] Impact — Kontribusi masih terbatas karena skala kecil (hanya 5 orang) dan belum bisa digeneralisasi ke kondisi nyata yang lebih luas.

Problem Statement (1 paragraf):
  Sistem keamanan pintu pada lingkungan perbankan masih banyak menggunakan metode konvensional seperti kunci fisik dan kartu akses yang memiliki keterbatasan seperti risiko kehilangan dan ketergantungan pada media fisik. Teknologi face recognition berbasis Convolutional Neural Network (CNN) menawarkan solusi autentikasi biometrik, namun performanya masih dipengaruhi oleh kualitas citra, jumlah dataset, dan variasi kondisi wajah. Oleh karena itu, diperlukan penelitian untuk menganalisis dan meningkatkan akurasi sistem face recognition dalam mengidentifikasi wajah secara optimal pada kondisi dataset terbatas dan variasi kualitas gambar, dengan menggunakan metrik akurasi sebagai indikator utama keberhasilan sistem.
```

---

## Latihan 1 — Dari Topik ke Masalah Riset

**Topik awal:** Face Recognition untuk Sistem Keamanan Akses Pintu

| Tahap | Hasil |
|-------|-------|
| Reality | *Sistem keamanan pintu di perbankan masih menggunakan kunci fisik dan kartu akses* |
| Observed Issue (Symptom) | *Pegawai tidak bisa mengakses pintu jika kartu tertinggal atau hilang* |
| Diagnosed Problem (Root Cause) | *Sistem autentikasi masih bergantung pada media fisik yang tidak praktis dan rentan* |
| Researchable Problem | *Belum optimalnya akurasi sistem face recognition berbasis CNN dalam mengidentifikasi wajah pada kondisi dataset terbatas dan variasi kualitas citra* |
| Measurable Variable | *Akurasi (%), jumlah dataset, kualitas citra (blur/pencahayaan), tingkat keberhasilan identifikasi* |

**Apakah terjebak solution-first thinking?** [ ✔ ] Ya
> Kembali ke tahap Diagnosed Problem, karena langsung lompat ke solusi (CNN & face recognition) tanpa memperdalam masalah dasar

---

## Latihan 2 — System Context Decomposition

Gambarkan konteks sistem dari masalah riset di Latihan 1.

| Komponen | Deskripsi |
|----------|----------|
| Input | *Citra wajah pegawai yang ditangkap kamera* |
| Process | *Akuisisi gambar → preprocessing → ekstraksi fitur → klasifikasi → identifikasi menggunakan CNN* |
| Output | *Hasil identifikasi wajah* |
| Outcome | *Akses pintu terbuka otomatis jika wajah dikenali* |
| Constraints | *Kualitas gambar (blur), pencahayaan, variasi ekspresi wajah, jumlah dataset terbatas* |
| Stakeholders | *Pegawai bank, pihak manajemen, developer sistem* |

**Komponen yang paling relevan dengan masalah riset adalah Process & Constraints.**

Alasanya:
- Masalah utama ada di proses identifikasi (CNN)
- Dipengaruhi langsung oleh constraints seperti dataset kecil dan kualitas gambar
- Di sinilah akurasi sistem ditentukan (inti riset)

---

## Latihan 3 — Problem Quality Check

Evaluasi problem statement yang sudah dibuat menggunakan 5 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Clarity | 4 | Masalah sudah cukup jelas, tetapi masih belum membatasi kondisi spesifik seperti lingkungan real-time atau skala implementasi |
| Measurability | 3  | Menggunakan akurasi sebagai metrik, namun tidak ada metrik lain seperti precision/recall sehingga evaluasi kurang mendalam |
| Relevance | 4 | Relevan untuk sistem keamanan modern, tetapi bukan topik baru sehingga kontribusi kebaruan terbatas |
| Testability | 3 | Bisa diuji, tetapi pengujian hanya pada dataset kecil dan kondisi terbatas sehingga validitas kurang kuat |
| Impact | 2 | Dampak masih kecil karena belum bisa digeneralisasi ke skala besar |

**Skor total:** 16 / 25

**Problem statement :**
> Sistem keamanan pintu di lingkungan perbankan masih banyak menggunakan metode konvensional seperti kunci fisik dan kartu akses yang memiliki keterbatasan dalam hal kepraktisan dan keamanan. Penggunaan teknologi face recognition berbasis Convolutional Neural Network (CNN) menawarkan alternatif autentikasi biometrik, namun performanya masih dipengaruhi oleh keterbatasan jumlah dataset, variasi kualitas citra, serta kondisi lingkungan seperti pencahayaan dan ekspresi wajah. Oleh karena itu, diperlukan penelitian untuk mengevaluasi dan meningkatkan akurasi sistem face recognition dalam mengidentifikasi wajah secara tepat pada kondisi dataset terbatas, dengan menggunakan metrik akurasi sebagai indikator utama keberhasilan sistem.

---

## Refleksi

> Bandingkan "masalah" yang biasa ditemui saat coding (bug, error) dengan masalah riset. Apa perbedaan fundamental dalam cara mendefinisikan dan mendekati keduanya?

**Jawaban:**
> Masalah coding (bug/error) bersifat teknis dan memiliki solusi langsung melalui debugging. Sedangkan masalah riset bersifat kompleks, berfokus pada gap pengetahuan, dan memerlukan analisis serta pembuktian ilmiah. Perbedaannya, coding bertujuan memperbaiki, sedangkan riset bertujuan memahami dan membuktikan.
