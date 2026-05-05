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

## A.3 — Literature Mapping & Gap Identification

LITERATURE MAPPING

* Topik      : Face Recognition berbasis Deep Learning untuk sistem identifikasi wajah
* Database   : Google Scholar
* Query      : (“face recognition” OR “face detection”) AND (“CNN” OR “FaceNet” OR “MTCNN”)
* Tahun      : 2023-2025
* Hasil awal : 10 paper → Screening → 5 paper final

Literature Matrix (concept-centric):

| Study | Tahun | Method | Data | Result | Limitation |
|-------|-------|--------|------|--------|------------|
|Khan et al.|2023|CNN(Improved MTCNN|Face detection dataset|Deteksi lebih akurat|Komputasi tinggi|
|He et al.|2023|CNN & Transformer|Face dataset|Lebih efisien & akurat|Kompleks|
|Xiao et al.|2023|MTCNN & CNN|Sistem pendidikan|Respon cepat|Terbatas kondisi|
|Khalifa et al.|2024|CNN & Attention|Face verification|Lebih robust|Model kompleks|
|Sharma et al.|2024|MTCNN & FaceNet|Sistem realtime|Akurasi tinggi|Bergantung kualitas citra|

### Pola yang ditemukan:
* Metode dominan     : Pendekatan berbasis Convolutional Neural Network (CNN) dengan pengembangan seperti CNN + Attention dan CNN + Transformer
* Dataset umum       : Dataset citra wajah dengan variasi terbatas, umumnya digunakan dalam konteks sistem real-time seperti pendidikan dan keamanan
* Limitasi berulang  : Ketergantungan pada kualitas citra (pencahayaan, pose), kurangnya robustness pada kondisi real-world, serta meningkatnya kompleksitas dan kebutuhan komputasi

### GAP IDENTIFICATION

#### Gap 1: [Jenis: performance ]
* Deskripsi    : Meskipun metode semakin kompleks (attention, transformer), sistem masih belum robust terhadap kondisi real-world seperti pencahayaan, pose, dan kualitas citra.
* Bukti        : Performa bergantung pada kualitas citra(Sharma et al.), sistem terbatas pada kondisi tertentu(Xiao et al.), Perlu model lebih kompleks untuk meningkatkan robustness(Khalifa et al.)
* Signifikansi : Keterbatasan ini menyebabkan sistem face recognition tidak dapat bekerja secara optimal dalam kondisi nyata, sehingga mengurangi keandalan pada aplikasi seperti keamanan dan sistem real-time.

#### Gap 2: [Jenis: Complexity / Method]
* Deskripsi    : Peningkatan performa model diikuti dengan meningkatnya kompleksitas arsitektur dan kebutuhan komputasi yang tinggi.
* Bukti        : Membutuhkan komputasi tinggi(Khan et al.), model CNN + Transformer lebih kompleks(He et al.), arsitektur lebih berat(Khalifa et al.)
* Signifikansi : Kompleksitas yang tinggi membatasi implementasi sistem pada perangkat dengan sumber daya terbatas, seperti sistem embedded atau aplikasi real-time.

Baseline Selection:
| Baseline | Relevansi | Representatif | Source |
|----------|-----------|---------------|--------|
|HaarCascade|Pengembangan metode deteksi wajah dari MTCNN untuk meningkatkan akurasi|Representasi deteksi wajah modern|Khan et al. (2023)|
|Attention-based CNN|Pengembangan CNN untuk meningkatkan akurasi dan robustness face recognition|Representasi CNN modern (state-of-the-art)|Khalifa et al.(2024)|
|MTCNN + Enhanced FaceNet|Kombinasi deteksi dan recognition modern dengan peningkatan fitur (attention)|Representasi pipeline terbaru|Karamizadeh et al.(2025)|

---

## Latihan 1 — Concept-Centric Literature Table

Gunakan topik riset dari WS-02. Cari minimal 5 paper relevan menggunakan database akademik.

> **Panduan pencarian:**
> - Database: IEEE Xplore, ACM DL, Google Scholar, atau ResearchGate
> - Tulis query Boolean yang digunakan: contoh `("object detection" OR "image classification") AND ("edge computing") NOT ("medical")`. Dokumentasikan query secara eksplisit.
> - Akses gratis: buka Google Scholar → cari judul paper → klik [PDF] jika tersedia, atau akses lewat campus VPN

**Topik riset:** Face Recognition berbasis Deep Learning untuk sistem identifikasi wajah

**Query pencarian:** ("face recognition" OR "face detection") AND ("CNN" OR "FaceNet" OR "MTCNN") NOT ("medical")

**Database:** Google Scholar

| # | Study | Tahun | Method | Dataset | Result | Limitasi |
|---|-------|-------|--------|---------|--------|----------|
| 1 | Soumya Suvra Khan, Md. Ashraful Islam, Md. Alamin Hossain | 2023 | Improved MTCNN(CNN) | WIDER FACE | Deteksi lebih akurat | Komputasi tinggi |
| 2 | Yu Xiao, Xiaofei Zhang, Li Wang | 2023 | MTCNN + CNN | Dataset pendidikan | Respon cepat | Terbatas kondisi |
| 3 | Ahmed Fawzy Khalifa, Mohamed Elhoseny, Aboul Ella Hassanien | 2024 | CNN + Attention | Face dataset | Akurasi meningkat | Model kompleks |
| 4 | Md. Rabiul Islam, Md. Al Mehedi Hasan, Tanzir Mahmud | 2024 | CNN-based Face recognition | Face dataset | Performa tinggi | Sensitif terhadap kualitas citra |
| 5 | S. Karamizadeh, A. Shamsinejad, M. H. Moattar | 2025 | MTCNN + FaceNet(Enhanced) | Real-world dataset | Lebih robust | Komputasi tinggi |

**Pola yang terlihat — Metode dominan:** Deep Learning berbasis CNN dengan pengembangan seperti Attention dan kombinasi metode

**Limitasi yang berulang:** Ketergantungan pada kualitas citra (pose, pencahayaan), serta meningkatnya kompleksitas dan kebutuhan komputasi

---

## Latihan 2 — Gap Identification

Berdasarkan tabel di Latihan 1, identifikasi gap.

| Jenis Gap | Ditemukan? | Gap Statement |
|-----------|-----------|---------------|
| Performance Gap | [✅] Ya | Performa sistem face recognition masih menurun pada kondisi real-world seperti pencahayaan rendah, variasi pose, dan kualitas citra yang buruk |
| Method Gap | [✅] Ya | Metode berbasis CNN masih memiliki keterbatasan dalam menangkap fitur global sehingga memerlukan pengembangan seperti attention dan transformer |
| Data Gap | [✅] Ya | Dataset yang digunakan masih terbatas dan belum sepenuhnya merepresentasikan kondisi dunia nyata yang beragam |
| Context Gap | [✅] Ya | Sebagian besar penelitian hanya diuji pada kondisi terkontrol dan belum banyak diterapkan pada lingkungan real-time yang kompleks |

**Gap utama yang dipilih:** Performance Gap (Robustness terhadap kondisi real-world)
**Mengapa gap ini penting (bukan sekadar "belum ada yang meneliti")?**
> Gap ini penting karena secara langsung mempengaruhi keberhasilan sistem face recognition dalam penggunaan nyata. Meskipun metode yang digunakan semakin kompleks, performa sistem masih sangat bergantung pada kondisi input seperti pencahayaan, pose, dan kualitas citra. Hal ini menyebabkan sistem kurang andal ketika diterapkan di lingkungan real-world, sehingga perlu dikembangkan metode yang lebih robust agar dapat bekerja secara konsisten dalam berbagai kondisi.

---

## Latihan 3 — Baseline Selection

| # | Baseline | Mengapa Relevan | Mengapa Representatif | Apakah SOTA? | Sumber |
|---|----------|----------------|----------------------|-------------|--------|
| 1 | MTCNN (Improved MTCNN) | Digunakan untuk face detection pada task yang sama | Banyak digunakan dalam penelitian face recognition terbaru | Bukan, tetapi masih umum digunakan | Soumya Suvra Khan, Md. Ashraful Islam, Md. Alamin Hossain (2023) |
| 2 | CNN + Attention | Digunakan untuk meningkatkan akurasi face recognition | Mewakili perkembangan metode modern berbasis CNN | Ya (mendekati SOTA) | Ahmed Fawzy Khalifa, Mohamed Elhoseny, Aboul Ella Hassanien (2024) |

**Apakah pemilihan baseline ini bisa dianggap straw man?** [❌] Tidak
> Justifikasi: Baseline yang dipilih mencakup metode yang umum digunakan (MTCNN) dan metode yang lebih modern (CNN + Attention), sehingga perbandingan yang dilakukan tetap adil dan representatif terhadap perkembangan penelitian saat ini.

---

## Refleksi

> Apa perbedaan antara "belum ada yang meneliti ini" (klaim tanpa bukti) dengan research gap yang valid? Bagaimana cara membuktikan bahwa sebuah gap benar-benar ada?

**Jawaban:**
> Perbedaan antara klaim “belum ada yang meneliti ini” dengan research gap yang valid adalah bahwa research gap harus didukung oleh bukti dari beberapa penelitian sebelumnya. Klaim tanpa bukti hanya bersifat asumsi, sedangkan research gap yang valid diperoleh melalui analisis literatur yang menunjukkan adanya keterbatasan atau masalah yang konsisten.

> Cara membuktikan bahwa sebuah gap benar-benar ada adalah dengan menunjukkan pola yang sama dari beberapa penelitian, seperti limitasi yang berulang atau hasil yang belum optimal pada kondisi tertentu. Dengan demikian, gap tersebut bukan hanya opini, tetapi didasarkan pada temuan ilmiah yang dapat dipertanggungjawabkan.
