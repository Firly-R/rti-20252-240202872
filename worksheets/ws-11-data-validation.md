# WS-11: Data Validation & Integrity

> **Bab 11 — Validasi Data & Integritas**

---

## Ringkasan Materi

### Data Trust Model

```
Raw Data → Data Cleaning → Consistency Check → Validation Process → Trusted Data
```

Data mentah belum bisa dipercaya. Harus melewati pipeline validasi sebelum siap untuk analisis statistik.

### Empat Pilar Data Quality

| Pilar | Deskripsi | Contoh Pelanggaran |
|-------|----------|-------------------|
| **Accuracy** | Nilai dalam range masuk akal | Akurasi = 1.5 (di luar [0,1]) |
| **Consistency** | Format seragam di semua run | Run 1: CSV, Run 2: JSON |
| **Completeness** | Tidak ada data hilang dari plan | 97 dari 100 run tercatat |
| **Validity** | Data sesuai desain eksperimen | Parameter baseline tercampur treatment |

### Proses Validasi Progresif

1. **Format validation** — Tipe file, header, kolom
2. **Range validation** — Nilai dalam batas logis
3. **Consistency validation** — Format seragam antar-run
4. **Logic validation** — Data cocok dengan desain eksperimen

Jika gagal di langkah awal → tidak perlu lanjut.

### Anomaly Detection — 3 Jenis

| Jenis | Deskripsi | Deteksi |
|-------|----------|---------|
| **Statistical outlier** | Nilai di luar distribusi normal | IQR: < Q1-1.5×IQR atau > Q3+1.5×IQR |
| **Contextual anomaly** | Normal absolut, abnormal dalam konteks | Run 1-10: ~91%, Run 11-20: ~88% |
| **Pattern anomaly** | Pola sistematis (bukan random) | Performa menurun berurutan |

**Prinsip:** Detect → Investigate → Document → Decide — **JANGAN langsung hapus.**

### Engineering vs Research Validation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Data sesuai spesifikasi bisnis | Data layak untuk analisis statistik |
| Missing data | Impute / set default | Investigasi penyebab → dokumentasi |
| Outlier | Bug → fix | Mungkin temuan → investigasi |
| Dokumentasi | Minimal (log error) | Komprehensif (anomali + keputusan) |

### Jebakan Kognitif

1. "Logging otomatis ≠ data benar" → bisa ada bug di logger
2. "Outlier = hapus" → bisa jadi temuan penting
3. "Dataset kecil tidak perlu validasi" → justru lebih rentan
4. "Mean normal = data benar" → [94, 95, 93, **44**, 94] → mean 84% terlihat wajar

---

## Template A.11 — Data Validation Checklist

```
DATA VALIDATION CHECKLIST

Completeness:
  [ ] Semua skenario tercakup
  [ ] Jumlah run sesuai rencana
  [ ] Tidak ada file output hilang
  Missing: 1 dari 5 data points (Run 4 gagal/anomali)

Format Consistency:
  [x] Semua file format sama (CSV/JSON/...)
  [x] Header konsisten
  [x] Tipe data konsisten (numerik tetap numerik)

Range & Logic:
  [ ] Nilai dalam range masuk akal
  [x] Tidak ada waktu negatif
  [x] Metrik 0–100%, tidak di luar range
  Anomali ditemukan: Rata-rata pull untuk Kondisi Fixed pada Run 4 bernilai 95.3 (di luar batas kewajaran IQR yakni 162.8) karena tercampur parameter Weighted

Cross-Validation:
  [ ] Run identik → hasil mendekati (Gagal di Run 4)
  [ ] Trend konsisten dengan ekspektasi teori

Keputusan:
  [ ] Data siap analisis
  [x] Perlu cleaning
  [x] Perlu re-run (skenario: Run 4 - Fixed vs Weighted)
```

---

## Latihan 1 — Completeness Check

Verifikasi apakah semua data yang direncanakan sudah terkumpul.

| Skenario | Run Direncanakan | Run Tercatat | Missing | Alasan |
|----------|-----------------|-------------|---------|--------|
| Eksperimen Fixed & Weighted (Run 1) | 1 | 1 | 0 | Berjalan lancar, file CSV tersimpan |
| Eksperimen Fixed & Weighted (Run 2) | 1 | 1 | 0 | Berjalan lancar, file CSV tersimpan |
| Eksperimen Fixed & Weighted (Run 3) | 1 | 1 | 0 | Berjalan lancar, file CSV tersimpan |
| Eksperimen Fixed & Weighted (Run 4) | 1 | 0 | 1 | Terjadi Memory Error (OOM) pada iterasi ke-85.000 akibat penumpukan data list di RAM. |
| Eksperimen Fixed & Weighted (Run 5) | 1 | 1 | 0 | Berjalan lancar setelah restart compiler, file CSV tersimpan. |

**Total expected:** 5 Run | **Total actual:** 4 Run | **Missing:** 1 Run

**Keputusan untuk data missing:**
> Mendokumentasikan kegagalan pada Run 4. Melakukan optimasi memori pada skrip Python dengan langsung menuliskan hasil per iterasi ke dalam CSV alih-alih menyimpannya di variabel memori, lalu melakukan re-run khusus untuk seed Run 4 agar data genap menjadi 5 run.

---

## Latihan 2 — Anomaly Investigation

Periksa data Anda untuk anomali. Gunakan metode IQR atau z-score.

**Dataset sampel (atau data Anda sendiri):**

| Run | Accuracy (%) |
|-----|-------------|
| 1 | 166.5 |
| 2 | 167.1 |
| 3 | 166.8 |
| 4 | 95.3 |
| 5 | 165.2 |

**Deteksi outlier:**
- Data diurutkan: 95.3, 165.2, 166.5, 166.8, 167.1
- Q1 = 165.2 | Q3 = 166.8 | IQR = Q3-Q1 = 1.6
- Batas bawah (Q1 - 1.5×IQR) = 162.8
- Batas atas (Q3 + 1.5×IQR) = 169.2
- Outlier terdeteksi: 95.3(Run 4)

**Investigasi (untuk setiap outlier):**

| Outlier | Nilai | Kemungkinan Penyebab | Keputusan |
|---------|-------|---------------------|-----------|
| *Run 4* | *95.3* | *Terjadi kesalahan logika saat re-run (Parameter Weighted secara tidak sengaja ter-aplikasikan ke fungsi Fixed pada skrip gacha.py).* | *Menginvestigasi dan memperbaiki bug parameter mode pada pemanggilan fungsi simulasikan_satu_rare_item. Lakukan re-run ulang, jangan langsung menghapus data.* |

---

## Latihan 3 — Validation Report

Buat laporan validasi ringkas untuk dataset eksperimen Anda.

**1. Completeness:** 100% data terkumpul
**2. Format:** [x] Konsisten (Semua berformat .csv dengan header Pull_Ke, Cumulative_Probability_Fixed, Cumulative_Probability_Weighted).
**3. Range check (anomali):** Terdeteksi 1 statistical outlier pada Run 4 untuk nilai rata-rata pull kondisi Fixed, dengan nilai jatuh jauh di bawah batas bawah kewajaran (162.8).
**4. Logic check:** [X] Ada ketidaksesuaian: Kondisi parameter algoritma tercampur akibat bug skrip saat simulasi Run 4, menyalahi aturan Pilar Validity.

**Kesimpulan:** [x] Perlu tindakan: Melakukan perbaikan skrip pencatatan log pada variabel perbandingan, mengeksekusi ulang Run 4, dan memvalidasi ulang seluruh data sebelum masuk ke tahap uji T-Test.

---

## Refleksi

> Apa perbedaan antara "data yang benar" dan "data yang dipercaya"? Mengapa proses validasi formal diperlukan meskipun data dikumpulkan secara otomatis?

> Perbedaan Data Benar vs Data Dipercaya:
>
> "Data yang benar" (berdasarkan sistem) adalah angka yang berhasil diproduksi tanpa menyebabkan error sistem, yang sering kali dalam konteks engineering dianggap sudah cukup. Namun, "data yang dipercaya" (trusted data) dalam konteks riset adalah data yang telah diuji silang terhadap desain eksperimen, konsisten, logis secara distribusi, dan dipastikan terbebas dari bias teknis maupun anomali parameter.

> Mengapa Validasi Formal Tetap Diperlukan:
>
> Meskipun pengumpulan data dieksekusi secara otomatis oleh mesin menggunakan csv.writer, logging otomatis tidak menjamin kebenaran logika (logging otomatis ≠ data benar). Bug pada kode, kebocoran memori, atau inisiasi variabel Random Number Generator yang tidak terisolasi dengan baik dapat menghasilkan angka yang seolah normal tetapi tidak valid secara rancangan penelitian. Oleh karena itu, pipeline validasi dari data mentah menuju data tepercaya bersifat wajib.
