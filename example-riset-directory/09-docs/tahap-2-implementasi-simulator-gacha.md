# Tahap 2 — Implementasi Simulator Gacha

**Status:** Draft awal
**Lokasi kode:** [../05-kode/gacha.py](../05-kode/gacha.py) dan [../05-kode/analysis.py](../05-kode/analysis.py)

---

## Tujuan

Mengimplementasikan simulator gacha yang membandingkan dua kondisi algoritma probabilitas:

- fixed probability sebagai baseline
- weighted probability sebagai intervensi dengan pity system

Simulator ini digunakan untuk menghasilkan data primer penelitian.

## Deliverable

- [x] Skrip simulasi utama [../05-kode/gacha.py](../05-kode/gacha.py)
- [x] Skrip analisis dan visualisasi [../05-kode/analysis.py](../05-kode/analysis.py)
- [x] Parameter penelitian yang dapat diubah pada bagian konfigurasi kode
- [x] Output CSV hasil simulasi di folder [../04-data](../04-data)
- [x] Grafik cumulative probability di folder [../06-output/figures](../06-output/figures)

## Struktur Logika Simulasi

1. Inisialisasi parameter penelitian.
2. Jalankan simulasi untuk setiap pemain virtual.
3. Rekam jumlah pull yang dibutuhkan sampai rare item diperoleh.
4. Hitung cumulative probability per pull ke-N.
5. Ekspor hasil ke CSV untuk kebutuhan analisis.

## Keputusan Implementasi

- Bahasa pemrograman: Python
- Output utama: CSV dan grafik
- Random seed dipakai agar hasil dapat direproduksi
- Parameter seperti base probability, soft pity, dan hard pity diatur secara eksplisit

## Catatan

Implementasi ini menjadi fondasi utama untuk Tahap 3 dan Tahap 4 karena data mentah dan hasil analisis berasal dari simulator ini.
