# Tahap 4 — Analisis Data dan Visualisasi

**Status:** Draft awal
**Lokasi kode:** [../05-kode/analysis.py](../05-kode/analysis.py)

---

## Tujuan

Mengolah data hasil simulasi menjadi informasi yang mudah dibaca dan dipakai untuk pembahasan hasil penelitian. Tahap ini menghasilkan statistik deskriptif, grafik cumulative probability, dan ringkasan temuan yang penting.

## Langkah Analisis

1. Membaca data hasil simulasi dari folder [../04-data](../04-data).
2. Menggabungkan beberapa file CSV menjadi satu data agregat.
3. Menghitung rata-rata pull untuk masing-masing kondisi.
4. Menghitung cumulative probability per pull ke-N.
5. Membuat grafik perbandingan fixed vs weighted probability.

## Output yang Diharapkan

- File agregat statistik di [../06-output/tables/aggregated_stats.csv](../06-output/tables/aggregated_stats.csv)
- Grafik perbandingan di [../06-output/figures/fig_cumulative_probability.png](../06-output/figures/fig_cumulative_probability.png)
- Ringkasan temuan yang akan dipakai pada bagian hasil penelitian

## Metrik Utama

- Rata-rata pull yang dibutuhkan sampai rare item diperoleh
- Cumulative probability pada pull tertentu, misalnya pull ke-50 dan pull ke-70
- Perbedaan performa antara fixed dan weighted probability

## Catatan

Hasil analisis ini akan menjadi bagian inti dari bab hasil dan pembahasan dalam naskah penelitian.
