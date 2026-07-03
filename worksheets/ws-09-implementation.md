# WS-09: Implementation & Environment

> **Bab 9 — Implementasi Riset & Kontrol Lingkungan**

---

## Ringkasan Materi

### Implementasi Riset ≠ Coding Biasa

Tujuan implementasi riset bukan membuat software yang berfungsi, melainkan membangun **instrumen pengukuran yang konsisten**. Setiap modul harus di-mapping ke variabel (dari Bab 6), parameter harus config-driven, dan logging aktif dari hari pertama.

> **Mengapa reproducibility penting?** Sains dibangun di atas prinsip verifikasi — temuan harus bisa dikonfirmasi oleh peneliti lain. _Replicability crisis_ yang terjadi di banyak paper riset ML/AI disebabkan oleh environment tidak terdokumentasi: orang lain tidak bisa reproduksi, hasil diragukan, kepercayaan terhadap temuan hilang. Prinsip: **dokumentasi environment = snapshot kredibilitas riset Anda.**

### Reproducible Implementation Model

```
Design → Implementation → Environment Setup → Execution Consistency → Reproducibility → Trustworthy Result
```

Setiap transisi memiliki syarat:
- Design → Implementation: kode sesuai mapping variabel-ke-komponen
- Implementation → Environment: versi, dependency, seed, path, OS eksplisit
- Environment → Consistency: seed terkunci, urutan deterministik
- Consistency → Reproducibility: dokumentasi lengkap
- Reproducibility → Trust: siapa pun ikuti dokumentasi → hasil sama/serupa

### Repeatability vs Reproducibility

| Level | Peneliti | Environment | Hasil |
|-------|---------|-------------|-------|
| **Repeatability** | Sama | Sama | Sama persis |
| **Reproducibility** | Berbeda | Berbeda (ikuti docs) | Sama/serupa |

Capai **repeatability** dulu, baru **reproducibility**.

### Engineering vs Research Perspective

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Sistem berfungsi untuk user | Instrumen pengukuran konsisten |
| Dependency | Update ke terbaru | Lock di versi spesifik |
| Testing | Unit, integration, E2E | Repeatability test (run ulang → sama?) |
| Dokumentasi | User guide, API docs | Environment spec, execution steps, expected output |
| Config | Default masuk akal | Setiap parameter eksplisit & adjustable |

### Jebakan Kognitif

1. Menunda environment setup → bug sulit dilacak
2. Tidak pakai version control → hasil tidak bisa direkonstruksi
3. Menolak Docker/container → "di laptop saya bisa" saat review
   - **Docker** = teknologi container yang "membungkus" aplikasi beserta seluruh dependency-nya dalam satu unit terisolasi. Hasilnya: kode berjalan identik di laptop, server, maupun reviewer lain. Intro singkat: `docker run -v $(pwd):/workspace environment-image python run_experiment.py`
4. 3× hasil sama ≠ repeatable (bisa cache/state tersimpan)

### Dependency Locking

Mengandalkan "install library terbaru" berbahaya: versi berbeda = perilaku berbeda = hasil tidak reproducible. Praktik:
- **Python**: buat `requirements.txt` dengan versi eksplisit: `scikit-learn==1.3.2`, lalu kunci dengan `pip freeze > requirements.txt`
- **Conda**: gunakan `conda env export > environment.yml` untuk snapshot lengkap
- **Node.js/R/Julia**: gunakan `package-lock.json` / `renv.lock` / `Project.toml` — semua fungsi serupa: lock versi + hash

### Istilah Penting

- **Environment Specification** — Deskripsi lengkap: hardware, OS, runtime, library + versi, config, seed
- **Dependency** — Komponen eksternal yang harus di-lock versinya
- **Config-driven** — Parameter dieksternalisasi ke file konfigurasi, bukan hardcode

---

## Template A.9 — Dokumentasi Setup Eksperimen

```
EXPERIMENT SETUP DOCUMENTATION

Hardware:
  CPU     : Intel Core i5
  RAM     : 12 GB
  GPU     : NVIDIA GeForce MX250
  Storage : 715 GB

Software:
  OS        : Windows
  Runtime   : Python
  Framework : Standar Library (Pure Python)

Dependencies:
| Library     | Version | Sumber     | Hash/Checksum |
|-------------|---------|------------|---------------|
| random      | Built-in| -          | -             |
| csv         | Built-in| -          | -             |
| collections | Built-in| -          | -             |

Konfigurasi:
  Config file     : Hardcoded (parameter global dalam gacha.py)
  Random seed     : 42
  Hyperparameters : TOTAL_SAMPEL=100000, SOFT_PITY=50, HARD_PITY=70

Reproducibility Check:
  [X] Dependency terdokumentasi
  [X] Seed ditetapkan di semua level (Python random)
  [X] Config di version control
  [X] README instruksi reproduksi lengkap
```

---

## Latihan 1 — Environment Specification

Dokumentasikan environment untuk eksperimen Anda (boleh environment saat ini atau yang direncanakan).

| Komponen | Spesifikasi |
|----------|------------|
| CPU | Intel Core 5 |
| RAM | 12 GB  |
| GPU | NVIDIA GeForce MX250 |
| OS | Windows 11 |
| Runtime | Python 3.10+ |
| Framework | Pure Python |
| Random Seed | 42 |

**Dependencies (minimal 5):**

| Library | Version | Alasan Dibutuhkan |
|---------|---------|-------------------|
| random | Built-in | Fungsi utama untuk menghasilkan angka acak (RNG) dalam simulasi. |
| csv | Built-in | Menulis hasil eksperimen ke format CSV untuk analisis lebih lanjut. |
| collections | Built-in | Menggunakan Counter untuk menghitung frekuensi hasil pull dengan efisien. |

---

## Latihan 2 — Repeatability Test Plan

Rancang tes repeatability sederhana: jalankan kode yang sama 3× di environment yang sama.

| Run | Seed | Metrik Utama | Hasil Sama? |
|-----|------|-------------|-------------|
| 1 | 42 | ~113.xx (tergantung logika) | — |
| 2 | 42 | ~113.xx (tergantung logika) | [x] Ya / [ ] Tidak |
| 3 | 42 | ~113.xx (tergantung logika) | [x] Ya / [ ] Tidak |

**Jika hasil berbeda, kemungkinan penyebab:**

> Penyebab umum adalah tidak adanya kontrol terhadap state acak (random state) atau adanya proses latar belakang yang menginterupsi clock prosesor jika metrik diukur berdasarkan waktu eksekusi. Dengan menetapkan random.seed(42), kita mengunci urutan angka acak yang dihasilkan Python.

___________________________________________________

**Checklist kontrol yang sudah diterapkan:**
- [x] Random seed di-set di semua level
- [x] Tidak ada background process yang mengganggu
- [x] Cache dibersihkan antar-run
- [x] Config file yang sama untuk semua run

---

## Latihan 3 — README Eksperimen

Tulis README minimum untuk eksperimen Anda (6 komponen wajib).

```
# Judul Eksperimen: Simulasi Efisiensi Algoritma Weighted Probability pada Gacha

## 1. Environment
- OS: Windows/Linux/macOS
- Runtime: Python 3.x
- Hardware: Standar PC (CPU-only)

## 2. Installation
Tidak diperlukan instalasi library pihak ketiga. Pastikan Python 3 sudah terinstal.

## 3. Data
Data bersifat sintetis, digenerasi menggunakan `gacha.py` dengan 100.000 iterasi.

## 4. Execution
Jalankan di terminal: `py gacha.py`

## 5. Configuration
Parameter diatur pada bagian konstanta global `gacha.py`.
- RANDOM_SEED = 42

## 6. Expected Output
- Tampilan log di terminal (rata-rata pull).
- File `hasil_simulasi_gacha.csv` yang berisi kolom `Pull_Ke`, `Cumulative_Probability_Fixed`, `Cumulative_Probability_Weighted`.
```

---

## Refleksi

> Apakah eksperimen Anda saat ini bisa direproduksi oleh orang lain tanpa bantuan Anda? Komponen apa yang masih hilang?

**Level saat ini:** [x] Repeatability / [ ] Reproducibility / [ ] Belum keduanya
**Komponen yang belum terdokumentasi:**
> Eksperimen ini sudah mencapai level repeatability karena hasil komputasi sudah konsisten dengan penggunaan seed. Untuk mencapai reproducibility penuh, saya perlu menambahkan berkas requirements.txt (meskipun saat ini hanya menggunakan library bawaan) dan dokumentasi yang lebih mendalam mengenai arsitektur algoritma pity agar peneliti lain bisa memahami logika di balik kode tersebut tanpa harus membaca baris kode satu per satu.
