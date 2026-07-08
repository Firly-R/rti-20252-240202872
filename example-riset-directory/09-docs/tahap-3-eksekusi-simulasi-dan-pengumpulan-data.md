# Tahap 3 — Eksekusi Simulasi dan Pengumpulan Data

**Status:** Draft awal
**Lokasi kode:** [../05-kode/gacha.py](../05-kode/gacha.py) dan [../04-data](../04-data)

---

## Tujuan

Menjalankan simulasi berulang untuk menghasilkan data penelitian yang cukup besar dan konsisten. Tahap ini menghasilkan data mentah yang nantinya dipakai untuk analisis statistik dan visualisasi.

## Rancangan Eksekusi

1. Jalankan simulasi untuk kondisi fixed probability.
2. Jalankan simulasi untuk kondisi weighted probability.
3. Simpan hasil tiap iterasi ke file CSV.
4. Ulangi eksekusi bila diperlukan untuk memperbesar sampel.

## Parameter yang Dipakai

- Total sampel: 100.000 responden virtual
- Base probability: 0,6%
- Soft pity: 50 pull
- Hard pity: 70 pull
- Random seed: 42

## Output yang Dihasilkan

Hasil simulasi disimpan ke folder [../04-data](../04-data), misalnya:

- hasil_simulasi_gacha_1.csv
- hasil_simulasi_gacha_2.csv
- hasil_simulasi_gacha_3.csv

File-file ini berisi data cumulative probability per pull untuk tiap kondisi percobaan.

## Catatan Pelaksanaan

- Eksekusi dapat dilakukan berulang untuk melihat stabilitas hasil.
- Setiap run sebaiknya menggunakan parameter yang sama agar hasil perbandingan tetap valid.
- Data hasil simulasi menjadi input utama untuk tahap analisis berikutnya.
