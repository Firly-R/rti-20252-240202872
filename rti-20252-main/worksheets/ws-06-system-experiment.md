# WS-06: System-Experiment Mapping

> **Bab 6 — System Design sebagai Experimental Artifact**

---

## Ringkasan Materi

### Sistem = Instrumen Pengujian, Bukan Produk

Seorang engineer bertanya "apakah sistem bekerja?" — seorang peneliti bertanya "apa yang bisa dibuktikan sistem ini?" Sistem dalam riset adalah **artifact** — objek yang sengaja dibuat untuk menguji klaim spesifik.

### System as Experiment Model

```
RQ → Variable → System Component → Experimental Setup → Output
```

Setiap komponen sistem harus bisa ditelusuri ke variabel riset (top-down), dan setiap pengukuran harus menjawab RQ (bottom-up).

### Mapping Variabel ke Komponen

| Tipe Variabel | Peran di Sistem | Contoh |
|---------------|----------------|--------|
| **IV** (Independent) | Modul yang bisa di-toggle/swap | Algoritma A vs B |
| **DV** (Dependent) | Modul pengukuran | Logger, metrics collector |
| **CV** (Control) | Config yang dikunci | Dataset, parameter tetap |

Jika variabel tidak bisa di-map ke komponen apapun → arsitektur perlu didesain ulang.

### 4 Prinsip Desain Eksperimental

| Prinsip | Pertanyaan Kunci |
|---------|-----------------|
| **Traceability** | Komponen ini melayani variabel yang mana? |
| **Modularity** | Bisakah IV diubah tanpa memengaruhi yang lain? |
| **Controllability** | Apakah CV dieksternalisasi ke config file? |
| **Measurability** | Apakah sistem otomatis menghasilkan data yang dibutuhkan? |

### Variable Isolation melalui Arsitektur

- **Modular architecture** — Pisahkan berdasarkan variabel
- **Configuration-driven** — Ubah config (YAML/JSON), bukan code
- **Feature toggles** — On/off flag untuk ablation study

  Contoh config YAML dengan feature toggles:
  ```yaml
  model:
    type: cnn          # IV: ganti "rf" untuk kondisi baseline
  features:
    use_temporal: true  # toggle komponen temporal
    use_normalization: true  # toggle preprocessing
  experiment:
    seed: 42
    runs: 5
  ```
  Dengan pendekatan ini, berbeda kondisi eksperimen = berbeda satu baris config, **tanpa mengubah kode**.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan sistem | Memenuhi kebutuhan user | Menguji hipotesis, menghasilkan bukti |
| Arsitektur | Optimasi performa & skalabilitas | Optimasi isolasi variabel & reprodusibilitas |
| Konfigurasi | Sering hardcoded | Dieksternalisasi ke config file |
| Fitur tambahan | Menambah nilai user | Menambah noise jika tidak terkait RQ |

### Istilah Penting

- **Artifact** — Objek yang sengaja dibuat untuk memecahkan masalah atau menguji proposisi
- **Traceability** — Kemampuan menelusuri hubungan RQ → variabel → komponen → output
- **Variable Isolation** — Mengubah hanya satu variabel sambil menahan yang lain konstan
- **Ablation Study** — Menguji kontribusi tiap komponen dengan melepasnya satu per satu
- **Configuration-driven Execution** — Semua parameter di config file, bukan hardcoded

---

## A.6 — Mapping RQ ke Arsitektur Sistem

### SYSTEM-EXPERIMENT MAPPING
Research Question: Bagaimana sistem simulasi gacha dapat digunakan untuk menguji pengaruh algoritma Weighted Probability terhadap peluang memperoleh item rare?

---

### Variable → Component Mapping:
| Variabel | Tipe | Komponen Sistem | Cara Manipulasi/Pengukuran |
|----------|------|-----------------|---------------------------|
| Weighted Probability | IV | Probability Engine | Mengubah nilai drop rate tiap pull |
| Jumlah Pull | IV | Pull Counter Module | Mengatur jumlah simulasi pull |
| Peluang Item Rare | DV | Probability Calculator | Menghitung cumulative probability rare item |
| Pity Threshold | CV | Pity System Config | Mengatur batas guaranteed rare |
| Base Probability | CV | Initial Probability Config | Mengatur probabilitas awal rare item |

---

## 4 Prinsip Desain:
  - [x] Traceability — Setiap komponen bisa ditelusuri ke variabel
  - [x] Variable Isolation — IV bisa diubah tanpa mengubah CV
  - [x] Measurement Integration — Pengukuran DV built-in
  - [x] Reproducibility — Setup bisa direkonstruksi

---

## Experimental Setup:

| Komponen | Detail |
|-----------|--------|
| Input Data | Nilai base probability, pity threshold, jumlah pull |
| Parameter | Drop rate, kenaikan probability, jumlah simulasi |
| Output Format | Tabel cumulative probability dan hasil rare item |

---

## Latihan 1 — Variable-to-Component Mapping

Gunakan RQ dan variabel dari WS-05. Petakan ke komponen sistem.

**RQ:**  Bagaimana algoritma Weighted Probability memengaruhi peluang memperoleh item rare pada sistem gacha game?


| Variabel | Tipe | Komponen Sistem | Cara Manipulasi / Pengukuran |
|----------|------|-----------------|---------------------------|
| Weighted Probability | IV | Probability Engine | Mengubah konfigurasi drop rate |
| Jumlah Pull | IV | Pull Simulation Module | Mengubah jumlah percobaan pull |
| Peluang Item Rare | DV | Result Logger | Menghitung cumulative probability |
| Pity Threshold | CV | Config File | Menentukan batas pity |
| Base Probability | CV | Config File | Menentukan probabilitas awal |

---

**Apakah semua variabel bisa di-map?** [x] Ya / [ ] Tidak

---

## Latihan 2 — 4 Prinsip Desain

Evaluasi desain sistem terhadap 4 prinsip.

| Prinsip | Status | Bukti / Penjelasan |
|---------|--------|-------------------|
| Traceability | ✅ | Setiap modul terhubung langsung dengan variabel penelitian |
| Modularity | ✅ | Probability Engine dan Pity System dipisahkan |
| Controllability | ✅ | Parameter disimpan pada config file |
| Measurability | ✅ | Sistem otomatis menghasilkan cumulative probability |

---

**Prinsip mana yang paling sulit dipenuhi?** 
> Modularity

**Strategi untuk mengatasinya:**
> Memisahkan Probability Engine, Pull Counter, dan Pity System menjadi modul independen agar perubahan weighted probability tidak memengaruhi komponen lain. 

---

## Latihan 3 — Ablation Study Planning

Jika sistem memiliki 3 komponen utama, rencanakan ablation study.

> **Panduan jumlah kondisi:** Untuk 3 komponen (A, B, C), kondisi minimal yang direkomendasikan:
> Full + (-A) + (-B) + (-C) = **4 kondisi dasar**. Jika waktu memungkinkan, tambahkan kombinasi ganda: (-A,-B), (-A,-C), (-B,-C) = **7 kondisi**. Sesuaikan dengan *computational cost* dan tenggat waktu penelitian.

| Kondisi | Komponen A | Komponen B | Komponen C | Hasil yang Diharapkan |
|---------|-----------|-----------|-----------|----------------------|
| Full | ✅ | ✅ | ✅ | Baseline sistem penuh |
| – A | ❌ (Fixed Probability) | ✅ | ✅ | Peluang rare item lebih rendah |
| – B | ✅ | ❌ | ✅ | Tidak ada guaranteed rare item |
| – C | ✅ | ✅ | ❌ | Probability increase lebih lambat |

**Komponen mana yang diprediksi paling berkontribusi?** 
> Weighted Probability

**Mengapa?**
> Karena weighted probability merupakan inti algoritma yang secara langsung menentukan perubahan peluang rare item pada setiap pull.


---

## Refleksi

> Apa risiko jika sistem dibangun seperti produk (monolitik, fitur lengkap) lalu baru dilakukan eksperimen? Mengapa arsitektur modular penting untuk riset?

**Jawaban:**
> Sistem monolitik membuat variabel penelitian sulit diisolasi sehingga perubahan satu fitur dapat memengaruhi hasil eksperimen lain dan menurunkan validitas penelitian.

> Arsitektur modular penting karena setiap komponen dipisahkan sehingga variabel dapat diuji secara terkontrol, lebih mudah dianalisis, dan eksperimen lebih mudah direproduksi.
