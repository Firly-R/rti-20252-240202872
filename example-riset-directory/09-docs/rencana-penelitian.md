# Rencana Penelitian: Analisis Pengaruh Algoritma Weighted Probability terhadap Peluang Rare Item pada Sistem Gacha Game

## 1. Ringkasan Penelitian

| Item | Keterangan |
|---|---|
| Judul | Analisis Pengaruh Algoritma Weighted Probability terhadap Peluang Rare Item pada Sistem Gacha Game |
| Fokus | Perbandingan algoritma fixed probability dan weighted probability dalam sistem gacha |
| Objek penelitian | Simulasi sistem gacha virtual dengan pity system |
| Metode | Eksperimen komparatif berbasis simulasi komputer |
| Variabel utama | Algoritma probabilitas, cumulative probability, average pulls to rare |
| Output utama | Data simulasi, grafik perbandingan, dan naskah jurnal |

## 2. Rumusan Masalah

Bagaimana pengaruh algoritma weighted probability terhadap cumulative probability dan rata-rata jumlah pull yang dibutuhkan untuk memperoleh rare item dibandingkan dengan algoritma fixed probability?

## 3. Tujuan Penelitian

1. Menganalisis perbedaan peluang kumulatif memperoleh rare item pada sistem fixed probability dan weighted probability.
2. Membandingkan rata-rata jumlah pull yang dibutuhkan untuk memperoleh rare item pada kedua algoritma.
3. Menghasilkan simulasi dan visualisasi yang dapat menjadi dasar penelitian lanjutan tentang desain probabilitas pada game gacha.

## 4. Variabel Penelitian

- Variabel independen: algoritma probabilitas (fixed vs weighted)
- Variabel dependen: cumulative probability, average pulls to rare
- Variabel kontrol: base probability, soft pity threshold, hard pity threshold, jumlah sampel simulasi

## 5. Alur Kerja (Roadmap)

- [x] **Tahap 1** — [Desain Eksperimen & Struktur Data](tahap-1-arsitektur-dan-skema-database.md) — *Draft awal*
- [x] **Tahap 2** — [Implementasi Simulator Gacha](tahap-2-implementasi-gateway.md) — *Draft awal*
- [x] **Tahap 3** — [Eksekusi Simulasi & Pengumpulan Data](tahap-3-pengujian-k6.md) — *Draft awal*
- [x] **Tahap 4** — [Analisis Data & Visualisasi](tahap-4-analisis-data.md) — *Draft awal*
- [x] **Tahap 5** — [Penulisan Draf Paper](tahap-5-draf-paper.md) — *Draft awal*

## 6. Deliverable Utama

- Simulator gacha berbasis Python
- Data hasil simulasi dalam format CSV
- Grafik cumulative probability
- Ringkasan statistik deskriptif
- Draf naskah jurnal

## 7. Catatan

Dokumen ini disusun berdasarkan penelitian nyata yang sudah ada di folder [../01-proposal](../01-proposal), [../05-kode](../05-kode), [../04-data](../04-data), [../06-output](../06-output), dan [../07-manuskrip](../07-manuskrip).
