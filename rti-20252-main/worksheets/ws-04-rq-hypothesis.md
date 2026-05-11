# WS-04: Research Question & Hypothesis

> **Bab 4 — Research Question, Contribution & Hypothesis**

---

## Ringkasan Materi

### RQ Bukan Pertanyaan Biasa

Research Question yang baik secara implisit mengandung cetak biru eksperimen: subjek, baseline, metrik, domain, dataset.

| Kualitas | Contoh |
|----------|--------|
| **Buruk** | "Bagaimana pengaruh deep learning terhadap deteksi malware?" |
| **Baik** | "Apakah CNN menghasilkan F1-Score lebih tinggi dari RF pada CIC-MalMem-2022?" |

Perbedaan: RQ yang baik menyebutkan **metode spesifik**, **metrik terukur**, **baseline**, dan **dataset**.

### Tiga Jenis RQ

| Jenis | Pola | Kebutuhan |
|-------|------|-----------|
| **Comparison** | A vs B → mana lebih baik? | ≥ 2 metode, metrik sama |
| **Improvement** | A' vs A → modifikasi lebih baik? | Pre/post, bukti perbaikan |
| **Exploratory** | Faktor X₁...Xₙ → pengaruh terhadap Y? | Multi-variabel, korelasi/regresi |

### Contribution Statement

Tiga jenis kontribusi: **Improvement** (metode terbukti lebih baik), **Comparison** (perbandingan sistematis yang belum ada), **Novel Approach** (pendekatan baru). Kontribusi harus terhubung langsung dengan gap — kontribusi tanpa gap = klaim tanpa justifikasi.

### Hypothesis H₀ / H₁

- **H₀** (Null) = Tidak ada perbedaan signifikan — asumsi default, harus dibuktikan salah
- **H₁** (Alternative) = Ada perbedaan signifikan — diterima hanya jika H₀ ditolak
- Harus **falsifiable**, mengandung **metrik terukur**, dirumuskan **SEBELUM eksperimen**

### Rantai Operasionalisasi

```
RQ → Variable → Metric → Data → Analysis
```

Jika rantai ini tidak lengkap, RQ belum mature. Bi-directional: RQ yang tidak bisa jadi hipotesis testable harus direvisi mundur.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan pertanyaan | Apa yang harus dibangun? | Apa yang harus dibuktikan? |
| Bentuk jawaban | Sistem yang berfungsi | Bukti empiris terukur |
| Sukses diukur oleh | User satisfaction, uptime | Signifikansi statistik, effect size |
| Jika gagal | Debug dan perbaiki | Laporkan, analisis mengapa |

### Istilah Penting

- **Research Question (RQ)** — Pertanyaan spesifik: variabel terukur + metrik + konteks
- **Contribution Statement** — Apa yang diketahui setelah riset selesai yang sebelumnya belum ada
- **H₀ / H₁** — Null vs Alternative Hypothesis
- **Falsifiability** — Kondisi hipotesis ditolak harus bisa didefinisikan sebelum eksperimen
- **Operationalization** — Proses mewujudkan konsep abstrak menjadi variabel terukur

---

## A.4 — RQ-Contribution-Hypothesis

### RQ-CONTRIBUTION-HYPOTHESIS

**Gap Statement  :** Sebagian besar penelitian tentang sistem gacha berfokus pada desain ekonomi, whale property, dan optimasi revenue, namun belum banyak penelitian yang secara spesifik menganalisis pengaruh mekanisme weighted probability terhadap perilaku probabilistik pemain dan efisiensi sistem pity pada game gacha modern.

--- 

# Research Question:

### Tipe           : 
- [x] Comparison
- [ ] Improvement
- [ ] Exploratory

### Formulasi      : 
> Apakah mekanisme weighted probability pada sistem gacha menghasilkan peluang perolehan item rare yang lebih efisien dibanding fixed-probability gacha berdasarkan expected pull rate dan probabilitas kemenangan pada sistem pity?

### Variabel IV  : 
Jenis algoritma probabilitas gacha (weighted probability vs fixed probability)

### Variabel DV  : 
Efisiensi peluang memperoleh item rare
  
### Metrik       : 
- Expected number of pulls
- Winning probability
- Pull efficiency
- Average success rate
  
### Dataset      : 
Data simulasi probabilitas gacha berdasarkan model pada jurnal Gacha Game Analysis and Design (2023)

### Baseline     :
Fixed-probability gacha game

---

# Quality Check RQ:

- [x] Variabel spesifik
- [x] Metrik jelas
- [x] Baseline ada
- [x] Konteks disebutkan
- [x] Memerlukan eksperimen (bukan hanya survei literatur)

----

# Contribution Statement:
  
### Apa yang baru diketahui :
Penelitian ini memberikan analisis mengenai bagaimana weighted probability memengaruhi efisiensi sistem gacha dibanding sistem probabilitas tetap, terutama terhadap peluang mendapatkan item rare dan pengaruhnya terhadap perilaku pull pemain.

### Jenis kontribusi        :
- [ ] Improvement
- [x] Comparison
- [ ] Novel approach
  
### Gap yang diisi          : 
Kurangnya analisis spesifik mengenai weighted probability pada sistem pity dan probabilitas dinamis di game gacha modern.

---

# Hypothesis Pair:

### H₀ :
Tidak terdapat perbedaan signifikan antara weighted probability dan fixed probability terhadap efisiensi peluang mendapatkan item rare pada sistem gacha.

### H₁ :
Weighted probability menghasilkan efisiensi peluang mendapatkan item rare yang lebih tinggi dibanding fixed probability pada sistem gacha.

### Threshold              : 
Perbedaan expected pull rate ≥ 10%

### Justifikasi threshold  :
Perbedaan 10% dianggap cukup signifikan untuk menunjukkan peningkatan efisiensi probabilitas pada mekanisme gacha dan dapat diamati melalui simulasi probabilistik.

---

## Latihan 1 — Dari Gap ke RQ

**Gap dari WS-03:** Belum banyak penelitian yang menganalisis weighted probability pada sistem pity gacha game secara spesifik menggunakan pendekatan probabilistik dan MDP.

**RQ versi pertama (tulis bebas):**
> Bagaimana pengaruh weighted probability terhadap sistem gacha game?

**Evaluasi RQ:**

| Komponen | Ada? | Isi |
|----------|------|-----|
| Metode spesifik | *Ya* | Weighted probability vs fixed probability |
| Metrik terukur | *Ya* | Expected pulls dan success rate |
| Baseline | *Ya* | Fixed probability |
| Dataset/konteks | *Ya* | Sistem gacha game dengan pity system |

**Tipe RQ:** Comparison

**RQ versi revisi (setelah evaluasi):**
> Apakah weighted probability pada sistem pity gacha menghasilkan expected pull rate yang lebih efisien dibanding fixed-probability gacha?

---

## Latihan 2 — Hypothesis Pair

Rumuskan pasangan hipotesis dari RQ di Latihan 1.

| Komponen | Isi |
|----------|-----|
| H₀ | *Tidak ada perbedaan signifikan expected pull rate antara weighted probability dan fixed probability* |
| H₁ |*Weighted probability memiliki expected pull rate lebih efisien dibanding fixed probability* |
| Metrik |*Expected pulls, winning probability* |
| Threshold | *≥ 10% peningkatan efisiensi* |
| Justifikasi threshold | *Menunjukkan peningkatan probabilitas yang cukup signifikan dalam simulasi sistem gacha* |

**Apakah hipotesis ini falsifiable?** 
Ya 
> Bagaimana cara membuktikannya salah?
> melakukan simulasi probabilitas dan menunjukkan bahwa weighted probability tidak menghasilkan peningkatan efisiensi dibanding fixed probability.

---

## Latihan 3 — Rantai Operasionalisasi

Lengkapi rantai dari RQ hingga metode analisis.

| Tahap | Isi |
|-------|-----|
| RQ | *Apakah weighted probability menghasilkan expected pull rate lebih efisien dibanding fixed probability?* |
| Variable (IV) | *Jenis probabilitas gacha* |
| Variable (DV) |*Efisiensi peluang memperoleh item rare* |
| Metric | *Expected pulls, success probability* |
| Data source | *Simulasi probabilitas berdasarkan model jurnal* |
| Analysis method | *Analisis probabilistik dan perbandingan statistik* |

**Apakah rantai lengkap?** Ya 

---

## Refleksi

**Judul:** Gacha Game Analysis and Design
**RQ yang diekstrak:** Bagaimana desain probabilitas pada gacha game memengaruhi revenue dan perilaku pemain?
**Komponen yang hilang:** Metrik evaluasi spesifik untuk weighted probability belum dijelaskan secara rinci sehingga masih perlu operasionalisasi lebih lanjut.
